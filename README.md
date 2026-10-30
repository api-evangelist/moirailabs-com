# Moirai Labs

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Moirai Labs is a smart-contract analytics platform for Web3 teams that turns raw EVM chain data (Ethereum, Polygon, Arbitrum, Optimism, Base, Linea) into product-grade metrics: cohort retention, method-level call breakdowns, daily reports, product dashboards and wallet profiling. The same credit-metered core is exposed three ways — a bearer-JWT REST API described by an OpenAPI 3.0.1 document with 36 operations (including durable, idempotent asynchronous analytics invocations), an A2A 1.0 agent ("Moirai Agents API", 11 skills, registered in the A2A Registry) and an MCP bridge on the agent host — alongside an OpenAI ai-plugin.json manifest, llms.txt and an RFC 9116 security.txt. Subscription plans meter contracts under analysis per 30-day period; the plan catalog is served anonymously by the API.

**Areas:** Company · Blockchain · Smart Contracts · Web3 · Analytics · cohort-analysis · Wallet Profiling · Ethereum · AI Agents · A2A · MCP · Agent-Native

## Moirai Labs on APIs.io

Everything profiled for Moirai Labs is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/moirailabs-com/](https://apis.io/providers/moirailabs-com/)** — or go straight to one of the APIs or properties below.

### APIs (10)

- [Moirai Agents API (A2A + MCP)](https://apis.io/apis/moirailabs-com/moirai-agents-api/) — A2A 1.0 agent ("A2A-compatible analytics and contract intelligence agent", version 0.1.0) with 11 skills —…
- [Moirai Labs Analytics Controller API](https://apis.io/apis/moirailabs-com/moirailabs-com-analytics-controller-api/) — The analytics-controller API from Moirai Labs — 7 operation(s) for analytics-controller.
- [Moirai Labs Analytics Invocation Controller API](https://apis.io/apis/moirailabs-com/moirailabs-com-analytics-invocation-controller-api/) — The analytics-invocation-controller API from Moirai Labs — 4 operation(s) for analytics-invocation-controller.
- [Moirai Labs Contract Info Controller API](https://apis.io/apis/moirailabs-com/moirailabs-com-contract-info-controller-api/) — The contract-info-controller API from Moirai Labs — 6 operation(s) for contract-info-controller.
- [Moirai Labs Functions Controller API](https://apis.io/apis/moirailabs-com/moirailabs-com-functions-controller-api/) — The functions-controller API from Moirai Labs — 1 operation(s) for functions-controller.
- [Moirai Labs Plan Controller API](https://apis.io/apis/moirailabs-com/moirailabs-com-plan-controller-api/) — The plan-controller API from Moirai Labs — 3 operation(s) for plan-controller.
- [Moirai Labs Report Controller API](https://apis.io/apis/moirailabs-com/moirailabs-com-report-controller-api/) — The report-controller API from Moirai Labs — 1 operation(s) for report-controller.
- [Moirai Labs Subscription Controller API](https://apis.io/apis/moirailabs-com/moirailabs-com-subscription-controller-api/) — The subscription-controller API from Moirai Labs — 2 operation(s) for subscription-controller.
- [Moirai Labs User Info Controller API](https://apis.io/apis/moirailabs-com/moirailabs-com-user-info-controller-api/) — The user-info-controller API from Moirai Labs — 3 operation(s) for user-info-controller.
- [Moirai Labs Wallet Profiling Controller API](https://apis.io/apis/moirailabs-com/moirailabs-com-wallet-profiling-controller-api/) — The wallet-profiling-controller API from Moirai Labs — 4 operation(s) for wallet-profiling-controller.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [moirailabs-com-mcp.yml](https://apis.io/servers/moirailabs-com/moirailabs-com-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Moirailabs Com Agentic Access](https://apis.io/agentic-access/moirailabs-com/moirailabs-com-agentic-access/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Moirailabs Com Openapi Overlay](https://apis.io/overlays/moirailabs-com/moirailabs-com-openapi-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Moirailabs Com Authentication](https://apis.io/security/moirailabs-com/moirailabs-com-authentication/)
- [Moirailabs Com Domain Security](https://apis.io/security/moirailabs-com/moirailabs-com-domain-security/)
- [Moirailabs Com Vulnerability Disclosure](https://apis.io/security/moirailabs-com/moirailabs-com-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Moirailabs Com Plans Pricing](https://apis.io/plans/moirailabs-com/moirailabs-com-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Moirailabs Com Rate Limits](https://apis.io/rate-limits/moirailabs-com/moirailabs-com-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://moirailabs.com/)
- [Documentation](https://moirailabs.com/a2a)
- [Pricing](https://moirailabs.com/pricing)
- [Sign up](https://moirailabs.com/auth)
- [Support](https://moirailabs.featurebase.app/en/help)
- [Blog](https://moirailabs.com/blog)
- [Terms of service](https://moirailabs.com/terms)
- [Privacy policy](https://moirailabs.com/privacy)
- [GitHub](https://github.com/moirailabs)

## API Evangelist rating

**Kin Score 49.5** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 48.9 |
| Contract governance | 4.5 |
| Operational transparency | 52.6 |
| Developer ergonomics | 30.4 |
| Access clarity | 76.3 |

**Agent readiness 49.6** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | verified |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | verified |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly |

**Regulatory alignment 31.3** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/moirailabs-com/](https://apis.io/providers/moirailabs-com/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Moirai Labs: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/moirailabs-com/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
