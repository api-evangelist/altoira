---
name: Onboard an investor into an Alto offering
description: >-
  Run the OAuth consent handoff to get an investor's Alto user ID, invite them to
  an offering, and redirect them to Alto to sign the Direction of Investment.
api: openapi/altoira-partner-api-openapi.yml
operations:
  - enableOffering
  - getUser
  - getInvestment
generated: '2026-08-06'
method: generated
source: https://readme.altoira.com/docs/understand-the-oauth-process-to-alto
---

# Onboard an investor into an Alto offering

To invite an investor into a deal you need their **Alto user ID**, and the only
way to get it is an OAuth handoff the investor completes themselves.

## This flow requires a human

Two steps are browser redirects the investor must perform in person. An agent can
build the URLs and drive everything around them, but **cannot complete them**.
Alto's Direction of Investment (DOI) is a legally required signature.

## Steps

1. **Send the investor to Alto for consent.** Redirect their browser to
   `GET /oauth/authorize` with:
   - `client_id` — your partner client ID
   - `response_type` — always `code`
   - `redirect_uri` — must match the value Alto has on file for you
   - `scope`

   The investor signs in to Alto (or creates an account) and authorizes your
   platform.

2. **Exchange the code.** Alto redirects back to your `redirect_uri` with a
   `code`. Exchange it at `POST /oauth/token`. You get back `token_type: Bearer`,
   `expires_in`, `access_token` and `refresh_token`. Refresh at
   `/oauth/token/refresh`.

   > Note: the published OpenAPI hardcodes the **sandbox** host in all three
   > OAuth flow URLs. Override the host to production explicitly — a client
   > generated straight from the spec will authenticate against sandbox.

3. **Read the investor's identity and IRA.** Call `getUser` with the bearer token
   (**user context** — `UserAuth`, not your Basic credentials). This returns
   `id` (the Alto user ID you need), name, email, and every IRA account they
   hold with its `investing_entity_name`, `ira_ein`, `ira_address`, authorized
   signer and `banking_information`.

   > **Store the Alto user ID per investment, not per person.** Alto states a
   > single customer may hold more than one Alto user ID and advises partners to
   > support different IDs across different investments.

4. **Invite the investor to the offering.** Call `enableOffering` (manager
   context — Basic `PlatformAuth`) with the offering `external_id` and the
   `alto_user_id`. This both grants access and sets/limits the investment amount.
   - `404 "Offering hasn't been created"` — create the offering first (see the
     `altoira-launch-offering` skill).
   - `422` — the investor has already signed off on the investment. The amount is
     locked; do not retry.

5. **Redirect the investor to sign the DOI.** Send them to
   `GET /offering/platform/{platform_code}/{external_id}`. Do this **only after**
   they have finished every commitment step on your own site — the redirect takes
   them off your platform.

   The investor does not sign any deal documents on your site. Alto's DOI is the
   only signature legally required at this point, and Alto executes the deal
   documents.

6. **Wait for confirmation.** When the DOI is signed Alto fires an
   `investment_signed` webhook. That is the confirmation the IRA's place in the
   offering is secured. You can also poll `getInvestment`.

## Done when

You have received `investment_signed`, or `getInvestment` returns a
`date_investor_esigned`.

## Rules

- Manager-context and user-context credentials are not interchangeable.
  `getUser` and `updateUser` need the investor bearer token; everything else
  needs your Basic credentials.
- `getInvestment` reports only the commitment amount for which the investor has
  actually executed a DOI. A requested-but-unsigned increase will not appear.
- See `asyncapi/altoira-investments-webhooks.yml` for the full event catalog.
