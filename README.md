# Tayler Middleton Therapy Website

Static website for [taylermiddleton.com](https://www.taylermiddleton.com) — a therapy practice in Toronto, ON. Built with plain HTML and CSS, hosted on GitHub Pages.

## Pages

- **Home** (`index.html`) — Welcome, Reach Out CTA, Google Maps
- **About** (`about.html`) — My Approach, About Me, Education
- **FAQ** (`faq.html`) — Session fees, sliding scale, scheduling
- **Contact** (`contact.html`) — Contact form (Web3Forms), office photos
- **Thank You** (`thanks.html`) — Post-submission redirect
- **Under Construction** (`index-under-construction.html`) — Preserved fallback page (excluded from indexing via `robots.txt`); see [Under Construction Fallback](#under-construction-fallback) below

## Tech Stack

- HTML5 + CSS3 (no JavaScript, no build step)
- **Self-hosted** Playfair Display + Raleway WOFF2 files in `fonts/` (no Google Fonts dependency)
- [Web3Forms](https://web3forms.com/) — Contact form submissions
- [GitHub Pages](https://pages.github.com/) — Hosting
- Google Maps Embed — Office location
- Psychology Today verified-seal widget (deferred so it doesn't block render)

## Local Development

Open any HTML file directly in a browser. No server or build step required.

## Deployment

Push to `main` — GitHub Pages deploys automatically.

## Under Construction Fallback

The original "Coming Soon" page is preserved at `index-under-construction.html`. It's a self-contained file (inline styles, contact card, Psychology Today badge, Google Maps embed, scoped footer override) and is blocked from indexing by `robots.txt`.

**If you ever need to revert the site to construction mode** (planned downtime, content rewrite, etc.):

1. Swap the files:
   ```sh
   git mv index.html index-full.html
   git mv index-under-construction.html index.html
   ```
2. Update `robots.txt` to disallow `about.html`, `faq.html`, `contact.html`, `thanks.html`, `index-full.html` and only allow `/$` (root). The previous construction-mode `robots.txt` is in git history if you need it.
3. Reduce `sitemap.xml` to only the root URL.
4. Commit and push.

To restore the full site, do the reverse — swap names back, restore the full `robots.txt`/`sitemap.xml` (see current versions in this repo as the reference state).

---

## ✅ Completed Setup

The site is **live**. The following work is done:

### ✅ DNS configured

DNS records at Squarespace point to GitHub Pages.

- **A records** for `taylermiddleton.com`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
- **CNAME** for `www` → `anthony-langford.github.io`
- Custom domain `www.taylermiddleton.com` is saved in repo Settings → Pages
- HTTPS is enforced (Let's Encrypt cert via GitHub Pages)
- Apex `taylermiddleton.com` 301-redirects to `https://www.taylermiddleton.com` — www is the canonical hostname everywhere (canonical tags, OG URLs, sitemap, JSON-LD). All external listings should also use the www variant.

### ✅ Site images (AVIF)

All site images live in `images/` as AVIF. AVIF gives ~5–10× smaller files than JPG at equivalent quality and is supported by all modern browsers (Chrome 85+, Firefox 93+, Safari 16+) — total weight for all 9 images is ~536 KB.

| Filename | Description | Used On |
|----------|-------------|---------|
| `hero.avif` | Mountain landscape banner | All pages (hero, via `styles.css` `.hero`) |
| `tayler-home.avif` | Tayler in cardigan | Home (Reach Out) — `index.html` |
| `tayler-about.avif` | Tayler in blazer | About (About Me) — `about.html` |
| `office-approach.avif` | Therapy room (wide) | About (My Approach background, via `styles.css` `.approach`) |
| `office-couch.avif` | Couch close-up | FAQ (Get In Touch) — `faq.html` |
| `flowers.avif` | White spring blossoms | About (Education) — `about.html` |
| `plant-blurry.avif` | Soft plant shadow | Contact (left background, via `styles.css` `.contact-hero__image`) |
| `office-interior.avif` | Office with bookshelf and lamp | Contact (bottom-left photo) — `contact.html` |
| `plant.avif` | Rubber plant | Contact (bottom-right photo) — `contact.html` |

**Replacing an image:** drop the new file at the same path with the same name and commit. Keep AVIF format and aim for files under ~200 KB. To convert from JPG/PNG, use [squoosh.app](https://squoosh.app/) (effort: max, quality: 50–60).

### ✅ Social sharing image (`og-image.jpg`)

`images/og-image.jpg` (1200×630, ~75 KB JPG) appears when the site is shared on Facebook, LinkedIn, X, iMessage, Slack, etc. It uses Tayler's home-page headshot on a cream background with the practice name in Playfair Display, a gold accent line, MSW/RSW credentials, and a "Therapy in Toronto" tagline.

**Why JPG instead of AVIF here:** social platforms still expect JPG/PNG for `og:image` — many don't reliably parse AVIF for preview cards. JPG is the safe universal format for this single file.

The file is referenced from `index.html` in three places (Open Graph `og:image`, Twitter `twitter:image`, and JSON-LD `image`).

**Regenerating:** if you ever need to rebuild it, the source script is at `/tmp/og-build.py` (uses Pillow + Playfair Display from Google Fonts); save a copy somewhere durable before that tmp file is wiped. To preview how it looks on real platforms after pushing, use [opengraph.xyz](https://www.opengraph.xyz/) or paste the URL into [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/).

### ✅ Hero title contrast

The shared `.hero__title` / `.hero__subtitle` styles in `styles.css` are white with a text-shadow, and the hero overlay is a subtle dark gradient — together this gives the title proper contrast over the mountain background image on every page.

### ✅ `robots.txt` — allow all pages

```
User-agent: *
Allow: /
Disallow: /index-under-construction.html

Sitemap: https://www.taylermiddleton.com/sitemap.xml
```

The construction fallback page is the only path excluded from crawling.

### ✅ `sitemap.xml` — all four pages

Lists `/`, `/about.html`, `/faq.html`, `/contact.html` with appropriate priorities.

### ✅ Contact form

Web3Forms is configured to deliver submissions to `info@taylermiddleton.com`. After successful submission users are redirected to `thanks.html`.

### ✅ Psychology Today badge

The verified seal is embedded on the home page (Reach Out section).

### ✅ Favicons

The "tm" italic monogram (Playfair Display on `#c2d1cc` sage background) is available at multiple sizes so Google Search, browser tabs, and mobile home-screen shortcuts can all pick the right one:

| File | Size | Used for |
|---|---|---|
| `favicon.ico` (root) | 16×16 + 32×32 | Legacy browsers |
| `images/favicon.svg` | vector | Modern browsers (any size, dark-mode aware) |
| `images/favicon-192.png` | 192×192 | Google Search results, Android home screen |
| `images/favicon-512.png` | 512×512 | Future PWA manifest / high-DPI |
| `images/apple-touch-icon.png` | 180×180 | iOS home screen |

> **Note on Google Search favicon refresh:** Google caches favicons aggressively and only re-fetches them every 1–2 weeks. After updating, the search result icon may continue showing the previous icon (or the generic globe) for a while. You can verify what Google currently has cached by visiting `https://www.google.com/s2/favicons?sz=64&domain=taylermiddleton.com`.

### ✅ Performance optimizations

Mobile Lighthouse score: 92+ (median of multiple runs). Desktop: 100. Core Web Vitals: all green.

- **Self-hosted fonts** — eliminates the ~750 ms Google Fonts CSS round-trip; WOFF2 files (~92 KB total) load from same-origin with `font-display: swap`
- **Psychology Today script deferred** — `defer` attribute removes the third-party verified-seal.js from the critical render path
- **All images use AVIF** — ~5–10× smaller than equivalent JPG; lazy-loaded where applicable
- **Google Maps iframe lazy-loaded** — only fetched when scrolled into view
- **No JavaScript build step** — entire site is static HTML/CSS, served straight from GitHub Pages CDN

### ✅ Accessibility

All pages pass WCAG AA with a 100 Lighthouse accessibility score.

- **Contrast ratios** — gold accent text uses `--gold-text: #8b6b2a` (4.97:1 on white); body text uses `--text-light: #5f5f5f` (6.16:1 on white); buttons use dark text on gold for 5.25:1
- **Heading hierarchy** — h1 → h2 → h3 with no skipped levels
- **Semantic landmarks** — every page has `<header>`, `<nav>`, `<main>`, `<footer>` so screen readers can navigate
- **Aria labels** — empty links (e.g., the Psychology Today badge anchor) have `aria-label` so screen readers can announce them
- **Image alt text** — all `<img>` elements have descriptive `alt` attributes

---

### ✅ Google Search Console

- Property verified via DNS TXT record (Domain property — covers apex, www, and any subdomain)
- `sitemap.xml` submitted under Sitemaps
- URL Inspection → Request Indexing run for `/`, `/about.html`, `/faq`, `/contact.html`

Performance data starts populating in GSC ~3–7 days after indexing requests; revisit the Performance tab weekly for the first few months to see what queries are surfacing the site.

### ✅ Legacy Wix URL redirects

The previous Wix site exposed pages at non-canonical slugs that Google had indexed before the migration. To prevent users from hitting 404s when clicking those old search results and to consolidate SEO signals onto the new pages, the old slugs are now handled as follows:

| Old Wix URL | Strategy | Mechanism |
|---|---|---|
| `/about-the-office` | 301-redirect → `/about.html` | `about-the-office.html` stub with `<meta http-equiv="refresh" content="0; url=/about.html">` |
| `/contact-schedule` | 301-redirect → `/contact.html` | `contact-schedule.html` stub with `<meta http-equiv="refresh" content="0; url=/contact.html">` |
| `/faq` | Adopted as the canonical URL | GitHub Pages already serves `faq.html` at both `/faq` and `/faq.html`, so the existing indexed URL keeps working. `<link rel="canonical">` in `faq.html` points at `/faq`, the sitemap lists `/faq`, and all internal nav links use `/faq`. |

Google treats `<meta http-equiv="refresh" content="0; ...">` as a 301 equivalent per [their documentation](https://developers.google.com/search/docs/crawling-indexing/301-redirects#metarefresh). The redirect stubs also include `<meta name="robots" content="noindex">` so the stubs themselves don't appear in search results.

**If more old Wix URLs surface later** (visible in GSC → Indexing → Pages → "Crawled - currently not indexed" or as 404s in real-user traffic), add new redirect stubs using the same pattern: a 10-line HTML file at the old slug name, with a meta refresh pointing at the new canonical URL.

After the redirects deployed, the recommended GSC follow-up:
1. (Optional) **GSC → Removals → New request** for `/about-the-office` and `/contact-schedule` to temporarily hide them while Google processes the 301s
2. Do **not** request indexing for the new `.html` URLs again — Google already has them in its crawl queue. The redirects + canonical signals will resolve the "Crawled - not indexed" state organically over the next few crawl cycles (1–4 weeks)

---

## Remaining TODOs

### Update External Listings

Update the website URL on all external profiles to `https://www.taylermiddleton.com`:

- **Psychology Today** — update website URL in your therapist profile
- **Google Business Profile** — ensure the practice is listed at [business.google.com](https://business.google.com) and the website URL is updated
- **Jane App** — verify booking link is correct (`https://colenmiddletontherapy.janeapp.com/locations/tayler-middleton/book`)
- **Lumino Health** — update if listed
- **Any other directories** — the Wix site can be deactivated once the new site is live and indexed

### Ensure Consistent NAP

NAP (Name, Address, Phone) must match **exactly** across all listings for local SEO:

| Field | Value |
|-------|-------|
| Name | Tayler Middleton Therapy |
| Address | 554 Palmerston Avenue, Suite #3, Toronto, ON, M6G 2P7 |
| Phone | 437-557-3403 |
| Email | info@taylermiddleton.com |

Verify this is identical on:
- This website (footer on every page)
- Google Business Profile
- Psychology Today
- Jane App booking page
- Any other directory listings

### ✅ Validate Structured Data

All four pages validated cleanly in [Google Rich Results Test](https://search.google.com/test/rich-results) and [Schema.org Validator](https://validator.schema.org/).

> **Note on FAQ rich results:** Google deprecated FAQ rich results on 2026-05-07 — expandable Q&A dropdowns no longer appear in search results, and the validation tooling will be removed in June 2026. The `FAQPage` JSON-LD in `faq.html` is kept intentionally because AI Overviews, ChatGPT, Claude, and Bing still parse it; there is no SEO penalty for keeping valid unused schema, and Google may reverse the decision later.

### Get Google Reviews

Ask clients to leave reviews on the Google Business Profile. Review quantity and quality heavily influence local search rankings. This is one of the highest-impact ongoing SEO activities for a local practice.
