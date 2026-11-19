# Deploy

GitHub Pages publishes this repo. The repository setting (confirmed against the Pages API) is: source branch `main`, source path `/`, custom domain `tinyterminal.app`, HTTPS. There is no deploy workflow in `.github/` and no second host.

Merging a pull request to `main` is the publish. Pages builds with Jekyll, usually within a few minutes. A CDN cache can lag behind the build.

Nothing here ships the Android app. Play builds happen from `tinyterminal`, on the machine that holds the upload key, and only after QA clearance and Thomas's go. This site never takes part in that build.

## What Jekyll does

`_config.yml` is the whole Jekyll configuration.

- `theme: null` so Pages does not add its default theme stylesheet at `assets/css/style.css`.
- `require_front_matter: true` (the `jekyll-optional-front-matter` behavior Pages turns on). A Markdown file with no front matter is copied as a static file. That is why a README that is not excluded becomes a public URL. Before `README.md` was excluded, <https://tinyterminal.app/README.md> served the two-line readme.
- `exclude` lists `README.md`, `readme.md`, `docs`, `CLAUDE.md`, and `.claude`, plus Jekyll's own default excludes. GitHub Pages currently builds with Jekyll 3.10, and on Jekyll 3 a custom `exclude` list replaces the defaults, so the defaults are repeated in the file. On Jekyll 4 they are appended, and repeating them is harmless.
- No page has front matter, so Jekyll copies each HTML, image, and text file unchanged.

Do not add `.nojekyll`. Pages would then copy the repo as-is, including the README, `docs/`, and `CLAUDE.md`.

## What visitors can and cannot request

Published, and linked or required:

- `/`, `/index.html`
- `/download.html` and `/download`
- `/privacy.html` and `/privacy`
- `/404.html` for unknown paths
- `/app-ads.txt`
- `/robots.txt`, `/sitemap.xml`
- `/favicon.ico`, `/favicon-32x32.png`, `/apple-touch-icon.png`
- `/assets/**` (css, fonts, images)
- `/CNAME` (Pages also reads this from the repo; fetching the URL is a side effect)

Not published:

- `/README.md` and `/readme.md`
- `/docs/` and everything under it
- `/CLAUDE.md`
- `.claude/`

`/privacy/` and `/download/` (with a trailing slash) are not the same as the extensionless URLs. They 404 today. Links in the repo use `privacy.html` and `download.html`, or the extensionless form without a trailing slash. Do not rename the HTML files: both the sitemap and the company privacy URL depend on the current names.

## How a change ships

1. Branch off `main`. One task, one pull request.
2. Edit the page or the docs. Do not add a changelog file; QA & Security owns that, and this repo does not have one.
3. Preview with the local server in [setup.md](setup.md). If the change is to `_config.yml`, also run a Jekyll build when Ruby is available:

   ```sh
   jekyll build --destination /tmp/tinyterminal-site
   ```

   The destination should contain the HTML pages and assets, and should not contain `README.md`, `docs/`, or `CLAUDE.md`. The built HTML should match the source files.
4. Open a pull request. DevOps does the security review, QA reviews, and the CEO merges. A change that alters the live pages (copy, images, the privacy text, `app-ads.txt`) also needs a clearance line in `kikanshathomas/ubersoft-company` `company/audit/cleared.md` and Thomas's go before it is merged. Docs-only edits still merge only through that review. Nobody pushes to `main` directly.
5. After the merge, confirm the live bytes. Pages and the CDN can take a few minutes. The query string avoids a cached copy:

   ```sh
   curl -sI "https://tinyterminal.app/privacy.html?v=$(date +%s)"
   curl -s "https://tinyterminal.app/index.html?v=$(date +%s)" | cmp - index.html && echo identical
   curl -sI "https://tinyterminal.app/README.md?v=$(date +%s)"
   ```

   The last one should be a 404 once this exclude list is what Pages built. The 404 is `404.html`.

If a listed page's text changed, update `lastmod` in `sitemap.xml` in the same pull request.
