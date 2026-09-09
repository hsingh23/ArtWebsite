# ADR 003 — Track project.mobirise alongside the exported site

- Date: 2025-05-07
- Status: Accepted
- Commits: `4c4cce5`, `07e0b54`, `ce06ea8`

## Context

Mobirise separates the editable project (`project.mobirise`, a JSON file
recording pages, blocks, parameters, theme, and even the AI prompt that
seeded the site) from the publishable export (`index.html` + `assets/`).
A repo could track only the export, treating the builder file as private.

## Decision

Commit both. Every builder edit updates `project.mobirise` and the
regenerated `index.html`/`assets/` in the same commit — demonstrated by
`07e0b54` (contact link + hero overlay change in both files) and `ce06ea8`
(stats change in both files).

## Consequences

- **Positive:** the repo is a complete, self-contained project — anyone with
  the Mobirise app can open `project.mobirise` and continue editing the site
  visually; the export alone would be a dead end of generated markup.
- **Positive:** diffs of `project.mobirise` document intent (what the builder
  was told to change), complementing the generated-code diff.
- **Negative:** republishes churn unrelated generated lines — the
  `mbr-additional.css?v=` cache-buster, branding links in
  `assets/theme/js/script.js`, the Formoid token — making diffs noisier than
  the logical change.
- **Negative:** hand-edits to `index.html` that bypass the builder create
  drift that the next republish will clobber. Rule adopted: trivial one-off
  fixes may touch `index.html` directly, but anything meant to survive must
  be made in the builder.
