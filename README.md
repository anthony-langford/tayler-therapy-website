# Tayler Middleton Therapy Website

Static website for [taylermiddleton.com](https://www.taylermiddleton.com) — a therapy practice in Toronto, ON. Built with plain HTML and CSS, hosted on GitHub Pages.

## Pages

- **Home** (`index.html`) — Welcome, Reach Out CTA, Google Maps
- **About** (`about.html`) — My Approach, About Me, Education
- **FAQ** (`faq.html`) — Session fees, sliding scale, scheduling
- **Contact** (`contact.html`) — Contact form (Web3Forms), office photos
- **Thank You** (`thanks.html`) — Post-submission redirect

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

---

## TODO

### Configure DNS

Update DNS records at your domain registrar to point to GitHub Pages:

**A records** for `taylermiddleton.com`:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**CNAME** for `www`:
```
anthony-langford.github.io
```

After DNS propagates (can take up to 48 hours):
1. Go to repo Settings → Pages → Custom domain → enter `www.taylermiddleton.com`
2. Check "Enforce HTTPS"

### Configure Web3Forms

1. Go to [web3forms.com](https://web3forms.com) dashboard
2. **Verify `info@taylermiddleton.com`** — Web3Forms sends a verification email to confirm the address
3. **Update the recipient email** to `info@taylermiddleton.com` so form submissions go to the practice inbox (not your personal email)
4. Test the form on the live site to confirm submissions arrive

### Fix Psychology Today Embed

The current badge uses a partial SVG that only shows the checkmark and "VERIFIED BY" text. To get the full badge with the "Psychology Today" wordmark:

1. Log in to the [Psychology Today member portal](https://member.psychologytoday.com/)
2. Find the **verification badge** or **website widget** section
3. Copy the full embed code — it will look like:
   ```html
   <a href="https://www.psychologytoday.com/profile/1148224" class="sx-verified-seal"></a>
   <script type="text/javascript" src="https://member.psychologytoday.com/verified-seal.js" data-badge="16" data-id="1148224" data-code="YOUR_CODE"></script>
   ```
4. Replace the `<div class="footer__badge">` contents in all pages (`index.html`, `about.html`, `faq.html`, `contact.html`, `thanks.html`) with the full embed code

### Replace Placeholder Images

Save these images from the current Wix site to `images/`:

| Filename | Description | Used On |
|----------|-------------|---------|
| `hero.jpg` | Mountain landscape banner | All pages (hero) |
| `tayler-home.jpg` | Tayler's portrait | Home (Reach Out) |
| `tayler-about.jpg` | Tayler's portrait | About (About Me) |
| `office-approach.jpg` | Therapy room interior | About (My Approach background) |
| `office-couch.jpg` | Office couch/pillows | FAQ (Get In Touch) |
| `flowers.jpg` | Cherry blossoms | About (Education) |
| `plant-blurry.jpg` | Blurry plant/leaves | Contact (left background) |
| `office-interior.jpg` | Office room | Contact (bottom left photo) |
| `plant.jpg` | Rubber plant | Contact (bottom right photo) |

After adding images, update the CSS and HTML to use local paths instead of Unsplash URLs:
- `styles.css` — replace Unsplash URLs in `.hero` and `.approach` background-image
- HTML files — replace `https://images.unsplash.com/...` `src` attributes with `images/filename.jpg`

**Optimize images** before committing — resize to max 1600px wide, compress with [squoosh.app](https://squoosh.app/) or similar.

### Add Favicon

1. Create or obtain a logo/icon
2. Generate favicon files at [favicon.io](https://favicon.io/)
3. Add to the project:
   - `favicon.ico` (root)
   - `images/favicon.svg`
   - `images/apple-touch-icon.png` (180x180px)

### Add Social Sharing Image

Create `images/og-image.jpg` (1200x630px recommended). This image appears when the site is shared on Facebook, LinkedIn, Twitter, etc. A simple option: the hero image with "Tayler Middleton Therapy" text overlaid.

### Google Search Console

1. Go to [search.google.com/search-console](https://search.google.com/search-console)
2. **Add property** → URL prefix → `https://www.taylermiddleton.com`
3. **Verify ownership** via HTML tag method — Google provides a meta tag like:
   ```html
   <meta name="google-site-verification" content="your-code-here">
   ```
   Add this tag to the `<head>` of every page, commit, and push
4. **Submit sitemap** → Sitemaps → enter `https://www.taylermiddleton.com/sitemap.xml`
5. **Request indexing** → URL Inspection → enter each page URL → Request Indexing

### Google Maps Embed

The current embed uses a search query URL. For a more reliable embed:
1. Go to [Google Maps](https://maps.google.com) → search "554 Palmerston Ave, Toronto"
2. Click Share → Embed a map → copy the iframe `src` URL
3. Replace the `src` in all pages that have the map (`index.html`, `about.html`, `faq.html`, `contact.html`)

### Update External Listings

Update the website URL on all external profiles to `https://www.taylermiddleton.com`:

- **Psychology Today** — update website URL in your therapist profile
- **Google Business Profile** — ensure the practice is listed at [business.google.com](https://business.google.com) and the website URL is updated
- **Jane App** — verify booking link is correct (`https://colenmiddletontherapy.janeapp.com/locations/tayler-middleton/book`)
- **Lumino Health** — update if listed
- **Any other directories** (Wix site can be deactivated after the new site is live and indexed)

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
