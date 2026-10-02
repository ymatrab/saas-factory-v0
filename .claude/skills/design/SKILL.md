---
name: design
description: SaaS Factory design workflow and design-skill comparison procedure (frontend-design vs ui-ux-pro-max vs others).
---

# SaaS Design Skill

## Workflow
1. Identify primary user action and page goal.
2. Simplify hierarchy/navigation before styling.
3. Define/reuse visual system.
4. Implement desktop and mobile together.
5. Cover interactive states.
6. Check contrast, labels, focus and keyboard basics.
7. Remove generic template sections that add no value.
8. Before restyling, confirm the selectors are actually rendered; apply rules/design.md (pricing layout, a11y minimums, incremental change).

## Design-skill comparison (until a winner is recorded)
Goal: show the owner which design skill produces the best result on a real page.
1. Pick one key page (landing hero + pricing is the default) and freeze its input: marketing copy blocks + typography brief + existing brand tokens.
2. Build one variant per generator skill from that same input: `frontend-design`, `ui-ux-pro-max`, and `design:design-system` (tokens/components approach). Each lives at `/design-lab/<skill>` — noindex, excluded from sitemap and nav.
3. Review every variant with the same reviewers: `design:design-critique` and `design:accessibility-review`, plus a mobile check in the in-app browser.
4. Push to a preview branch and give the owner the preview URLs with a scorecard (1–5 each): conversion clarity, visual distinctiveness, fidelity to the copy, accessibility, mobile, code maintainability, effort/tokens used.
5. After the owner picks, record the result in rules/design.md "Design skill scorecard", ship the winner on the real route and delete `/design-lab`.
