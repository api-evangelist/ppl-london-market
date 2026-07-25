---
name: Poll PPL notifications and the transaction log
description: >-
  Event-consumption flow. PPL publishes no webhooks, so an agent observes placement activity by
  polling the PPL Next Gen Events API for notifications and the business transaction log.
api: openapi/ppl-london-market-events.json
base_url: https://api.londonmarketgroup.co.uk/ppl/nextgen/events/v1
generated: '2026-07-25'
method: generated
source: openapi/ppl-london-market-events.json + conventions/ppl-london-market-conventions.yml
operations:
  - Notification_GetAll_v1
  - Notification_GetById_v1
  - Notification_MarkAllAsRead_v1
  - Transaction_GetAll_v1
  - Transaction_GetById_v1
---

# Poll PPL notifications and the transaction log

**PPL has no event push.** There is no webhook catalogue, no callbacks object in any of the five
OpenAPI documents, and no AsyncAPI artifact. The Events API is strictly pull-based. Any agent that
needs to react to placement activity must poll.

## Before you start

Entra ID bearer token with `scp: user_impersonation`, the environment's registered X.509 client
certificate, and `X-Auth-Impersonated-User` + `X-Auth-Team` on every call.

## Steps

1. **Poll notifications.** `GET /notifications` — `Notification_GetAll_v1`. Filter with the
   declared parameters: `recipientEmail`, `recipientTeamId`, `recipientTeamName`, `senderEmail`,
   `placementId`, `programmeId`, `contractId`, `contractVersion`, `sectionId`, `category`,
   `categoryType`, `type`, `processStatus`, `isTechnical`, `createdDate`, `expiryDate`,
   `clientName`, `companyName`. Sort with `sort`; page with `pageNumber` / `pageSize`.
2. **Read one.** `GET /notifications/{notificationId}` — `Notification_GetById_v1`.
3. **Clear the queue.** `POST /notifications/markAllAsRead` — `Notification_MarkAllAsRead_v1`.
   This is a bulk state change across the user's notifications. Do not call it as a side effect of
   a read loop, and never call it before every notification you intended to process has actually
   been processed.
4. **Reconcile against the transaction log.** `GET /transactions` — `Transaction_GetAll_v1`
   (filters include `contractId`, `transactionType`, `authorEmail`, `authorOnBehalfEmail`,
   `createdDate`), and `GET /transactions/{transactionId}` — `Transaction_GetById_v1`. The
   transaction log is the audit record for contract-related engagements; use it, not the
   notification list, when you need a definitive history.

## Rules you must follow

- **Poll politely.** 429 is declared on every operation and PPL publishes no limit values.
  Use a conservative interval with exponential backoff on 429, and filter server-side with
  `createdDate` rather than pulling everything and filtering locally.
- **Keep query strings short.** 414 (URI Too Long) is a declared response on every operation —
  the filter surface is wide enough that it genuinely fires.
- **Page by number.** Responses carry `page_number`, `page_size`, `count`, `total_results` and
  no link relations. Iterate until `page_number * page_size >= total_results`.
- **Notifications are not idempotent state.** `Notification_MarkAllAsRead_v1` is a POST with no
  concurrency precondition and no replay key — calling it twice is not harmful, but calling it
  early loses your work queue.
- **Errors.** `{ "errors": [ { "code", "message", "field", "argument" } ] }`; statuses 400, 401,
  404, 414, 429, 500.
