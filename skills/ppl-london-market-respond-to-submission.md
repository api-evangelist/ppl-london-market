---
name: Respond to a broker submission as an underwriter
description: >-
  Carrier-side flow. Retrieve submissions sent by a broker, work the negotiation of terms of
  cover, reassign it to another underwriter if needed, and send the response back to the broker,
  using the PPL Next Gen Submissions API.
api: openapi/ppl-london-market-submissions.json
base_url: https://api.londonmarketgroup.co.uk/ppl/nextgen/submissions/v1
generated: '2026-07-25'
method: generated
source: openapi/ppl-london-market-submissions.json + conventions/ppl-london-market-conventions.yml
operations:
  - Submission_GetAll_v1
  - Submission_GetById_v1
  - Negotiation_GetAll_v1
  - Negotiation_GetById_v1
  - Negotiation_Post_v1
  - Negotiation_Put_v1
  - Negotiation_Reassign_v1
  - Submission_Send_v1
---

# Respond to a broker submission

You are acting as an **underwriter / carrier** on PPL Next Gen. This is the quote side of the
platform: the broker has sent a submission, and you work and answer it here.

## Before you start

Same market gate as every PPL call: an Entra ID bearer token carrying `scp: user_impersonation`,
the registered X.509 client certificate for the environment, and the `X-Auth-Impersonated-User`
and `X-Auth-Team` headers set to the underwriter and their carrier team. An invalid pair returns
404 with `INVALID_ROLE_OR_TEAM`. See `authentication/ppl-london-market-authentication.yml`.

## Steps

1. **Find the submissions.** `GET /submissions` — `Submission_GetAll_v1`. Filter with the declared
   query parameters, for example `status`, `brokerCompanyName`, `clientName`,
   `uniqueMarketReference`, `inceptionDate`, `receivedDate`, `underwriterEmail`, `isLeader`,
   `hasSubjectivities`, `hasLineConditions`. Page with `pageNumber` / `pageSize`.
2. **Open one.** `GET /submissions/{submissionId}` — `Submission_GetById_v1`.
3. **List its negotiations.** `GET /submissions/{submissionId}/negotiations` —
   `Negotiation_GetAll_v1`.
4. **Read the negotiation you are working.**
   `GET /submissions/{submissionId}/negotiations/{negotiationId}` — `Negotiation_GetById_v1`.
   Capture its last-modified value now; you need it for every write below.
5. **Work the terms.** `PUT /submissions/{submissionId}/negotiations/{negotiationId}` —
   `Negotiation_Put_v1`. **Requires `X-Last-Modified`.** Use this to record the written line,
   accept or decline roles, respond to stamps and line conditions, and answer subjectivities.
   To open a fresh negotiation instead, `POST /submissions/{submissionId}/negotiations` —
   `Negotiation_Post_v1`.
6. **Reassign if this is not your risk.**
   `PUT /submissions/{submissionId}/negotiations/{negotiationId}/reaassign` —
   `Negotiation_Reassign_v1`. **Requires `X-Last-Modified`.** Note the operation path is spelled
   `reaassign` in the published specification — use it verbatim.
7. **Send the response back to the broker.** `POST /submissions/{submissionId}/send` —
   `Submission_Send_v1`. **Consequential.** This puts your answer in front of the broker. Confirm
   with a human before calling it; there is no undo operation in the API.

## Rules you must follow

- **No idempotency key.** Writes are protected by the `X-Last-Modified` optimistic-concurrency
  precondition, taken from a fresh `Negotiation_GetById_v1`, not by a replay key. Re-read before
  every retry rather than replaying the same request.
- **Do not confuse the two negotiation surfaces.** The Submissions API and the Placements API both
  declare operations named `Negotiation_GetAll_v1`, `Negotiation_GetById_v1`, `Negotiation_Post_v1`
  and `Negotiation_Put_v1`. They are different operations in different specs — the Submissions ones
  hang off `/submissions/{submissionId}`, the Placements ones off `/contracts/{contractId}`. Always
  qualify by spec file.
- **Errors.** Single envelope `{ "errors": [ { "code", "message", "field", "argument" } ] }`;
  statuses 400, 401, 404, 414, 429, 500. Known codes: `MANDATORY_PARAMETER`, `UNAUTHENTICATED`,
  `INVALID_PARAMETER_FORMAT`, `INVALID_ROLE_OR_TEAM`.
- **Throttling.** Handle 429 with backoff; no published limits.
- **No push.** There is no webhook or callback. If you need to know when a broker responds, poll
  the Events API (`Notification_GetAll_v1`, `Transaction_GetAll_v1`).
