---
name: design-tokens-migration
description: A practical migration playbook to move from hardcoded UI values (colors/spacing/typography) to design tokens, with an inventory method, naming rules, rollout strategy, and copy/paste templates.
---

# Design Tokens Migration

Use this skill to migrate an existing UI codebase from ad-hoc styling values to a tokenized system that is consistent, reviewable, and scalable.

## When to Use
- Your UI has many hardcoded hex values, spacing numbers, and one-off type styles.
- You are introducing (or consolidating) a design system.
- You need a low-risk migration plan that avoids breaking themes and visual regressions.

## Inputs
Ask for:
- Target platforms: web (CSS), iOS/Android, Flutter, etc.
- Styling stack: CSS variables, Tailwind, CSS-in-JS, Sass, Flutter ThemeData, etc.
- Design source of truth: Figma libraries? existing tokens? none?
- The scope boundary: one product area, one app, or entire monorepo.
- Constraints: theming (light/dark), white-labeling, legacy browser support.

## Workflow
1. Define the token model
   - Start with the smallest useful set: color, spacing, typography, radius, elevation.
   - Decide on token tiers:
     - Foundation (raw): palette/scale values.
     - Semantic: intent-based (e.g., text.primary, surface.default).
     - Component (optional): button.background.
2. Inventory current usage
   - Capture the top offenders first (most-used colors/spacings) before chasing one-offs.
   - Group by category (colors/spacings/type) and by intent (text, background, border).
3. Create naming rules
   - Prefer semantic names for app usage.
   - Keep foundation scale names consistent (e.g., spacing.0/1/2 or spacing.2xs/xs/s/m).
4. Introduce tokens without changing UI
   - Add tokens and wire them up as aliases for existing values.
   - Migrate one surface at a time to reduce risk and review load.
5. Migrate gradually
   - Replace hardcoded values with tokens in small PRs.
   - Track progress by category and by code ownership area.
6. Enforce
   - Add lint/code review rules: no new raw hex, no arbitrary spacing.
   - Document "escape hatches" and how to request new tokens.

## Outputs

### Token Inventory Template
```md
| Current Value | Category | Where Used (examples) | Proposed Token | Token Tier | Notes |
|---|---|---|---|---|---|
| #1A73E8 | color | Primary buttons, links | color.brand.primary | semantic | Brand blue; check contrast on surfaces |
| 8px | spacing | Card padding, gap | spacing.s | foundation | Map to spacing scale |
| 14px / 20px | typography | Body text | type.body.sm | semantic | Define weight + letter spacing |
```

### Token Naming Rules (Copy/Paste)
```text
Foundation
- color.palette.<hue>.<step>
- spacing.<step>
- radius.<step>
- elevation.<step>

Semantic
- color.text.primary|secondary|inverse|disabled
- color.surface.default|raised|sunken
- color.border.default|subtle|focus
- color.action.primary|danger|success|warning
```

### Migration PR Checklist
```text
PR: Design tokens migration

Scope
- [ ] Scope is limited (one feature/component area)
- [ ] Before/after screenshots included (key states)

Token usage
- [ ] No new raw hex values introduced
- [ ] No arbitrary spacing introduced
- [ ] Replaced values map to existing tokens (or new tokens added with rationale)

Theming
- [ ] Works in all supported themes (light/dark/brand variants)
- [ ] Tokens are semantic in app code (foundation tokens only in token definitions)

Safety
- [ ] Visual regressions checked for key pages
- [ ] Rollback is straightforward (no large refactor bundled)
```

## Risks
- Token drift: adding near-duplicate tokens because naming rules are unclear.
- Over-semanticization too early: creating many intent tokens without stable design decisions.
- Unsafe bulk changes: massive replace-all PRs that are hard to review or rollback.
- Hidden theming breakage: tokens that look correct in one theme but fail in others.
