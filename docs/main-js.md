# `js/main.js` — behaviour

Single self-contained IIFE, no dependencies. Every feature is opt-in
via a `data-*` attribute or a known class name — the script never
assumes markup that isn't there.

## Modules inside the file

### `applyTheme(mode)` / `currentTheme()`

- `currentTheme()` returns `localStorage['lp-theme']` if present,
  otherwise the OS `prefers-color-scheme`.
- `applyTheme()` sets `data-theme` and `color-scheme` on `<html>`,
  swaps the sun/moon icon on every `[data-theme-toggle]`, and
  updates `aria-pressed`.

### `initNav()`

- Adds `.is-scrolled` to `.site-header` past 8px of scroll.
- Wires `[data-nav-toggle]` to toggle `.is-open` on `[data-nav-links]`,
  updates `aria-expanded`, closes on link click, closes on outside click.

### `initReveals()`

- Observes every `.reveal` element and adds `.is-visible` once it
  enters the viewport (root margin `-60px 0px`).
- Unobserves immediately — reveals are one-shot.
- Falls back to making everything visible if `IntersectionObserver`
  is unavailable.

### `initCounters()`

- Reads every `[data-counter]`, parses `prefix + number + suffix`
  (e.g. `"10k+"`, `"99.9%"`), animates with an ease-out-cubic curve
  over 1.6 s.
- Triggers only when the element is 35% visible.

### `initMisc()`

- **Smooth anchors** — intercepts `a[href^="#"]`, scrolls to the target
  with `scrollIntoView({behavior:'smooth'})`, updates the URL hash.
- **Year** — fills every `[data-year]` with the current year.
- **Form validation** — on `form[data-validate]` submit, highlights
  empty required fields and flashes the submit button label.
- **Active-section highlight** — observes `section[id]` and marks
  the matching `.nav-links a` as active.

### `boot()`

Called on `DOMContentLoaded` (or immediately if the document is
already parsed). Wires the theme toggle click, subscribes to OS
theme changes, then calls all the `init*` functions.

## Markup hooks

| Selector                | Effect                                        |
| ----------------------- | --------------------------------------------- |
| `[data-theme-toggle]`   | Button that flips light/dark                  |
| `[data-nav-toggle]`     | Hamburger that opens the mobile drawer        |
| `[data-nav-links]`      | Drawer container                              |
| `[data-counter]`        | Number animated on scroll                     |
| `[data-year]`           | Auto-filled with the current year             |
| `form[data-validate]`   | Enables client-side required-field validation |

## Local storage

| Key         | Value               |
| ----------- | ------------------- |
| `lp-theme`  | `"light"` / `"dark"`|

## Site

Generated for **Pizzaria Italia**. If you remove or rename any of the hooks
above, the corresponding behaviour simply becomes a no-op — nothing
throws.