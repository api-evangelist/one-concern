# One Concern

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

One Concern is a Palo Alto, California climate-resilience analytics company that builds a digital twin of the built environment to quantify physical climate and natural-catastrophe risk in units of time rather than broad-brush hazard bands. Its Domino AI platform models the recovery of an individual building together with the lifelines it depends on — power distribution, ports, airports, roads and bridges, the surrounding residential community — and returns business-interruption downtime statistics, property-damage ratios and a 1CRX resilience score for a given latitude and longitude, per peril (flood, tropical-cyclone wind, seismic ground shaking, or all perils integrated), per return period or planning horizon, and under baseline or 2050 climate-change scenarios. The company sells to insurers, reinsurers, financial services and real estate, and exposes the platform to customers through the Domino AI API, a five-operation REST contract documented at developer.oneconcern.com and served from api.oneconcern.com behind a Tyk gateway with a customer-issued x-1c-api-token header.

**Areas:** Climate Risk · Catastrophe Modeling · Resilience · Insurance · Reinsurance · Risk Analytics · Geospatial · Business Interruption · Real Estate · Financial Services · Artificial Intelligence

## One Concern on APIs.io

Everything profiled for One Concern is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/one-concern/](https://apis.io/providers/one-concern/)** — or go straight to one of the APIs or properties below.

### APIs (1)

- [One Concern Location API](https://apis.io/apis/one-concern/one-concern-location-api/) — The Location API from One Concern — 5 operation(s) for location.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [One Concern Domino Ai Overlay](https://apis.io/overlays/one-concern/one-concern-domino-ai-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [One Concern Authentication](https://apis.io/security/one-concern/one-concern-authentication/)
- [One Concern Domain Security](https://apis.io/security/one-concern/one-concern-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [One Concern Plans Pricing](https://apis.io/plans/one-concern/one-concern-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [One Concern Rate Limits](https://apis.io/rate-limits/one-concern/one-concern-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://oneconcern.com/en/)
- [Documentation](https://developer.oneconcern.com/overview)
- [Getting started](https://developer.oneconcern.com/overview)
- [API reference](https://developer.oneconcern.com/api-spec)
- [Support](https://oneconcern.com/en/contact/)
- [Blog](https://oneconcern.com/en/news/)
- [Terms of service](https://oneconcern.com/en/terms/)
- [Privacy policy](https://oneconcern.com/en/privacy/)
- [GitHub](https://github.com/oneconcern)

## API Evangelist rating

**Kin Score 33.8** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 66.1 |
| Contract quality | 41.6 |
| Contract governance | 4.5 |
| Operational transparency | 2.6 |
| Developer ergonomics | 58.9 |
| Access clarity | 21.1 |

**Agent readiness 27.5** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 20.5** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/one-concern/](https://apis.io/providers/one-concern/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for One Concern: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/one-concern/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
