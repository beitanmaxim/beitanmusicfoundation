# Beitan Music Foundation — Website

Static site, two pages. No build step, no dependencies.

## Run locally
Open `index.html` directly, or serve the folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Structure
```
index.html                    — homepage (Hero · Mission · Programmes ·
                                 Exhibitions · Founder · Partners · Support · Contact)
exhibition-stradivari.html     — "Stradivari · Guarneri · Amati" exhibition page
img/                           — all photos, partner logos, favicons, BM logo SVGs
```

## Notes
- Fonts (Cinzel, Inter, Playfair Display) load from Google Fonts — needs internet on first paint.
- Contact form posts via Web3Forms; replace the `access_key` in `index.html` with the foundation's own key before going live (falls back to `mailto:` offline).
- Light/dark theme toggle is remembered in `localStorage`.
