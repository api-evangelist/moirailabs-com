---
name: moirailabs-com-cohort-and-method-report
description: Produce a cohort retention and method-usage report for a registered contract from the synchronous analytics endpoints and the daily reports.
api: openapi/moirailabs-com-openapi.yml
operations: ['getCohortAnalysis', 'getMethodAnalysis', 'getProductMetrics', 'getReports', 'getCohortTransactions']
method: generated
generated: '2026-09-19'
---
# Build a cohort + method report for a contract

Mirrors the A2A skills `analytics.cohorts`, `analytics.methods`, `analytics.metrics`, `analytics.transactions` and
`reports.daily` (see `mcp/moirailabs-com-tool-crosswalk.yml`). Use this when the caller wants an answer now and accepts
the synchronous endpoints' limits; use the async-invocation skill for anything long-running or retried.

## Steps

1. `getProductMetrics` — `GET /analytics/metrics?contractAddress=0x…` → `ProductMetricsResponse` (headline KPIs).
2. `getCohortAnalysis` — `GET /analytics/cohorts?contractAddress&interval&startDate&endDate` → `CohortAnalysisResponse`
   with `CohortData[]`. `interval` is `daily|weekly|monthly`; dates are `YYYY-MM-DD`. This operation additionally declares
   an explicit required `Authorization` header parameter — send the same bearer.
3. `getMethodAnalysis` — `GET /analytics/methods?contractAddress` → `MethodAnalysisResponse` (per-method call breakdown).
4. `getCohortTransactions` — `GET /analytics/cohort-transactions?contractAddress&period&granularity` →
   `TransactionWithCohort[]` when the report needs transaction-level rows.
5. `getReports` — `GET /api/reports/daily/{contractAddress}` → `DailyReportResponse[]` (dau, newWalletsAmount,
   failedTx, gasUsed, `methodsByCohorts`). Weekly/monthly rollups are not served — aggregate the daily rows yourself; the
   A2A skills `reports.weekly` and `reports.monthly` have no REST counterpart.

## Rules

- All five are reads: idempotent and safe to retry, but there is no rate-limit header on them — space calls out and treat
  a 429 (undocumented here) like the invocation 429.
- The contract must be registered and synced first (`getContractStatus.syncing == false`), otherwise numbers are partial;
  the API does not flag partial data on these endpoints.
- Several `DailyReportResponse` fields (`usersByCohorts`, `methodsByCohorts`, `txsPerDayByMethods`) are JSON serialized
  inside strings — parse them before charting.

## Conventions that apply to every step

- Auth: `Authorization: Bearer <JWT>` on every call unless noted. Tokens are issued through the Moirai Labs dashboard (https://moirailabs.com/auth); there is no OAuth flow and no token endpoint in the contract. A missing token returns `401 {"code":"unauthorized","message":"Missing bearer token"}`.
- Base URL: `https://api.moirailabs.com/api/v1` (the spec says `http://`; the host 301s to https — send https from the start so the bearer never travels in the clear).
- Send an `X-Request-ID` (`^[A-Za-z0-9._:-]{1,128}$`) on every call and log the echoed value; it is the only correlation handle the provider offers.
- Errors are `{code, message, details}` over `application/json`, not RFC 9457. See `errors/moirailabs-com-problem-types.yml`.
- Contract identity at the edge is `(chainId, 0x address)`; `address` must be exactly 42 characters.
- No pagination exists: list responses are unbounded arrays.
