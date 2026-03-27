# CLAUDE.md

This file provides guidance to Claude Code when working with this repository.

## Project

Hugo-based marketing and documentation site for [Polyphon](https://polyphon.ai). Deployed to GitHub Pages via `.github/workflows/deploy-site.yml`.

## Build & Development

```sh
hugo server                  # local dev server at http://localhost:1313
hugo --minify                # production build → public/
npm ci && npm run pagefind   # build full-text search index (run after hugo --minify)
```

There is no CSS build pipeline — `themes/polyphon/assets/css/main.css` is vanilla CSS, edited directly.

## Content Structure

```
content/
  _index.md               # Homepage
  blog/                   # Release posts (one leaf bundle per release)
  docs/
    polyphon/             # Main app documentation
    integrations/
      obsidian-polyphon/  # Obsidian plugin docs
    for-developers/       # API and MCP server reference
  roadmap.md              # Roadmap page (data sourced from data/roadmap.yaml)
  about.md
  search.md
```

Blog posts and most docs pages use Hugo **leaf bundles** (a directory with `index.md` + assets). Create new posts as directories, not bare `.md` files.

## Configuration

- `hugo.yaml` — site config; `params.downloadVersion` is the current release version. **Do not edit by hand** — it is updated automatically by the `update-download-version.yml` workflow in the `polyphon` repo on each release.
- `data/homepage.yaml` — feature cards on the homepage
- `data/roadmap.yaml` — roadmap items with status, dates, and GitHub discussion links
- `themes/polyphon/` — custom theme (not a git submodule; edit in place)

## Theme

The custom theme lives entirely in `themes/polyphon/`. Design system highlights:
- OKLCH color space for light/dark mode palettes
- Geist Sans variable font (served from `static/fonts/`)
- Provider accent colors (Anthropic, OpenAI, Gemini, Copilot, Ollama) defined as CSS custom properties in `main.css`

## Release Workflow (automated)

When a Polyphon release is published, the `update-download-version.yml` workflow in the `polyphon` repo automatically:
1. Updates `params.downloadVersion` in `hugo.yaml`
2. Creates a new blog post in `content/blog/polyphon-vX.Y.Z-released/`
3. Commits, pushes, and triggers a site deploy

## Relationship to Sibling Projects

- **`../polyphon`** — desktop app; drives `downloadVersion` updates and release blog posts via GitHub Actions
- **`../obsidian-polyphon`** — Obsidian plugin; its user-facing docs live in `content/docs/integrations/obsidian-polyphon/`

## Ecosystem

This project is part of the polyphon-ai workspace. See `../.github/CLAUDE.md` for how the projects relate to each other.
