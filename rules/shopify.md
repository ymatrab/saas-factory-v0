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

## Background work on serverless
- Never run catalog-wide work in one request: persist a cursor/phase on a job row, process a bounded slice (~40 s, ≤100 products) per call, drive it from a fetcher after first paint — never in a page loader (BFS LCP).
- Writing `$app` metafields fires `products/update` for that product → store a signature of the fields you care about and skip unchanged webhooks, or you build an infinite loop. Never tie-break on `updatedAt`.
- Job dedupe via a partial unique index must also handle re-queueing a running job (P2002) — supersede, don't throw.
- `metafieldsSet` is atomic per call: on userErrors retry items individually and skip deleted owners.
- A hook/component used during render must not live in a `*.client.ts` file (stripped from the server bundle). Keep a dependency-free import-resolution check in `scripts/check.mjs` — tsc doesn't run locally.

## Billing
- Off-platform billing is banned. Choose **Shopify App Pricing** (hosted plan page, no code, no `app_subscriptions/update` webhook, default for new apps) or the **Billing API** (in-app plan page, more code). Opting into App Pricing blocks new Billing API recurring charges.
- `test: true` must also apply to **development stores** (`shop.plan.partnerDevelopment`), or reviewers can't approve charges once global test mode is off.
- Shopify cancellation is immediate; say so in downgrade copy. Track one trial per shop yourself.
- Merchants must be able to upgrade/downgrade in-app (req. 1.2.3). "Switch to Free" must cancel ACTIVE **and** ACCEPTED (scheduled) subscriptions. After a declined charge Shopify still returns to your returnUrl — cap polling, then show "declined". Set `trialUsedAt` only when the subscription is ACTIVE.
- Plan comparison must not show unreleased features ("Coming soon") — hide them behind the capability flag.

## Public pages
- Privacy/support pages served from the app domain; legal text 404s until an owner-approval env flag, and any page 404s while an owner placeholder remains. Placeholder regex must allow accents and annotations (`/\[\p{Lu}[\p{Lu}\d _\/.'’-]{2,}[^\]]*\]/u`); owner notes as HTML comments, stripped on render.
- robots.txt + `X-Robots-Tag: noindex` on /app, /api, /proxy, /webhooks, /auth and `/`.

## Compliance and listing
- Mandatory webhooks: `customers/data_request`, `customers/redact`, `shop/redact` (`compliance_topics` in toml; 401 on bad HMAC) + `app/uninstalled` cleanup.
- Listing: name leads with the brand (≤30 chars); 1600×900 screenshots (3–6, real UI, no pricing/reviews, alt text); 1200×1200 icon; **English review screencast required**; test credentials; emergency contact; privacy policy URL. Listing languages do **not** include Arabic (French yes).
- Protected customer data level 0 → opt out at submission. Shopify recommends 14-day trials (7 allowed).
