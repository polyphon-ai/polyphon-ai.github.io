# polyphon.ai

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

Marketing and documentation website for [Polyphon](https://polyphon.ai) — built with Hugo, deployed to GitHub Pages.

## Development

**Prerequisites:** Hugo extended, Node.js ≥ 18

```sh
hugo server                   # local dev at http://localhost:1313
hugo --minify                 # production build → public/
npm ci && npm run pagefind    # build full-text search index (run after hugo --minify)
```

There is no CSS build pipeline. `themes/polyphon/assets/css/main.css` is vanilla CSS — edit it directly.

## Content

```
content/
  _index.md                         # Homepage
  blog/                             # Release posts (leaf bundles)
  docs/
    polyphon/                       # Main app docs
    integrations/obsidian-polyphon/ # Obsidian plugin docs
    for-developers/                 # JSON-RPC API and MCP server reference
  roadmap.md                        # Sourced from data/roadmap.yaml
  about.md
```

Create blog posts and doc pages as Hugo **leaf bundles** (a directory containing `index.md` + any assets), not bare `.md` files.

## Configuration

| File | Purpose |
|---|---|
| `hugo.yaml` | Site config; `params.downloadVersion` tracks the current release |
| `data/homepage.yaml` | Feature cards on the homepage |
| `data/roadmap.yaml` | Roadmap items with status, dates, and discussion links |
| `themes/polyphon/` | Custom theme (not a submodule — edit in place) |

`params.downloadVersion` is updated automatically by the `update-download-version.yml` workflow in the [`polyphon`](https://github.com/polyphon-ai/polyphon) repo on each release. Do not edit it by hand.

## Theme

The custom theme lives in `themes/polyphon/`. Key details:

- OKLCH color space for light/dark mode palettes
- Geist Sans variable font (served from `static/fonts/`)
- Provider accent colors (Anthropic, OpenAI, Gemini, Ollama, etc.) as CSS custom properties

## Release automation

When a Polyphon release is published, the `update-download-version.yml` workflow in the `polyphon` repo automatically:

1. Updates `params.downloadVersion` in `hugo.yaml`
2. Creates a new leaf bundle in `content/blog/polyphon-vX.Y.Z-released/`
3. Commits, pushes, and triggers a GitHub Pages deploy

Direct site edits (docs, theme, roadmap) are committed here independently.

## Related projects

| Repo | Relationship |
|---|---|
| [`polyphon`](https://github.com/polyphon-ai/polyphon) | Desktop app — drives version updates and release blog posts |
| [`obsidian-polyphon`](https://github.com/polyphon-ai/obsidian-polyphon) | Obsidian plugin — its docs live in `content/docs/integrations/obsidian-polyphon/` |
| [`polyphon-js`](https://github.com/polyphon-ai/polyphon-js) | JavaScript/TypeScript SDK — API reference in `content/docs/for-developers/api.md` |

## License

Apache 2.0 — see [LICENSE](LICENSE)
