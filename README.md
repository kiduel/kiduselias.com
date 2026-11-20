# kiduselias.com

A fast, single-page static site. No framework, no build step. Everything that ships is in `site/`.

```
site/
  index.html            the whole site (CSS and JS inline, ~19 KB gzipped)
  404.html              "This page didn't ship" page
  assets/fonts/         Geist, Geist Mono, Instrument Serif italic (self-hosted, ~68 KB)
  assets/img/           app screenshots and icons as WebP (lazy-loaded)
  og.jpg                link-preview image (LinkedIn, X, iMessage, Slack)
  apple-touch-icon.png  iPhone home-screen icon
  favicon.svg
  about/, experience/…  tiny pages that send old Google Sites URLs to the new sections
  .nojekyll             tells GitHub Pages to serve files as-is
  robots.txt, sitemap.xml
```

## Preview locally

```bash
python3 -m http.server 4321 --directory site
```

Then open http://localhost:4321

## Deploy

Hosted free on **GitHub Pages** from the `gh-pages` branch, which holds just the contents of `site/`.
To publish changes, commit to `main`, then run:

```bash
git push origin main && git push --force origin "$(git subtree split --prefix site main)":gh-pages
```

GitHub rebuilds in about a minute. (`gh-pages` is generated from `site/`, so force-pushing it is safe;
GitHub sometimes adds its own commits there when the domain setting changes.)

**Domain:** `www.kiduselias.com` is a CNAME to `kiduel.github.io` (set at Squarespace Domains), and the
`CNAME` file in `site/` tells GitHub Pages which domain to serve. The bare `kiduselias.com` forwards to `www`.

## Editing

- Copy lives in `site/index.html`. Each section is marked with a `<!-- ───── Section ───── -->` comment.
- Colors are CSS variables at the top of the `<style>` block (`--accent` is the orange). Dark and light themes are both defined there.
- To add a screenshot, convert it to WebP at 540 px wide:
  `cwebp -q 78 -resize 540 0 input.png -o site/assets/img/name.webp`
- Quick-navigation menu items (⌘K / the mobile menu) are the `items` array near the bottom of `index.html`.
