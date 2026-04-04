# Australasian Database Conference (ADC)

This repository hosts the static website for **Australasian Database Conference (ADC)**, an annual conference on database systems, data management, data mining and data analytics. Each year's site lives in its own directory and is deployed to `https://adc-conference.github.io/<year>/`.

The root URL (`https://adc-conference.github.io`) redirects to the current year.

## Repo Structure

```
├── index.html          ← Root redirect + landing page (update yearly)
├── robots.txt          ← Crawling rules
├── sitemap.xml         ← Sitemap index pointing to each year's sitemap
├── sc/                 ← Static build output for Steering Committee Site
├── 2024/               ← Static build output for 2024
├── 2025/               ← Static build output for 2025
│   └── sitemap.xml
├── 2026/               ← Static build output for 2026
│   └── sitemap.xml
└── README.md
```

Each year folder contains the complete static export (e.g. from Next.js `next export`) for that edition. They are fully independent — no shared assets or dependencies between years.

---

## For Maintainers: Adding a New Year

When setting up a new year (e.g. `2027/`), follow this checklist:

### 1. Add your built site

Drop your static build output into a new `2027/` directory. Make sure it includes its own `sitemap.xml`.

### 2. Update `index.html`

Change the redirect target and canonical link to the new year:

```html
<meta http-equiv="refresh" content="0; url=https://adc-conference.github.io/2027/">
<link rel="canonical" href="https://adc-conference.github.io/2027/">
```

Add a link to the new year in the `<nav>`:

```html
<a href="/2027/">2027</a>
```

### 3. Update `sitemap.xml`

Add a new `<sitemap>` entry at the top:

```xml
<sitemap>
  <loc>https://adc-conference.github.io/2027/sitemap.xml</loc>
  <lastmod>2027-XX-XX</lastmod>
</sitemap>
```

### 4. SEO checklist for your year's site

These are recommended but not enforced at the repo level — implement them in your source project before building:

- **Canonical tags** on every page (`<link rel="canonical" href="https://adc-conference.github.io/2027/page/">`)
- **Unique `<title>` and `<meta name="description">`** — don't reuse another year's metadata
- **Cross-edition navigation** — include a link or nav bar to other years so crawlers can discover the full site
- **Event structured data** — add [JSON-LD `Event` schema](https://schema.org/Event) to your homepage for rich search results
- **Open Graph tags** for social sharing previews

---

## How It Works

| File | Purpose |
|---|---|
| `index.html` | Instantly redirects visitors to the latest year. Also contains a minimal landing page with links to all editions, which search engines can index. |
| `robots.txt` | Tells crawlers where to find the sitemap index. |
| `sitemap.xml` | A [sitemap index](https://www.sitemaps.org/protocol.html#index) that references each year's individual sitemap, so search engines can discover all editions from one entry point. |

## License

Apache License 2.0. See [LICENSE](LICENSE) for details.
