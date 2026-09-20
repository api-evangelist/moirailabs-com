---
name: moirailabs-com-register-contract
description: Register a smart contract for analytics indexing, wait for the indexer to catch up, and remove it when done.
api: openapi/moirailabs-com-openapi.yml
operations: ['registerContract', 'getContractStatus', 'getUserContracts', 'getContract', 'deleteContract']
method: generated
generated: '2026-09-19'
---
# Register a contract and wait for sync

Every analytics call in this API is keyed on a contract the account has registered, and a plan caps how many
(`PlanResponse.contractAmount`; the live `/plans/active` catalog returns 1/3/5/10 contracts for entusiast/startup/business/enterprise while the pricing page advertises 1 free, 3, 10, 15 and Unlimited — the two disagree, see `plans/moirailabs-com-plans-pricing.yml`) Register first, confirm sync, then query.

## Steps

1. `getUserContracts` — `GET /contracts/user`. Count the array against the plan's `contractAmount` before registering; the
   contract publishes no specific error for an exhausted slot.
2. `registerContract` — `POST /contracts` with `ContractInfoRequest {chainId, address, type?}`. `chainId` is the EIP-155
   integer (1 Ethereum, 137 Polygon, 42161 Arbitrum, 10 Optimism, 8453 Base, 59144 Linea — the chains the site names).
   Response is `ContractInfoResponse` with the platform `id` (uuid) you will need for `getTokenAnalysis`.
3. `getContractStatus` — `GET /contracts/status?contractAddress=0x…`. Poll `ContractSyncStatusResponse` until `syncing`
   is false or `progress` reaches 100 (`currentBlock` vs `targetBlock`). No Retry-After is given here; back off yourself.
4. `getContract` — `GET /contracts/{id}` to re-read the record by uuid when you only stored the id.
5. `deleteContract` — `DELETE /contracts/{contractAddress}` to free the slot. This is the only reversal on this surface
   and the contract states no window; whether indexed history is retained for a re-registration is not documented.

## Idempotency and safety

- `registerContract` carries no `Idempotency-Key`. A retried POST after a timeout may create a duplicate registration;
  re-read `getUserContracts` before retrying rather than retrying blind.
- `deleteContract` is a real destructive action against a plan-metered slot — confirm with the user before calling it in an
  autonomous loop.

## Conventions that apply to every step

- Auth: `Authorization: Bearer <JWT>` on every call unless noted. Tokens are issued through the Moirai Labs dashboard (https://moirailabs.com/auth); there is no OAuth flow and no token endpoint in the contract. A missing token returns `401 {"code":"unauthorized","message":"Missing bearer token"}`.
- Base URL: `https://api.moirailabs.com/api/v1` (the spec says `http://`; the host 301s to https — send https from the start so the bearer never travels in the clear).
- Send an `X-Request-ID` (`^[A-Za-z0-9._:-]{1,128}$`) on every call and log the echoed value; it is the only correlation handle the provider offers.
- Errors are `{code, message, details}` over `application/json`, not RFC 9457. See `errors/moirailabs-com-problem-types.yml`.
- Contract identity at the edge is `(chainId, 0x address)`; `address` must be exactly 42 characters.
- No pagination exists: list responses are unbounded arrays.
