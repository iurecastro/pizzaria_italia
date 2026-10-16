# `css/styles.css` — design system

Single plain CSS file. No preprocessor, no build step. Organised
top-to-bottom into five clearly labelled blocks so it reads like a
short design-system document.

## Block 1 — Tokens

Everything is driven by CSS custom properties on `:root`:

- **Colors:** `--brand`, `--brand-2`, `--accent`, `--brand-contrast`,
  `--bg`, `--surface`, `--surface-2`, `--text`, `--text-soft`,
  `--text-muted`, `--border`, `--border-strong`.
  Current brand: primary `#FF6347`, accent `#FFD700`.
- **Typography:** `--font-body` (`Open Sans`) and `--font-heading`
  (`Raleway`), plus two tracking tokens.
- **Layout:** `--container`, `--container-sm`, `--section-y`, `--gutter`.
- **Radii:** `--r-xs` → `--r-full`.
- **Shadows:** `--shadow-xs` → `--shadow-lg`.
- **Motion:** `--ease`, `--dur-fast`, `--dur`, `--dur-slow`.

`[data-theme="dark"]` overrides the color tokens for dark mode.
`@media (prefers-reduced-motion: reduce)` zeroes out every duration.

## Block 2 — Base

Universal reset, typography scale (`h1`–`h4`, `p`, `a`, lists), form
inheritance, focus rings, `.container`, `.section`, `.section-head`,
`.eyebrow`, the `.grid` family and a handful of utility classes.

## Block 3 — Components

Reusable primitives that do not belong to any single section:

- `.btn` + modifiers (`.btn-primary`, `.btn-ghost`, `.btn-light`,
  `.btn-lg`, `.btn-sm`, `.btn-icon`).
- `.badge`.
- `.card` (and `.card--glass`, `.card--plain`), plus `.card-icon`.
- `.site-header`, `.brand`, `.brand__mark`, `.nav-links`, `.nav-actions`,
  `.nav-toggle` — including the mobile drawer at `<=860px`.
- `.field` — form label + input + textarea + select with focus ring.

## Block 4 — Sections

One block per landing-page section:

- `.hero` — shared shell plus four variants: `--split`, `--centered`,
  `--gradient`, `--minimal`.
- `.logos` — ticker wrapper.
- `.features--grid` — **fixed 3x2 grid**, standard layout for the
  6-card features section.
- `.stats__grid`, `.stat`.
- `.steps`, `.step`.
- `.testimonial`, `.pricing__grid`, `.plan`.
- `.faq` (uses native `<details>` / `<summary>`).
- `.cta-block`, `.contact`.
- `.site-footer`, `.footer-grid`, `.footer-col`, `.footer-social`,
  `.footer-bottom`.

## Block 5 — Animations

- `@keyframes` used by the ticker and future accents.
- `.reveal` + `.reveal.is-visible` — scroll-reveal utility driven by
  `IntersectionObserver` in `js/main.js`.
- Delay modifiers `.reveal--d1` → `.reveal--d6`.

## Retheming

To retheme the entire site, edit only the first block:

```css
:root {
    --brand:   #FF6347;
    --accent:  #FFD700;
    --font-body:    'Open Sans', ...;
    --font-heading: 'Raleway', ...;
}
Everything downstream (buttons, cards, hero gradients, footer) uses
those tokens — nothing hard-codes a hex value except purely decorative
overlays.