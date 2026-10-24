# art2: digitalitility.com

## Goal
Serve the static page "digitalitility, the edge of web" at https://digitalitility.com. The former Hugo art portfolio was retired after fxhash went offline.

## Tech
- Plain HTML in `landing/` (index, identical 404 so old URLs land on it, CNAME, .nojekyll). No build step, no dependencies.
- Deploy: `.github/workflows/gh-pages.yml` publishes `landing/` to the `gh-pages` branch on push to `main`; GitHub Pages serves that branch.

## Content archive
- `content/` keeps the old portfolio posts and images (one page bundle per work), `content/donation/index.md` the fxhash donation records.
- `static/` keeps the portrait photo.
- The Hugo setup (theme hello-friend-ng, config.toml) is only in git history, before the commit that retired it. It last built with Hugo extended 0.105.0.
