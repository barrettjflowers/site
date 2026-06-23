# barrettjflowers.dev

Personal site and digital garden, served via GitHub Pages with Jekyll.

## structure

```
site/
├── docs/                          # GitHub Pages root (published to barrettjflowers.dev)
│   ├── _config.yml                # Jekyll config — title, plugins, permalink settings
│   ├── _layouts/
│   │   └── default.html           # Base Jekyll layout — boilerplate, back link, stylesheet
│   ├── blog/                      # Digital garden content (Markdown posts with YAML front matter)
│   │   ├── arboretum.md           #    trees & shrubs digital collection
│   │   ├── ascii.md               #    ASCII art archive (stub)
│   │   ├── bibliographia.md       #    book recommendations
│   │   ├── filmography.md         #    film/video recommendations
│   │   ├── gallery.md             #    gallery (stub, needs content)
│   │   └── verbose.md             #    personal info, favorites, socials, projects
│   ├── static/                    # Static assets
│   │   ├── bg.jpg                 #    dark-theme background
│   │   ├── bg.old                 #    previous background image
│   │   ├── giscus-dark.css        #    Giscus comment widget — dark theme
│   │   ├── giscus-light.css       #    Giscus comment widget — light theme
│   │   ├── hesperocyparis-macrocarpa.jpg   # Monterey cypress photo (arboretum)
│   │   └── sequoioideae.jpg       #     Coastal redwood photo (arboretum)
│   ├── CNAME                      # Custom domain — barrettjflowers.dev
│   ├── index.html                 # Homepage — bio, graph viz, search, theme toggle, comments
│   ├── resume.html                # Resume — fetches content from barrettjflowers/simple-resume
│   └── style.css                  # Global stylesheet — dark/light/accessible themes
└── README.md                      # This file
```

## features

- **Themes** — dark (default, forest-green bg), light, and accessible high-contrast; persisted in localStorage
- **Graph** — D3.js force-directed graph visualizing site file structure (clickable nodes)
- **Search** — autocomplete dropdown over vault links; `f` to focus, `?` for legend, `a` for accessibility
- **Comments** — Giscus widget (GitHub Discussions) on the homepage

## deployment

Push to `main` — GitHub Pages builds and deploys from `docs/` automatically.

## plugins

- `jekyll-seo-tag`
- `jekyll-sitemap`

