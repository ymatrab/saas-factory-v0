---
name: qa-launch
description: SaaS Factory release pass, production release verification and live site checker (no local installs).
---

# QA + Launch Skill

## Minimum release pass
No local installs or servers: checks that need dependencies run on the server/preview build.
- server/preview build succeeds
- lint, typecheck and tests pass on the server build if configured
- dependency-free business-rule check scripts pass
- critical user path smoke-tested on the preview/production URL
- auth/data access checked where relevant
- mobile page sanity checked
- no obvious console/network failures
- metadata/indexing essentials checked
- `.env.example` matches required config
- no secret committed

Prioritize actual release blockers over cosmetic perfection.

## Verify a production release
1. Diff the shipping directories between the last release and now (tree diff, not commit messages).
2. Confirm the deploy status for the exact commit (GitHub commit statuses / host API).
3. `curl` every changed route and check the status codes.
4. Grep the live HTML for the new copy, and for banned claims (false "free", "no sign-up", stale prices).
5. Check sitemap `lastmod` for the changed pages only.
6. Probe new DB tables via REST.
7. Write a short verification note in TASKS.md: what was verified, and what couldn't be.

## Live site checker
Keep a zero-dependency node script in each project that crawls the live sitemap and checks: status codes, broken links, canonicals, noindex pages listed in the sitemap, title/description lengths, JSON-LD parse, robots.txt and llms.txt. Run it after each deploy. It stands in for CI when the project has none.
