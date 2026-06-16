# Beitan Music Foundation — Website

Static site. No build step, no dependencies — just HTML, CSS, and a little JS.

## Pages
- `index.html` — homepage
- `exhibition-stradivari.html` — Stradivari · Guarneri · Amati exhibition
- `img/` — all photos, partner logos, favicons

## Run locally
Open `index.html` directly, or serve the folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy
Upload the whole folder to any static host (GitHub Pages, Netlify, Vercel, or classic web hosting). `index.html` must sit at the site root. No server-side code required.

## Notes
- Fonts (Cinzel, Inter, Playfair Display) load from Google Fonts — needs internet on first paint.
- The contact form posts via Web3Forms; the access key is in `index.html`. It falls back to a `mailto:` link if the request fails.
- Light/dark theme toggle is remembered in `localStorage`.
- Security headers (CSP, X-Frame-Options, referrer policy) are set via `<meta>` tags in each page's `<head>`.
