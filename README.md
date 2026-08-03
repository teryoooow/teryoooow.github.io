# Terelle Sarmiento — Portfolio

Personal portfolio for **Terelle Sarmiento**, QA Engineer (mobile & web testing, test automation, performance testing).

**Live site:** https://teryoooow.github.io

## Contents

- `index.html` — single-page portfolio (self-contained CSS/JS, dark/light themes)
- `headshot.jpg` — profile photo
- `Terelle_Sarmiento_Resume_2026.pdf` — résumé (downloadable from the site)

## Local development

```bash
# serve the folder, then open http://localhost:8000
python -m http.server 8000
```

## Testing

A Playwright-based QA suite (kept locally, outside this repo) runs 23 checks against the site:
console errors, link/anchor integrity, asset loading, theme toggle + persistence, scroll reveals,
mobile menu, and horizontal-overflow at desktop/tablet/mobile widths.

© 2026 Terelle Sarmiento
