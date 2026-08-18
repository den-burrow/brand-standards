# Changelog

All notable changes to this project are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project aims to follow [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

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
