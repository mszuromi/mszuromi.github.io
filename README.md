# mszuromi.github.io

Personal academic website for **Matthew Szuromi** — plain HTML, CSS, and a little
vanilla JavaScript. No build step, no frameworks, no dependencies to maintain.

Live (once deployed): <https://mszuromi.github.io>

## Files

| File | What it is |
|------|------------|
| `index.html` | The main one-page site (About, Research, Publications, CV). |
| `cv.html` | Full CV — also the source for the downloadable PDF. |
| `styles.css` | All styles for `index.html` (light + dark themes). |
| `script.js` | Theme toggle, mobile menu, active-section highlighting. |
| `assets/favicon.svg` | "MS" monogram favicon. |
| `assets/Matthew_Szuromi_CV.pdf` | Generated from `cv.html` (see below). |
| `.nojekyll` | Tells GitHub Pages to serve files as-is (skip Jekyll). |

## Editing content

Everything is hand-editable text — open the `.html` files and change the words.

- **Bio / About:** the `<section id="about">` block in `index.html`.
- **Research:** the three `<article class="card">` blocks in `index.html`.
- **Publications:** the `<ol class="pubs">` list in `index.html`, and the matching
  list in `cv.html`.
- **Colors / fonts:** the `:root` variables at the top of `styles.css`.

### Add a real headshot

1. Drop a square image at `assets/headshot.jpg` (≈ 600×600 px looks crisp).
2. In `index.html`, find the `<div class="avatar">` block and replace the
   `<span>MS</span>` with:
   ```html
   <img src="assets/headshot.jpg" alt="Matthew Szuromi" />
   ```

### Regenerate the CV PDF

The PDF is just `cv.html` printed to paper size. After editing `cv.html`, either:

- Open `cv.html` in a browser → **Print** → *Save as PDF*, save over
  `assets/Matthew_Szuromi_CV.pdf`; **or**
- Run headless Chrome:
  ```sh
  "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
    --headless=new --disable-gpu --no-pdf-header-footer \
    --print-to-pdf="assets/Matthew_Szuromi_CV.pdf" \
    "file://$PWD/cv.html"
  ```

## Local preview

It's a static site, so just open `index.html` in a browser. For a local server
(nicer for testing relative links):

```sh
python3 -m http.server 8000   # then visit http://localhost:8000
```

## Deploying to GitHub Pages

This repo is named `mszuromi.github.io`, so GitHub serves it as a **user site** at
`https://mszuromi.github.io` straight from the `main` branch.

1. Create a public repo on GitHub named exactly `mszuromi.github.io`.
2. Push this folder to it:
   ```sh
   git add -A && git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/mszuromi/mszuromi.github.io.git
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a
   branch**, branch `main`, folder `/ (root)`. Save. The site is live in a minute.

### Optional: custom domain

Buy a domain (~$10–15/yr), add a `CNAME` file containing just the domain
(e.g. `mattszuromi.com`), point the domain's DNS at GitHub Pages, and enable the
domain under Settings → Pages. Until then, `mszuromi.github.io` works perfectly.
