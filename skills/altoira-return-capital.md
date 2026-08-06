---
name: Return capital to an Alto IRA
description: >-
  Refund, cancel, distribute or issue a capital call against an existing Alto
  investment — the money-movement operations, and how to do them safely on an API
  with no idempotency key.
api: openapi/altoira-partner-api-openapi.yml
operations:
  - getUser
  - getInvestment
  - investmentRefund
  - investmentCancel
  - investmentDistribution
  - issueNewCapitalCall
generated: '2026-08-06'
method: generated
source: https://readme.altoira.com/docs/banking-information
---

# Return capital to an Alto IRA

These operations move real money in and out of a retirement account. Read the
safety rules before running any of them.

## Safety rules — read first

1. **There is no idempotency key on this API.** Not on refunds, not on
   distributions, not on capital calls. A retried call is a second transaction.
2. **`investmentDistribution` documents a retryable `503`.** That is exactly the
   case where a blind retry duplicates a payment. Always call `getInvestment`
   first and check `investment_transactions.distributions` before retrying.
3. **These are `physical`-consequence operations.** Escalate to a human before
   executing. See `agentic-access/altoira-agentic-access.yml`.

## Getting the destination bank account

**Always re-read `getUser` before returning cash.** Alto maintains distinct bank
accounts across investors' IRAs and offers **no** generic omnibus account. The
`accounts[].banking_information` object on the `getUser` response — `bank`,
`recipient`, `routing_number`, `account_number` — is the only source of current
routing information. Do not cache it across transactions.

Alto recommends ACH; the same coordinates work for a wire if one is genuinely
required. Funds are sent per IRA, in individual transactions — Alto's API assumes
one transfer per investor.

## Choosing the operation

| Situation | Operation |
|---|---|
| Investor pulled out, funds **not** yet sent | `investmentCancel` |
| Investor pulled out, funds **already** sent | `investmentRefund` |
| Returning some or all committed capital | `investmentRefund` |
| Paying out gains or proceeds | `investmentDistribution` |
| Drawing down more of a commitment | `issueNewCapitalCall` |

All four are manager context — HTTP Basic `PlatformAuth` — and are addressed by
the composite path key `{external_id}` + `{alto_user_id}`.

## Steps

1. **Read current state.** Call `getInvestment` with the offering `external_id`,
   the `alto_user_id`, and optionally the `investment_id` query parameter. It
   returns `amount_committed_to_invest`, `amount_invested_to_date`,
   `date_investor_esigned`, and every `capital_calls`, `investment_refunds` and
   `distributions` transaction with its status.

2. **Read the destination account.** Call `getUser` in user context and take
   `accounts[].banking_information`.

3. **Execute the right operation.**

   - `investmentCancel` — cancels if funds have not moved. A `422` with
     `"Cannot cancel, please issue a capital_refund."` means funds have already
     been sent: branch to `investmentRefund`. A `422` with `"Offering not found"`
     means your `external_id` is wrong.

   - `investmentRefund` — returns capital. Declares only a `200`; no failure
     modes are documented.

   - `investmentDistribution` — pays out. This is the only operation with fully
     schema'd errors (`{"error": true, "message": "..."}`):
     - `404` `Investment not found for the given investment_id, offering, and user.`
     - `422` `No bank account is configured for this investment's IRA.` — go back
       to `getUser`.
     - `503` `Unable to verify bank account information due to a temporary
       service issue; please retry.` — **reconcile with `getInvestment` before
       retrying.**

   - `issueNewCapitalCall` — draws capital. Declares only a `200`.

4. **Verify.** Call `getInvestment` again and confirm the new transaction appears
   with the expected `dollar_amount`. Transaction statuses are `pending`,
   `cancelled`, `completed`, `hold` (refunds and distributions) and `pending`,
   `final_review`, `approved`, `cancelled` (capital calls).

5. **Watch for the webhook.** `investment_cancelled` fires when the investor tells
   Alto they are not taking part — but **only** if they had completed their DOI.

## Done when

`getInvestment` shows the transaction and the status has moved off `pending`.
