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
index.html               Home (Spanish): brand, app catalogue (one .card.card-app per app, 64 px app icon on the left), contact
en/index.html            Home (English)
404.html                 Not-found page (noindex, not in the sitemap)
assets/site.css          Shared styles (light/dark), the only stylesheet
favicon.ico              Website icon (also assets/brand/)
assets/brand/            Website icon PNGs and the nawqira Open Graph image
assets/<appname>/        App images (icon-192.png, feature-es.png, feature-en.png, shots/)
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

## App page standard (approved 2026-10-18)
Every app page (`/<appname>/` and `/en/<appname>/`) uses the shared blocks in `assets/site.css`,
in this order: `.app-hero` (icon 96 px, name, tagline = the Play short description, platform
line) → `.facts` (true facts about this version only) → store-badge comment (Google Play badge
only once published) → `.gallery` (screenshots) → `.features` → `.note` (safety/limits) →
Documents. Per-app personality = two colours on `<body class="app-<appname>">`:
`--app-accent` and `--app-accent-2` (light and dark values). No decorative motifs by default
(contour lines were tried for Orienta AR and declined by the owner).
- **Screenshots:** real screens from the app's store set (1080×2160, status bar removed), one
  theme per set, ES and EN sets; no device mock-ups and no text baked in. Captions and alt
  text are HTML. Served as JPEG (quality 86) at 360 and 540 px wide in
  `assets/<appname>/shots/<lang>-<n>-<name>-<width>.jpg`, `srcset` + `loading="lazy"` +
  `width`/`height`. Same order as on Google Play.
- **Colours:** nawqira green `#1b5e20` / dark `#81c784` on cream `#fcfdf7` / dark `#151714`
  (the app themes use the same values). System font stack; card radius 12 px, screenshot
  radius 16 px, icon radius 22 %.
- Never show third-party content without permission (e.g. a commercial paper map).
  Permitted third-party content carries its credit on the image (owner decision: not repeated in the caption).

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
- 2026-10-18: SEO + languages published (owner-approved): ES/EN pages with hreflang, descriptions, Open Graph, JSON-LD (publisher = privacy controller), robots.txt, sitemap.xml, website icon (proposal B), accessibility. Analytics prepared, not active; ads as invisible markers only. All URLs, assets, redirects and the 404 checked live. Search Console: owner verifying by DNS TXT; sitemap to submit after verification.
- 2026-10-18: Search Console (owner): domain property nawqira.com verified via Cloudflare DNS TXT (keep that record); sitemap submitted, status Correct, 6 pages discovered; / indexed; /orientaar/ indexing requested. Initial SEO setup phase closed by the owner. Next: review Indexing → Pages and Performance after Google processes the site (EN pages included). No DNS, sitemap, analytics or ads changes without owner approval.
- 2026-10-18: Orienta AR page redesigned (owner-approved): screenshot gallery (4 real screens per language, 360/540 px JPEG), facts, feature cards, safety note; reusable app-page blocks in site.css; standard in README. Checked live (pages, 16 screenshots, CSS).
- 2026-10-19: Orienta AR ES page: Map AR and Bearings screenshots added (es-5-mapar, es-6-bearings; ES only, no EN captures yet). They show the Ediciones Desnivel map with the credit band on the image and «Mapa: © Ediciones Desnivel — La Pedriza del Manzanares 1:15.000» in the caption (`figcaption small`). Same day, owner request: gallery order Home, Compass, Map AR, Bearings, Academy, Exercises (file numbers keep the Play order); credit only on the image, removed from the captions. Website use decided by the owner 2026-10-19 based on Desnivel's reply (OrientaAR `docs/THIRD_PARTY_PERMISSIONS.md`).
- 2026-10-19: Home ES/EN: app card shows the app icon (64 px, `icon-192.png`, decorative `alt=""`) left of the texts (`.card-app`, `.card-icon`), owner request.
- 2026-10-22: Support: "Apoya nawqira" / "Support nawqira" section on the homes (between Apps and Contact; owner text, EN translated by Claude) with a plain link styled as `.button` to https://buymeacoffee.com/nawqira (owner page), plus a footer link on the home and app pages. No Buy Me a Coffee script, widget or image: the site still loads nothing third-party and sets no cookies. Website privacy note: one bullet on Buy Me a Coffee + "Updated" date.
- 2026-10-22: Buy Me a Coffee page (owner account, https://buymeacoffee.com/nawqira): profile picture = cream ring + "n" on full-bleed nawqira green (1000 px), cover = flat nawqira green #1b5e20 (2400×600, "portada D"; gradients showed banding). Generated by Claude, uploaded by the owner; source files kept in the git-ignored `resources/buymeacoffee/` (not published). Amounts show in USD (BMC account setting; owner to decide).
- 2026-10-21: Orienta AR ES/EN pages: platform line and JSON-LD `inLanguage` now list the app's six languages (es, en, ca, eu, gl, fr); the website itself stays ES/EN. Requested by the owner.
- 2026-10-21: Orienta AR EN page: Map AR and Bearings screenshots added (en-5-mapar, en-6-bearings; same order as ES, credit on the image only; owner decision). Facts: "Sin publicidad" / "No ads" instead of "Sin publicidad invasiva" / "No intrusive ads" (this version has no ads; owner decision).
- 2026-10-22: A tu Paso privacy policy published at `/atupaso/privacy/` (ES + EN, effective 2026-10-22, app 0.9.9+; source of truth `aTuPaso/docs/PRIVACY.md`), added to `sitemap.xml`; owner request. The A tu Paso app page and home card come later (after the app's last TalkBack test).
