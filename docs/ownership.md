# Ownership

Who changes the source files in this repo. Review is still the company rule: the department opens the pull request, DevOps does the security review, QA reviews, and the CEO merges. A change to the live pages also needs a line in the QA ledger (`kikanshathomas/ubersoft-company`, `company/audit/cleared.md`) and Thomas's go.

| Area | Department | Files |
|---|---|---|
| What the product is, and whether a claim still matches the game | Product | [overview.md](overview.md), and the factual claims on the pages |
| Sentences visitors read (headlines, FAQ, download wording) | Marketing | `index.html`, `download.html`, the footer shared by the pages |
| Privacy policy text | Marketing, from the company source | `privacy.html`, copied from `ubersoft-company` `games/idle-airport/store/privacy-policy.md`. Change the company file first |
| Screenshots, icons, Open Graph image, color tokens | Design | `assets/img/`, favicons, the token block in each page |
| Page structure, scripts, this `docs/` set, the README | Engineering | HTML structure, `assets/css/fonts.css`, `docs/`, `README.md` |
| Domain, Pages project, `_config.yml` excludes | DevOps | `CNAME`, `_config.yml`, the Pages setting (branch `main`, path `/`) |
| Changelog, if this repo ever has one | QA & Security | There is no `changelog.md` today. Another department does not add one. Store release notes belong to the packaging flow, not to this site |
| Support mailbox and the Ko-fi link | Support | `mailto:support@ubersoft.pro`, <https://ko-fi.com/ubersoft> |

`app-ads.txt` is a public AdMob record. Marketing and DevOps both care that it keeps matching the app's publisher id. Do not edit it as part of a wording change.

## Do not edit

- Do not put keystores, upload-key material, Play licence keys, or ad-unit ids in this repo.
- Do not treat `tinyterminal-dev` or `tinyterminal` as part of a site pull request. Game and packaging changes are their own pull requests.
- There is no Park or Guide tree here. Nothing in this repo is excluded from ordinary review for that reason.

## Changelog

This repo has no changelog. [deploy.md](deploy.md) is the publish procedure. QA & Security owns any future changelog and would add it in a QA pull request. If that file should stay off the public site, the same pull request adds it to `exclude` in `_config.yml`.
