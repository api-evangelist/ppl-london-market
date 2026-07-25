---
name: Place a risk on PPL — placement to bound contract
description: >-
  Broker-side flow. Build the placement hierarchy (Placement → Programme → Contract → Section),
  add carrier participations, negotiate terms and send the negotiation to the market, using the
  PPL Next Gen Placements API.
api: openapi/ppl-london-market-placements.json
base_url: https://api.londonmarketgroup.co.uk/ppl/nextgen/placements/v1
generated: '2026-07-25'
method: generated
source: openapi/ppl-london-market-placements.json + conventions/ppl-london-market-conventions.yml
operations:
  - Placement_Post_v1
  - Programme_Post_v1
  - Contract_Post_v1
  - Section_Post_v1
  - Participation_Post_v1
  - Negotiation_Post_v1
  - Negotiation_Send_v1
  - Contract_AssignRoles_v1
  - Placement_GetById_v1
  - Contract_GetById_v1
  - Negotiation_GetById_v1
---

# Place a risk on PPL

You are acting as a **broker** on the London Market's PPL Next Gen platform. This is real
(re)insurance placement — every write below creates or changes a market record that other firms
see. Treat every step as consequential.

## Before you start

You cannot call this API without completed market onboarding. There is no API key and no
self-serve signup. Confirm all of the following, and stop if any is missing:

- A Microsoft Entra ID (Azure AD) bearer token whose `scp` claim includes `user_impersonation`.
  If your sign-in token lacks it, acquire an on-behalf-of token before calling.
- The registered X.509 client certificate for the environment you are calling (Sand, PreProd and
  Prod each need their own).
- The `X-Auth-Impersonated-User` (the market user you act for) and `X-Auth-Team` (their broker
  team) header values. A wrong pair returns **404 with `INVALID_ROLE_OR_TEAM`**, not 403.

Full detail: `authentication/ppl-london-market-authentication.yml`.

## Steps

1. **Create the placement.** `POST /placements` — `Placement_Post_v1`. Body: `client_name`,
   `description`, `effective_year`, `user_email`. Keep the returned `placement_id`.
2. **Add a programme.** `POST /placements/{placementId}/programmes` — `Programme_Post_v1`.
   Keep the `programme_id`.
3. **Create the contract.** `POST /contracts` — `Contract_Post_v1`. This is the object the market
   recognises by its Unique Market Reference (UMR). Keep the `contract_id`.
4. **Add sections.** `POST /contracts/{contractId}/sections` — `Section_Post_v1`. Sections are the
   unit carriers actually write lines against. Keep each `section_id`.
5. **Assign roles on the contract** where required: `POST /contracts/{contractId}/assignRoles` —
   `Contract_AssignRoles_v1`.
6. **Add carrier participations.**
   `POST /contracts/{contractId}/sections/{sectionId}/participations` — `Participation_Post_v1`.
   Resolve the carrier, underwriter and stamp first from the Organisations API (see the
   `resolve-market-reference-data` skill) — do not guess an underwriter email or a stamp.
7. **Open the negotiation.** `POST /contracts/{contractId}/negotiations` — `Negotiation_Post_v1`.
   The body carries `written`, `roles`, `stamps`, `subjectivities` and `contract_document`.
8. **Send it to the market.**
   `POST /contracts/{contractId}/negotiations/{negotiationId}/send` — `Negotiation_Send_v1`.
   **This operation requires the `X-Last-Modified` header** — read the negotiation first with
   `Negotiation_GetById_v1` and carry its last-modified value forward. This is the point of no
   return: the negotiation becomes visible to the carrier. Confirm with a human before calling it.
9. **Track the response.** Poll the Submissions/Placements negotiation resources, or the Events
   API (`Notification_GetAll_v1`) — PPL has no webhooks, so polling is the only option.

## Rules you must follow

- **Concurrency, not idempotency keys.** There is no `Idempotency-Key` header. Every `PUT`
  (`Placement_Put_v1`, `Programme_Put_v1`, `Contract_Put_v1`, `Section_Put_v1`,
  `Participation_Put_v1`, `Negotiation_Put_v1`) and `Negotiation_Send_v1` requires the
  **`X-Last-Modified`** request header, taken from a fresh read of the resource. A stale value
  fails the precondition rather than overwriting another firm's edit. Never retry a `POST` blindly
  — POSTs are not idempotent and a blind retry can create a duplicate placement, section or
  negotiation.
- **Read before you write.** Always `GET` the resource (`Placement_GetById_v1`,
  `Contract_GetById_v1`, `Negotiation_GetById_v1`) immediately before an update, both to get the
  current state and to obtain the concurrency value.
- **Errors.** All failures return the same envelope: `{ "errors": [ { "code", "message", "field",
  "argument" } ] }` — not RFC 9457 problem+json. Known codes: `MANDATORY_PARAMETER`,
  `UNAUTHENTICATED`, `INVALID_PARAMETER_FORMAT`, `INVALID_ROLE_OR_TEAM`. Declared statuses are
  400, 401, 404, 414, 429, 500. **414 is real here** — the collection filters are wide, so keep
  query strings short. See `errors/ppl-london-market-problem-types.yml`.
- **Throttling.** 429 is declared on every business operation. Back off and retry; PPL publishes
  no limit values, and quotas are set per consumer in the LIMOSS API Gateway subscription.
- **Pagination.** Collections take `pageNumber` and `pageSize` and return `page_number`,
  `page_size`, `count`, `total_results`. There are no next/prev links — page by number until
  `page_number * page_size >= total_results`.
- **Never invent identifiers.** UMRs, placement ids, underwriter emails, stamps and facility panel
  ids all come from a prior read. Nothing in this flow may be guessed.
