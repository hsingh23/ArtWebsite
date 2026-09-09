# ArtWebsite — Artist Portfolio (Painting in Bali)

Static single-page artist portfolio and contact site for the custom domain
**art.paintinginbali.com**, generated with **Mobirise Website Builder v6.0.1**
and published via **GitHub Pages** straight from this repository's `main`
branch. No build step, no package manager, no server: what is committed is
what is served.

## What and why

The site presents the artist ("Rossi Art" / "Painting in Bali") to prospective
clients: a fullscreen parallax hero, career stats, an embedded intro video, a
scrolling portfolio gallery, an about section, testimonials, latest news,
an FAQ accordion, and a contact block (contact form, phone/email/address list,
Google map, social links). It exists to give the art practice a fast, cheap,
zero-maintenance web presence — a plain HTML/CSS/JS bundle that GitHub Pages
serves directly.

## Features

- Single-page layout composed of Mobirise blocks (17 sections from navbar to footer)
- Fullscreen parallax hero (`jarallax`) with "View Work" call-to-action
- Career metrics strip (Years Active / Works Sold / Exhibits Shown)
- Embedded YouTube intro video and a fullscreen YouTube background video section
- Scrolling portfolio gallery (`scroll-gallery`) and moving marquee text strip
- Testimonials carousel (`embla`) with autoplay and drag support
- Latest-news card grid and a 5-question Bootstrap accordion FAQ
- Contact: Formoid-powered form, contact detail list with Google Maps embed, social icon row
- Responsive Bootstrap 5 grid with hamburger navigation on small screens
- Smooth scrolling, sticky navbar, Mobirise/Socicon icon fonts, Manrope web font

## Stack

| Layer     | Technology |
|-----------|------------|
| Generator | Mobirise Website Builder v6.0.1 (theme `startm5`) |
| Layout    | Bootstrap 5.1 (vendored CSS + bundle JS) |
| Font      | Manrope (Google Fonts, weights 400/700) |
| Effects   | jarallax (parallax), embla (carousel), smooth-scroll, YT/Vimeo players |
| Forms     | Formoid (`assets/formoid/formoid.min.js` + hidden form token) |
| Hosting   | GitHub Pages with custom domain via root `CNAME` file |

Theme palette (from `project.mobirise`): background `#F0E6E6`, primary red
`#E5383B`, secondary `#333132`; rounded images, rounded large ghost buttons.

## Quickstart

There is nothing to install or build. To view the site:

```bash
# from the repo root
open index.html          # or serve it, if you prefer:
python3 -m http.server 8000 && open http://localhost:8000
```

To edit the site properly, open `project.mobirise` in the Mobirise builder,
edit, re-publish/export, and commit the regenerated `index.html` +
`assets/` changes together with the updated `project.mobirise`.

To deploy, push to `main` — GitHub Pages serves it at
https://art.paintinginbali.com (requires the domain's DNS CNAME record to
point at the Pages host, which is already configured).

## Repository structure

```
.
├── index.html            # the entire site — one hand-of-god Mobirise export
├── project.mobirise      # Mobirise builder project source (JSON; edit here, not index.html)
├── CNAME                 # GitHub Pages custom domain: art.paintinginbali.com
├── assets/
│   ├── bootstrap/        # vendored Bootstrap 5 CSS/JS
│   ├── mobirise/css/     # mbr-additional.css — site-specific overrides (cache-bust ?v=)
│   ├── theme/            # Mobirise theme CSS/JS (script.js also carries branding links)
│   ├── images/           # all photos/artwork images (Pexels stock placeholders)
│   ├── parallax/  scrollgallery/  embla/   # effect libraries
│   ├── formoid/          # contact-form handler
│   ├── socicon/  web/assets/  dropdown/   # icon fonts, navbar dropdown, misc
│   └── ytplayer/ vimeoplayer/ smoothscroll/ mbr-switch-arrow/
└── .gitignore / .gitattributes
```

## Environment

None. This is a fully static site with no environment variables, no runtime
configuration, and no secrets required to run locally. (Note: `index.html`
ships with an embedded Google Maps embed key and a Formoid form token —
builder-generated values already scoped to the published page.)

## Notes and known debt

- Many links still point to the Mobirise placeholder `https://mobiri.se`
  (nav Home/Portfolio, buttons, social icons, footer) — leftover template
  defaults awaiting real destinations.
- Some copy is template filler ("Lorem ipsum" intro, "Intro with video"
  heading, placeholder phone `+1 555 123 4567`, address, and testimonials).
- Branding is mixed: hero says "Rossi Art", navbar says "Painting in Bali",
  about text describes "Antonio Rossi … from Chicago" — template persona
  versus actual Bali-based identity need reconciling.
- `assets/.DS_Store` and root `.DS_Store` are macOS noise committed by accident.

See `AGENTS.md` for working conventions and `architectural-diary/` for the
project's history and decision records.
