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
- [Google Fonts](https://fonts.google.com/) — Playfair Display, Raleway
- [Web3Forms](https://web3forms.com/) — Contact form submissions
- [GitHub Pages](https://pages.github.com/) — Hosting
- Google Maps Embed — Office location

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
- Apex `taylermiddleton.com` redirects to `https://www.taylermiddleton.com`

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

Standard `.ico`, SVG, and Apple Touch icon variants in `/images/` and at root.

---

## Remaining TODOs

### Google Search Console

1. Go to [search.google.com/search-console](https://search.google.com/search-console)
2. **Add property** → URL prefix → `https://www.taylermiddleton.com`
3. **Verify ownership** via HTML tag method — Google provides a meta tag like:
   ```html
   <meta name="google-site-verification" content="your-code-here">
   ```
   Add this tag to the `<head>` of `index.html` (and ideally `about.html`, `faq.html`, `contact.html` too), commit, and push.
4. **Submit sitemap** → Sitemaps → enter `https://www.taylermiddleton.com/sitemap.xml`
5. **Request indexing** → URL Inspection → enter each page URL → Request Indexing

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

### Validate Structured Data

After the site is live, validate the JSON-LD schemas:
1. [Google Rich Results Test](https://search.google.com/test/rich-results) — paste each page URL, confirm no errors
2. [Schema.org Validator](https://validator.schema.org/) — verify JSON-LD is well-formed
3. Check that FAQ page shows as eligible for rich results (expandable FAQ dropdowns in search)

### Get Google Reviews

Ask clients to leave reviews on the Google Business Profile. Review quantity and quality heavily influence local search rankings. This is one of the highest-impact ongoing SEO activities for a local practice.
