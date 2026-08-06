---
name: Launch an Alto offering
description: >-
  Create an offering in Alto and upload the documents Alto requires before any
  investor can direct IRA capital into it.
api: openapi/altoira-partner-api-openapi.yml
operations:
  - createOffering
  - createDocument
  - createDocumentViaZip
  - getOffering
  - updateOffering
  - getOfferings
generated: '2026-08-06'
method: generated
source: https://readme.altoira.com/docs/create-offering
---

# Launch an Alto offering

Alto recommends creating every IRA-eligible offering **before** it goes live on
your platform. Creating it once lets you invite every Alto investor without
re-sending deal details each time — the only per-investor value is that
investor's dollar commitment.

## Authentication

All operations here run in **manager context**: HTTP Basic (`PlatformAuth`) with
the credentials Alto assigned to you. Do not use an investor bearer token.

## Base URL

- Sandbox: `https://altoira.sandbox.altoira.com`
- Production: `https://www.altoira.com`

## Steps

1. **Check whether the offering already exists.** Call `getOffering` with your
   `external_id`. A `404 "You have not created the deal in Alto"` means it does
   not exist yet. Skip to step 2. A `200` means it exists — go to step 4 instead
   of creating a duplicate.

2. **Create the offering.** Call `createOffering` with your `external_id` as the
   path key. `external_id` is *your* internal ID for this offering — you own this
   namespace, so use a value you can resolve back to the deal. The body carries:
   - name and incorporation of the company or fund
   - the type of security offered
   - the bank information Alto will send funds to on completion

   A `409` means an offering already exists for that `external_id`. Treat it as
   "already created" and move on — do not retry with a mutated ID.

3. **Upload the required documents.** Alto requires at minimum:
   - the operating agreement of the corporation
   - the purchase agreement outlining what an investing entity agrees to

   Prefer `createDocument` (one file per call, `multipart/form-data`, with the
   `type` query parameter classifying the upload) — this is Alto's recommendation.
   Use `createDocumentViaZip` only when you genuinely need to push an archive.

4. **Amend if needed.** `updateOffering` changes a previously created offering.
   It returns `422` in two cases, both with a readable message:
   - `Cannot change value for existing field: {field}` — the field already has a
     value and is immutable. Do not retry; the value is set.
   - `No data was detected in your payload` — you sent nothing updatable.

5. **Confirm.** `getOfferings` lists everything you have created. Note that it
   takes no pagination parameters and returns the whole collection.

## Done when

The offering exists and all required documents are uploaded. Only then can
investors be added — see the `altoira-onboard-investor` skill.

## Rules

- **No idempotency key exists on this API.** `createOffering` is protected by the
  `409` conflict only because `external_id` is your key. Always pre-check with
  `getOffering` rather than relying on retry safety.
- 10 of the 17 operations in this API declare no error responses at all. Do not
  assume an undocumented failure returns a parseable body — branch on HTTP status
  first. See `errors/altoira-problem-types.yml`.
- There is no pagination, no rate-limit signaling and no request-id header on this
  API. See `conventions/altoira-conventions.yml`.
