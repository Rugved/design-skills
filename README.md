# Flat utilitarian UI — design reference

Portable style guide for **dashboards, admin panels, and internal tools**. Use on any greenfield project when building UI under time pressure.

**How to use (interview or new project):** paste this in Cursor / Claude:

> Follow the design system in https://github.com/Rugved/design-skills — README only. Flat ops dashboard. No shadows, no nested cards.

Or attach this file / `@README` if the repo is open.

---

## Hard rules (always)

These override default component library styling (shadcn, Material, etc.).

- **No box shadows** on panels, cards, or buttons.
- **No card-in-card** — one white surface per section; depth = border + spacing only.
- **No gradients**, glassmorphism, or decorative hero backgrounds.
- **No nested elevated cards** inside panels.
- **Lists = rows** with `border-bottom` dividers, not separate floating cards per item.
- **Facts = label/value pairs** (`dl` / grid), not inset mini-tiles or metric boxes inside rows.
- **Two primary actions** per row or panel; everything else in a `⋯` overflow menu.
- **Queue / priority list is the hero**; map, timeline, or preview is secondary context.

---

## Color tokens

### Text (fixed — every project)

| Role | Hex |
|------|-----|
| Primary | `#292929` |
| Secondary | `#5D5D5D` |
| Tertiary | `#9E9E9E` |

Never use pure `#000000` for body text.

### Surfaces (light theme default)

| Role | Hex |
|------|-----|
| Page background | `#F7F6F3` (warm bone) |
| Panel / card | `#FFFFFF` |
| Muted fill (selected row, secondary bg) | `#F3F3F1` |
| Border / divider | `#EAEAEA` |

### Accent & semantic (light)

| Role | Hex |
|------|-----|
| Primary action (CTA) | `#16A34A` on white text |
| Success badge bg / text | `#EDF3EC` / `#346538` |
| Warning badge bg / text | `#FBF3DB` / `#956400` |
| Critical badge bg / text | `#FDEBEC` / `#9F2F2D` |

Keep **accent** (brand/action) separate from **semantic** (state). Do not use the same hue for both.

### Dark theme

Provide `:root` light tokens + `.dark` overrides. Do not naively invert — pick dark equivalents with the same contrast relationships. Example accent in dark: `#E86B4A`.

---

## Typography

**Stack:** `-apple-system, BlinkMacSystemFont, "SF Pro Text", "SF Pro Display", system-ui, sans-serif`

**Letter-spacing:** `-0.15px` on `html` or `body`, inherited everywhere.

**Weights:** 400 body, 500 emphasis (headers, stats, active nav). No bolder weights — hierarchy from size and color.

**Closed scale — only these sizes:**

| Class / use | Size | Line height |
|-------------|------|-------------|
| Caption, labels, table meta | 12px | 1.4 |
| Body, table cells | 13px | 1.45 |
| Section / panel headers | 14px | 1.4 |
| Page title, hero stat | 24px | 1.2 |

**Numbers in columns or live-updating stats:** `font-variant-numeric: tabular-nums`

---

## Radii

| Element | Radius |
|---------|--------|
| Nav items, small inputs | 8px |
| Panels, cards, tables | 12px |
| Pills, badges, primary CTAs | 999px (full pill) |

---

## Icons

- **14px** — navigation, inline affordances
- **20px** — panel headers, stat areas
- Stroke icons, consistent weight (~1.6px). Lucide is fine for speed.

---

## Layout pattern (ops dashboard)

```
┌ Header — title, time/context, optional theme toggle ─────────────┐
├ Stat strip — 3–4 KPIs in ONE flat panel, vertical dividers ──────┤
├ Priority queue (hero) ────┬ Context + detail (map / timeline) ─┤
├ Full-width table or grid (all items) ────────────────────────────┤
└──────────────────────────────────────────────────────────────────┘
```

- Stat strip: single `.flat-panel` with `divide-x`, not separate cards per metric.
- Queue items: full-width rows inside one panel.
- Selected row: subtle `bg-muted/40`, not a new elevated card.

---

## Components

### Flat panel (base primitive)

Every major section uses this — border only, no shadow:

```css
.flat-panel {
  background: #ffffff;
  border: 1px solid #eaeaea;
  border-radius: 12px;
}
```

Page background stays `#F7F6F3`; panels sit on top as white modules.

### Queue row

- `border-b border-[#eaeaea] last:border-b-0`
- Title line: `13px medium #292929`
- Meta line: `12px #5D5D5D`
- Badge top-right: muted pastel pill (see semantic colors)
- Below: 2×4 `dl` grid of facts (Window, Status, Customer, Last signal — adapt labels to domain)

### Buttons

- Primary: solid accent (`#16A34A`), white text, pill radius, **no shadow**
- Secondary: outline or ghost on `#F3F3F1`
- Destructive actions only in overflow menu unless truly primary

### Badges / status

- Small pill, uppercase optional, wide tracking
- Background = muted pastel; text = darker semantic hue
- Never bright saturated fills on large areas

### Tables

- Header row: `12px #9E9E9E`, uppercase or medium weight
- Cells: `13px`, tabular nums for numbers
- Row hover: `#F3F3F1`, not shadow
- Outer wrapper: `.flat-panel overflow-hidden`

---

## CSS starter (drop into `globals.css`)

```css
:root {
  --background: #f7f6f3;
  --foreground: #292929;
  --card: #ffffff;
  --border: #eaeaea;
  --muted: #f3f3f1;
  --muted-foreground: #9e9e9e;
  --primary: #16a34a;
  --primary-foreground: #ffffff;
  --radius: 0.75rem;
}

body {
  background: var(--background);
  color: var(--foreground);
  font-size: 13px;
  line-height: 1.45;
  letter-spacing: -0.15px;
}

.flat-panel {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 12px;
}
```

---

## What NOT to do (common AI slop)

- Inter / Roboto as unconsidered default
- Purple-blue gradients, heavy shadows, glass cards
- Card-in-card metric tiles
- Marketing-page motion (scroll reveals, bento heroes) on tool UI
- Emoji as section markers
- Generic copy: "Elevate", "Seamless", "Next-Gen"
- Placeholder names: "John Doe", "Acme Corp"

---

## Agent checklist (before shipping UI)

1. Page bg bone, panels white, borders `#EAEAEA` only
2. Zero shadows on custom layout (override library defaults if needed)
3. Type scale stuck to 12 / 13 / 14 / 24
4. Priority list readable in <10 seconds — ranked, with reason visible
5. Two primary actions; rest in `⋯`
6. At least 3 seeded rows with realistic names and distinct states

---

## One-line Cursor prompt

```
Build [FEATURE]. Follow github.com/Rugved/design-skills README: flat utilitarian dashboard, warm bone bg, white bordered panels, no shadows, no nested cards, row-based queue, 12/13/14/24px type, green accent, muted pastel badges.
```
