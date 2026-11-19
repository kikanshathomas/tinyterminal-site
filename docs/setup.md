# Setup

Nothing to install. The site is the files in the repo. Preview is a static file server.

## Preview

From the repository root:

```sh
python3 -m http.server 8000
```

Then open:

- <http://127.0.0.1:8000/> — home
- <http://127.0.0.1:8000/download.html> — download
- <http://127.0.0.1:8000/privacy.html> — privacy
- <http://127.0.0.1:8000/404.html> — not-found page (open the file directly; this server does not use it for missing paths)
- <http://127.0.0.1:8000/app-ads.txt> — the AdMob file

Check a narrow window as well. Below 860px the nav becomes a menu button. On the home page, open a screenshot (lightbox) and close it with Escape and by clicking the dark backdrop.

This server shows every file, including `README.md` and `docs/`. GitHub Pages does not. To see the published set, build with Jekyll the way [deploy.md](deploy.md) describes, or inspect the live site after a merge.

GoatCounter still runs in a local preview if the browser can reach `gc.zgo.at`. That request is the same one the privacy page discloses. There is no other network call.

## What to edit

- Copy, FAQ answers, and the download wording: the HTML files. Keep the visible claims aligned with the game.
- Colors: the custom properties at the top of the page you are editing. Take values from `games/idle-airport/style/tokens.js`. The same block is copied on each page; a color change that should be site-wide has to be made on each page that carries the block.
- A screenshot: replace both the PNG and the WebP, and keep them 540×960. The phone frame is 230px wide. The lightbox reads the WebP from `data-full`.
- The large app icon: `app-icon.png` (104×104) plus `app-icon-208.webp` and `app-icon-512.webp`. The nav mark is the 64 and 96 pair, PNG and WebP.
- The share image: `assets/img/og.png` at 1200×630. The width and height in the Open Graph tags match that file.
- Fonts: replace a `.woff2` only together with the `@font-face` rule in `assets/css/fonts.css`, and keep `OFL.txt`.
- Privacy wording: edit `games/idle-airport/store/privacy-policy.md` in `ubersoft-company` first, then copy that text into `privacy.html`. The page is the public copy of that file. Do not rewrite the policy only on the website.
- The Play listing: do not add a store URL, badge, or QR code until the listing is public. The comments in `index.html` and `download.html` say what a later change adds (the official badge, and a self-hosted QR script, the way `zbilltracker-site` does).

## What not to edit

- Do not add YAML front matter to any file. Pages would stop copying that file byte for byte.
- Do not add `.nojekyll`. That would publish this README, `docs/`, and `CLAUDE.md`.
- Do not put secrets, keystores, ad-unit ids, or signing material in this repo. `app-ads.txt` is already the public publisher line and should be left as a single ads.txt record.
