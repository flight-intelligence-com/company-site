# FLIGHT INTELLIGENCE Ι.Κ.Ε. — corporate site

Bilingual (EN/EL) static site. No build step, no framework, no third-party
requests (system fonts only — keeps the site itself GDPR-clean: no IP leakage to
font CDNs, no consent banner needed).

```
index.html              EL landing  (indexable, default at root)  ⇄ en.html
en.html                 EN landing  (indexable)                   ⇄ index.html
etairika-stoixeia.html  EL compliance (noindex) ← legally operative
company-details.html    EN compliance (noindex)                   ⇄ etairika-stoixeia.html
styles.css              Shared styles (brand tokens)
favicon.svg             Expanded compass mark on navy
robots.txt              Blocks both compliance pages from crawling
sitemap.xml             Lists the two landing pages with hreflang
.gitignore              Excludes the local-only brand bundle
```

A language toggle (EL · EN) sits in every header. The Greek compliance page is
the legally operative Άρθρο 47 disclosure; the English `company-details.html`
is a convenience translation that says so and links back to the Greek.

## Brand assets in use

- **Logo (header):** horizontal lockup = the **expanded compass mark** (flat-top
  hex inside a thin ring with four cardinal ticks and a centered aircraft arrow)
  + the **FLIGHT INTELLIGENCE** wordmark. No product name anywhere — the
  product stays unnamed until the EUIPO mark is filed. The mark recolours per
  header: sky-blue strokes / ice arrow on the navy header, navy strokes /
  sky-blue arrow on the light header.
- **Watermark:** the same expanded mark — full-strength on the navy hero,
  faint "light form" on the compliance pages.
- **Favicon:** a denser variant (larger hex, no outer ring, accent arrow) — the
  most legible glyph at tiny sizes.
- **Source of truth:** the local `flightintelligence-brand/` design bundle.
  Excluded from git via `.gitignore` — it leaks the unreleased product name
  and must never ship.

## The two-layer privacy posture (as agreed with counsel)

- Landings are indexable so the company is findable; no sensitive data on them.
- Compliance pages carry partner data but are kept off search two ways:
  `<meta name="robots" content="noindex,nofollow">` on each page, plus `Disallow`
  in `robots.txt`. They stay reachable by humans via the footer link.
- Partner **«διεύθυνση»** is the registered office, not home addresses, on
  GDPR 6(1)(c) + data-minimisation grounds. Both pages state this in a footnote,
  so an auditor reads the omission as deliberate.

## Already filled in

- Domain **flight-intelligence.com** · email **info@flight-intelligence.com**
- Seat **ToWork — Vasilissis Olgas 83, 54642 Thessaloniki**
- Κ.Α.Δ. main 62.10.11.07 + six secondaries

## Still to fill before publishing (orange `.todo` markers)

- [ ] **Αρ. Γ.Ε.ΜΗ. / GEMI No.** — once the σύσταση is registered (all four pages)
- [ ] **Μερίδια / units** — per-partner share count (percentages 34/33/33 shown; confirm vs the καταστατικό)
- [ ] **Last-updated date** on both compliance pages
- [ ] **Confirm the company-address reading with Foteiou** (the no-objection email) before going live

## Publish on GitHub Pages

1. Create a repo, add all files at the root, push to `main`.
2. Repo → **Settings → Pages** → Source: *Deploy from a branch* → `main` / `/ (root)`.
3. Live in ~1 min at `https://<user-or-org>.github.io/<repo>/`.

### Custom domain — flight-intelligence.com

1. Settings → Pages → **Custom domain** → `flight-intelligence.com` (writes `CNAME`).
2. DNS: apex → four `A` records `185.199.108.153`, `185.199.109.153`,
   `185.199.110.153`, `185.199.111.153`; `www` → `CNAME` to `<user-or-org>.github.io`.
3. Tick **Enforce HTTPS** once the cert provisions.
