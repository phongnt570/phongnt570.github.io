# CLAUDE.md

## Project

Personal academic website for Tuan-Phong Nguyen, served at **tuan-phong.com** via GitHub Pages (repo `phongnt570.github.io`, branch `main`). Domain is configured in [CNAME](CNAME). The site is a Jekyll project — GitHub Pages auto-builds on push; no GitHub Actions workflow.

## Structure

- [index.html](index.html) — page layout (head, bio, contact, services), with a Liquid `{% for %}` loop where the publications list lives. Has Jekyll front matter at the top so Liquid is processed.
- [_data/publications.yml](_data/publications.yml) — every paper as a YAML entry (title, url, authors with `highlight`, venue, optional `acceptance_rate` / `award`, links). Add a new paper here, not in HTML.
- [_includes/publication.html](_includes/publication.html) — Liquid template that renders one entry from `_data/publications.yml`.
- [_config.yml](_config.yml) — Jekyll config. Empty theme; UTF-8 encoding; excludes for local-only files.
- [static/css/custom.css](static/css/custom.css) — site-specific styles on top of Bootstrap
- [static/css/bootstrap.min.css](static/css/bootstrap.min.css), [static/js/bootstrap.bundle.min.js](static/js/bootstrap.bundle.min.js) — Bootstrap 5 vendored
- [static/fonts/](static/fonts/) — self-hosted Lora woff2 subsets (latin, vietnamese, italic-latin)
- [static/img/](static/img/) — `phong.webp` (avatar served to browsers), `phong.jpg` (original used as `og:image`), `favicon.svg`
- Icons are inline SVG (no FontAwesome).

## Adding a new publication

Append an entry to [_data/publications.yml](_data/publications.yml) at the top (newest first):

```yaml
- id: publication_19
  title: Your paper title
  url: https://link-to-pdf-or-abstract       # optional; omit if no main link
  authors:
    - { name: Author One, highlight: false }
    - { name: Tuan-Phong Nguyen, highlight: true }
  venue: ACL 2026
  venue_style: bold                          # 'bold' for accepted venues, 'italic' for preprints/workshops/demos
  acceptance_rate: 22%                        # optional
  award: best paper nomination                # optional
  links:
    - { label: paper, url: https://... }
    - { label: code, url: https://... }
```

No HTML edits required.

## Preview locally

Click **Preview** in the Claude app → **"Preview site"** ([.claude/launch.json](.claude/launch.json)). It runs `bundle exec jekyll serve --livereload` on `http://127.0.0.1:4894`; saving any source file triggers a rebuild + browser reload.

Or run manually:

```sh
bundle exec jekyll serve --host 127.0.0.1 --port 4894 --livereload
```

### First-time setup

System Ruby on macOS (2.6.x) is too old for modern Jekyll. Use Homebrew Ruby:

```sh
brew install ruby
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"   # add to ~/.zshrc to persist
bundle install
```

`bundle install` installs Jekyll into `vendor/bundle/` (git-ignored).

The local `Gemfile` pins Jekyll 4.x, which is newer than what GitHub Pages uses to build (3.9). For this site's features (Liquid `for` / `include`, `_data`, `_includes`) output is the same; if you start using newer-only features, switch the deploy path to a GitHub Actions workflow.

## Conventions

- Commit messages: short, lowercase, imperative (e.g. `add service`, `fix typo`, `update paper link`).
- Don't commit: `.DS_Store`, `.map` files, `.conda/`, `_site/`, `.jekyll-cache/`, `vendor/` (all in [.gitignore](.gitignore)).
- Don't leave large blocks of commented-out HTML — delete; git history is the archive.
- No analytics or third-party tracking is loaded.

## Python env

The `.conda/` directory is a local Python 3.14 env used for one-off scripts (image processing, scraping, data extraction). It is git-ignored. Call `.conda/bin/python` directly when you need it.
