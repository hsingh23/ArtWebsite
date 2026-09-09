# Changelog

All notable changes to this project are documented here, newest first.

> **History rewrite note (2026-09-08):** commit messages were rewritten via a
> messages-only `git filter-branch` (trees and file contents untouched) to
> replace vague subjects ("updates", "contact", "Website initial") with
> conventional-commit messages. Hashes changed; content did not. The pre-rewrite
> tip was `7de95fe`; a local backup branch `backup/pre-docs-20260908` preserves it.

## 2025-05-07

- **ce06ea8** — `fix: correct homepage stats to 2 years active and 30+ works sold`
  - Change the metrics block from placeholder figures (7 years, 300+ sold) to 2 years active and 30+ works sold, in both `index.html` and `project.mobirise`.
  - Refresh Mobirise-generated branding links in `assets/theme/js/script.js` and bump the `mbr-additional.css` cache-bust query from a site republish.
- **30cf03f** — `chore: merge remote main to pick up CNAME from GitHub`
  - Reconcile locally diverged `main` with the remote; the remote side contributed the GitHub Pages `CNAME` file (custom domain), nothing else.
- **07e0b54** — `feat: point Contact nav link to art@paintinginbali.com mailto`
  - Replace the `mobiri.se` placeholder href on the navbar Contact item with `mailto:art@paintinginbali.com` (also in `project.mobirise`).
  - Drop the hero section's black 50% overlay so the parallax background renders unfiltered.
- **91a9d26** — `chore: add CNAME mapping site to art.paintinginbali.com`
  - Add a top-level `CNAME` file containing `art.paintinginbali.com`, binding the GitHub Pages site to that custom subdomain.
- **4c4cce5** — `feat: import initial Mobirise-built artist portfolio site`
  - Import the complete Mobirise v6.0.1 export: single-page `index.html`, the `project.mobirise` builder source, and vendored assets (Bootstrap 5, theme CSS/JS, jarallax, embla carousel, Formoid, smooth-scroll, YouTube/Vimeo players, icon fonts) plus gallery images.
  - Establishes the site as a self-contained static bundle with no build step.
- **2c5cbc4** — `chore: initialize repo with gitignore and gitattributes`
  - Add a stock Node.js-style `.gitignore` template and a `.gitattributes` enforcing LF normalization as repo scaffolding.

## 2026-09-08

- Documentation release: `README.md`, `AGENTS.md`, this `CHANGELOG.md`, the
  `architectural-diary/` (project history and decision records), and `prompt.md`
  (one-shot recreation prompt), added on top of the rewritten history.
