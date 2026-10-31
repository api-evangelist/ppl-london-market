# PPL

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

PPL (Placing Platform Limited) is the London Market's not-for-profit electronic placing platform, incorporated in England and Wales in 2013 and trading since the first risk was bound on the platform in July 2016. Owned collectively by the market it serves, PPL lets brokers and carriers quote, negotiate, bind and renew open-market (re)insurance risks electronically across almost all classes of business written in London, and is used by roughly 200 carriers and 200 broking firms. It is market infrastructure rather than a carrier or a broker - it writes no insurance and carries no risk - and it is one of the accredited placing platforms underpinning Lloyd's Blueprint Two, generating the Core Data Record for bound business. Its API posture is unusual for insurance and genuinely good: the PPL Next Gen API Developer Portal at developer.pplnextgen.com is publicly readable and publishes a real API catalogue of five REST collections - Organisations, Placements, Submissions, Documents and Events - each with a downloadable OpenAPI 3.0 document and a Postman collection, built on REST standards and the ACORD GRLC (Global Reinsurance and Large Commercial) data model. Actually calling the APIs is market-gated rather than self-serve: consumers must be onboarded by PPL, subscribe to LIMOSS API Common Services, be guested into the Microsoft Entra ID (Azure AD) tenant of the LIMOSS API Gateway, and register an X.509 certificate per environment. The surface covers quote and bind (submission negotiation, contract negotiation, participations, firm order) and contract issuance via the Market Reform Contract document set; there is no claims or FNOL API, and no webhook or event-push surface - the Events API is pull-based.

**Areas:** Insurance · United Kingdom · London Market · Lloyd's of London · Reinsurance · Commercial Insurance · Brokerage · Underwriting · Placement · Market Infrastructure · ACORD · Electronic Placing

## PPL on APIs.io

Everything profiled for PPL is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/ppl-london-market/](https://apis.io/providers/ppl-london-market/)** — or go straight to one of the APIs or properties below.

### APIs (13)

- [PPL Contract API](https://apis.io/apis/ppl-london-market/ppl-london-market-contract-api/) — Enables the creation and management of Contract structured data.
- [PPL Document API](https://apis.io/apis/ppl-london-market/ppl-london-market-document-api/) — The document API from PPL — 6 operation(s) for document.
- [PPL Health API](https://apis.io/apis/ppl-london-market/ppl-london-market-health-api/) — The health API from PPL — 1 operation(s) for health.
- [PPL Negotiation API](https://apis.io/apis/ppl-london-market/ppl-london-market-negotiation-api/) — Enables the creation and management of the flow of negotiations from a Broker to an Underwriter. Negotiations shown will be those which (1) have been…
- [PPL Notification API](https://apis.io/apis/ppl-london-market/ppl-london-market-notification-api/) — The notification API from PPL — 3 operation(s) for notification.
- [PPL Organisation API](https://apis.io/apis/ppl-london-market/ppl-london-market-organisation-api/) — The organisation API from PPL — 5 operation(s) for organisation.
- [PPL Participation API](https://apis.io/apis/ppl-london-market/ppl-london-market-participation-api/) — Enables the creation, management and processing of Open Market Underwriters and Facility Panel Underwriters that are willing to participate in the…
- [PPL Placement API](https://apis.io/apis/ppl-london-market/ppl-london-market-placement-api/) — Enables the creation and management of the Placement structure that comprises of Programmes and Contracts.
- [PPL Programme API](https://apis.io/apis/ppl-london-market/ppl-london-market-programme-api/) — Enables the creation and management of Programme structures within a Placement. This also includes the capability to add existing Contracts into a programme.
- [PPL Section API](https://apis.io/apis/ppl-london-market/ppl-london-market-section-api/) — Enables the creation and management of Contract sections, as structured data. Each Section represents of a specific partition of the overall risk to be…
- [PPL Submission API](https://apis.io/apis/ppl-london-market/ppl-london-market-submission-api/) — Enables the retrieval of Submissions for Underwriters.
- [PPL Transaction API](https://apis.io/apis/ppl-london-market/ppl-london-market-transaction-api/) — The transaction API from PPL — 2 operation(s) for transaction.
- [PPL Version API](https://apis.io/apis/ppl-london-market/ppl-london-market-version-api/) — The version API from PPL — 1 operation(s) for version.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [ppl-nextgen](https://apis.io/servers/ppl-london-market/ppl-nextgen/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Ppl London Market Agentic Access](https://apis.io/agentic-access/ppl-london-market/ppl-london-market-agentic-access/)

#### Collections (5)

Postman and Open Collection request collections.

- [document](https://apis.io/collections/ppl-london-market/open-ppl-london-market-documents/)
- [event](https://apis.io/collections/ppl-london-market/open-ppl-london-market-events/)
- [organisation](https://apis.io/collections/ppl-london-market/open-ppl-london-market-organisations/)
- [placement](https://apis.io/collections/ppl-london-market/open-ppl-london-market-placements/)
- [submission](https://apis.io/collections/ppl-london-market/open-ppl-london-market-submissions/)

#### Overlays (5)

OpenAPI overlays, including conversational phrasing for each operation.

- [Ppl London Market Documents Overlay](https://apis.io/overlays/ppl-london-market/ppl-london-market-documents-overlay/)
- [Ppl London Market Events Overlay](https://apis.io/overlays/ppl-london-market/ppl-london-market-events-overlay/)
- [Ppl London Market Organisations Overlay](https://apis.io/overlays/ppl-london-market/ppl-london-market-organisations-overlay/)
- [Ppl London Market Placements Overlay](https://apis.io/overlays/ppl-london-market/ppl-london-market-placements-overlay/)
- [Ppl London Market Submissions Overlay](https://apis.io/overlays/ppl-london-market/ppl-london-market-submissions-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Ppl London Market Authentication](https://apis.io/security/ppl-london-market/ppl-london-market-authentication/)
- [Ppl London Market Domain Security](https://apis.io/security/ppl-london-market/ppl-london-market-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Ppl London Market Scopes](https://apis.io/scopes/ppl-london-market/ppl-london-market-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://placingplatformlimited.com/)
- [Documentation](https://developer.pplnextgen.com/Get-Started)
- [Getting started](https://developer.pplnextgen.com/Get-Started)
- [API reference](https://developer.pplnextgen.com/Explore-Innovate)
- [Sign up](https://developer.pplnextgen.com/Get-Started/Registration-Onboarding)
- [Support](https://developer.pplnextgen.com/Support)
- [Blog](https://placingplatformlimited.com/blog/)
- [Terms of service](https://developer.pplnextgen.com/Terms-And-Conditions)
- [Privacy policy](https://placingplatformlimited.com/privacy-notice/)

## API Evangelist rating

**Kin Score 45.3** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 48.9 |
| Contract governance | 4.5 |
| Operational transparency | 5.3 |
| Developer ergonomics | 70.8 |
| Access clarity | 34.2 |

**Agent readiness 29.0** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | — |

**Regulatory alignment 41.2** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/ppl-london-market/](https://apis.io/providers/ppl-london-market/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for PPL: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/ppl-london-market/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
