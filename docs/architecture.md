# Architecture

Four static HTML files, one font stylesheet, images, and the root files Pages must keep public (`CNAME`, `robots.txt`, `sitemap.xml`, `app-ads.txt`, and the favicons). No bundler, no framework, no package.json, and no `.github` workflow. Publishing is GitHub Pages on `main`, described in [deploy.md](deploy.md).

## Pages

Each page is one HTML file with its CSS in a `<style>` block. The nav, footer, and color tokens are copied into `index.html`, `download.html`, and `privacy.html` so a page does not depend on a shared sheet. `assets/css/fonts.css` is the only external stylesheet. It declares four weights of Inter (400, 500, 700, 800), latin subset, from `@fontsource/inter` 5.1.0. `assets/fonts/OFL.txt` is the SIL Open Font License and has to stay next to the font files.

`404.html` is the exception. GitHub Pages serves it for unknown paths. It has no nav and no footer. Its `<style>` block still contains the shared chrome rules so the head matches the other pages. Those chrome rules match no element on the 404 page. They were left in place: deleting them is a large edit to a live error page, and a mistake would change how that page looks. See "Checked and kept" below.

There is no separate `.js` file. Scripts are inline:

| Page | Script | Why it is there |
|---|---|---|
| Home | `IntersectionObserver` | Adds `.in` so sections below the hero fade in. The hero already has `.in`. |
| Home | Lightbox | A screenshot button's `data-full` is the full-size WebP. Escape, or a click on the backdrop, closes it and returns focus. |
| Home, download, privacy | Nav toggle | Below 860px the links collapse. The button sets `aria-expanded`. |
| Home, download, privacy | `#cpyear` | Shows `2026` until the calendar year is later, then a range (`2026–2027`). |
| All four pages | GoatCounter | The only third-party request. `count.v4.js` from `gc.zgo.at`, with a subresource integrity hash, for `https://tinyterminal.goatcounter.com/count`. The privacy page describes what it records. |

`@media (scripting: none)` and `@media (prefers-reduced-motion: reduce)` on the home page show the reveal sections without the animation. The hero does not wait on JavaScript.

## Color tokens

The custom properties at the top of each page are taken from `games/idle-airport/style/tokens.js` in `ubersoft-company`. Values in use match that file (`--page`, `--card`, `--ink`, `--teal`, `--teal-deep`, and the rest of the names that rules actually reference).

Some names in that block are not referenced by any rule: `--card-locked`, `--chip`, `--ink-faint`, `--gold`, `--gold-soft`, `--coral`, `--mint`, `--apron`, `--taxi-yellow`, and `--elev-sheet`. They stay so a later edit uses the game palette instead of inventing a color. `--elev-card`, `--elev-toast` match `tokens.js`. `--elev-shot`, `--elev-menu`, and `--elev-lightbox` are site shadows derived from those.

## Images

| File | Size | Where it is used |
|---|---|---|
| `assets/img/app-icon.png` | 104×104 | Fallback for the large icon on the home and download pages |
| `assets/img/app-icon-208.webp`, `app-icon-512.webp` | 208 and 512 | 2× and 4× sources for that icon |
| `assets/img/app-icon-64.png`, `app-icon-96.png` and the matching `.webp` | 64 and 96 | Nav and footer mark (`2x` / `3x`) |
| `assets/img/og.png` | 1200×630 | Open Graph and Twitter image |
| `assets/img/shot-floor`, `shot-fleet`, `shot-harbor`, `shot-away` | 540×960, PNG and WebP | Home-page phones. The page shows them at 230×409. The WebP is also the lightbox image |
| `favicon.ico`, `favicon-32x32.png` | ico, 32×32 | Tab icon |
| `apple-touch-icon.png` | 180×180 | Home-screen icon |

Every image file in the tree is referenced. PNG and WebP are both required: the `<picture>` element uses WebP and falls back to PNG.

## Files that are public on purpose

- `app-ads.txt` is the AdMob authorization file. Google fetches <https://tinyterminal.app/app-ads.txt>. The publisher id in it is the public id the Android app already ships. Do not delete the file, do not add a comment line, and do not exclude it.
- `CNAME` contains `tinyterminal.app`. Pages uses it for the custom domain. It is also reachable as a URL; that is normal for Pages, and the file stays.
- `robots.txt` allows all crawlers and names the sitemap.
- `sitemap.xml` lists the home page, `download.html`, and `privacy.html`. It does not list `404.html`. When the text of a listed page changes, update that URL's `lastmod`.

## Checked and kept

A pass over every `href`, `src`, `srcset`, and CSS `url()`, plus the sitemap, `CNAME`, the privacy and support links, and the live site, found no unused page, asset, script, backup copy, or commented-out block.

Left on purpose:

- The unused token names above.
- The shared chrome CSS inside `404.html`.
- The HTML comments on the home and download pages that say not to add a Play badge or store URL yet. Those are instructions, not disabled markup. There is no commented-out badge in the file.
- `class="donate"` on the Ko-fi link. No stylesheet rule uses it. Removing the class would not change the page; it was left because it is a harmless hook, not a dead file.
- `assets/fonts/OFL.txt`. The font license requires it.
