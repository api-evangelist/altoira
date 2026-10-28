# AltoIRA

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

Alto (AltoIRA) is a Nashville-based self-directed IRA platform that lets everyday investors hold alternative assets — private equity, venture funds, startups, real estate, farmland, private credit and cryptocurrency — inside tax-advantaged Traditional, Roth and SEP retirement accounts. Alto Trust Company acts as the IRA custodian and Alto Securities, LLC (FINRA/SIPC) operates the Alto Marketplace of curated private-market offerings. Alto reports custody of roughly $2B in assets for about 30,000 self-directed IRA investors and support for more than 2,500 issuers who have raised capital on the platform. For issuers and investment platforms, Alto publishes a partner REST API (the "AltoIRA.com API") on a ReadMe developer hub that covers OAuth investor handoff, offering creation, document upload, investor invitation, investment retrieval, refunds, cancellations, distributions and capital calls, plus an investment-status webhook feed.

**Areas:** Company · Financial Services · Retirement · Self-Directed IRA · Alternative Investments · Private Markets · Fintech · Custody · Cryptocurrency · Wealth Management · Investing · Capital Raising

## AltoIRA on APIs.io

Everything profiled for AltoIRA is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/altoira/](https://apis.io/providers/altoira/)** — or go straight to one of the APIs or properties below.

### APIs (5)

- [AltoIRA Handoffs API](https://apis.io/apis/altoira/altoira-handoffs-api/) — These are the endpoints you will redirect your investors to (these are NOT api endpoints so you cannot use the Try it out tool)
- [AltoIRA Investment API](https://apis.io/apis/altoira/altoira-investment-api/) — The actions are performed as the manager of an offering, not as a specific user. Authentication uses the `Basic Auth` header (same as the Offering endpoints)
- [AltoIRA Offering API](https://apis.io/apis/altoira/altoira-offering-api/) — The actions are performed as the manager of an offering, not as a specific user. Authentication uses the `Basic Auth` header
- [AltoIRA User API](https://apis.io/apis/altoira/altoira-user-api/) — These actions are performed within the context of a specific user (uses OAuth2 with an `Authorization: Bearer` header)
- [AltoIRA OAUTH API](https://apis.io/apis/altoira/altoira-oauth-api/) — Provides access to an investor's account. Generates a token to be used with the "user" endpoints below

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (2)

Event-driven and webhook contracts.

- [Alto Investment Status Webhooks](https://apis.io/asyncapis/altoira/altoira-investments-asyncapi/)
- [Altoira Investments Webhooks](https://apis.io/asyncapis/altoira/altoira-investments-webhooks/)

#### Event channels (1)

Individual events and webhooks the provider emits.

- [/](https://apis.io/channels/altoira/investmentevents/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [altoira](https://apis.io/servers/altoira/altoira/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Altoira Agentic Access](https://apis.io/agentic-access/altoira/altoira-agentic-access/)

#### Collections (5)

Postman and Open Collection request collections.

- [AltoIRA.com Handoffs API](https://apis.io/collections/altoira/open-altoira-handoffs-api/)
- [AltoIRA.com Investment API](https://apis.io/collections/altoira/open-altoira-investment-api/)
- [AltoIRA.com OAUTH API](https://apis.io/collections/altoira/open-altoira-oauth-api/)
- [AltoIRA.com Offering API](https://apis.io/collections/altoira/open-altoira-offering-api/)
- [AltoIRA.com User API](https://apis.io/collections/altoira/open-altoira-user-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Altoira Partner Api Overlay](https://apis.io/overlays/altoira/altoira-partner-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Altoira Authentication](https://apis.io/security/altoira/altoira-authentication/)
- [Altoira Domain Security](https://apis.io/security/altoira/altoira-domain-security/)
- [Altoira Trust Center](https://apis.io/security/altoira/altoira-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Altoira Scopes](https://apis.io/scopes/altoira/altoira-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.altoira.com/)
- [Documentation](https://readme.altoira.com/docs/understand-the-oauth-process-to-alto)
- [Getting started](https://readme.altoira.com/docs/understand-the-oauth-process-to-alto)
- [API reference](https://readme.altoira.com/reference)
- [Pricing](https://www.altoira.com/pricing)
- [Sign up](https://app.altoira.com/register)
- [Support](https://www.altoira.com/help-center)
- [Blog](https://www.altoira.com/insights)
- [Trust centre](https://trust.altoira.com/)
- [Terms of service](https://www.altoira.com/terms-of-service)
- [Privacy policy](https://www.altoira.com/privacy-policy)
- [GitHub](https://github.com/AltoIRA)
- [Status](https://status.altoira.com/)

## API Evangelist rating

**Kin Score 46.7** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 53.8 |
| Contract governance | 4.5 |
| Operational transparency | 26.3 |
| Developer ergonomics | 47.0 |
| Access clarity | 38.2 |

**Agent readiness 42.3** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 34.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/altoira/](https://apis.io/providers/altoira/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for AltoIRA: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/altoira/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
