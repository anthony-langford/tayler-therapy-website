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

## DNS Configuration

Point the domain to GitHub Pages:

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

---

## TODO

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

### Update External Listings

- **Psychology Today** — update website URL to `https://www.taylermiddleton.com` if it still points to Wix
- **Google Business Profile** — ensure the practice is listed and website URL is updated
- **Jane App** — verify booking link is correct (`https://colenmiddletontherapy.janeapp.com/locations/tayler-middleton/book`)
- **Ensure consistent NAP** — name, address, phone must match exactly across all listings

### Google Maps Embed

The current embed uses a search query URL. For a more reliable embed:
1. Go to [Google Maps](https://maps.google.com) → search "554 Palmerston Ave, Toronto"
2. Click Share → Embed a map → copy the iframe `src` URL
3. Replace the `src` in all 4 pages + `thanks.html`
