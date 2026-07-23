# Flat utilitarian design reference

Portable **visual style** for any surface — web, mobile, desktop, or mockup.

This doc fixes **how things look**: color, type, borders, spacing, component styling. It does **not** prescribe layout, product type, or platform. Derive structure from the brief; apply these tokens on top.

**How to use:** paste in Cursor / Claude:

> Follow https://github.com/Rugved/design-skills README for visual style only. Flat UI — no shadows, no nested surfaces. Layout and platform from the brief.

Or `@README` if the repo is open.

---

## Core principles

- **Flat surfaces** — depth from border and spacing, not elevation.
- **No box shadows** on containers, cards, or buttons.
- **No nested surface-in-surface** — one module per grouped block; avoid card-in-card.
- **No gradients or glassmorphism** unless the brief explicitly calls for it (keep subtle).
- **Separation** — `1px` borders at `#EAEAEA` and whitespace, not layered boxes.
- **Lists** — consecutive rows with dividers inside one module, not a separate floating card per item.
- **Grouped information** — label + value pairs, not inset mini-tiles.

---

## Color tokens

### Text (every project)

| Role | Hex |
|------|-----|
| Primary | `#292929` |
| Secondary | `#5D5D5D` |
| Tertiary | `#9E9E9E` |

Avoid pure `#000000` for body text.

### Surfaces (light)

| Role | Hex |
|------|-----|
| Canvas / screen background | `#F7F6F3` (warm bone) |
| Module / card / sheet | `#FFFFFF` |
| Muted fill (hover, selected, secondary) | `#F3F3F1` |
| Border / divider | `#EAEAEA` |

### Accent & semantic (light)

| Role | Hex |
|------|-----|
| Primary action | `#16A34A` on white text |
| Success | `#EDF3EC` bg / `#346538` text |
| Warning | `#FBF3DB` bg / `#956400` text |
| Critical / error | `#FDEBEC` bg / `#9F2F2D` text |

Keep **accent** (brand / primary action) separate from **semantic** (state).

### Dark theme

Define light tokens first, then `.dark` (or platform equivalent) overrides. Do not naively invert — preserve contrast relationships. Example dark accent: `#E86B4A`.

---

## Typography

**Stack (Apple-first, degrades elsewhere):**  
`-apple-system, BlinkMacSystemFont, "SF Pro Text", "SF Pro Display", system-ui, sans-serif`

On Android / cross-platform builds, map to the platform system sans (Roboto is acceptable **only** as the Android system fallback, not as a lazy web default).

**Letter-spacing:** `-0.15px` on the root text style, inherited.

**Weights:** 400 body, 500 emphasis. No heavier weights — hierarchy from size and color.

**Closed scale — only these sizes:**

| Use | Size | Line height |
|-----|------|-------------|
| Caption, labels, meta | 12px | 1.4 |
| Body, inputs | 13px | 1.45 |
| Subheads, toolbar titles | 14px | 1.4 |
| Screen title, key figure | 24px | 1.2 |

**Numeric data:** tabular figures (`font-variant-numeric: tabular-nums` or platform equivalent).

---

## Radii

| Element | Radius |
|---------|--------|
| Inputs, chips, small controls | 8px |
| Modules, sheets, dialogs | 12px |
| Pills, badges, primary actions | full pill (999px) |

---

## Icons

- **14px** — inline, toolbar, list accessories
- **20px** — section headers, feature marks
- Stroke style, ~1.6px consistent weight

---

## Component styling

Apply to whatever components the brief needs — no required component set.

### Module (base surface)

```css
.flat-surface {
  background: #ffffff;
  border: 1px solid #eaeaea;
  border-radius: 12px;
}
```

Canvas stays `#F7F6F3`; content modules sit as white bordered blocks.

### List item

- Divider between items (`#EAEAEA`), not separate cards
- Primary line: 13px medium `#292929`
- Secondary line: 12px `#5D5D5D`
- Optional status pill: muted pastel (semantic colors above)

### Inputs

- Label: 12px `#5D5D5D`
- Field: 13px, 8px radius, 1px `#EAEAEA` border, white fill
- Group related fields inside one module with internal padding

### Buttons

- Primary: `#16A34A`, white label, pill shape, no shadow
- Secondary: outline or muted fill `#F3F3F1`
- One clear primary action per view when possible

### Badges / status

- Small pill, pastel background, darker label color
- Avoid large saturated color blocks

---

## Token reference (CSS)

Translate the same values to SwiftUI, Compose, Figma variables, etc.

```css
:root {
  --background: #f7f6f3;
  --foreground: #292929;
  --surface: #ffffff;
  --border: #eaeaea;
  --muted: #f3f3f1;
  --muted-foreground: #9e9e9e;
  --primary: #16a34a;
  --primary-foreground: #ffffff;
}

body {
  background: var(--background);
  color: var(--foreground);
  font-size: 13px;
  line-height: 1.45;
  letter-spacing: -0.15px;
}
```

---

## Avoid

- Unconsidered Inter / Roboto on web when system stack is available
- Purple-blue gradients, heavy shadows, glass cards
- Card-in-card nesting
- Emoji as UI markers
- Generic marketing copy: "Elevate", "Seamless", "Next-Gen"
- Placeholder names: "John Doe", "Acme Corp"

---

## Checklist

1. Bone canvas, white modules, `#EAEAEA` borders only
2. No shadows on custom surfaces
3. Type scale locked to 12 / 13 / 14 / 24
4. Layout and components driven by the brief — not a template
5. Realistic content, not lorem ipsum

---

## Cursor prompt

```
Build [FEATURE] for [web | iOS | Android | mockup]. Follow github.com/Rugved/design-skills README for visual style — warm bone canvas, white bordered modules, no shadows, no nested surfaces, 12/13/14/24px type, green accent, muted pastel status colors. Layout and IA from the brief: [describe].
```
