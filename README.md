# Den & Burrow — Design Standard

A shared, framework-agnostic stylesheet and brand assets for Den & Burrow
internal tools (the `*.denandburrow.com` apps). Use it so every tool — the
Dashboard hub, the Invoice tool, the Build Affordability Calculator, and
whatever comes next — looks like it belongs to the same family.

This is the visual standard distilled from those tools: a clean, Apple-style
system with the "DB" monogram, system fonts, a `#0071e3` accent, soft shadows,
and 8–12px radii.

## What's here

```text
denburrow.css        Full standard: imports tokens.css + base reset + db- components
tokens.css           Design tokens only (CSS variables) — for Tailwind/other tools
example.html         Live component reference (open it in a browser)
assets/
  db-monogram-black.png   Full-res master (1536px), black — for light backgrounds
  db-monogram-gold.png    Full-res master (1536px), gold — for dark backgrounds
  logo-144.png            Web-ready header logo (black)
  logo-gold-144.png       Web-ready header logo (gold / dark mode)
  favicon-32.png          Favicon
  apple-touch-icon.png    iOS home-screen icon (180px)
```

## Install (npm / Vite / build tools)

The repo is public, so any tool can install it straight from GitHub — no token
needed, including on Netlify/CI:

```bash
npm install github:den-burrow/brand-standards
```

```js
// Full standard (tokens + base reset + db- components) — plain/Vite tools:
import 'brand-standards/denburrow.css';

// OR just the design tokens (no base/components) — Tailwind or tools with their
// own base layer:
import 'brand-standards/tokens.css';
```

Vite bundles the logo assets referenced by the CSS automatically. To pin a
version, install from a tag/commit (e.g. `github:den-burrow/brand-standards#v1.0.0`).

## Quick start (plain HTML)

```html
<link rel="stylesheet" href="denburrow.css" />
<link rel="icon" type="image/png" sizes="32x32" href="assets/favicon-32.png" />
<link rel="apple-touch-icon" href="assets/apple-touch-icon.png" />
```

Then either consume the **tokens** in your own CSS, or use the bundled
**component classes** (prefixed `db-`). Both are supported — pick whichever
fits the tool.

```html
<header class="db-header">
  <div class="db-brand">
    <div class="db-logo" role="img" aria-label="Den & Burrow"></div>
    <div>
      <h1>My Tool</h1>
      <p class="db-brand-sub">Den &amp; Burrow</p>
    </div>
  </div>
</header>

<button class="db-btn db-btn--primary">Submit</button>
```

## Design tokens

All tokens are CSS custom properties on `:root` (and overridden under
`[data-theme="dark"]`). Reference them anywhere:

```css
.my-thing { color: var(--db-text); background: var(--db-card); }
```

| Token | Light | Purpose |
| --- | --- | --- |
| `--db-bg` | `#f7f7f8` | Page background |
| `--db-card` | `#ffffff` | Card / surface |
| `--db-border` | `#e5e5ea` | Hairline borders |
| `--db-border-strong` | `#d2d2d7` | Input borders |
| `--db-text` | `#1d1d1f` | Primary text |
| `--db-muted` | `#6e6e73` | Secondary text |
| `--db-accent` | `#0071e3` | Links, focus, accent button |
| `--db-accent-hover` | `#0077ed` | Accent hover |
| `--db-danger` | `#d70015` | Errors / destructive |
| `--db-success` | `#1d7d4f` | Success |
| `--db-radius-sm/md/lg` | `8 / 10 / 12px` | Corner radii |
| `--db-shadow` / `--db-shadow-hover` | — | Elevation |
| `--db-font` | system stack | Typeface |

Font stack: `-apple-system, BlinkMacSystemFont, 'SF Pro Text', 'Segoe UI', Roboto, sans-serif`.

## Component classes

- Layout: `db-container`, `db-header`, `db-brand`, `db-logo`, `db-brand-sub`
- Type: `db-eyebrow` (uppercase section label), `db-muted`, `db-tabular`
- Surfaces: `db-card`, `db-card--interactive`
- Buttons: `db-btn` + `db-btn--primary | --accent | --secondary | --danger`
- Fields: `db-field`, `db-label`, `db-help`, `db-input`, `db-select`,
  `db-textarea`, `db-input-group` + `db-adornment`, `db-check`, `db-radio`,
  `db-radio-card`
- Feedback: `db-status` + `db-status--success | --error`
- Tables: `db-table`
- A11y: `db-visually-hidden`

Open `example.html` to see all of them rendered.

## Dark mode (optional)

Tokens already include a `[data-theme="dark"]` palette and the logo swaps to the
gold monogram automatically. Dark mode is **opt-in** — set the attribute on
`<html>`. To avoid a flash of the wrong theme, resolve it before first paint:

```html
<script>
  (function () {
    var pref = null;
    try { pref = localStorage.getItem('theme'); } catch (e) {}
    var dark = pref === 'dark' ||
      ((!pref || pref === 'auto') && window.matchMedia &&
        window.matchMedia('(prefers-color-scheme: dark)').matches);
    document.documentElement.dataset.theme = dark ? 'dark' : 'light';
  })();
</script>
```

Light-only tools can simply never set the attribute.

## Logo paths

`denburrow.css` references the logo via two variables:

```css
--db-logo: url('./assets/logo-144.png');
--db-logo-dark: url('./assets/logo-gold-144.png');
```

If your assets live elsewhere (CDN, different folder), override them in your own
CSS after the import:

```css
:root { --db-logo: url('/static/db-logo.png'); }
```

For environments that can't serve static files (e.g. Google Apps Script), embed
the monogram as a base64 data URI — see the Dashboard project's `Logos.html`
for a working example.

## Using it in a build (React/Vite, etc.)

Copy `denburrow.css` and `assets/` into the project (or install from the shared
repo) and import the stylesheet once at the entry point:

```js
import './denburrow.css';
```

Reference assets from the public/static directory as usual.

## Used by

- **den-burrow/mortgage-calculator** — imports `denburrow.css` (full standard).
- **den-burrow/subinvoice** (invoice.denandburrow.com) — Tailwind app; imports
  `tokens.css` and bridges its Tailwind theme to the `--db-*` vars.
- **Dashboard** (Apps Script) — the original source of these tokens; mirrors them
  inline because Apps Script can't install npm packages. Keep it in sync.

## Versioning & contributions

`denburrow.css` carries a version comment at the top. When the brand changes:

1. Update the tokens / components here first.
2. Bump the version.
3. Roll the change into each tool.

The canonical monogram masters are `assets/db-monogram-black.png` (light) and
`assets/db-monogram-gold.png` (gold/dark). Regenerate the smaller web variants
from those if the mark ever changes.
