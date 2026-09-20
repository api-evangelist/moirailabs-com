---
name: moirailabs-com-async-analytics-invocation
description: Run a durable analytics calculation with Idempotency-Key and Prefer negotiation, poll it safely, fetch the stored result, and cancel if needed.
api: openapi/moirailabs-com-openapi.yml
operations: ['create', 'status', 'result', 'cancel']
method: generated
generated: '2026-09-19'
---
# Run an analytics invocation (the idempotent, resumable path)

The synchronous analytics GETs (`/analytics/metrics`, `/cohorts`, …) have no idempotency, no rate-limit signal and no
resumability. `POST /analytics/invocations` is the same calculations as durable jobs with all three. Prefer it for agents.

## Steps

1. Generate a fresh `Idempotency-Key` per logical request and keep it with the request body. Reusing a key with a
   different body returns `409`; a key whose stored result has expired returns `410` — mint a new key in both cases.
2. `create` — `POST /analytics/invocations` with `AnalyticsInvocationCreateRequest`: `operation` is one of
   `COHORT_TRANSACTIONS | COHORTS | DASHBOARD | PRODUCT_DASHBOARD | METRICS | METHODS | TOKENS` and `request` is the matching
   `*InvocationRequest` (e.g. COHORTS needs `contractAddress, interval (daily|weekly|monthly), startDate, endDate`).
   Send `Prefer: wait=N` to block up to N seconds, or `Prefer: respond-async` to return immediately.
   - `200` — finished inside the wait budget; the body is the result.
   - `202` — still running. Read `Location` (status URL), `Retry-After` (seconds) and the body's
     `AnalyticsInvocationStatusResponse.links {self, result, cancel}`.
   - `429` — per-user active-invocation quota or create rate limit hit; honour `Retry-After`.
   - `403` — the bearer cannot access that contract; `404` — invocations are disabled for the account; `400` — bad
     operation/body/Prefer/key; `422` — failed permanently inside the wait budget.
3. `status` — `GET /analytics/invocations/{id}`. Poll at the `Retry-After` / `retryAfterSeconds` cadence. Terminal
   states are `SUCCEEDED | FAILED | CANCELLED | EXPIRED`; `WAITING_DEPENDENCY` means another invocation (`dependencyId`)
   must finish first. `attempt`/`maxAttempts` show server-side retries.
4. `result` — `GET /analytics/invocations/{id}/result`. `200` returns the stored result and does not rerun the
   calculation; `202` not ready; `409` cancelled; `410` expired; `422` failed permanently (read `errorCode`/`errorMessage`
   from the status body).
5. `cancel` — `POST /analytics/invocations/{id}/cancel` when the user no longer needs the answer or to free active
   quota before a 429. `202` accepted, `409` already complete. This is the one reversal with a stated condition
   (before completion); there is no time window.

## Rules

- Never poll faster than `Retry-After`; the 429 on create is the only rate-limit signal in the API and it is per user,
  so a runaway poller starves every other agent on the same account.
- Result retention is finite (`410` exists) but the window is not published — copy the result out on first read.

## Conventions that apply to every step

- Auth: `Authorization: Bearer <JWT>` on every call unless noted. Tokens are issued through the Moirai Labs dashboard (https://moirailabs.com/auth); there is no OAuth flow and no token endpoint in the contract. A missing token returns `401 {"code":"unauthorized","message":"Missing bearer token"}`.
- Base URL: `https://api.moirailabs.com/api/v1` (the spec says `http://`; the host 301s to https — send https from the start so the bearer never travels in the clear).
- Send an `X-Request-ID` (`^[A-Za-z0-9._:-]{1,128}$`) on every call and log the echoed value; it is the only correlation handle the provider offers.
- Errors are `{code, message, details}` over `application/json`, not RFC 9457. See `errors/moirailabs-com-problem-types.yml`.
- Contract identity at the edge is `(chainId, 0x address)`; `address` must be exactly 42 characters.
- No pagination exists: list responses are unbounded arrays.
