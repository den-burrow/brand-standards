# Changelog

All notable changes to this project are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project aims to follow [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- `print.css` — the shared print frame for Den & Burrow documents: cover,
  header lockup, footer, and one canonical set of ink/rule/accent tokens. It
  exists because the Site Report (`01.3`) and the Design Direction Report
  (`01.4`) had drifted into four different "brand" accents between them, and
  they land in the same client packet.
  - The accent is `--db-brand-gold`, which `tokens.css` already nominated for
    "marks, rules, chart series and print". It retires the site report's
    hard-coded `#a8331f` brick red and the brief's `#ae8a54` brass **as frame
    colours** — a document may still use its own colours inside the frame,
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
