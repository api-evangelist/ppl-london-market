# PPL (ppl-london-market)

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
