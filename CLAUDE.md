# CLAUDE.md

## Project

Personal academic website for Tuan-Phong Nguyen, served at **tuan-phong.com** via GitHub Pages (repo `phongnt570.github.io`, branch `main`). Domain is configured in [CNAME](CNAME).

## Structure

- [index.html](index.html) — entire site in one file (publications, news, bio, contact). Icons are inline SVG (no FontAwesome).
- [static/css/custom.css](static/css/custom.css) — site-specific styles on top of Bootstrap
- [static/css/bootstrap.min.css](static/css/bootstrap.min.css), [static/js/bootstrap.bundle.min.js](static/js/bootstrap.bundle.min.js) — Bootstrap 5 vendored
- [static/fonts/](static/fonts/) — self-hosted Lora woff2 subsets (latin, vietnamese, italic-latin)
- [static/img/](static/img/) — `phong.webp` (avatar, served to browsers), `phong.jpg` (original, used as `og:image`), `favicon.svg`

No build step, no SSG, no `package.json`. Edit HTML/CSS directly and commit.

## Preview locally

In the Claude app, click **Preview** → pick **"Preview site"** ([.claude/launch.json](.claude/launch.json)). It serves the repo at `http://127.0.0.1:4894` using the local `.conda` Python.

Or run manually:

```sh
.conda/bin/python -m http.server 4894
```

The `.conda/` directory at the repo root is a local Python 3.14 env — activate or call `.conda/bin/python` directly if you need Python for anything. It is git-ignored.

## Conventions

- Commit messages: short, lowercase, imperative (e.g. `add service`, `fix typo`, `update paper link`).
- Don't commit: `.DS_Store`, `.map` files, `.conda/` (all in [.gitignore](.gitignore)).
- Don't leave large blocks of commented-out HTML — delete; git history is the archive.
- No analytics or third-party tracking is loaded.

## Known cleanup candidates

- The publications list in [index.html](index.html) is large and repetitive; a static-site generator (Astro/11ty/Jekyll) would make adding papers easier, but the user has not committed to migrating.
