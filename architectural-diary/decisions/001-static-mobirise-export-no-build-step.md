# ADR 001 — Static Mobirise export with no build step

- Date: 2025-05-07
- Status: Accepted (implicit; reaffirmed 2026-09-08)
- Commits: `2c5cbc4`, `4c4cce5`

## Context

The artist needed a portfolio site. Requirements were effectively: looks
good, shows work, has a contact path, costs nothing to run, and requires no
programming to maintain. There was no existing codebase, no team, and no
appetite for a framework.

## Decision

Generate the site with Mobirise Website Builder v6.0.1 (AI-assisted, prompt:
"Artist website, with portfolio, contact and list of services") and commit the
raw export — one `index.html`, a `project.mobirise` project file, and vendored
`assets/` — with zero build tooling. What is committed is what is served.

## Consequences

- **Positive:** deploy = push; hosting = free GitHub Pages; performance is a
  single page load with local assets; nothing to patch or upgrade except when
  the builder re-exports.
- **Positive:** the whole system is inspectable in one 788-line HTML file.
- **Negative:** vendor libs are frozen (Bootstrap 5.1, jarallax, embla …) and
  will age; no bundling means no tree-shaking, so the page ships libraries it
  only partially uses.
- **Negative:** programmatic edits are awkward — the builder is the intended
  editor, and hand-edits to `index.html` risk being overwritten on republish
  (see ADR 003).
- The Node-style `.gitignore` from `2c5cbc4` is vestigial scaffolding; there
  is and will be no `node_modules`.
