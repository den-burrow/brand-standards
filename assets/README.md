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

## The 2026 master export — identified and renamed

Identified and renamed on 2026-08-31 by reading the pixels, not the file names.
The export is **four variants in three colors**, and the old `_1` to `_12` names
carried none of that.

| Variant | Black | White | Gold | Size |
|---|---|---|---|---|
| Arch + monogram + wordmark + DESIGN \| BUILD | `db-lockup-tagline-black.png` | `db-lockup-tagline-white.png` | `db-lockup-tagline-gold.png` | 1500×2501 |
| Arch + monogram + wordmark | `db-lockup-black.png` | `db-lockup-white.png` | `db-lockup-gold.png` | 1500×2501 |
| Arch + monogram | `db-arch-black.png` | `db-arch-white.png` | `db-arch-gold.png` | 1500×2501 |
| Monogram alone | `db-monogram-black.png` | `db-monogram-white.png` | `db-monogram-gold.png` | 1536×1536 |

All twelve are PNG with a transparent background.

### The ink colors, measured

| Name | Hex | Note |
|---|---|---|
| black | `#000201` | **Not** pure `#000000`. Two units of green, one of blue. |
| white | `#ffffff` | The reversed set, for a dark ground. |
| gold | `#9a7d15` | Was `#a38b00` until 2026-08-31. See below. |

**The gold conflict is settled: the token wins.** The artwork shipped at
`#a38b00`, greener and brighter than `--db-brand-gold: #9a7d15`. Max chose the
token value on 2026-08-31, so **all five gold assets were refilled with
`#9a7d15`** — `db-arch-gold.png`, `db-lockup-gold.png`,
`db-lockup-tagline-gold.png`, `db-monogram-gold.png` and `logo-gold-144.png`.
Only the RGB changed; every alpha channel and every dimension is untouched.
The artwork and `tokens.css` now agree, so nothing has to be remembered.

**One consequence is not resolved.** `logo-gold-144.png` is `--db-logo-dark`
and `db-monogram-gold.png` is copied into the tools, and both are used on DARK
grounds. `#9a7d15` on `--db-card` (`#2c2c2e`) is **3.53:1**, below 4.5:1 — and
`#a38b00` was 4.15:1, so this made it slightly worse. That is exactly what the
lifted `--db-brand-gold: #dac062` dark value exists for (7.76:1). **A gold mark
for dark surfaces probably wants its own file at `#dac062`.** Nobody has asked
for one yet.

### Two of the twelve were already here

`_4` and `_12` were **byte-identical** to `db-monogram-black.png` and
`db-monogram-gold.png` — same md5, not merely similar. They were deleted rather
than renamed, because renaming them would have collided with the curated files
the tools already copy at build time. `db-monogram-white.png` (was `_8`) is new:
there was no reversed monogram before.

### Still to decide

Nothing points at the new names yet. `tokens.css` still uses `logo-144.png` and
`logo-gold-144.png`, and `sync-brand-icons.mjs` still copies the monograms.
Whether the 2026 lockups replace those is open, and `tokens.css` and
`sync-brand-icons.mjs` have to change together when it is settled.
