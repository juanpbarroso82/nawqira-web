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
index.html               Home (Spanish): brand, app catalogue (one .card per app), contact
en/index.html            Home (English)
404.html                 Not-found page (noindex, not in the sitemap)
assets/site.css          Shared styles (light/dark), the only stylesheet
favicon.ico              Website icon (also assets/brand/)
assets/brand/            Website icon PNGs and the nawqira Open Graph image
assets/<appname>/        App images (icon-192.png, feature-es.png, feature-en.png)
<appname>/index.html     App page, Spanish       e.g. orientaar/
en/<appname>/index.html  App page, English       e.g. en/orientaar/
<appname>/privacy/       App privacy policy, bilingual ES + EN in one page (stable URL)
privacy/                 Website privacy note, bilingual
robots.txt, sitemap.xml  SEO (sitemap lists real pages with real last-modified dates)
docs/                    Internal notes (ADS.md, ANALYTICS.md); excluded in robots.txt
CNAME                    Custom domain for GitHub Pages (nawqira.com)
.nojekyll                Serve files as-is
```
`<appname>` matches the last part of the app's applicationId (`com.nawqira.<appname>`).
**Published URLs never change** (they are registered in Google Play).

## Languages and SEO (approved 2026-10-18)
- Presentation pages exist in Spanish (`/…`) and English (`/en/…`), linked with `hreflang`
  (es, en, x-default = Spanish), a self-referencing `canonical` and an ES/EN switch. No automatic
  redirects by location or browser language.
- Every page: unique `<title>` and meta description, Open Graph tags, skip link.
- Structured data (JSON-LD) only with facts visible on the page: `WebSite` on the homes,
  `MobileApplication` on app pages; publisher = the privacy controller (Person + brand). No ratings, reviews, price or download link until the app
  is actually published on Google Play.
- When a page changes, update its `<lastmod>` in `sitemap.xml` to the publication date.

## Adding a new app
1. Copy `orientaar/` to `<appname>/` and `en/orientaar/` to `en/<appname>/`; replace texts,
   images (`assets/<appname>/`), hreflang/canonical URLs and JSON-LD.
2. Write its privacy policy from the app project's `docs/PRIVACY.md` (that file stays the
   source of truth; keep both in sync and update the effective date on every change).
3. Add a card to `index.html` and `en/index.html`, and the pages to `sitemap.xml`.
4. Commit and push; check `https://nawqira.com/<appname>/privacy/`.

## Visual identity
Website icon (owner choice 2026-10-18, proposal B): green "n" in a green ring on cream —
`favicon.ico` (16/32/48), `assets/brand/favicon-32.png`, `apple-touch-icon.png` (opaque 180),
`icon-512.png`; Open Graph image `assets/brand/og-nawqira.png` (1200×630, symbol + name only,
no claim). It is the website icon, **not a definitive logo**. App pages reuse the approved app
store graphics (`assets/<appname>/`). Structured-data publisher = the privacy controller
(Person "Juan Pedro Barroso", brand nawqira, nawqira@gmail.com); never an invented company.

## Rules
- Plain static HTML/CSS; no cookies, analytics, trackers, external fonts or scripts.
  Cloudflare Web Analytics is prepared but not active (`docs/ANALYTICS.md`); advertising is
  prepared as invisible markers only (`docs/ADS.md`). Both need explicit approval to activate.
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
