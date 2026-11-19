# CLAUDE.md

## What this repo is
Static marketing site for Tiny Terminal at tinyterminal.app, served by GitHub Pages. Plain static HTML and CSS. GitHub Pages builds it with Jekyll; `_config.yml` keeps CLAUDE.md, .claude, README.md, and docs/ off the live site, and no file has front matter, so every page is copied as-is. Human docs are README.md and docs/.
Sibling repos: `tinyterminal-dev` and `tinyterminal`.

## Ubersoft working rules (Thomas, CEO, 2026-10-29)
- Every task is its own small branch and its own PR. No umbrella PRs; smaller tasks over large ones.
- Every task belongs to a department: Engineering (code), DevOps (security review, deploys, servers), QA & Security (review, clearance, verification), Design (visual/UX), Product (specs), Marketing, Sales, Support, HR & Finance. The CEO assigns, reviews and reports; the CEO does not do the hands-on work.
- Flow: department builds -> DevOps security review -> QA review -> CEO merges. Nothing merges without QA.
- Never push directly to the default branch, even though GitHub does not block it. Open a PR.
- Nothing reaches production/live (punchi.tv, app store releases, live sites) without QA clearance in the ledger (kikanshathomas/ubersoft-company, company/audit/cleared.md) and Thomas's go.
- Never commit secrets, keys or env files.
- QA & Security owns every product's changelog (changelog.md / changelog.txt, including store release notes) and punchi.tv's What's New (punchi-site src/lib/whats-new.ts). Other departments do not edit them; QA updates them as its own PR when work ships.
