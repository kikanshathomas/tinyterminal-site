# Overview

Tiny Terminal's public website. It introduces the game, answers the usual questions, states the privacy policy, and tells people the Google Play listing is not up yet.

It is for someone deciding whether to play, and for a reviewer who needs the privacy policy or the AdMob app-ads file. It is not the game, and it is not the Play Console listing.

## What the pages say

Tiny Terminal: Idle Airport is a calm, top-down idle game. You build a small airport into a busy hub. It is free to play, with ads, and a one-time Remove Ads purchase. There is no account. Progress stays on the phone. The home page says the game is coming soon to Google Play. `download.html` does not link to a store URL, because that URL would 404 until the listing is public.

The privacy page is the public copy of `games/idle-airport/store/privacy-policy.md` in `kikanshathomas/ubersoft-company`. Effective date: November 17, 2026. The company file names the URL <https://tinyterminal.app/privacy>. GitHub Pages serves that path and `/privacy.html` as the same file.

## Repo roles

Ubersoft keeps three repos for this product:

| Repo | What lives there |
|---|---|
| `kikanshathomas/tinyterminal-dev` | The game. Source is `app/src/`. A build there produces the JS the app ships. |
| `kikanshathomas/tinyterminal` | The Capacitor Android wrap. It copies a built `www/` from the dev repo and produces the Play bundle. Application id `com.tinyterminal.app`. |
| `kikanshathomas/tinyterminal-site` | This website. Static HTML, CSS, images, `CNAME`, and `app-ads.txt`. |

`tiny-core` is the shared library the Tiny games are built with. The dev repo pins it. This website does not vendor it and does not import it.

Changing a sentence on the site does not change the game. Changing the game does not update this site until someone edits these pages. Claims on the pages (two airports, three planes, twelve boosts a day, no account, ads and one purchase) have to stay true to the game. When the game changes one of those, Marketing updates the page in its own pull request.

## What this repo is not

- Not a place for the Android project, keystores, or Play signing. Those stay with the packaging repo, and keys stay off every repo.
- Not a place for game source or for `www/` build output.
- Not a company documentation library. These `docs/` files are the source of truth for the site. `ubersoft-company` has no `library/` tree yet; when that catalog exists it should mirror this folder, not replace it.
