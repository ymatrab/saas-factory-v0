---
name: design
description: SaaS Factory design workflow — Inspo direction selection (3 distinct real-world references, owner picks), original design system, implementation, and the design-skill comparison procedure.
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

## Direction selection (required before implementing a new product or a redesign)
Tools: Inspo MCP (real production sites: screens, palettes, fonts, DESIGN.md, components) + `awesome-design-md` + `ui-ux-pro-max`. Skip only for small changes inside an accepted direction.
1. Understand the product: audience, core action, trust needs, PROJECT.md "Messaging & conversion".
2. Search Inspo for relevant real-world references (start with `recommend(brief)`; use `find_similar` / search to widen). `awesome-design-md` and `ui-ux-pro-max` may add candidates.
3. Select **3 visually distinct directions**. They must NOT be variations of the same modern SaaS look; they differ substantially in macrostructure, typography, density, color philosophy, geometry, navigation and visual rhythm. Example spread: A restrained / Swiss / professional · B editorial / structural / distinctive · C expressive / playful / product-led.
4. Give the owner the 3 Inspo URLs. For each, 2–3 sentences: visual personality, why it fits the product, which design DNA will be borrowed.
5. **Stop and wait for the owner's choice.** Build nothing before it.
6. Never copy the chosen site (layout, copy, logo, illustrations, signature colors or proprietary fonts).
7. Extract principles from it (`get_design_system` for tokens/type ramp/spacing as evidence) and create an original design system: own tokens, type scale, components, recorded in the project's design doc.
8. Implement with the scorecard's preferred skills (rules/design.md) + `skill-kit` when installed, then review (`design:design-critique`, `design:accessibility-review`).

## Design-skill comparison (only when the owner asks to compare skills)
Goal: show the owner which design skill produces the best result on a real page.
1. Pick one key page (landing hero + pricing is the default) and freeze its input: marketing copy blocks + typography brief + existing brand tokens.
2. Build one variant per generator skill from that same input: `frontend-design`, `ui-ux-pro-max`, and `design:design-system` (tokens/components approach). Each lives at `/design-lab/<skill>` — noindex, excluded from sitemap and nav.
3. Review every variant with the same reviewers: `design:design-critique` and `design:accessibility-review`, plus a mobile check in the in-app browser.
4. Push to a preview branch and give the owner the preview URLs with a scorecard (1–5 each): conversion clarity, visual distinctiveness, fidelity to the copy, accessibility, mobile, code maintainability, effort/tokens used.
5. After the owner picks, record the result in rules/design.md "Design skill scorecard", ship the winner on the real route and delete `/design-lab`.
