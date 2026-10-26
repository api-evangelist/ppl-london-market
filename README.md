# PPL (ppl-london-market)

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

PPL (Placing Platform Limited) is the London Market's not-for-profit electronic placing platform, incorporated in England and Wales in 2013 and trading since the first risk was bound on the platform in July 2016. Owned collectively by the market it serves, PPL lets brokers and carriers quote, negotiate, bind and renew open-market (re)insurance risks electronically across almost all classes of business written in London, and is used by roughly 200 carriers and 200 broking firms. It is market infrastructure rather than a carrier or a broker — it writes no insurance and carries no risk — and it is one of the accredited placing platforms underpinning Lloyd's Blueprint Two, generating the Core Data Record for bound business.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/ppl-london-market/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/ppl-london-market/refs/heads/main/apis.yml)

## API Posture

PPL is the counter-example to the rule that insurance is not API-native. The [PPL Next Gen API Developer Portal](https://developer.pplnextgen.com/) is publicly readable and publishes a real API catalogue of five REST collections — Organisations, Placements, Submissions, Documents and Events — each with a downloadable OpenAPI 3.0 document and a Postman collection. The APIs are built on REST standards and the ACORD GRLC (Global Reinsurance and Large Commercial) data model, and a live ACORD Solutions Group ADEPT Placing data-exchange gateway runs in production with AXA XL.

It is not, however, self-serve. Reading the documentation is open; calling the APIs is market-gated behind three sequential gates:

1. Developer Portal onboarding, by request to the PPL team.
2. Subscription to LIMOSS API Common Services, and guesting of the account identity into the LIMOSS API Gateway Microsoft Entra ID (Azure AD) tenant — separately for each of the Sand, PreProd and Prod environments.
3. Registration of an X.509 client certificate per API Gateway environment.

There are no API keys, no free tier, no public sandbox credentials, and no self-service signup.

Of the four insurance API verbs, PPL covers **quote** (Submissions API), **bind** (Placements API) and **issue** (Documents API, over the Market Reform Contract). It has **no FNOL or claims surface** — London Market claims run through separate infrastructure. Everything is partner-facing: brokers and carriers, never consumers.

There is no webhook catalogue, no callbacks in any specification, and no AsyncAPI. The Events API is pull-only.

> **Note on identity:** `pplfirst.com` is **not** this company. That domain belongs to PPL First / Public Partnerships LLC, a US Medicaid self-directed-care financial management services provider. The London Market PPL is Placing Platform Limited at `placingplatformlimited.com`, with its platform and developer portal on `pplnextgen.com`.

## Tags

- Insurance
- United Kingdom
- London Market
- Lloyd's of London
- Reinsurance
- Commercial Insurance
- Broker
- Underwriting
- Placement
- Market Infrastructure
- ACORD
- Electronic Placing

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## APIs

### PPL Placements API

Manages the Placement structure in PPL Next Gen — Placements, Programmes, Contracts and the Sections within a Contract — together with carrier and underwriter participations, role assignment, and the broker-side negotiation of terms. This is the bind-side surface of the platform. OpenAPI 3.0.1, 16 paths and 32 operations.

- **Human URL:** [https://developer.pplnextgen.com/placements](https://developer.pplnextgen.com/placements)
- **Base URL:** `https://api.londonmarketgroup.co.uk/ppl/nextgen/placements/v1`
- **OpenAPI:** [openapi/ppl-london-market-placements.json](openapi/ppl-london-market-placements.json)

### PPL Submissions API

Enables underwriters to retrieve Submission requests supplied by a broker and to manage their negotiation of terms of cover, including reassignment of a negotiation and sending a response back to the broker. This is the quote-side surface of the platform. OpenAPI 3.0.1, 8 paths and 10 operations.

- **Human URL:** [https://developer.pplnextgen.com/submissions](https://developer.pplnextgen.com/submissions)
- **Base URL:** `https://api.londonmarketgroup.co.uk/ppl/nextgen/submissions/v1`
- **OpenAPI:** [openapi/ppl-london-market-submissions.json](openapi/ppl-london-market-submissions.json)

### PPL Organisations API

Retrieves the organisation reference data held in the platform that is a prerequisite for interacting with Placement and Firm Order resources — broker and carrier organisations, their team structures, members and roles, market facilities, market underwriters and underwriter stamps. OpenAPI 3.0.1, 7 paths and 7 operations.

- **Human URL:** [https://developer.pplnextgen.com/organisations](https://developer.pplnextgen.com/organisations)
- **Base URL:** `https://api.londonmarketgroup.co.uk/ppl/nextgen/organisations/v1`
- **OpenAPI:** [openapi/ppl-london-market-organisations.json](openapi/ppl-london-market-organisations.json)

### PPL Documents API

Manages document files and document metadata across the Placement hierarchy, including the Market Reform Contract (MRC) itself and its supporting documents, with versioning, content retrieval, download and a separate secured content and download path. This is the contract-issuance surface. OpenAPI 3.0.1, 8 paths and 11 operations.

- **Human URL:** [https://developer.pplnextgen.com/documents](https://developer.pplnextgen.com/documents)
- **Base URL:** `https://api.londonmarketgroup.co.uk/ppl/nextgen/documents/v1`
- **OpenAPI:** [openapi/ppl-london-market-documents.json](openapi/ppl-london-market-documents.json)

### PPL Events API

Retrieves informative and actionable notifications about an interested party's involvement in the placement process, plus the business transaction log for contract-related engagements. Pull-based only — notifications and transactions are polled over REST; PPL publishes no webhook, callback or AsyncAPI event-push surface. OpenAPI 3.0.1, 7 paths and 7 operations.

- **Human URL:** [https://developer.pplnextgen.com/events](https://developer.pplnextgen.com/events)
- **Base URL:** `https://api.londonmarketgroup.co.uk/ppl/nextgen/events/v1`
- **OpenAPI:** [openapi/ppl-london-market-events.json](openapi/ppl-london-market-events.json)

## Links

- [Website](https://placingplatformlimited.com/)
- [Developer Portal](https://developer.pplnextgen.com/)
- [API Catalogue](https://developer.pplnextgen.com/Explore-Innovate)
- [Get Started](https://developer.pplnextgen.com/Get-Started)
- [Authentication Information](https://developer.pplnextgen.com/Get-Started/Authentication-Information)
- [Registration and Onboarding](https://developer.pplnextgen.com/Get-Started/Registration-Onboarding)
- [API Integrations (marketing)](https://placingplatformlimited.com/api-integrations/)
- [Platform Login](https://www.pplnextgen.com/PPL_Authentication/)
- [Blog](https://placingplatformlimited.com/blog/)
- [LinkedIn](https://www.linkedin.com/company/ppl-placing-platform-limited/)
