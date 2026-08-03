# Ox Mode

A one-page static site for **Ox Mode** — "a bounded season in which unused strength
accepts a rightful purpose."

Live: **https://ox-mode.com** (`www` 301s to the apex)

DNS is **Netlify DNS** — the zone was delegated off Porkbun's own nameservers on
2026-08-03 because Porkbun's servers let the default `*` parking wildcard shadow an
explicit `www` CNAME. Porkbun email forwarding was carried across with the zone
(MX `fwd1`/`fwd2.porkbun.com` + the SPF TXT); don't drop those records.
Netlify project: `oxmode` → https://oxmode.netlify.app

## Provenance

Delivered to Mike Wolf by **Mark** as a portable static export
(`Ox_Mode_Static_Site.zip`, dated 2026-07-28) — a Vite/RSC build exported to flat
files. We own it. The first commit in this repo is that export byte-for-byte, so
the diff of everything since is exactly what the estate changed.

## What changed after the handoff (2026-08-03)

| Change | Why |
|---|---|
| `og:url` / `og:image` / `twitter:image` pointed at `http://localhost:3000` | Every social share would have resolved to nothing. Now absolute on `https://ox-mode.com`. |
| Hero + OG image were a single 3.8 MB PNG | The hero is the LCP element. Added `og.webp` (517 KB, q85) for the page and `og.jpg` (768 KB) for social scrapers, which don't reliably take WebP. Verified visually identical at 1:1 crop. Master PNG retained as `og.png`. |
| No `width`/`height` on the hero `<img>` | Layout shift. Now `1536×1024` with `fetchpriority="high"`. |
| No favicon | SOMA-APP-STANDARD §13. `favicon.svg` + `apple-touch-icon.png`, drawn from the site's own wordmark (`#8d2f25` on `#f2eadb`). |
| No feedback affordance | SOMA-APP-STANDARD §8 (enforced). Vendored `soma-feedback` chip → shared VPS feedback service, reviewed via the central queue (§15). |
| No `canonical` / `og:site_name` | Basic share + index hygiene. |

Nothing in the copy, layout, type, or palette was touched. The design is as delivered.

## Files

- `index.html` — the complete one-page site
- `styles.css` — the complete visual design (Tailwind v4 build output)
- `og.webp` / `og.jpg` / `og.png` — hero + social image (serving / social / master)
- `favicon.svg`, `apple-touch-icon.png` — tab identity
- `vendor/soma-feedback/` — canonical SOMA feedback chip, vendored unmodified from
  `SOMA/standards/soma-feedback/`. Do not fork behavior here; update upstream.
- `netlify.toml` — publish root + asset caching
- `README.txt` — the original handoff instructions, kept as delivered

## Deploy

Git-linked to Netlify (SOMA-APP-STANDARD §20) — pushing `main` deploys production.

```bash
netlify deploy          # draft URL for review
netlify deploy --prod   # production
```

_Site delivered by Mark. Estate integration 2026-08-03 by Mike Wolf + Claude (Opus 5)._
