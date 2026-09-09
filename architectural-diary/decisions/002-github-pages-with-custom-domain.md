# ADR 002 — Host on GitHub Pages with custom domain art.paintinginbali.com

- Date: 2025-05-07
- Status: Accepted
- Commits: `91a9d26`, `30cf03f`

## Context

The static export needed hosting. The owner already had a GitHub account
(hsingh23) and the `paintinginbali.com` domain with a subdomain intended for
the art site.

## Decision

Serve the repository's `main` branch via GitHub Pages and bind the custom
subdomain by committing a root `CNAME` file containing
`art.paintinginbali.com` (created through the GitHub web UI, hence the
no-newline file and "Create CNAME" message). The matching DNS record points
the subdomain at the Pages endpoints.

## Consequences

- **Positive:** zero-cost HTTPS hosting with automatic deploys on push;
  the custom domain gives the artist a professional, memorable URL.
- **Positive:** the CNAME-in-repo approach means domain config is versioned
  alongside content — visible in `git log`.
- **Negative:** the domain is a subdomain of a domain controlled elsewhere;
  if DNS lapses the site silently breaks with no in-repo signal.
- **Negative:** Pages serves only from branch — the single `main` branch is
  both development and production; every push to `main` is a release
  (mitigated in practice by previewing locally before pushing).
- The HTTPS-vs-HTTP asset URLs in the page (YouTube, Google Maps, Google
  Fonts) are all protocol-safe or https, so no mixed-content issues arose.
