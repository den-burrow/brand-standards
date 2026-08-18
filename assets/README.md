# assets

Two different kinds of file live here.

## Curated — safe to use

These have stable names and something depends on each one. Do not rename them.

| File | Used by |
|---|---|
| `logo-144.png` | `tokens.css` → `--db-logo` |
| `logo-gold-144.png` | `tokens.css` → `--db-logo-dark` |
| `db-monogram-black.png` | the tools, copied at build time |
| `db-monogram-gold.png` | the tools, copied at build time |
| `favicon-32.png` | browser tab icon |
| `apple-touch-icon.png` | iOS home screen |

The Hub copies several of these into `public/` during its build, with
`dashboard/scripts/sync-brand-icons.mjs`. Renaming one breaks that script.

## The 2026 master export — not in use yet

`2026-Logo_MASTER - Assets_1.png` through `_12.png`.

- **Nine** are the full lockup at 1500×2501: the arch outline, the DB monogram,
  the DEN & BURROW wordmark, and the DESIGN | BUILD line.
- **Three** are the monogram alone at 1536×1536 (`_4`, `_8`, `_12`).

They are committed exactly as they came out of the design file, under the
exporter's own names. That is deliberate. The point of committing them was to
stop them existing on one disk only. **Nothing references them.**

### Before using them

The names carry no meaning — `_1` and `_5` are both tall, and which is black,
which is gold and which is reversed is not recorded anywhere. Someone who knows
the set has to:

1. Identify what each of the twelve is.
2. Rename them on the pattern the curated files use, for example
   `logo-lockup-black.png`, `monogram-gold.png`.
3. Decide which ones replace the current curated files, and update `tokens.css`
   and `sync-brand-icons.mjs` together.

Do not point `tokens.css` at a file called `2026-Logo_MASTER - Assets_7.png`.
The space in the name and the number that means nothing would both outlive the
person who chose them.
