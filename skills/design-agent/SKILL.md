---
name: design-agent
description: Apply Ved's personal UI design system when building a dashboard, admin panel, internal tool, settings page, mockup, or any styled HTML/React artifact from scratch. Use this whenever the request is design- or UI-shaped — "build a dashboard", "make a settings page", "design a pricing table", "mock up X" — even if the user doesn't name the tokens explicitly. Covers typography (SF Pro, a fixed 12/13/14/24px scale), the neutral text hierarchy, icon sizing, and radii conventions. Do not use this for pure content/copy tasks, or when the project already has its own design system on disk (CLAUDE.md, tokens file, existing component styles) — an existing project system always wins over this skill.
---

# Ved's design system

This is a personal default, not a universal rule. It exists because re-deriving type scale and grey values from scratch every time produces inconsistent results across projects. When it applies, follow it exactly; when it conflicts with something more specific (the user's explicit instructions in this conversation, or a design system already present in the project), that more specific source always wins.

## Typography

- Font stack: `-apple-system, BlinkMacSystemFont, "SF Pro Text", "SF Pro Display", system-ui, sans-serif` — this resolves to actual San Francisco on Apple devices without needing a font file, and degrades gracefully elsewhere.
- Weights: regular (400) for body text, medium (500) for emphasis — numbers, active states, headers. Nothing bolder; the hierarchy comes from color and size, not heavy weights.
- Letter-spacing: `-0.15px` everywhere, set once on `body` and inherited.
- Type scale is closed: **12px, 13px, 14px, 24px**. No in-between sizes. Roughly: 12px for captions, labels, pills, and table metadata; 13px for body copy and table cells; 14px for nav items and section/panel headers; 24px for the one or two numbers or titles per screen that should dominate (stat values, page titles). If a design seems to need a 5th size, that's a sign to lean harder on color/weight instead, not to add a size.

## Color hierarchy

Three greys carry all text hierarchy:
- `#292929` — primary text
- `#5D5D5D` — secondary text
- `#9E9E9E` — tertiary text / placeholders / disabled

These are fixed regardless of project. What is *not* fixed — surface/background colors, the accent hue, and semantic colors (success/warning/critical) — should be chosen per project, grounded in the subject, the same way you'd choose them for any artifact. Keep semantic color separate from the accent color; they answer different questions (state vs. brand) and collapsing them makes warnings and highlights indistinguishable.

Design both light and dark themes: tokens on `:root`, overridden under `@media (prefers-color-scheme: dark)` and again under `:root[data-theme="dark"]` / `:root[data-theme="light"]` so the viewer's manual toggle wins over the OS preference in both directions. Don't naively invert the light palette — pick dark-mode equivalents that keep the same relative contrast.

## Icons

- 14px for navigation (sidebar items, top nav, inline nav affordances).
- 20px inside cards (card headers, stat tiles, panel icons).
- Stroke-based, not filled — consistent stroke width (around 1.6–1.8px), round caps/joins. Prefer hand-built inline SVG over an icon font/library so weight and sizing stay exact.

## Radii

- 8px for navigation elements: sidebar nav items, search inputs, small inline controls.
- 16px for cards and panels — the unit that says "this is one module."
- Full pill (`border-radius: 999px`) for CTA buttons, status pills/chips, and badges — anything meant to read as an action or a state, not a container.

## Applying this to dashboards and tools specifically

A dashboard is scanned, not read — lead with information design, not decoration:
- Surface the summary before the detail: stat cards / KPIs above tables and logs.
- Encode state in form as well as color — a pill, a stripe, a badge — so what needs attention is visible before the reader parses the number.
- Give sparklines real craft: a faint area fill under the line, a subtle baseline grid, an emphasized dot at the last point. Generate the path from data programmatically rather than hand-typing coordinates.
- `font-variant-numeric: tabular-nums` on any numbers that sit in a column or update in place, so digits don't jitter.

## What this skill doesn't decide

Layout concept, subject-specific copy, accent hue, and semantic colors are still yours to derive fresh each time from the actual subject — this skill fixes the *system*, not the *design*. Avoid generic AI-design defaults (purple-to-blue gradients, warm cream + terracotta, Inter/Space Grotesk as an unconsidered default, emoji as section markers) the same way you would on any other artifact.
