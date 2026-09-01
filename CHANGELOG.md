# Changelog

All notable changes to this project are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project aims to follow [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- `--db-brand-slate` — a fourth identity color, `#324d76` light and `#8da7ce`
  dark. Chosen 2026-08-31 as the Stripe brand color for invoices, and a brand
  color in its own right.
  - **Why a new hue rather than a lighter navy.** Raising lightness on a 237°
    hue at 69% saturation is how periwinkle is made, so a "less deep navy" could
    only ever walk toward periwinkle. The palette's own geometry pointed
    elsewhere: gold at 47° and navy at 237° are already near-complementary and
    green at 78° is analogous to the gold, which leaves **100–210° empty**.
    Slate sits at 216°. `--db-brand-navy` is untouched, so nothing already drawn
    in navy moves.
  - **Its dark value breaks the house saturation rule on purpose.** The other
    three all land on S 62%; slate's own is 40%, and forcing it to 62 turns it
    into the periwinkle it was chosen to avoid. Hue and saturation are held and
    only lightness moves, 33% → 68%. It reads 5.68:1 on `--db-card`.

- `db-monogram-white.png` — the reversed monogram, which the set never had.

### Changed

- **The gold artwork now matches `--db-brand-gold`.** Every gold asset shipped
  at `#a38b00` while `tokens.css` said `#9a7d15`; the token won, and all five
  files were refilled — the three lockups, the monogram and `logo-gold-144.png`.
  Only the RGB changed, so every alpha channel and dimension is untouched.
  - **Unresolved:** `logo-gold-144.png` is `--db-logo-dark` and
    `db-monogram-gold.png` is copied into the tools, and both are used on dark
    grounds where `#9a7d15` is 3.53:1 — below 4.5:1, and slightly worse than the
    `#a38b00` it replaced. The lifted `#dac062` is what dark surfaces are meant
    to use. A gold mark for dark grounds probably wants its own file.

- **The 2026 logo export is named for what it is.** `_1` to `_12` became
  `db-lockup-tagline-*`, `db-lockup-*`, `db-arch-*` and `db-monogram-*` in
  black, white and gold, identified by reading the pixels. `_4` and `_12` were
  byte-identical to the existing curated monograms and were deleted rather than
  renamed. The measured ink is recorded in `assets/README.md`: black is
  `#000201`, not `#000000`.

- `print.css` — the shared print frame for Den & Burrow documents: cover,
  header lockup, footer, and one canonical set of ink/rule/accent tokens. It
  exists because the Site Report (`01.3`) and the Design Direction Report
  (`01.4`) had drifted into four different "brand" accents between them, and
  they land in the same client packet.
  - The accent is `--db-brand-gold`, which `tokens.css` already nominated for
    "marks, rules, chart series and print". It retires the site report's
    hard-coded `#a8331f` brick red and the brief's `#ae8a54` brass **as frame
    colors** — a document may still use its own colors inside the frame,
    because the site report's parcel outline is a map key and the brief's
    swatch row is the client's palette, not ours.
  - Ink converges on one pair (`#1f1e1a` / `#57554e`) replacing the site
    report's `#1a1a18` and the brief's `#33352c`.
  - It deliberately does **not** set `@page`. The site report is landscape
    sheets, the brief is portrait and flows; each declares its own geometry.
  - `--db-print-logo` is a data URI of the curated `assets/logo-144.png`, so a
    self-contained deliverable can inline the whole file and still show the
    mark with no external reference. The accent and cover-ground tokens carry
    literal fallbacks for that same case, where the `@import` cannot resolve.

- `--db-warning` design token (light `#b25000`, dark `#ff9f0a`) and a
  `db-status--warning` component variant, for the "needs attention, not an
  error" state that sits between success and danger.
- The 2026 logo master export: twelve PNGs in `assets/`, nine of the full
  lockup (arch, monogram, wordmark, "DESIGN | BUILD") at 1500×2501 and three of
  the monogram alone at 1536×1536. Committed exactly as exported, under the
  exporter's own file names. **Nothing references them yet** — `tokens.css`
  still points at `logo-144.png` and `logo-gold-144.png`. Naming and curation
  are a separate job; see `assets/README.md`.
- Continuous integration: CSS syntax validation on every push and pull request.
- Pull request and issue templates to standardize how changes are proposed and tracked.
- Dependabot configuration. Security updates for npm, monthly GitHub Actions
  updates, and no routine npm version bumps (`open-pull-requests-limit: 0`).
- This changelog.
