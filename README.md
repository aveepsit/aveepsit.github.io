# aveepsit.github.io

GitHub Pages user site for **Aveepsit**, served on the custom domain
[aveepsit.in](https://aveepsit.in).

## What's in the repo

| File        | Purpose                                                            |
|-------------|--------------------------------------------------------------------|
| `README.md` | This file. Also the page GitHub Pages renders, since there is no `index.html`. |
| `CNAME`     | Tells GitHub Pages to serve the site at `aveepsit.in`.             |

That's everything. There is no HTML, CSS, JavaScript, Jekyll config
(`_config.yml`), theme, or build step.

## How it's served

- GitHub Pages publishes the `main` branch from the repository root.
- With no `index.html`, Pages runs its default Jekyll build and renders
  `README.md` as the homepage, so the live site shows only this README.
- The `CNAME` file maps the site to `aveepsit.in`. The domain's DNS also has
  to point at GitHub Pages (apex `A` records to GitHub's Pages IPs, or an
  `ALIAS`/`ANAME` record); the `CNAME` file alone does nothing if DNS is not
  set up.

## History

| Date       | Commit    | Change                                    |
|------------|-----------|-------------------------------------------|
| 2020-12-17 | `05dde64` | Initial commit (README only)              |
| 2020-12-17 | `2a31493` | Added `CNAME` for the `aveepsit.me` domain |
| 2026-11    | —         | Switched the custom domain to `aveepsit.in` |

## Current state

This is an empty placeholder. To turn it into a real site:

1. Add an `index.html` (plain static site) or a `_config.yml` plus Markdown
   pages (Jekyll), and push to `main`.
2. Point `aveepsit.in` DNS at GitHub Pages, set it under
   **Settings → Pages → Custom domain**, and turn on **Enforce HTTPS** once
   the certificate is issued.
