# tinyterminal-site

Public marketing site for **Tiny Terminal: Idle Airport**, the first game in Ubersoft's Tiny series, at <https://tinyterminal.app/>.

This repository is the website only. It does not contain the game. The pages are hand-written HTML and CSS, and GitHub Pages publishes the `main` branch. There is no app build in this repo.

Longer notes:

| Doc | What it covers |
|---|---|
| [docs/overview.md](docs/overview.md) | What the site is, who it is for, and the three repos |
| [docs/architecture.md](docs/architecture.md) | How the pages, assets, and visit counter fit together |
| [docs/setup.md](docs/setup.md) | How to edit a page and preview it |
| [docs/deploy.md](docs/deploy.md) | How GitHub Pages publishes the site, and what it leaves out |
| [docs/ownership.md](docs/ownership.md) | Who may change which part |

There is no API. There is no changelog file. QA & Security owns product changelogs; do not add one in this repo from another department's pull request.

## Page map

GitHub Pages serves each `name.html` file at both `/name.html` and `/name`. Keep these filenames. The sitemap lists the `.html` form. The privacy-policy source in `ubersoft-company` uses <https://tinyterminal.app/privacy>, which is the same page.

| File | Public URL | Role |
|---|---|---|
| `index.html` | <https://tinyterminal.app/> | Home: features, screenshots, FAQ, download call to action |
| `download.html` | <https://tinyterminal.app/download.html> | Get-the-game page. No Play Store link until that listing is public |
| `privacy.html` | <https://tinyterminal.app/privacy.html> | Privacy policy, effective November 17, 2026 |
| `404.html` | unknown URLs | Not-found page. `noindex`. Not in the sitemap |
| `app-ads.txt` | <https://tinyterminal.app/app-ads.txt> | AdMob app-ads authorization. It has to stay at the site root |
| `CNAME` | not a page | Custom domain `tinyterminal.app`. Pages reads this file |
| `robots.txt` | <https://tinyterminal.app/robots.txt> | Allows crawling and points at the sitemap |
| `sitemap.xml` | <https://tinyterminal.app/sitemap.xml> | `/`, `/download.html`, `/privacy.html` |
| `favicon.ico`, `favicon-32x32.png`, `apple-touch-icon.png` | site root | Browser and home-screen icons |
| `assets/css/fonts.css`, `assets/fonts/` | | Self-hosted Inter (SIL OFL 1.1). The license is `assets/fonts/OFL.txt` |
| `assets/img/` | | App icon, Open Graph image (1200×630), screenshots (540×960 PNG and WebP) |
| `_config.yml` | not published | Jekyll settings for the Pages build |

Support on the pages is [support@ubersoft.pro](mailto:support@ubersoft.pro). "Support Development" goes to <https://ko-fi.com/ubersoft>. The company site is <https://ubersoft.pro>. Those are not pages in this repo.

## The other repos

| Repo | Role |
|---|---|
| [tinyterminal-dev](https://github.com/kikanshathomas/tinyterminal-dev) | Game source. Edit the game there (`app/src/`). Plain JS and one Canvas. |
| [tinyterminal](https://github.com/kikanshathomas/tinyterminal) | Android packaging. Capacitor wraps a build from the dev repo for Google Play (`com.tinyterminal.app`). |
| **tinyterminal-site** (this repo) | This website. |

Design records (the spec, art, brand, color tokens, and the privacy-policy source) live in [`ubersoft-company` `games/idle-airport/`](https://github.com/kikanshathomas/ubersoft-company/tree/main/games/idle-airport). The shared Tiny engine is [tiny-core](https://github.com/kikanshathomas/tiny-core). Only the dev repo depends on it. This site does not.

## Edit and preview

From this directory:

```sh
python3 -m http.server 8000
```

Open <http://127.0.0.1:8000/>, then `download.html`, `privacy.html`, and `404.html`. Details and the things that preview does not imitate are in [docs/setup.md](docs/setup.md).

## Publish

Merging to `main` is a publish. Pages builds `main` with Jekyll and serves tinyterminal.app. `_config.yml` keeps this README, `docs/`, `CLAUDE.md`, and `.claude` off the public site. The review rule is in [docs/deploy.md](docs/deploy.md).
