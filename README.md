# takahiro-h16.github.io

Personal site built with [Quarto](https://quarto.org).
Published at <https://takahiro-h16.github.io>.

## Local development

```bash
quarto preview    # live-reloading server at http://localhost:4200
quarto render     # one-off build into _site/ (git-ignored)
```

## Layout

| Path | Purpose |
|------|---------|
| `_quarto.yml` | Site-wide config: navbar, theme, MathJax, folded code blocks |
| `index.qmd` | Home — one-line self-definition + short intro |
| `projects.qmd` | Card grid, generated from everything in `projects/` |
| `projects/*.qmd` | One file per project; its YAML fills in the card |
| `about.qmd` | Background and CV link |
| `assets/` | Static files copied verbatim into the site (`cv.pdf` = exported resume) |
| `ja/` | Japanese twin of every page above, same file names (`ja/_metadata.yml` sets `lang: ja`) |
| `_includes/lang-switch.html` | Navbar EN ⇄ 日本語 button; on `ja/` pages also points the navbar at the Japanese pages |
| `styles.css` | Small style overrides (Japanese font on `ja/` pages, listing cards) |

## Adding a project

Create `projects/<slug>.qmd` with at least:

```yaml
---
title: "Project title"
description: "One sentence shown on the card."
date: 2026-10-04
categories: [Tag, Tag]
---
```

The listing on `projects.qmd` picks it up automatically, newest first.

For the Japanese version, add `ja/projects/<slug>.qmd` with the same slug, so the
language button can jump between the two. The same rule holds for any new page:
`foo.qmd` ⇄ `ja/foo.qmd`.

### Code blocks

`code-fold: true` in `_quarto.yml` only collapses **executable cells**
(` ```{python} `), not plain ` ```python ` fences. Pages that only want to
*display* code should declare

```yaml
execute:
  enabled: false
```

in their front matter — the cell is then folded but never run, so rendering
needs no Python kernel.

## Deployment

Pushing to `main` triggers `.github/workflows/publish.yml`, which renders the
site and pushes it to the `gh-pages` branch. GitHub Pages must be configured
once under **Settings → Pages → Source → Deploy from a branch → `gh-pages` / `/ (root)`**.
