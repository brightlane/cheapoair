# CheapoAir Deals - Affiliate Website

A fully static 24-page affiliate website promoting CheapoAir.com.
Built from a single Python script. Auto-deploys to GitHub Pages on every push.

**Live site:** https://brightlane.github.io/cheapoair/

---

## Repo Structure

```
cheapoair/
├── build.py                        # Run this to generate all 27 files
├── README.md                       # This file
├── .github/
│   └── workflows/
│       └── deploy.yml              # Auto-build and deploy on push to main
└── dist/                           # Generated output — never edit manually
    ├── index.html
    ├── cheap-flights.html
    ├── cheap-hotels.html
    ├── vacation-packages.html
    ├── last-minute-deals.html
    ├── international-flights.html
    ├── domestic-flights.html
    ├── business-class-deals.html
    ├── weekend-getaways.html
    ├── travel-tips.html
    ├── best-time-to-book.html
    ├── flight-hacks.html
    ├── travel-insurance.html
    ├── flights-to-cancun.html
    ├── flights-to-miami.html
    ├── flights-to-new-york.html
    ├── flights-to-las-vegas.html
    ├── flights-to-london.html
    ├── flights-to-paris.html
    ├── flights-to-tokyo.html
    ├── flights-to-bali.html
    ├── about.html
    ├── contact.html
    ├── 404.html
    ├── robots.txt
    ├── sitemap.xml
    └── llms.txt
```

---

## Quick Start

### Build locally
```bash
python build.py
```
All 27 files are written to `/dist`. No pip installs needed — standard library only.

### Preview locally
```bash
cd dist
python -m http.server 8000
# Open http://localhost:8000/cheapoair/
```

---

## GitHub Actions — Auto Deploy

Every push to `main` triggers the workflow automatically:

```
push to main
  → python build.py
  → /dist uploaded to GitHub Pages
  → live at https://brightlane.github.io/cheapoair/
```

### Setup (one time only)

1. Go to **Settings → Pages → Source → GitHub Actions**
2. Push any commit to `main`
3. Done — Actions tab shows the build status

---

## Pages

All 24 pages link to your affiliate URL throughout — nav, hero, deal cards, CTA strips, and footer.

| Page | Buyer Intent | What's on It |
|------|-------------|--------------|
| `/` | Browse / brand | Hero, 9 deal cards, features, destinations grid, CTA |
| `/cheap-flights.html` | High-volume search | 9 deals, how-it-works steps, 8 tips checklist, 5 FAQs |
| `/cheap-hotels.html` | Hotel bookings | 9 hotel deals, why-book features |
| `/vacation-packages.html` | Bundle buyers | 9 flight+hotel packages |
| `/last-minute-deals.html` | Urgency buyers | 9 last-minute deals with urgency copy |
| `/international-flights.html` | Long-haul search | 9 international deals, route data table |
| `/domestic-flights.html` | US travel | 9 US route deals |
| `/business-class-deals.html` | High-value buyers | 6 premium deals, business class features grid |
| `/weekend-getaways.html` | Impulse travel | 9 weekend deals |
| `/travel-tips.html` | Informational | 12 money-saving tip cards |
| `/best-time-to-book.html` | Informational | 8-route data table, 5 golden rules |
| `/flight-hacks.html` | Informational | 10 advanced hacks with full explanations |
| `/travel-insurance.html` | Add-on sales | Coverage table, CTA |
| `/flights-to-cancun.html` | Destination search | 6 deals, 5 FAQs |
| `/flights-to-miami.html` | Destination search | 6 deals, 5 FAQs |
| `/flights-to-new-york.html` | Destination search | 6 deals, 5 FAQs |
| `/flights-to-las-vegas.html` | Destination search | 6 deals, 5 FAQs |
| `/flights-to-london.html` | Destination search | 6 deals, 5 FAQs |
| `/flights-to-paris.html` | Destination search | 6 deals, 5 FAQs |
| `/flights-to-tokyo.html` | Destination search | 6 deals, 5 FAQs |
| `/flights-to-bali.html` | Destination search | 6 deals, 5 FAQs |
| `/about.html` | Trust building | Mission, affiliate disclosure |
| `/contact.html` | Partnerships | Booking support, disclosure |
| `/404.html` | Error recovery | Animated 404 with affiliate CTA |

---

## Customisation

### Change the affiliate URL
Edit the top of `build.py`:
```python
AFF = "https://convert.ctypy.com/aff_c?offer_id=28692&aff_id=21885"
```
Every link across all 24 pages updates in one rebuild.

### Change the base URL or subpath
```python
BASE = "https://brightlane.github.io/cheapoair"
SUB  = "/cheapoair"
```
Update both if you move to a custom domain.

### Add a new destination page
Add an entry to the `DESTINATIONS` list in `build.py`:
```python
("flights-to-rome", "Rome", "Italy", "Colosseum",
 "linear-gradient(135deg,#7f1d1d,#f59e0b)", "$279",
 "The Colosseum, Vatican City, and the world's best pasta await.",
 [
     ("New York -> Rome", "Direct", "linear-gradient(135deg,#dc2626,#b91c1c)", "$329", "coral"),
     ("Chicago -> Rome", "Europe", "linear-gradient(135deg,#0ea5e9,#0369a1)", "$349", "gold"),
     ("LA -> Rome", "Via London", "linear-gradient(135deg,#4a044e,#9d174d)", "$369", "green"),
     ("Miami -> Rome", "Nonstop", "linear-gradient(135deg,#064e3b,#10b981)", "$339", "coral"),
     ("Boston -> Rome", "Direct", "linear-gradient(135deg,#0c4a6e,#0369a1)", "$319", "gold"),
     ("Dallas -> Rome", "1 Stop", "linear-gradient(135deg,#431407,#ea580c)", "$359", "green"),
 ]),
```
Run `python build.py` and the page, sitemap entry, nav footer link, and all internal links are created automatically.

### Update deal prices
Each deal is a tuple:
```python
("Route Name", "Badge Text", "CSS gradient", "$Price", "badge-colour", "Note")
```
Badge colour options: `"coral"` (red), `"gold"` (yellow), `"green"` (emerald).

---

## SEO Files

| File | Purpose |
|------|---------|
| `robots.txt` | Allows all crawlers, points to sitemap, hides build files |
| `sitemap.xml` | 24 URLs with priorities and change frequencies for Google |
| `llms.txt` | AI/LLM instructions per llmstxt.org — helps AI assistants surface the site |

---

## Requirements

- Python 3.8 or higher
- Standard library only — no pip installs needed
- Git + GitHub account

---

## Known Issues Fixed

| Issue | Fix Applied |
|-------|------------|
| `SyntaxError: invalid character` on deploy | All non-ASCII characters removed from Python source. HTML output retains all emoji via `&#XXXXX;` HTML entities. |
| Internal links 404 on GitHub Pages | All `href` paths use `/cheapoair/` subpath matching the GitHub Pages URL structure for the `brightlane/cheapoair` repo. |
| `BASE_URL` mismatch across versions | Correct value: `BASE = "https://brightlane.github.io/cheapoair"` and `SUB = "/cheapoair"` |

---

## Affiliate Disclosure

This site earns commissions through the CheapoAir affiliate program. All prices shown are illustrative examples — actual live fares are displayed at time of booking on CheapoAir.com. The disclosure appears in the footer of every page and on the About page. This site is not affiliated with or operated by CheapoAir.com — it is an independent affiliate partner.

---

## License

MIT — free to use, modify, and deploy.
