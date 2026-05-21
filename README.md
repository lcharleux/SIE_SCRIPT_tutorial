# SCRIPT Tutorials

This repository hosts the documentation site for the SCRIPT training material. The site is built with [Hugo](https://gohugo.io/) and the [Docsy](https://www.docsy.dev/) documentation theme.

## Structure

| Path | Purpose |
| --- | --- |
| `content/blocks/` | Published course blocks for LaTeX, Git, Python, Docker, and advanced Python. |
| `content/workflow/` | Recommended path through the training blocks. |
| `config/_default/` | Hugo and Docsy configuration. |
| `layouts/shortcodes/` | Local compatibility shortcodes used by the migrated course content. |
| `layouts/_default/index.json` | Search index template for Docsy offline search. |
| `assets/` | Site images, icons, and logos retained from the previous site. |

The previous portfolio-style content sections are still present under `content/` but are temporarily ignored in `config/_default/hugo.yaml`. Their course content has been migrated into `content/blocks/`.

## Prerequisites

- Hugo Extended 0.152 or newer.
- Go 1.19 or newer for Hugo modules.
- Node.js and pnpm for PostCSS assets.

## Install Dependencies

```bash
pnpm install
```

## Run Locally

```bash
pnpm dev
```

The site is served locally by Hugo. If port `1313` is already in use, run:

```bash
hugo server -D --bind 127.0.0.1 --port 1314
```

## Build

```bash
pnpm build
```

This runs `hugo --minify` and writes the generated site to `public/`.

## Add Course Content

Add new documentation pages under `content/blocks/`. Use page bundles for course pages that include images:

```text
content/blocks/block4-docker/
├── _index.md
├── 01-first-container/
│   └── index.md
└── cheatsheets/
    └── docker-commands/
        └── index.md
```

Use `weight` in front matter to control the order in the left navigation:

```yaml
---
title: "Docker Compose"
linkTitle: "Docker Compose"
weight: 30
---
```

## Deployment

The production build command is:

```bash
pnpm build
```

The generated `public/` directory can be published by GitHub Pages or Netlify.
