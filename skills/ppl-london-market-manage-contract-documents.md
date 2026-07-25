---
name: Manage Market Reform Contract documents
description: >-
  Contract-issuance flow. Upload, version, retrieve and download documents across the PPL
  placement hierarchy — including the Market Reform Contract (MRC) and its supporting documents —
  using the PPL Next Gen Documents API.
api: openapi/ppl-london-market-documents.json
base_url: https://api.londonmarketgroup.co.uk/ppl/nextgen/documents/v1
generated: '2026-07-25'
method: generated
source: openapi/ppl-london-market-documents.json + conventions/ppl-london-market-conventions.yml
operations:
  - Document_GetAll_v1
  - Document_Post_v1
  - Document_GetById_v1
  - Document_Put_v1
  - Document_Delete_v1
  - Document_GetContent_v1
  - Document_PostDownload_v1
  - Document_GetSecurityContent_v1
  - Document_PostSecurityDownload_v1
---

# Manage Market Reform Contract documents

The Documents API is PPL's contract-issuance surface. Documents are attached to a context in the
placement hierarchy and are addressed by **version** once created.

## Before you start

Entra ID bearer token with `scp: user_impersonation`, the environment's registered X.509 client
certificate, and `X-Auth-Impersonated-User` + `X-Auth-Team` on every call.

## Steps

1. **Find documents.** `GET /documents` — `Document_GetAll_v1`. Filter by `placementId`,
   `contextId`, `contextType`, `classType`, `type`, `fileName`, `description`, `teamName`,
   `uploadUserEmail`, `createdDate`, `modifiedDate`. Page with `pageNumber` / `pageSize`.
2. **Upload a document.** `POST /documents` — `Document_Post_v1`. Attach it to the correct context
   (the placement, contract or section it belongs to). Keep the returned `document_version_id`.
3. **Read one version.** `GET /documents/versions/{documentVersionId}` — `Document_GetById_v1`.
   This returns metadata; capture the last-modified value before any update.
4. **Update metadata / create a new version.** `PUT /documents/versions/{documentVersionId}` —
   `Document_Put_v1`. **Requires the `X-Last-Modified` header.**
5. **Get the content.** `GET /documents/versions/{documentVersionId}/content` —
   `Document_GetContent_v1`.
6. **Download.** `POST /documents/versions/{documentVersionId}/download` —
   `Document_PostDownload_v1`.
7. **Secured content and download.** Some documents sit behind the separate secured path:
   `GET /documents/versions/{documentVersionId}/security/content` —
   `Document_GetSecurityContent_v1`, and
   `POST /documents/versions/{documentVersionId}/security/download` —
   `Document_PostSecurityDownload_v1`. Use these when the standard content path is not authorised
   for the document; do not treat a failure on the standard path as the document not existing.
8. **Delete a version.** `DELETE /documents/versions/{documentVersionId}` —
   `Document_Delete_v1`. Destructive and consequential on a bound contract — confirm with a human
   first.

## Rules you must follow

- **Version, not document, is the address.** Everything after creation is keyed on
  `documentVersionId`. Do not assume a document id works on the version paths.
- **`X-Last-Modified` is required on `Document_Put_v1`.** Re-read with `Document_GetById_v1`
  immediately before updating.
- **The MRC is the contract.** Treat Market Reform Contract documents as the legal record of the
  placement, not as attachments. Never replace or delete one on an assumption.
- **Errors and throttling.** Same envelope and statuses as the rest of the platform — 400, 401,
  404, 414, 429, 500, with `{ "errors": [ { "code", "message", "field", "argument" } ] }`.
- **No push.** Document events are not pushed; poll the Events API if you need to observe changes.
