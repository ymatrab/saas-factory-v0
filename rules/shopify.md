# Shopify App Rules

Learned building NicheUp (2026-10). Re-check shopify.dev before each new app: the platform changes several times a year.

## Stack and setup
- **Template:** Shopify React Router app template (`@shopify/shopify-app-react-router`, Prisma session storage on Postgres). Admin UI = Polaris **web components** (`<s-page>`…) + App Bridge script tag first in `<head>`. Do not start new screens in Polaris React.
- **Where things live:** create the app in the **Dev Dashboard** (client ID/secret, App Automation Token, dev stores). Listing, payouts, emergency contact and protected-data forms stay in the **Partner Dashboard**. List these owner tasks in step 1.
- **Auth:** Shopify managed install (scopes in `shopify.app.toml`) + token exchange. Public apps created after 2026-04-01 must use **expiring offline tokens** (`future.expiringOfflineAccessTokens`; store refresh tokens).
- **No local CLI:** hand-write `shopify.app.toml` with the client ID and run `shopify app deploy --config production --allow-updates` in a GitHub Action with `SHOPIFY_APP_AUTOMATION_TOKEN`. The first deploy writes extension `uid`s; the workflow must commit them back (`contents: write`, `[skip ci]`).
- **Vercel:** `@vercel/react-router` preset; build = `prisma generate && prisma migrate deploy && react-router build`; `DIRECT_URL` is required for migrations; SQLite is unusable.

## Scopes
- Request the minimum; review rejects extras. `read_product_listings` is for sales channels only. Theme app extensions need no scope; `read_themes` only to detect app-block support. Writing `$app` product metafields needs `write_products`; app proxy needs `write_app_proxy`.

## Storefront
- Product page: app block rendering from `$app` metafields (no runtime fetch) — Lighthouse drop must stay ≤10 points.
- Cart drawers have **no official app-block support**: app embed + small JS + signed app proxy, claimed only for themes actually tested, with a cart-page block fallback. Never patch `window.fetch` globally.
- RTL: set `dir` from `request.locale.direction` on the block root (Dawn doesn't set it on `<html>`); `<bdi>` around prices/Latin text.

## Admin UI gotchas (Polaris web components)
- `s-button` ignores `type="submit"` when `commandFor`/`command` is set and has no `form` attribute → modal confirm buttons must `fetcher.submit()` in `onClick`, then `hideOverlay()`.
- Slot buttons (`slot="primary-action"`) must be direct children of `s-page`/`s-section`; wrapping them in a `<Form>` silently drops the slot.
- Shopify sends `?locale=` only on the first embedded load. Cookies in the admin iframe are third-party (req. 1.1.1) → persist locale server-side (shop row), cookie only as a fast path.
- No documented RTL API in Polaris web components: set `dir` on your own wrapper and test.

## Billing
- Off-platform billing is banned. Choose **Shopify App Pricing** (hosted plan page, no code, no `app_subscriptions/update` webhook, default for new apps) or the **Billing API** (in-app plan page, more code). Opting into App Pricing blocks new Billing API recurring charges.
- `test: true` must also apply to **development stores** (`shop.plan.partnerDevelopment`), or reviewers can't approve charges once global test mode is off.
- Shopify cancellation is immediate; say so in downgrade copy. Track one trial per shop yourself.
- Merchants must be able to upgrade/downgrade in-app (req. 1.2.3).

## Compliance and listing
- Mandatory webhooks: `customers/data_request`, `customers/redact`, `shop/redact` (`compliance_topics` in toml; 401 on bad HMAC) + `app/uninstalled` cleanup.
- Listing: name leads with the brand (≤30 chars); 1600×900 screenshots (3–6, real UI, no pricing/reviews, alt text); 1200×1200 icon; **English review screencast required**; test credentials; emergency contact; privacy policy URL. Listing languages do **not** include Arabic (French yes).
- Protected customer data level 0 → opt out at submission. Shopify recommends 14-day trials (7 allowed).
