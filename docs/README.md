# Documentation — Pizzaria Italia

Pizza in London, Italian style.

Index of every file generated for this landing page. Each entry has a
dedicated document in this folder describing what the file contains,
how it is organised, and how it connects to the rest.

## Files

| File                       | Documentation                    | Purpose                                          |
| -------------------------- | -------------------------------- | ------------------------------------------------ |
| `index.html`               | [`index-html.md`](index-html.md) | Page markup (semantic HTML5)                     |
| `css/styles.css`           | [`styles-css.md`](styles-css.md) | Full design system (tokens → base → sections)    |
| `js/main.js`               | [`main-js.md`](main-js.md)       | Behaviour: theme, nav, reveals, counters, form   |
| `images/favicon.svg`       | [`favicon-svg.md`](favicon-svg.md) | Brand-mark favicon (vector, gradient)          |

## Site configuration

- **Base framework:** Bootstrap 5 (base utilities + icons)
- **Body font:** `Open Sans`
- **Heading font:** `Raleway`
- **Primary color:** `#FF6347`
- **Accent color:** `#FFD700`
- **Mood:** elegant, modern, inviting
- **Language:** `en`

## How the pieces fit together

1. `index.html` is the entry point. It loads `css/styles.css` and
   `js/main.js` (deferred), and references `images/favicon.svg`.
2. `css/styles.css` defines every visual layer, from CSS custom
   properties (tokens) down to the section-level styles.
3. `js/main.js` attaches behaviour without touching the markup
   structure — it only reads `data-*` attributes and class names.
4. `images/favicon.svg` is referenced once from the `<head>`.