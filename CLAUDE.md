# FLIGHT INTELLIGENCE Ι.Κ.Ε. — corporate site

Project context for Claude Code. This file is read automatically at the start of
each session — treat it as living memory and keep it current as the project moves.

## What this is

A bilingual (EN/EL) **static** site with two jobs:

1. **Public landing** — a deliberately minimal holding page. Indexable. Reveals
   nothing about the product or clients.
2. **Άρθρο 47 corporate-transparency disclosure** — legally required for a Greek
   Ιδιωτική Κεφαλαιουχική Εταιρεία (Ι.Κ.Ε.). Kept off search engines.

Hosted on **GitHub Pages**, custom domain **flight-intelligence.com**. No build
step, no framework, no dependencies — that simplicity is a feature (auditable,
trivially hostable), not an accident.

## File map

| File | Role | Pair |
|---|---|---|
| `index.html` | EL landing (**default at root**, indexable) | ⇄ `en.html` |
| `en.html` | EN landing (indexable) | ⇄ `index.html` |
| `etairika-stoixeia.html` | EL compliance (**noindex**) — *legally operative* | ⇄ `company-details.html` |
| `company-details.html` | EN compliance (**noindex**) | ⇄ `etairika-stoixeia.html` |
| `styles.css` | All styles + brand tokens (design system already ported) | |
| `favicon.svg` | Compass glyph | |
| `sitemap.xml` | Lists the two landings (with hreflang) | |
| `robots.txt` | Disallows both compliance pages; references sitemap | |
| `.gitignore` | Excludes the local brand bundle | |

A language toggle (EL · EN) sits in every header. **EL is the default** —
visiting the root URL serves Greek; English lives at `/en.html`.

## Hard constraints — do not break

These encode legal and strategic decisions, not style preferences:

1. **No third-party requests.** System fonts only — no Google Fonts, no CDN, no
   phone-home analytics. The site must stay GDPR-clean (no consent banner needed).
   All graphics are inline SVG; do not introduce external asset fetches.
2. **The product name is confidential.** Never write "AviaLens" or otherwise name
   the product anywhere public — the EUIPO mark is not yet filed. Copy refers only
   to "our first product" / «το πρώτο μας προϊόν».
3. **Compliance pages stay off search.** Keep the `<meta name="robots"
   content="noindex,nofollow">` tag on both compliance pages *and* their
   `Disallow` lines in `robots.txt`. They are reached only via the footer link —
   that low-prominence-but-linked state is intentional and legally sufficient.
4. **Partner «διεύθυνση» = registered office, never home addresses.** This is a
   deliberate GDPR posture (Art. 6(1)(c) legal-obligation basis + data
   minimisation). Keep the footnote on both compliance pages that documents it.
   Do not add residential addresses, even if it looks "more compliant."
5. **The Greek compliance page is authoritative.** `etairika-stoixeia.html` is the
   legal Άρθρο 47 disclosure; `company-details.html` is a labelled convenience
   translation. Keep their data factually identical — change one, change both.
6. **Keep EN/EL in sync.** Any content or structure change to one language's page
   must be mirrored to its pair, and the language-toggle links kept correct.

## Brand

Design system already ported into this project — tokens live at the top of
`styles.css` (`--navy`, `--mid`, `--light`, …) and the mark is inlined as SVG
in every header. In brief: navy + blues, system fonts, the **expanded compass
mark** (flat-top hex in a thin ring with four cardinal ticks and a centered
aircraft arrow) in the header lockup, recolouring per dark/light header via
the `.mk-*` classes; the same mark as a watermark (full-strength on the navy
hero, faint on the compliance pages); a denser compass favicon optimized for
16–32px; wordmark **FLIGHT INTELLIGENCE** (uppercase, with a space).

## Local-only assets

`flightintelligence-brand/` is the source-of-truth design bundle from Claude
Design (HTML/CSS/JSX prototypes + pre-exported SVGs). It is **excluded from
git** via `.gitignore` and **must never ship** to GitHub Pages — it openly
names the unreleased product, violating hard constraint #2. Use it as a
geometric/color reference only; do not link to or fetch from it at runtime.
The two SVGs the site mirrors are
`flightintelligence-brand/project/assets/logo/FI-mark-expanded.svg` (header
lockup + watermark) and `…/FI-favicon.svg` (favicon).

## Open TODOs

Placeholders are wrapped in `.todo` spans (render orange). Grep for `todo` or `⟨`:

- [ ] **ΓΕΜΗ / GEMI number** — fill on all four pages once the σύσταση registers.
- [ ] **Μερίδια / share-unit counts** per partner — percentages (34/33/33) already
      shown; confirm the unit counts against Foteiou's καταστατικό.
- [ ] **Last-updated date** on both compliance pages.
- [ ] **Registered name spacing** — the legal επωνυμία is currently rendered solid
      (`FLIGHTINTELLIGENCE Ι.Κ.Ε.`) while the brand is two words. Confirm what the
      registry actually uses and align the compliance pages if it carries the space.
- [ ] **Publish gate:** go live only after Foteiou's no-objection on the
      company-address reading (the no-objection email is drafted).

## Run / preview

No install or build. Serve the folder with any static server:

```bash
python3 -m http.server 8000      # then open http://localhost:8000
# or: npx serve
```

## Deploy (GitHub Pages)

1. Push all files to the repo root on `main`.
2. Settings → Pages → *Deploy from a branch* → `main` / `/ (root)`.
3. Custom domain `flight-intelligence.com` (writes a `CNAME`). DNS: apex → four
   `A` records `185.199.108.153`, `185.199.109.153`, `185.199.110.153`,
   `185.199.111.153`; `www` → `CNAME` to `<user-or-org>.github.io`. Enable
   **Enforce HTTPS** once the cert provisions.

## Editing conventions

- Plain HTML/CSS; keep it dependency-free and build-step-free unless there's a
  concrete reason not to.
- After any edit, sanity-check the four inter-page links and both language toggles.
- When in doubt about a legal field, the καταστατικό (and Foteiou) is the source
  of truth — not assumptions.
