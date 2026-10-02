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
