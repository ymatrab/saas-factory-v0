# SaaS Factory V0

This repository is a project-scoped SaaS builder. These instructions apply only inside this folder/repository.

## Mission
Turn an already-decided SaaS brief into a real, sellable, production-ready web product with strong UX/UI, working business logic, SEO/GEO/AEO foundations, launch-ready content, tests, GitHub readiness, and Cloudflare deployment readiness.

## Default stack
- Next.js + TypeScript
- Supabase: Postgres, Auth, Storage when needed
- Sanity: editable marketing/content only when useful
- GitHub: source control
- Cloudflare: deployment/hosting (keep the project's existing host, e.g. Vercel, if it already has one)
- pnpm unless the project already uses another package manager

Do not replace the default stack unless the user explicitly asks or the current repository already uses another justified stack.

## Core operating principle
This factory is execution-first, not research-first. Assume product validation and major positioning decisions were done before this system starts.

Do targeted research only when it is necessary to implement correctly, resolve uncertainty, verify current technical documentation, or perform an explicitly requested SEO/content task.

## Owner workflow
- No local installs or local servers. Verify through preview/production deploys. Typecheck, lint, tests and build run on the server build only. Locally, run only dependency-free `node` check scripts.
- Pick sensible defaults and proceed. Ask only for production merges, spend, or decisions only the owner can make.
- Re-verify inherited conclusions (memory, audits, plans) against current code/data before acting on them. The owner's latest decision wins; update project memory immediately when they reverse one.

## V0 agents
Use the minimum number of agents necessary:
1. orchestrator — planning and coordination
2. builder — all application engineering and integrations
3. design — UX, UI, visual system, frontend presentation
4. marketing — positioning, sales/conversion copy, funnel, conversion typography brief (runs before design)
5. seo — technical SEO, GEO, AEO, search-oriented site structure
6. content — SEO/editorial content, FAQs, Sanity publishing
7. qa-launch — testing, security sanity checks, build/release/deployment verification

Agents may invoke any installed skill their agent file lists; skills that require local installs are skipped.

Never call every agent by default.

## Token-efficiency rules
- Prefer one capable agent finishing a task over multiple narrow agents discussing it.
- Do not ask two agents to analyze the same issue unless the first result is insufficient or a high-risk independent review is justified.
- Do not perform broad market research unless explicitly requested.
- Do not repeatedly reread the entire repository. Search first, then inspect only relevant files.
- Read PROJECT.md and TASKS.md before rediscovering project decisions.
- Reuse accepted design, SEO, and content decisions.
- Keep plans concise and implementation-oriented.
- Avoid long narrative reports when a short decision + action list is enough.
- Do not generate documentation purely for completeness.
- Do not invoke SEO/content/design agents for a backend-only bug.
- Do not invoke builder for content-only work unless code changes are necessary.
- Invoke marketing only when conversion copy, pricing presentation or funnel is in scope.
- Parallelize only genuinely independent tasks.
- When a change is small and clear, execute directly instead of creating a large planning phase.

## Definition of done
A feature is not complete because code exists. Relevant completion criteria include:
- real business logic works
- verified on the live/preview URL, with what could not be verified noted (see rules/launch.md; regulated items follow the approval gate there)
- every public claim (free, limits, counts, prices, competitor facts) matches real behavior
- no lorem ipsum or fake placeholder product content
- responsive UX
- meaningful loading, empty, success, and error states
- auth/authorization are correct when used
- Supabase RLS is enabled and appropriate when user data is stored
- environment variables are documented in .env.example without secrets
- lint/typecheck/tests/build pass where configured (on the server build)
- no obvious console/runtime errors
- basic accessibility checks pass
- metadata/canonical/sitemap/robots/schema are correct where relevant
- no secrets are committed
- production/deployment implications are considered

## Environment variables
Agents may add and manage variable names and configuration files, but must never commit secrets.
- Keep .env.example current.
- Keep .env*, secrets, service keys, tokens, and private credentials out of Git.
- Public browser variables must be intentionally public.
- Server-only credentials must remain server-side.
- When connected tooling/CLI access is available, the appropriate agent may configure deployment secrets directly.

## Change discipline
Before changing an existing SaaS:
1. inspect current implementation
2. preserve working business logic unless the task explicitly changes it
3. identify the smallest safe change
4. implement
5. validate

Never rebuild a working area merely because another pattern is preferred.

## Product quality bar
The result should feel like a focused commercial SaaS, not a demo template:
- clear primary action
- simple navigation
- coherent visual hierarchy
- intentional pricing/CTA structure when monetized
- strong mobile behavior
- concise conversion copy
- trustworthy details, not fake social proof
- useful SEO pages only when they have distinct intent/value

## Project memory
Each SaaS project should maintain only these compact files when needed:
- PROJECT.md — durable product/stack/decision summary (also records vendor fallbacks, waived controls, failed-deploy hypotheses)
- TASKS.md — current/completed/blocked/next work
- SEO.md — accepted SEO architecture/keywords/decisions
- CONTENT.md — accepted content plan/publication state

Do not create additional persistent files unless they solve a real recurring need.

## Rule precedence
1. explicit current user instruction
2. current project/repository constraints
3. project files (PROJECT.md, accepted plans)
4. rules in ./rules
5. agent-specific instructions
6. generic skill guidance

## Learned rules
The files in ./rules are enriched from real Makecepeit, PayDocs, and future build experience. Treat accepted learned rules as reusable defaults, not immutable laws. If a project genuinely needs an exception, document the reason briefly in PROJECT.md.
