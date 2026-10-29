# J&A Freight Systems — Marketing Website

Corporate marketing website for J&A Freight Systems, a Chicago-based freight logistics company. Built as a pure static HTML/CSS/JS site — no framework, no build step required.

---

## What This Project Is

| Detail | Value |
|--------|-------|
| Type | Static multi-page website (core pages + 7 service-line pages, MBE page, coverage page) |
| Stack | HTML5, CSS3, Vanilla JavaScript |
| Fonts | Barlow Condensed (headings) + Barlow (body) via Google Fonts |
| Map | MapLibre GL JS 4.7.1 (service-reach map on the Home page) |
| Forms | Netlify Forms (submissions collected in Netlify dashboard) |
| Deployment | Netlify, auto-deploys from `main` of github.com/jandafreight/J-A-Freight-Website |

---

## How To Run Locally

No build tools needed. Open any page directly in a browser:

```bash
# Option 1 — open index.html directly
open ja-freight-website/index.html

# Option 2 — serve with Python (avoids CORS issues with local video files)
cd ja-freight-website
python3 -m http.server 8080
# then visit http://localhost:8080
```

> **Tip:** Use the Python server if hero background videos don't play — some browsers block `file://` video requests.

---

## Folder Organization

```
ja-freight-repo/              ← Repo root (this is what gets deployed)
├── index.html                ← Home page
├── about.html                ← About Us
├── shippers.html             ← For Shippers
├── carriers.html             ← For Carriers
├── technology.html           ← Technology platform
├── careers.html              ← Join J&A (job listings + application form)
├── positions.html            ← Open positions detail
├── contact.html              ← Contact Us
├── mbe-certified-freight-broker.html ← MBE / supplier-diversity page (SEO audit, Oct 2026)
├── coverage.html             ← Service coverage: hubs, regions, lanes (SEO audit)
├── services/                 ← One page per service line (SEO audit). Paths inside use ../
│   ├── full-truckload.html, ltl.html, refrigerated-freight.html, drayage.html,
│   └── hazmat.html, warehouse.html, managed-transportation.html
├── sitemap.xml               ← Lists every indexable page — add new pages here
├── robots.txt                ← Points crawlers at sitemap.xml
├── _redirects                ← Netlify redirects (legacy WordPress URLs → new pages)
├── css/
│   └── styles.css            ← All styles (single stylesheet)
├── js/
│   └── main.js               ← All JavaScript (single script file)
├── assets/                   ← Images, SVGs, and videos
│   ├── *.png / *.jpg         ← Logos, headshots, illustrations
│   ├── *.svg                 ← Vector assets (e.g. LogoFooterYellow.svg)
│   └── *.mp4                 ← Background / hero videos
├── .gitignore
├── netlify.toml              ← Netlify deployment config
└── README.md                 ← This file
```

---

## How To Edit Content

### Change text on a page
Open the relevant `.html` file in any text editor. Content lives directly in the HTML — look for headings (`<h1>`, `<h2>`), paragraphs (`<p>`), and list items (`<li>`).

### Change the navigation or footer
Navigation and footer are **duplicated** across every page (no server-side includes). To update a nav link or footer text, edit each `.html` file. Pages inside `services/` reference shared files with a `../` prefix. Search for the text you want to change across all files at once:

```bash
grep -rn "text to find" ja-freight-website/
```

### Change colors or fonts
All design tokens are in `css/styles.css` at the top of the file under `:root { }`. Key values:

| Token | Value | Used for |
|-------|-------|----------|
| `--navy` | `#14365C` | Primary navy |
| `--navy-deep` | `#0B2138` | Dark navy backgrounds |
| `--gold` | `#FFC20D` | Brand gold / CTAs |
| `--gold-dk` | `#E2A900` | Gold hover state |

### Swap a background video
Replace the `.mp4` file in `assets/` with the new file using the **same filename**, or update the `<source src="...">` path inside the `<video>` tag in the relevant HTML file.

---

## How To Deploy

The live site (https://jandafreight.com) is hosted on Netlify and linked to the
`jandafreight/J-A-Freight-Website` GitHub repository. Every push to `main`
triggers a production deploy automatically; there is no build step.

**Normal workflow:**
1. Create a branch, make your changes, and open a pull request against `main`
2. Netlify builds a deploy preview for the PR (link appears in the PR checks) — share it for review
3. Merge to `main` — Netlify publishes to jandafreight.com within about a minute

`netlify.toml` holds the publish folder and the custom 404 redirect; everything
else (domain, SSL, form notifications, redirects in `_redirects`) is managed in
the Netlify dashboard or in this repo.

Netlify also collects form submissions (see **Form Submissions** below).

---

## How To Add A New Page

1. Copy an existing page (e.g. `about.html`) and rename it (e.g. `new-page.html`)
2. Update the `<title>` tag, `<meta name="description">`, the `<link rel="canonical">` / `og:` tags, and the `<h1>` heading
3. Edit the content sections
4. Add a link to the new page in the `<nav>` or footer block of the existing pages (search for `<nav` to find them quickly)
5. Add the page's URL to `sitemap.xml`
6. The new page automatically inherits all styles from `css/styles.css` and scripts from `js/main.js`

## SEO Notes (added Oct 2026 from the consultant's site audit)

- Every page has a `<link rel="canonical">`, Open Graph tags, and a keyword `<h2 class="hero-kicker">` under the hero `<h1>`.
- Stat counters (`data-count`) keep their final value in the static HTML so crawlers can read it; `js/main.js` resets them to 0 before animating.
- `_redirects` 301s the legacy WordPress URLs and returns 410 for the compromised `/page-220/` URL.
- The footer social icons link to the company Facebook and LinkedIn pages only. Add other networks when accounts exist.

---

## Form Submissions

All forms use **Netlify Forms** — no backend server required. Submissions appear in the Netlify dashboard under **Forms → Submissions**.

| Form | Page | Netlify form name |
|------|------|-------------------|
| Contact Us | `contact.html` | `contact` |
| Job Application | `careers.html` | `job-application` |
| Newsletter signup | Footer on all pages | `newsletter-signup` |

> **Note:** Forms only work when the site is hosted on Netlify. When running locally, form submits will 404 — this is expected.

To receive email notifications for form submissions: Netlify dashboard → **Forms → [form name] → Form notifications → Add notification → Email**.

---

## Brand Assets

| Asset | File | Usage |
|-------|------|-------|
| Icon mark | `assets/Group-1321315098.png` | Navbar logo |
| Wordmark (yellow) | `assets/LogoFooterYellow.svg` | Footer |
| 40th anniversary | `assets/logo-40years.png` | Carriers page |
| MBE certification | `assets/mbe-certification-copy-1.png` | About page |

Brand colors: Navy `#0B2138` · Gold `#FFC20D`

---

## Local Development Notes

- **Videos** (`assets/*.mp4`) are large files (~10 MB each). They are tracked in git and deployed as-is by Netlify.
- **No npm / Node.js** is required. The site has zero dependencies that need installing.
- **MapLibre GL JS** is loaded from CDN (see `<head>` in `index.html`). An internet connection is required to render the service-reach map.
