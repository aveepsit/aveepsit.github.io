# aveepsit.github.io

GitHub Pages user site for **Aveepsit**, served on the custom domain
[aveepsit.in](https://aveepsit.in).

## What's in the repo

| File        | Purpose                                                            |
|-------------|--------------------------------------------------------------------|
| `README.md` | This file. Also the page GitHub Pages renders, since there is no `index.html`. |
| `CNAME`     | Tells GitHub Pages to serve the site at `aveepsit.in`.             |
| `_config.yml` | Jekyll config. Only excludes `infra/` from the published site.   |
| `infra/dns.yaml` | CloudFormation template for the Route 53 DNS records.         |

There is no HTML, CSS, JavaScript, theme, or build step.

## How it's served

- GitHub Pages publishes the `main` branch from the repository root.
- With no `index.html`, Pages runs its default Jekyll build and renders
  `README.md` as the homepage, so the live site shows only this README.
- The `CNAME` file maps the site to `aveepsit.in`. The domain's DNS also has
  to point at GitHub Pages (apex `A` records to GitHub's Pages IPs, or an
  `ALIAS`/`ANAME` record); the `CNAME` file alone does nothing if DNS is not
  set up.

## DNS (Route 53 via CloudFormation)

`infra/dns.yaml` manages the AWS side: a hosted zone for `aveepsit.in`, apex
`A`/`AAAA` records for GitHub Pages, `www` as a `CNAME` to
`aveepsit.github.io`, and an optional GitHub domain-verification `TXT` record.

Deploy with a new hosted zone:

```sh
aws cloudformation deploy \
  --stack-name aveepsit-dns \
  --template-file infra/dns.yaml
```

Then copy the `NameServers` output to the domain's name-server settings at the
registrar:

```sh
aws cloudformation describe-stacks --stack-name aveepsit-dns \
  --query "Stacks[0].Outputs" --output table
```

If the domain was registered in Route 53, it already has a hosted zone. Pass
its ID instead of creating a second one:

```sh
aws cloudformation deploy \
  --stack-name aveepsit-dns \
  --template-file infra/dns.yaml \
  --parameter-overrides ExistingHostedZoneId=Z0123456789ABC
```

Add `GitHubVerificationCode=<value>` to `--parameter-overrides` once GitHub
gives you the verification code. Deleting the stack keeps the hosted zone
(`DeletionPolicy: Retain`), so the registrar's name servers stay valid.

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
