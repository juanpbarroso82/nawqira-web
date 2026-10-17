# nawqira-web

Public website of the **nawqira** brand (always lowercase): `https://nawqira.com`.
`nawqira.es` redirects permanently (301) to `nawqira.com`. Hosted free on GitHub Pages.
This repository is **public** and holds only the website; app source code stays in its own
private repositories.

## Purpose (phase 1, approved 2026-10-17)
Host the privacy policy of every nawqira app (required by Google Play), basic information
about nawqira and a contact channel. Later phases may grow into a small corporate site
(app catalogue, one page per app, project information, legal documents) on this same
structure, without a rewrite.

## Layout
```
index.html               Home: brand, app catalogue (one .card per app), contact
404.html                 Not-found page
assets/site.css          Shared styles (light/dark), the only stylesheet
<appname>/index.html     App page            e.g. orientaar/
<appname>/privacy/       App privacy policy  e.g. orientaar/privacy/  (ES + EN)
CNAME                    Custom domain for GitHub Pages (nawqira.com)
.nojekyll                Serve files as-is
```
`<appname>` matches the last part of the app's applicationId (`com.nawqira.<appname>`).
**Published URLs never change** (they are registered in Google Play).

## Adding a new app
1. Copy `orientaar/` to `<appname>/` and replace the texts.
2. Write its privacy policy from the app project's `docs/PRIVACY.md` (that file stays the
   source of truth; keep both in sync and update the effective date on every change).
3. Add a card to `index.html`.
4. Commit and push; check `https://nawqira.com/<appname>/privacy/`.

## Rules
- Plain static HTML/CSS; no cookies, analytics, trackers, external fonts or scripts.
- No personal data beyond the public contact nawqira@gmail.com. Never invent a legal entity,
  postal address or registration data.
- Paid services and DNS changes need the product owner's approval.

## DNS (reference)
- `nawqira.com`: DNS managed in Cloudflare, records **DNS only** (grey cloud): apex A/AAAA to
  GitHub Pages, `www` CNAME `juanpbarroso82.github.io`, plus the GitHub Pages
  domain-verification TXT. HTTPS by GitHub Pages (Let's Encrypt), "Enforce HTTPS" on.
- `nawqira.es`: registered at IONOS, DNS moved to Cloudflare (IONOS MX records kept);
  proxied placeholder A records (192.0.2.1) for `@` and `www` + redirect rule (301) to
  `https://nawqira.com` keeping path and query; HTTPS by Cloudflare.

## Status
- 2026-10-17: phase-1 site prepared and committed locally; publication authorized by the
  product owner.
- 2026-10-18: live at https://nawqira.com (HTTPS enforced; www and http redirect). nawqira.es and www.nawqira.es redirect (301, path + query kept) to https://nawqira.com, HTTPS by Cloudflare (checked 2026-10-18; IONOS MX kept).
- 2026-10-18: Orienta AR policy v0.5.3 (controller Juan Pedro Barroso, effective 2026-10-18) and website privacy note (/privacy/) published; all links checked (200).
