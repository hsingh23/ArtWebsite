# ADR 004 — Contact strategy: mailto link plus builder-backed form

- Date: 2025-05-07
- Status: Accepted (needs follow-up)
- Commits: `4c4cce5`, `07e0b54`

## Context

A portfolio site lives or dies by its contact path. Mobirise ships a Formoid
integration: a styled form posting to the builder's form endpoint with a
hidden per-form token. Out of the box, the navbar "Contact" item pointed at
the `mobiri.se` placeholder.

## Decision

Keep the Formoid form as the on-page contact mechanism (no custom backend
exists or is wanted), and make the navbar Contact link a real
`mailto:art@paintinginbali.com` (`07e0b54`) so the primary navigation path
works regardless of form backend behavior.

## Consequences

- **Positive:** mailto is dependency-free, works on every device with a mail
  client, and uses the custom-domain email that matches the brand.
- **Positive:** zero server code for the form; Formoid handles submission and
  spam-ish filtering on their side.
- **Negative:** the form depends on a third-party endpoint
  (`https://mobirise.eu/`) and an opaque token; if the builder account or
  service changes, the form breaks silently.
- **Negative:** form success/failure feedback is generic ("Thanks for filling
  out the form!" / "Oops...! some problem!") and unbranded.
- Follow-up candidates: verify the Formoid inbox actually receives mail;
  consider replacing the form with a `mailto:` action or a forms provider
  under the owner's control.

## Security note

`index.html` embeds the Formoid token and a Google Maps embed API key as
builder-generated values. They are scoped to the published page but should
never be duplicated into other files or repos.
