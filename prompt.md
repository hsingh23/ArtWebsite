# prompt.md — One-shot recreation prompt for the Painting in Bali artist portfolio

Use this single prompt to recreate this website from scratch in a fresh,
empty repository. It captures every design and content decision embodied in
the original. (Written 2026-09-08 from the site as of commit `ce06ea8`.)

---

## Goal

Build and deploy a **static, single-page artist portfolio website** for the
brand **"Painting in Bali"** (hero brand text: **"Rossi Art"**), published at
**https://art.paintinginbali.com** via GitHub Pages. The page presents the
artist's work and persona, establishes credibility through stats and
testimonials, and offers multiple contact paths. No build step, no server,
no database: a single `index.html` plus vendored CSS/JS/font/image assets,
committable to git and deployable by pushing to `main`.

## Stack

- Plain HTML5 + CSS + JavaScript; one page (`index.html`), ~788 lines.
- Bootstrap 5.1 (vendored `bootstrap.min.css`, `bootstrap-grid.min.css`,
  `bootstrap-reboot.min.css`, `bootstrap.bundle.min.js`).
- Effect/behavior libraries, all vendored under `assets/`:
  - `parallax/jarallax.js` + `jarallax.css` — parallax backgrounds
  - `scrollgallery/scroll-gallery.js` — moving portfolio gallery
  - `embla/embla.min.js` + `embla/script.js` — testimonial carousel
  - `smoothscroll/smooth-scroll.js` — anchor smooth scrolling
  - `ytplayer/index.js`, `vimeoplayer/player.js` — background video players
  - `dropdown/js/navbar-dropdown.js` — navbar behavior
  - `mbr-switch-arrow/mbr-switch-arrow.js` — accordion arrow toggle
  - `theme/js/script.js` — Mobirise theme glue
  - `formoid/formoid.min.js` — contact form handler
- Icon fonts: Mobirise icons (`web/assets/mobirise-icons2/mobirise2.*`,
  font-family "Moririse2") and Socicon (`socicon/`, brand icons + per-network
  background colors).
- Web font: **Manrope** (weights 400 and 700) from the Google Fonts CSS API,
  loaded with the preload-then-stylesheet pattern and a `<noscript>` fallback.
- Generator lineage: originally a Mobirise v6.0.1 AI export (theme `startm5`)
  — recreate the same result in clean hand-authored markup.

## Visual design (be exact)

Theme "StartM5" tokens (from `project.mobirise`):

| Token | Value |
|---|---|
| Background | `#F0E6E6` (warm blush) |
| Primary (buttons, accents) | `#E5383B` (signal red) |
| Secondary / text | `#333132` (near-black) |
| Success / Info / Warning / Danger | `#25C57B` / `#0CBBDE` / `#EAB000` / `#C72332` |
| Font (all display levels + body) | Manrope |
| Type scale | display-1 = 5rem, display-2 = 4rem, display-5 = 2.5rem, display-4 = 1.2rem, display-7 = 1.4rem |
| Shape language | rounded images, rounded buttons, large buttons with ghost (outline) border style |
| Motion | NO scroll animations, NO scroll-to-top button, links not underlined |

Overall feel: soft blush canvas, bold red primaries, generous fullscreen
imagery, oversized display numerals, everything rounded. Favicon is a gallery
image (`assets/images/photo-1580196923-ddad5b516c88.jpeg`).
Page `<title>`: "Artist Portfolio Website: View Artwork, Contact, and
Services". Include the meta description (digital-gallery/artist-portfolio wording).

Stylesheet order in `<head>`: mobirise2 icons → Bootstrap css/grid/reboot →
jarallax.css → dropdown style.css → socicon styles.css → theme style.css →
Google Fonts preload → site-specific `assets/mobirise/css/mbr-additional.css`
(cache-busted with `?v=<short-hash>`). Script order at end of `<body>`:
bootstrap bundle → jarallax → smooth-scroll → ytplayer → navbar-dropdown →
scroll-gallery → embla.min → embla script → mbr-switch-arrow → vimeoplayer →
theme script → formoid.

## Page structure — sections in order

Each is a `<section>` with a unique id; replicate content and layout:

1. **Sticky navbar** (`menu`): fixed-top, expand-lg, custom 4-span hamburger.
   Logo image at 4.3rem + caption "Painting in Bali" (black, display-4).
   Links: Home, Portfolio (both placeholder `#`), **Contact →
   `mailto:art@paintinginbali.com`** with primary-color accent. Right side:
   primary button "Get Quote". Collapses to hamburger below lg.
2. **Fullscreen parallax hero** (`header18`): full-viewport jarallax
   background image; **no overlay** (an earlier 50% black overlay was
   deliberately removed to brighten the image); left-aligned white display-1
   heading **"Rossi Art"**; subline "Where passion meets canvas, colors come
   alive."; white-outline button "View Work".
3. **Metrics strip** (`features10`): three big-number cards — **2** Years
   Active / **30+** Works Sold / **15** Exhibits Shown (display-1 numerals,
   no card imagery).
4. **Intro with video** (`header07`): heading "Intro with video", one-line
   lorem-ipsum paragraph, buttons "Get Started" (primary) and "Read More"
   (primary-outline), below it a responsive 1280×720 YouTube embed
   (video id `-BSQlJxCDcI`) with `mute=1&autoplay=1&loop=1`.
5. **Portfolio scroll gallery** (`gallery07`): full-width auto-scrolling
   grid, 4 artwork images, container animated `translate3d` drifting left.
6. **About** (`article15`): display-5 subtitle "A canvas of emotions,
   brought to life." beside three short paragraphs telling the artist's
   story (graphic-design roots → fine art, city-life inspiration, art as a
   connector).
7. **Partners** (`clients04`): "Our Partners" title, single row of six
   logo/photo tiles (col-lg-2 each).
8. **Call to action** (`header14`): parallax band; centered card (col-lg-8)
   with display-1 "Transform Your Vision" and a primary "Get Started" button.
9. **Testimonials carousel** (`slider2` + embla): center-aligned, autoplay
   every 5s, draggable, skip-snaps; three slides each with a round photo, a
   bold display-5 quote, name, and role — "Incredible artistry; exceeded
   expectations." / Eleanor Hughes / CEO; "Transformed my restaurant's
   ambiance." / Daniel Carter / Chef; "Brought my book to life visually." /
   Sophia White / Author. Prev/next arrow buttons with screen-reader labels.
10. **Latest news** (`features03`): four col-lg-3 cards with image, title,
    date, blurb, "See" button — Gallery Debut (May 7, 2025, "New exhibit at
    the National Gallery."), Art Today Feature (April 20, 2025), Radio
    Interview (March 1, 2025, station KXYZ), Award Winner (February 14,
    2025, "Best Artist").
11. **FAQ accordion** (`list1`): "Common Questions" + five collapsible
    cards — How are artworks made? ("Each piece is crafted with
    precision."); How do collaborations work? ("I work closely with
    clients."); What makes your art? ("My style is unique and vibrant.");
    What materials do you use? ("I use top-quality materials."); How long
    does it take? ("The process takes about 4-6 weeks."). Down-arrow icon
    rotates on expand.
12. **Fullscreen image break** (`image02`): full-viewport parallax photo,
    no content.
13. **Marquee strip** (`gallery10`): two infinite-loop rows of display-1
    text drifting left (speed 0.05): words "Captivating Artistry * Unique
    Creations * " alternating with "Best offers / Free delivery / Perfect
    design / Comfort / Support 24/7 / Vibes" cloud-emoji separators.
14. **Fullscreen background video** (`header18` variant): muted autoplay
    looping YouTube background (id `tBw39LOPG7g`) with a 30%-opacity pure
    black overlay and no content.
15. **Social follow** (`social4`): "Follow Us Now!" heading and four brand
    icon buttons (Facebook, Twitter/X, Instagram, TikTok) with per-network
    colored circles, `target="_blank"`.
16. **Contact form** (`form5`): "Get In Touch"; col-lg-8 centered form with
    Name (text), Email (email), Phone (url input type), Message (textarea),
    and a primary Send button; hidden success/danger alert areas. Wire to
    the Formoid handler: `<form method="POST">` with a hidden
    `data-form-email` token field and `data-form-type="formoid"`.
17. **Contact info + map** (`contacts02`/`map1`): left card listing Phone
    `+1 555 123 4567`, WhatsApp (same number), Email `art@example.com`,
    Address "123 Artsy Avenue, Creative City", Work Time "Mon-Fri: 9am-5pm";
    right half a full-height Google Maps embed centered on Indonesia.
18. **Footer** (`footer3`): link row (Portfolio / Services / About /
    Contact), five social icons (Facebook, Twitter, Instagram, LinkedIn,
    Twitch), copyright "© 2025 Artistry Creations. All rights reserved."
    plus the small builder-credit badge bar.

## Data model

There is no database. All "data" is static, embedded in the page:

- **Images**: ~20 JPEGs under `assets/images/` (Pexels-style stock photos of
  artwork/galleries/interiors), each referenced by relative path; the favicon
  reuses one gallery image.
- **Content records** (inline HTML): 3 metrics, 3 testimonials, 4 news items,
  5 FAQ entries, 5 contact fields, 2 videos, 1 map location.
- **Config files**: `CNAME` (one line: `art.paintinginbali.com`),
  `.gitattributes` (LF normalization), `.gitignore`.

If a future dynamic version is wanted, the natural schema is:
`artwork { id, title, image, year, medium, sold }`, `testimonial { quote,
name, role, avatar }`, `news_item { title, date, body, image, link }` —
kept here only as guidance.

## External APIs by name

- **Google Fonts CSS API** — Manrope 400/700 stylesheet.
- **YouTube embedded player** (iframe `youtube.com/embed/<id>`) — videos
  `-BSQlJxCDcI` (intro, muted/autoplay/loop) and `tBw39LOPG7g` (background,
  muted/loop/controls=0).
- **Google Maps Embed API** — `maps/embed/v1/place?q=Indonesia`; requires a
  browser API key supplied by the implementer (do not commit a personal key
  in new code without reviewing exposure).
- **Formoid** — form posts (via `formoid.min.js`) to `https://mobirise.eu/`
  with a hidden per-form token; replace with any form backend if rebuilding
  independently (e.g., a forms provider under the site owner's account).

## Phased build order

1. **Scaffold repo**: `.gitignore`, `.gitattributes`; empty `index.html`
   with head meta, title, favicon link.
2. **Vendor assets**: commit `assets/` tree — Bootstrap, theme CSS/JS, icon
   fonts, effect libraries, images. Link stylesheets/scripts in the exact
   order listed above.
3. **Skeleton + navbar + hero**: sticky navbar, fullscreen parallax hero
   with the brand headline.
4. **Content sections top-to-bottom**: metrics → intro/video → gallery →
   about → partners → CTA → testimonials → news → FAQ → image break →
   marquee → bg video → social → contact form → contacts/map → footer.
5. **Behavior pass**: initialize jarallax on parallax sections, embla
   autoplay/drag on testimonials, accordion collapse, scroll gallery motion,
   marquee animation, smooth scroll, dropdown toggle.
6. **Contact wiring**: mailto on navbar Contact; form fields + Formoid
   integration (or chosen backend) with success/danger alerts.
7. **Responsive pass**: verify hamburger below lg, grid collapses
   (3-col metrics → stacked, 4-col news → 2 → 1), fullscreen sections on
   mobile, iframes scale.
8. **Deploy**: enable GitHub Pages on `main`, add root `CNAME` file with
   `art.paintinginbali.com`, point the domain's DNS CNAME at the Pages host,
   verify HTTPS.
9. **Content-truth pass**: replace template placeholders (nav/button links,
   lorem intro, phone/address, testimonials) with the artist's real details —
   the original deferred this (see ADR 005 in `architectural-diary/`).

## Acceptance criteria

- [ ] `index.html` is a single self-contained page; opening it locally (no
      server) renders everything except third-party iframes correctly.
- [ ] Sections appear in the order above with the exact copy quoted above.
- [ ] Navbar Contact opens `mailto:art@paintinginbali.com`; mobile hamburger
      expands the menu.
- [ ] Hero and image-break sections fill the viewport with parallax on
      scroll; hero has no dark overlay.
- [ ] Metrics read 2 / 30+ / 15 in display-1 numerals.
- [ ] Testimonial carousel autoplays every 5 s, is draggable, and has
      working prev/next buttons.
- [ ] FAQ accordion expands/collapses all five items with arrow feedback.
- [ ] Marquee strip animates continuously without layout shift.
- [ ] Background video section plays muted/looped with 0.3 black overlay.
- [ ] Contact form renders Name/Email/Phone/Message + Send and submits to
      the configured backend without page error.
- [ ] Map embed loads centered on Indonesia.
- [ ] No console errors; all asset paths relative and resolving.
- [ ] Colors match the palette (#F0E6E6 bg, #E5383B primary, #333132 text);
      Manrope used everywhere; buttons/images rounded.
- [ ] Pushing to `main` publishes to https://art.paintinginbali.com over
      HTTPS via the `CNAME` file.
