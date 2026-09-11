# barrettjflowers.dev

Personal site and digital garden, served via GitHub Pages with Jekyll.

## structure

```
site/
├── docs/                          # GitHub Pages root (published to barrettjflowers.dev)
│   ├── _config.yml                # Jekyll config — title, plugins, permalink settings
│   ├── _layouts/
│   │   └── default.html           # Base Jekyll layout — boilerplate, back link, stylesheet
│   ├── vault/                     # Digital garden content (Markdown posts with YAML front matter)
│   │   ├── bibliographia.md       #    book recommendations
│   │   ├── botanicum.html         #    plant collection — draggable species cards
│   │   ├── filmography.md         #    film/video recommendations
│   │   ├── gallery.md             #    gallery (stub, needs content)
│   │   ├── jw-to-markdown.md      #    jw library to markdown
│   │   ├── resume.html            #    Resume — fetches content from barrettjflowers/simple-resume
│   │   └── verbose.md             #    personal info, favorites, socials, projects
│   ├── static/                    # Static assets
│   │   ├── bg.jpg                 #    dark-theme background
│   │   ├── bg.old                 #    previous background image
│   │   ├── giscus-dark.css        #    Giscus comment widget — dark theme
│   │   ├── giscus-light.css       #    Giscus comment widget — light theme
│   │   ├── hesperocyparis-macrocarpa.jpg   # Monterey cypress photo (botanicum)
│   │   └── sequoioideae.jpg       #     Coastal redwood photo (botanicum)
│   ├── style/
│   │   └── style.css              # Global stylesheet — dark/light/accessible themes
│   ├── CNAME                      # Custom domain — barrettjflowers.dev
│   └── index.html                 # Homepage — bio, graph viz, search, theme toggle, comments
└── README.md                      # This file
```

## features

- **Themes** — dark (default, forest-green bg), light, and accessible high-contrast; persisted in localStorage
- **Graph** — D3.js force-directed graph visualizing site file structure (clickable nodes)
- **Search** — autocomplete dropdown over vault links; `f` to focus
- **Comments** — Giscus widget (GitHub Discussions) on the homepage

## deployment

Push to `main` — GitHub Pages builds and deploys from `docs/` automatically.

## plugins

- `jekyll-seo-tag`
- `jekyll-sitemap`

