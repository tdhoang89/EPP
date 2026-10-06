# Equation Painting — white paper site

Static, dependency-free site (HTML + CSS; mathematics via KaTeX from a CDN). Push the contents of this folder to a GitHub repository and enable GitHub Pages (Settings → Pages → Deploy from a branch → root). `.nojekyll` is included so no file is skipped.

- `index.html` — bilingual landing page (read online, download PDF, simple explanation, try it yourself)
- `paper-vi.html`, `paper-en.html` — the full paper, Vietnamese and English
- `simple-vi.html`, `simple-en.html` — one-page plain-language explanation
- `pdf/` — the two PDFs
- `specs/` — the two self-contained specifications; give one to a code-executing AI to reproduce the picture pixel for pixel
- `figures/` — figures used by the pages (downscaled for the web; hashes in captions refer to the original renders)
