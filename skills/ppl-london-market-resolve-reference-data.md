---
name: Resolve London Market reference data before placing
description: >-
  Prerequisite lookup flow. Resolve broker and carrier organisations, market facilities, market
  underwriters and underwriter stamps from the PPL Next Gen Organisations API before touching any
  Placement or Firm Order resource.
api: openapi/ppl-london-market-organisations.json
base_url: https://api.londonmarketgroup.co.uk/ppl/nextgen/organisations/v1
generated: '2026-07-25'
method: generated
source: openapi/ppl-london-market-organisations.json + conventions/ppl-london-market-conventions.yml
operations:
  - brokerOrganisations_v1
  - carrierOrganisations_v1
  - brokerMarkets_Facilities_v1
  - brokerMarkets_Underwriters_v1
  - brokerMarkets_Stamps_v1
---

# Resolve London Market reference data

PPL states that the organisation reference data held in the platform is a **prerequisite** for
interacting with Placement and Firm Order resources. Run this flow first; never hand-write a
carrier name, underwriter email, team id, facility panel id or stamp into a placement call.

## Before you start

Entra ID bearer token with `scp: user_impersonation` and the environment's registered X.509 client
certificate. `X-Auth-Impersonated-User` is required on all five operations;
`X-Auth-Team` is additionally required on the three market operations
(`brokerMarkets_Facilities_v1`, `brokerMarkets_Underwriters_v1`, `brokerMarkets_Stamps_v1`) but not
on the two organisation lookups.

## Steps

1. **Resolve the broking firm.** `GET /brokerOrganisations` — `brokerOrganisations_v1`. Filter with
   `companyId`, `search`, `placementId`; page with `pageNumber` / `pageSize`, sort with `sort`.
   Take the team ids and team names from here — they are what `X-Auth-Team` expects on subsequent
   calls.
2. **Resolve the carrier.** `GET /carrierOrganisations` — `carrierOrganisations_v1`. Same filter
   shape, including `offPlatform` for carriers who are not on the platform.
3. **List the facilities available to the broker.** `GET /marketFacilities` —
   `brokerMarkets_Facilities_v1`. Use the returned facility panel identifiers when a section is
   placed against a facility rather than the open market.
4. **List the underwriters.** `GET /marketUnderwriters` — `brokerMarkets_Underwriters_v1`. Filter
   with `underwriterEmail`, `search`, `placementId`, `offPlatform`. Underwriters are addressed by
   **email**, so this lookup is what makes a participation valid.
5. **Get that underwriter's stamps.** `GET /marketUnderwriters/{underwriterEmail}/stamps` —
   `brokerMarkets_Stamps_v1`. Stamps carry agency type, agency code, stamp role and risk codes.
   The stamp you attach to a negotiation must come from this call.

## Rules you must follow

- **Everything here is read-only.** All five operations are GET. Nothing in this skill changes
  market state, so it is safe to run before asking a human to approve a write.
- **Cache carefully.** Reference data changes slowly but it does change — teams, stamps and
  facility panels are amended. Re-resolve at the start of each placement rather than reusing a
  cached identifier from an earlier session.
- **Never fabricate a market identifier.** Underwriter emails, agency codes, stamp ids, team ids
  and facility panel ids must all originate from a response to one of these calls.
- **Errors.** `{ "errors": [ { "code", "message", "field", "argument" } ] }`; declared statuses
  400, 401, 404, 414, 429, 500. A 404 with `INVALID_ROLE_OR_TEAM` usually means the
  `X-Auth-Team` / `X-Auth-Impersonated-User` pair is wrong, not that the organisation is missing.
- **Health check.** Both `/health` (anonymous) and `/version` (authenticated) exist on this API if
  you need to confirm reachability before a run.
