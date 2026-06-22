# mszuromi.github.io

Personal academic website for **Matthew Szuromi** — plain HTML, CSS, and a little
vanilla JavaScript. No build step, no frameworks, no dependencies to maintain.

Live at **<https://mattszuromi.com>** — hosted on Cloudflare Pages, auto-deployed from `main`. (The old GitHub Pages URL `mszuromi.github.io` may also still resolve.)

## Files

| File | What it is |
|------|------------|
| `index.html` | Home page — animated cortical-column hero (canvas) + an About section. |
| `research.html` | Research areas, each with its related publications. |
| `cv.html` | Full CV — cosmic on screen, clean light for print; source for the PDF. |
| `aboutme.html` | "About Me" — personal interests page. |
| `styles.css` | Shared cosmic theme (dark, gold ink, serif) for every page. |
| `script.js` | Mobile menu + footer year. |
| `assets/favicon.svg` | "MS" monogram favicon. |
| `assets/Matthew_Szuromi_CV.pdf` | Generated from `cv.html` (see below). |
| `.nojekyll` | Tells GitHub Pages to serve files as-is (skip Jekyll). |

## Editing content

Everything is hand-editable text — open the `.html` files and change the words.
The header/nav is duplicated in each page (no build step); if you change a nav
link, update it in `index.html`, `research.html`, `aboutme.html`, and the
toolbar in `cv.html`.

- **Bio / About:** the `<section class="about-section">` block in `index.html` (below the hero).
- **Research areas + their publications:** the `<article class="card">` blocks in
  `research.html` — each paper lives inside the area it belongs to.
- **CV:** `cv.html` (then regenerate the PDF — see below).
- **About Me:** `aboutme.html`.
- **Colors / fonts:** the `:root` variables at the top of `styles.css`.

### The home animation

The hero is a live cortical column rendered on a `<canvas>` — pyramidal and
stellate neurons in cortical layers, with sparse excitatory (gold) and inhibitory
(cyan) spiking. Moving the cursor through it excites nearby neurons (an
undocumented easter egg). It all lives in the `<script>` at the bottom of
`index.html`; the firing behaviour is just numbers (base accrual, cursor strength,
coupling, refractory) in the `step()` and `fire()` functions.

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
