# Design Rules

- Focused SaaS over generic template aesthetics.
- Strong hierarchy: one clear primary action per important screen.
- Responsive and mobile behavior must be intentionally designed.
- Every async workflow needs appropriate loading/success/error states.
- Do not use fake social proof.

## Learned rules
- **Pricing shows everything.** All plans side by side, the full feature list in each card, and a comparison table. Mark paid-only items before the user clicks them.
- **Accessibility minimums.** Tap targets ≥44px, text contrast ≥4.5:1, errors announced to screen readers, visible focus, inputs ≥16px so iOS doesn't zoom.
- **Evolve, don't replace.** Do not swap the established palette, fonts or geometry in one pass. Change incrementally, with evidence, unless the owner asks for a redesign.
- **Style what actually renders.** Before restyling, grep that the class/selector is used. Review automated token/style migrations for corrupted values (e.g. 8-digit hex) and lost semantic colors (error/success tints).

## Design skill scorecard
Preferred skill for new pages is decided by the owner after a comparison (design skill). One line per evaluation: date · project · page · winner · why.
- 2026-10-03 · PayDocs · home hero + pricing · A (`frontend-design`) look on C (`design:design-system`) components · A most distinctive and on-brief, C most maintainable/accessible; B (`ui-ux-pro-max`) read as generic SaaS. Default for new pages: `frontend-design` for direction, `design:design-system` for the component layer.
