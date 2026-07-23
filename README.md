# Flat utilitarian UI — design reference

Portable **visual style** for any web UI — dashboard, form, landing page, checkout, settings, mobile web, etc.

**Layout is not prescribed here.** Structure comes from tomorrow's brief. This doc only fixes how things *look*: color, type, borders, spacing, components.

**How to use:** paste in Cursor / Claude:

> Follow https://github.com/Rugved/design-skills README for **visual style only**. Match layout to the brief. Flat UI — no shadows, no nested cards.

Or `@README` if the repo is open.

---

## What always applies (any project type)

These override default component library styling (shadcn, Material, etc.).

- **No box shadows** on panels, cards, or buttons.
- **No card-in-card** — one white surface per section; depth = **border + spacing only**.
- **No gradients**, glassmorphism, or decorative backgrounds (unless the brief explicitly asks for marketing flair — then keep it subtle).
- **No nested elevated cards** inside panels.
- **Separation = `1px #EAEAEA` borders and whitespace**, not elevation.
- **Lists** → rows with `border-bottom` dividers inside one panel, not a floating card per item.
- **Grouped facts** → label/value pairs (`dl` grid or stacked label + value), not inset mini-tile cards.

---

## What does NOT always apply

Read the brief first. **Do not force a dashboard layout** if the project isn't one.

| If the brief is… | Layout comes from the brief, not this doc |
|------------------|-------------------------------------------|
| Marketing / landing | Hero + sections, single column, or split hero — not a stat strip + queue |
| Form / wizard / settings | Single column, stepped sections, sidebar nav |
| E-commerce / checkout | Product grid, cart, step flow |
| Social / feed | Timeline or card feed (still flat — no shadows) |
| Dashboard / ops / admin | See optional pattern at bottom |

**Rule:** derive IA from the user problem. Apply this doc's **tokens and surfaces** to whatever structure you choose.

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
| Muted fill (hover, selected, secondary bg) | `#F3F3F1` |
| Border / divider | `#EAEAEA` |

### Accent & semantic (light)

| Role | Hex |
|------|-----|
| Primary action (CTA) | `#16A34A` on white text |
| Success badge bg / text | `#EDF3EC` / `#346538` |
| Warning badge bg / text | `#FBF3DB` / `#956400` |
| Critical badge bg / text | `#FDEBEC` / `#9F2F2D` |

Keep **accent** (brand/action) separate from **semantic** (state).

### Dark theme

Provide `:root` light tokens + `.dark` overrides. Do not naively invert. Example dark accent: `#E86B4A`.

---

## Typography

**Stack:** `-apple-system, BlinkMacSystemFont, "SF Pro Text", "SF Pro Display", system-ui, sans-serif`

**Letter-spacing:** `-0.15px` on `html` or `body`, inherited everywhere.

**Weights:** 400 body, 500 emphasis. No bolder weights — hierarchy from size and color.

**Closed scale — only these sizes:**

| Use | Size | Line height |
|-----|------|-------------|
| Caption, labels, meta | 12px | 1.4 |
| Body, inputs, table cells | 13px | 1.45 |
| Section headers, nav | 14px | 1.4 |
| Page title, key number | 24px | 1.2 |

**Live or columnar numbers:** `font-variant-numeric: tabular-nums`

---

## Radii

| Element | Radius |
|---------|--------|
| Nav items, inputs, small controls | 8px |
| Panels, sections, modals | 12px |
| Pills, badges, primary CTAs | 999px |

---

## Icons

- **14px** — nav, inline affordances
- **20px** — section headers, feature icons
- Stroke icons, ~1.6px weight. Lucide is fine for speed.

---

## Components (visual style — any layout)

### Flat panel

Base primitive for any grouped content:

```css
.flat-panel {
  background: #ffffff;
  border: 1px solid #eaeaea;
  border-radius: 12px;
}
```

Page background `#F7F6F3`; content sits in white bordered modules.

### List row (when the UI has a list)

- `border-b border-[#eaeaea] last:border-b-0`
- Title: `13px medium #292929`
- Meta: `12px #5D5D5D`
- Optional badge: muted pastel pill (semantic colors above)

### Form fields

- Labels: `12px #5D5D5D`
- Inputs: `13px`, `8px` radius, `1px #EAEAEA` border, white bg
- Group fields in one `.flat-panel` with internal spacing — not one card per field

### Buttons

- Primary: `#16A34A`, white text, pill radius, **no shadow**
- Secondary: outline or ghost on `#F3F3F1`
- Limit visible primary CTAs per screen — don't pepper green buttons everywhere

### Badges / status

- Small pill, muted pastel background, darker text
- Never large saturated fills

### Tables (when the UI has a table)

- Header: `12px #9E9E9E`
- Cells: `13px`, tabular nums
- Row hover: `#F3F3F1`
- Wrapper: `.flat-panel overflow-hidden`

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

## What NOT to do

- Inter / Roboto as unconsidered default
- Purple-blue gradients, heavy shadows, glass cards
- Card-in-card nesting
- Forcing a dashboard template on a non-dashboard brief
- Emoji as section markers
- Generic copy: "Elevate", "Seamless", "Next-Gen"
- Placeholder names: "John Doe", "Acme Corp"

---

## Visual checklist (any project)

1. Bone page bg, white panels, `#EAEAEA` borders only
2. Zero shadows on layout (override library defaults if needed)
3. Type scale: 12 / 13 / 14 / 24 only
4. Layout matches the brief — not a default dashboard
5. Realistic seeded content, not lorem ipsum

---

## Optional: ops / triage dashboard layout

**Use only if the brief is an action dashboard** (dispatch, support queue, admin monitor, etc.). Skip entirely otherwise.

```
┌ Header — title, context ─────────────────────────────────────────┐
├ Stat strip — KPIs in ONE flat panel, vertical dividers ──────────┤
├ Priority list (hero) ─────┬ Detail / context panel ──────────────┤
├ Full-width table or grid ────────────────────────────────────────┤
└──────────────────────────────────────────────────────────────────┘
```

- Priority list = ranked rows in one panel
- Selected row = `bg-muted/40`, not a new elevated card
- Detail panel labels adapt to domain (not hardcoded to dispatch)

---

## Cursor prompts

**Any project (default):**
```
Build [FEATURE]. Follow github.com/Rugved/design-skills README for visual style only — warm bone bg, white bordered panels, no shadows, no nested cards, 12/13/14/24px type, green accent. Layout must match this brief: [describe IA].
```

**Only if brief is an ops dashboard:**
```
… Also use the optional triage dashboard layout section in that README.
```
