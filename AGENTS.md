# barrettjflowers.dev — GitHub Pages static site

Personal site and digital garden. Jekyll builds the `docs/` directory and GitHub Pages publishes it to `barrettjflowers.dev` (CNAME). No build tooling runs locally.

## local dev

start local webserver: python3 -m http.server 8000

Note: serving with python http.server does NOT run Jekyll. Only static HTML is served — vault `.md` files render as raw markdown, and extension-less URLs (`/vault/verbose`) won't resolve. Verify Jekyll behavior by pushing to `main`; the GH Pages build runs Jekyll (kramdown, pretty permalinks).

## layout

- `docs/` — GitHub Pages root (published to barrettjflowers.dev)
  - `index.html` — homepage: bio, vault index, D3 graph, 3D glyph render, theme toggle, search, Giscus comments
  - `_config.yml` — Jekyll config (title, url, kramdown, pretty permalinks, jekyll-seo-tag + jekyll-sitemap plugins)
  - `_layouts/default.html` — base layout for vault Markdown pages (header, back link, search, theme JS)
  - `vault/` — digital garden content (see section below)
  - `style/style.css` — global stylesheet with dark/light themes via CSS variables
  - `style/giscus-{dark,light}.css` — Giscus comment widget themes
  - `static/` — images (`bg.jpg`, plant photos) and `.obj` 3D models (`flower.obj`, `teapot.obj`)
  - `rss.json` — manual JSONFeed of "shower thoughts" (sourced from GitHub Discussions #2)
  - `CNAME` — custom domain `barrettjflowers.dev`
- `README.md` — human-readable overview, largely duplicated by this file

## vault

Digital garden content in `docs/vault/`. Two kinds of files:

1. **Markdown pages** (`verbose.md`, `bibliographia.md`, `filmography.md`, `jw-to-markdown.md`, `gallery.md`) — render through `_layouts/default.html`; need YAML front matter (`title`, `layout: default`, optional `date`). Jekyll's `pretty` permalink means the live URL is extension-less (`/vault/verbose`).
2. **Raw HTML pages** (`resume.html`, `botanicum.html`, `shower-thoughts.html`) — hand-written pages that duplicate the header/search/theme boilerplate instead of using the Jekyll layout. They keep the `.html` extension in URLs.

Navigation conventions: vault links use extension-less URLs for `.md` pages and literal `.html` for the raw HTML pages. When adding a vault entry, update: the vault `<section>` in `index.html`, the graph nodes/links, and (since each page duplicates the search script) the hardcoded `vaultLinks` array in `_layouts/default.html` (and in standalone HTML pages).

Caveats: `gallery.md` is a stub whose body currently duplicates book recommendations; `botanicum.html` uses absolute `/static/...` image paths.

## D3 graph

On `index.html` (~lines 104–225): a D3 v7 force-directed graph visualizing the site's file structure. Data is **hardcoded inline** in two arrays:

- `nodes` — `{ id, type: "file"|"folder", url? }`. Nodes with a `url` navigate on click.
- `links` — `{ source, target }` edges describing the directory tree (`index.html` → folders → files).

Rendered into `#graph-container` inside the `<section class="graph">`. `d3.forceSimulation` with `forceLink` (distance 40), `forceManyBody` (strength −100), and `forceCenter`. Each node is a `<circle>` with a text label, all styled `#7E857C`; nodes are draggable (via `d3.drag`, pinned with `fx`/`fy`). Click navigates via `d.url` unless the node was just dragged (`d.dragged` flag). When the site structure changes, update both arrays by hand.

## other notable concepts

- **Themes** — `data-theme` attribute on `<html>` toggles CSS variables in `style/style.css`; `dark` (default) is green-black with `static/bg.jpg`, `light` is near-white. Persisted in `localStorage.theme`. Each page runs its own toggle JS.
- **Search** — header `<input>` with an autocomplete dropdown over vault links; `f` focuses it, arrow keys navigate, Enter follows. Script is duplicated per page (`index.html` reads links from the `.vault` section DOM; `_layouts/default.html` and raw HTML pages use a hardcoded array).
- **Giscus comments** — homepage is discussion #1 (`data-term="1"`), `shower-thoughts.html` is discussion #2 (`data-term="2"`). Themes must be synced to the page theme via `postMessage`.
- **3D render** — `glyph-camera`/`glyph-scene`/`glyph-mesh` custom elements from `https://esm.sh/glyphcss/elements` render `static/flower.obj`; draggable via `glyph-orbit-controls`.
- **Misc homepage widgets** — 88x31 visitor counter from `88x31.lol`.

## deployment / workflow

- Push to `main` → GitHub Pages builds from `docs/` automatically.
- `_config.yml` excludes `README.MD` and `CNAME` from the output; `include` has `.well-known`.
- No tests or linting configured for this repo; validate by viewing the built site.