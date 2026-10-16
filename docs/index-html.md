# `index.html` — page markup

Semantic HTML5 document. Contains **only markup** — no inline styles
and no inline behaviour beyond one tiny anti-FOUC snippet.

## Structure

```
<!DOCTYPE html>
<html lang="en" data-theme="light">
<head>
    meta (charset, viewport, theme-color, SEO, Open Graph, Twitter)
    <link rel="icon" ... images/favicon.svg>
    <link rel="preconnect" ... google fonts>
    <link rel="stylesheet" ... Google Fonts>
    <link rel="stylesheet" ... bootstrap-icons>
    Loads Bootstrap 5 CSS from a CDN (before the local stylesheet).
    <link rel="stylesheet" href="css/styles.css">
    inline anti-FOUC script
</head>
<body>
    <header class="site-header"> ... </header>          ← nav + theme toggle
    <section class="hero" id="top"> ... </section>      ← hero
    ... section blocks ...                              ← features, stats, etc.
    <footer class="site-footer"> ... </footer>          ← footer
    <script src="js/main.js" defer></script>
</body>
</html>
```

## Head

- `<title>` and `<meta name="description">` come from the SEO spec.
- Open Graph and Twitter card tags mirror the title and description.
- Google Fonts URL is built from `font_body` and `font_heading`.
- Bootstrap Icons is always loaded (feature/testimonial icons rely on it).
- `data-theme="light"` on `<html>` is immediately overwritten by the
  inline script using `localStorage['lp-theme']` or the OS preference.

## Sections rendered

In order: `hero, logos, features, stats, testimonials, pricing, faq, cta, contact`.

The **features** section always renders exactly **6 cards**
in a fixed 3×2 grid (`grid grid--3` inside `section.features--grid`).

## Anti-FOUC

A single inline `IIFE` in the `<head>` reads the stored theme and
sets `data-theme` on `<html>` **before paint**. This is the only
piece of JavaScript allowed to stay inline — deferring it would
cause a flash of the wrong theme.

## External dependencies

- Google Fonts (body + heading).
- Bootstrap Icons (icon font).
- Loads Bootstrap 5 CSS from a CDN (before the local stylesheet).
- `css/styles.css` — local.
- `js/main.js` — local, loaded with `defer`.