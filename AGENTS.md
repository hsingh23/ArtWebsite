# AGENTS.md — working guide for AI agents

## What this repo is

A static, single-page artist portfolio site exported from **Mobirise Website
Builder v6.0.1** and served by **GitHub Pages** at `art.paintinginbali.com`.
There is no build system, no package manager, no test suite, and no runtime
beyond the browser. Total tracked content: one HTML page, one builder project
file, vendored asset libraries, and images.

## Commands

```bash
# Preview locally (no build step exists)
python3 -m http.server 8000        # then open http://localhost:8000
open index.html                    # good enough for most inspections

# Git
git status
git log --oneline

# Deploy = push to main (GitHub Pages serves it automatically)
git push origin main
```

There are no install/test/lint commands. Do not invent build tooling; adding
a framework would fight the Mobirise workflow (see decision 001).

## Architecture map

```
index.html          ← THE deployed artifact. 788 lines, 17 <section> blocks:
                       menu-5 (sticky navbar) → hero-16 (parallax header18)
                       → metrics-2 (stats) → header07-1 (intro + YouTube embed)
                       → gallery-14 (scroll gallery) → about-us-15 (article)
                       → partners-1 (clients) → call-to-action-1 (header14)
                       → testimonials-1 (embla slider2) → news-1 (features03)
                       → faq-1 (list1 accordion) → image-13 (fullscreen parallax)
                       → features-69 (gallery10 marquee) → video-5 (bg video)
                       → follow-us-1 (social4) → contact-form-3 (form5/formoid)
                       → contacts-2 (map1 + details) → footer-3
project.mobirise    ← builder source of truth (JSON). Blocks appear as
                       "_name": "menu02", "header18", "gallery07", …
CNAME               ← custom domain binding for GitHub Pages
assets/…            ← all JS/CSS/fonts/images the page references (relative paths)
```

Data flow: browser loads `index.html` → static CSS/JS from `assets/` →
third-party iframes (YouTube, Google Maps) and the Formoid endpoint on
interaction. Nothing else.

## Conventions

- **Never hand-edit `index.html` as the primary edit path** unless it is a
  trivial text/link fix you are prepared to redo. The intended loop is:
  edit in Mobirise (which updates `project.mobirise`) → re-publish → commit
  the regenerated `index.html` + `assets/` diff **together** with
  `project.mobirise`, so the two never drift (decision 003).
- Mobirise re-exports churn unrelated lines (cache-bust `?v=` query on
  `mbr-additional.css`, branding URLs in `assets/theme/js/script.js`, the
  Formoid token). Expect that noise in diffs; do not "clean it up" selectively.
- Commit messages: conventional commits (`feat:`, `fix:`, `chore:`, …),
  imperative subject ≤72 chars, body explaining why. This history was
  rewritten on 2026-09-08 to enforce that (see CHANGELOG.md note).
- Images are committed under `assets/images/`; referenced with relative paths
  only. Keep new assets there.
- Do not commit `.DS_Store` (two slipped in historically; leave them unless
  doing a dedicated cleanup commit that also updates `.gitignore`).

## Gotchas

- **`mbr-additional.css?v=WlsqWN`** — the query string is a cache-buster that
  changes on republish; treat changes to it as build noise.
- **Formoid form** posts to `https://mobirise.eu/` with a hidden token; it is
  the builder's form backend, not a custom endpoint. The `mailto:` nav link
  (art@paintinginbali.com) is the reliable contact path today.
- **Placeholder content is everywhere**: `https://mobiri.se` links, lorem-ipsum
  intro, fake phone/address/testimonials, "Intro with video" heading. Check
  before "fixing" — some are intentional-until-replaced (decision 005).
- **Mixed branding** ("Rossi Art" vs "Painting in Bali" vs "Antonio Rossi /
  Chicago") — template persona vs actual domain identity.
- **Embedded credentials-ish values**: a Google Maps embed API key and the
  Formoid token live in `index.html`. Never copy them into new files, docs,
  or commits outside the builder export.
- **Force-push history**: main was rewritten (messages only) on 2026-09-08.
  Old clones may reject pulls; `git pull --rebase` or re-clone resolves it.
  Local branch `backup/pre-docs-20260908` holds the pre-rewrite tip.
- The GitHub remote uses SSH (`git@github.com:hsingh23/ArtWebsite.git`);
  the merge commit in history references the HTTPS URL — both point at the
  same repo.

## Verifying changes

1. Serve locally (`python3 -m http.server 8000`) and load the page.
2. Walk the sections: navbar collapse on narrow window, parallax hero scroll,
   embla testimonial drag, FAQ accordion expand, form render, map iframe.
3. Confirm no console errors (missing asset = broken relative path).
4. `git status` — only intended files changed; `project.mobirise` and
   `index.html` should move together for builder edits.
5. Push to `main` and verify https://art.paintinginbali.com after Pages rebuilds.

## Pointers

- `CHANGELOG.md` — every commit, newest first, with the rewrite note.
- `architectural-diary/main.md` — narrative project history.
- `architectural-diary/decisions/` — ADRs (generator choice, hosting, dual
  source, contact strategy, placeholder debt).
- `prompt.md` — full one-shot recreation prompt for this site.
