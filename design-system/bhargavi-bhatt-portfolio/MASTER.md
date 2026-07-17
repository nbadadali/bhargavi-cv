# Design System Master File

> **LOGIC:** When building a specific page, first check `design-system/pages/[page-name].md`.
> If that file exists, its rules **override** this Master file.
> If not, strictly follow the rules below.

---

**Project:** Bhargavi Bhatt Portfolio
**Generated:** 2026-07-18 (curated override of ui-ux-pro-max auto-suggestion — see notes below)
**Category:** Personal / Executive Portfolio
**Design Dials:** Variance 4/10 (Balanced / Modern) | Motion 4/10 (Standard) | Density 3/10 (Spacious)

**Curation note:** `ui-ux-pro-max --design-system` auto-suggested a generic teal "Healthcare App" palette (`#0891B2`/cyan) and Figtree/Noto Sans typography — this reads like a clinical app, not a senior personal/executive brand. Overridden below with a warm, editorial palette from the tool's own "Luxury/Premium Brand" color entry, paired with an editorial serif+sans typography combo. The Swiss Modernism 2.0 layout system, spacing scale, motion pattern, and accessibility rules from the auto-suggestion were kept as-is — those matched well.

---

## Global Rules

### Color Palette

| Role | Hex | CSS Variable |
|------|-----|--------------|
| Primary (text/ink) | `#1C1917` | `--color-primary` |
| On Primary | `#FFFFFF` | `--color-on-primary` |
| Secondary (muted text) | `#44403C` | `--color-secondary` |
| Accent/CTA (warm bronze/gold) | `#A16207` | `--color-accent` |
| Background | `#FAFAF9` | `--color-background` |
| Foreground | `#0C0A09` | `--color-foreground` |
| Muted surface | `#E8ECF0` | `--color-muted` |
| Border | `#D6D3D1` | `--color-border` |
| Destructive | `#DC2626` | `--color-destructive` |
| Ring | `#1C1917` | `--color-ring` |

**Dark mode:** invert to `--color-background: #14120F`, `--color-foreground: #F5F3F0`, `--color-primary: #F5F3F0`, keep accent `#C9871A` (lightened for contrast on dark), `--color-muted: #211E1A`, `--color-border: #33302C`.

**Color Notes:** Warm near-black + warm off-white + bronze/gold accent — sophisticated, editorial, distinct from generic SaaS blue/teal. Sourced from ui-ux-pro-max's "Luxury/Premium Brand" palette entry (WCAG-adjusted accent).

### Typography

- **Heading/Display Font:** Fraunces (serif, editorial, some optical-size personality)
- **Body/UI Font:** Inter (sans, highly readable at small sizes)
- **Mood:** premium, editorial, confident, senior, distinctive
- **Google Fonts:** [Fraunces + Inter](https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600;9..144,700&family=Inter:wght@300;400;500;600;700&display=swap)

**CSS Import:**
```css
@import url('https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600;9..144,700&family=Inter:wght@300;400;500;600;700&display=swap');
```

### Spacing Variables

*Density: 3/10 — Spacious*

| Token | Value | Usage |
|-------|-------|-------|
| `--space-xs` | `4px` / `0.25rem` | Tight gaps |
| `--space-sm` | `8px` / `0.5rem` | Icon gaps, inline spacing |
| `--space-md` | `24px` / `1.5rem` | Standard padding |
| `--space-lg` | `32px` / `2rem` | Section padding |
| `--space-xl` | `48px` / `3rem` | Large gaps |
| `--space-2xl` | `64px` / `4rem` | Section margins |
| `--space-3xl` | `96px` / `6rem` | Hero padding |

### Shadow Depths

| Level | Value | Usage |
|-------|-------|-------|
| `--shadow-sm` | `0 1px 2px rgba(28,25,23,0.05)` | Subtle lift |
| `--shadow-md` | `0 4px 6px rgba(28,25,23,0.08)` | Cards, buttons |
| `--shadow-lg` | `0 10px 15px rgba(28,25,23,0.10)` | Modals, dropdowns |
| `--shadow-xl` | `0 20px 25px rgba(28,25,23,0.12)` | Hero images, featured cards |

---

## Component Specs

### Buttons

```css
.btn-primary {
  background: var(--color-primary);
  color: var(--color-on-primary);
  padding: 14px 28px;
  border-radius: 4px;
  font-weight: 600;
  transition: all 200ms ease;
  cursor: pointer;
}
.btn-primary:hover { background: var(--color-accent); transform: translateY(-1px); }

.btn-secondary {
  background: transparent;
  color: var(--color-primary);
  border: 1.5px solid var(--color-primary);
  padding: 14px 28px;
  border-radius: 4px;
  font-weight: 600;
  transition: all 200ms ease;
  cursor: pointer;
}
.btn-secondary:hover { border-color: var(--color-accent); color: var(--color-accent); }
```

### Cards

```css
.card {
  background: var(--color-on-primary);
  border: 1px solid var(--color-border);
  border-radius: 8px;
  padding: 24px;
  transition: all 250ms ease;
}
.card:hover { box-shadow: var(--shadow-lg); transform: translateY(-2px); }
```

---

## Style Guidelines

**Style:** Swiss Modernism 2.0 (layout) + Editorial Premium (color/type)

**Keywords:** 12-column grid, mathematical spacing, asymmetric balance, rational hierarchy, warm editorial palette

**Best For:** Corporate/executive personal sites, professional services, editorial

**Key Effects:** `display: grid; grid-template-columns: repeat(12, 1fr); gap: 1.5rem`, mathematical ratios, clear hierarchy

### Page Pattern

**Section order (single-page scroll):** Hero → About → Experience (timeline) → Expertise (skills grid) → Focus Areas (therapeutic areas) → Highlights (achievement stats) → Education & Certifications → Contact → Footer

---

## Motion

**Scroll Reveal (Standard)** — Trigger: IntersectionObserver on scroll | Duration: 350-450ms | Easing: `cubic-bezier(0.16, 1, 0.3, 1)`

Fade + translateY(16px→0) on section entry, staggered ~60-80ms per item on grids/lists. Implemented in vanilla JS (no GSAP dependency — kept the site framework-free per the approved build plan). Fully gated behind `prefers-reduced-motion: no-preference`.

---

## Anti-Patterns (Do NOT Use)

- ❌ Playful design, hidden credentials, AI purple/pink gradients
- ❌ Emojis as icons — use inline SVG icons
- ❌ Missing `cursor: pointer` on clickable elements
- ❌ Layout-shifting hovers (avoid scale transforms that shift surrounding layout)
- ❌ Low contrast text — maintain 4.5:1 minimum
- ❌ Instant state changes — always transition 150-300ms
- ❌ Invisible focus states

---

## Pre-Delivery Checklist

- [ ] No emojis used as icons (use SVG instead)
- [ ] `cursor-pointer` on all clickable elements
- [ ] Hover states with smooth transitions (150-300ms)
- [ ] Light mode: text contrast 4.5:1 minimum
- [ ] Focus states visible for keyboard navigation
- [ ] `prefers-reduced-motion` respected
- [ ] Responsive: 375px, 768px, 1024px, 1440px
- [ ] No content hidden behind fixed navbars
- [ ] No horizontal scroll on mobile
