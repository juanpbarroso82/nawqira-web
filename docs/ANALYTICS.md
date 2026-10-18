# Visitor statistics — Cloudflare Web Analytics, prepared, NOT active

_Product-owner decision 2026-10-18: prepare the integration but do not add the script until the
privacy-note update is approved and the GDPR / Spanish audience-measurement questions are
resolved. No Google Analytics, cookies or alternative tools._

## Facts (checked 2026-10-18)
- nawqira.com is **DNS-only** in Cloudflare (served directly by GitHub Pages), so Cloudflare's
  automatic injection cannot work. The beacon must be added manually: Cloudflare dashboard →
  Web Analytics → Add a site → hostname `nawqira.com` → copy the JS snippet.
- No Web Analytics beacon is present on the live site today (checked in the served HTML), so
  there is nothing to duplicate. Never enable automatic setup as well.
- Cloudflare states: free; no cookies or localStorage; no fingerprinting via IP; collects page
  URL, referrer, country, browser and page-load timing; beacon from
  `static.cloudflareinsights.com`, data to `cloudflareinsights.com`; 6 months of data access.
  Ad blockers may block the beacon.
- Legal: cookieless measurement is commonly used without a consent banner, but the EDPB
  Guidelines 2/2023 consider that ePrivacy Art. 5(3) can cover scripts that read data from the
  browser. No AEPD statement on this specific service was found. Owner to confirm with an adviser.

## Activation checklist (after approval)
1. Publish the updated website privacy note (approved text) and change the footer link text to
   "Esta web no usa cookies · Privacidad" / "This site uses no cookies · Privacy".
2. Add the snippet once per page, just before `</body>`, on every HTML page (incl. 404).
3. Verify: beacon request in the browser, data in the dashboard, no other tracker present.
4. Update README "Rules" and the workspace memory rule (analytics: Cloudflare only).

## Draft privacy text
Kept out of this public repository until approved (owner's private app repository,
`OrientaAR/docs/WEBSITE_ANALYTICS_PRIVACY_DRAFT.md`).
