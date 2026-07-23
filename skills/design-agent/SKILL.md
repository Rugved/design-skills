---
name: design-agent
description: Apply Ved's flat utilitarian visual design system when building any styled UI — web, mobile, desktop, or mockup. Use for design- or UI-shaped requests even when tokens aren't named explicitly. Covers typography (SF Pro / system stack, 12/13/14/24px scale), text hierarchy, surfaces, borders, icon sizing, and radii. Does not prescribe layout or product type. Skip when the project already has its own design system on disk — existing project tokens always win.
---

# Ved's design system

Personal visual defaults for consistent polish under time pressure. Fixes the *system* (tokens, surfaces, type), not layout or product structure. When this conflicts with explicit user instructions or an on-disk design system, the more specific source wins.

## Core principles

- Flat surfaces — depth from border (`#EAEAEA`) and spacing, not elevation.
- No box shadows on containers or buttons.
- No nested surface-in-surface (card-in-card).
- No gradients or glassmorphism unless the brief requires it.

## Typography

- Stack: `-apple-system, BlinkMacSystemFont, "SF Pro Text", "SF Pro Display", system-ui, sans-serif` — San Francisco on Apple without a font file; map to platform system sans elsewhere.
- Weights: 400 body, 500 emphasis only.
- Letter-spacing: `-0.15px` on root, inherited.
- Closed scale: **12px, 13px, 14px, 24px** only. No fifth size — use color/weight instead.
  - 12px: captions, labels, meta
  - 13px: body, inputs
  - 14px: subheads, toolbar titles
  - 24px: screen title or key figure
- Tabular nums on numeric data that updates or aligns in columns.

## Color hierarchy

Fixed text greys:
- `#292929` — primary
- `#5D5D5D` — secondary
- `#9E9E9E` — tertiary / disabled

Fixed light surfaces:
- Canvas `#F7F6F3`, module `#FFFFFF`, muted `#F3F3F1`, border `#EAEAEA`

Default accent: `#16A34A` (primary action). Semantic pastels: success `#EDF3EC`/`#346538`, warning `#FBF3DB`/`#956400`, critical `#FDEBEC`/`#9F2F2D`. Keep accent separate from semantic state.

Support light + dark themes. Don't naively invert — preserve contrast relationships.

## Icons

- 14px inline / toolbar; 20px section headers.
- Stroke-based, ~1.6px weight, consistent across the screen.

## Radii

- 8px — inputs, small controls
- 12px — modules, sheets, dialogs
- 999px — pills, badges, primary actions

## What this skill doesn't decide

Layout, navigation pattern, screen structure, copy, and platform-specific IA come from the brief. Avoid generic AI slop: purple gradients, heavy shadows, Inter as unconsidered default, emoji markers.
