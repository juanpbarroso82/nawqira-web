# Advertising on nawqira.com — prepared, NOT active

_Product-owner decision 2026-10-18: prepare only invisible markers and this document. No AdSense
account, script, banner or visible empty space until the owner explicitly approves activation._

## Allowed placements (marked in the HTML with a comment)
| Marker | Pages | Position |
|---|---|---|
| `<!-- ad-slot: home-after-apps -->` | `/`, `/en/` | after the app cards, before Contact |
| `<!-- ad-slot: app-after-content -->` | `/<appname>/`, `/en/<appname>/` | after the app description, before Documents |

**Never:** privacy policies, the website privacy note, the 404 page, the header, above the main
content, between list items, as pop-ups, interstitials, sticky/anchor or auto-playing video.
At most one discreet ad per page.

## Switching on later (all steps need explicit approval)
1. AdSense account and site approval (small sites are often rejected for "low-value content").
2. In the EEA/UK: a Google-certified consent management platform (TCF); AdSense offers one.
   No ad loads before the visitor's choice.
3. `ads.txt` at the site root with the publisher ID.
4. Spanish LSSI-CE legal notice (name, NIF, address) — open question, see the app project's
   `docs/BUSINESS_ADDRESS_OPTIONS.md`; update the website privacy note and the footer.
5. Replace each marker with `<aside class="ad-slot" aria-label="Publicidad">…</aside>`
   (`.ad-slot` in `assets/site.css` reserves height to avoid layout shifts).
6. One switch: load the ad and consent scripts from a single shared file so removing that file
   (and the slots) disables ads everywhere.
