# SCRIPT — Scientific Computing & Reproducible IT Practices and Tools


This repository hosts the public site for the PANDA training path. It is based on the [Hugo Blox](https://hugoblox.com/) Academic CV starter and Tailwind CSS v4 for styling. Here you will find the pages describing each track (LaTeX, Git, Python, Docker, …) and the accompanying static assets (images, Mermaid scripts, Markdown content).

## Repository structure

| Path                        | Purpose |
|----------------------------|---------|
| `content/`                 | All site pages (courses, posts, workflow, …). |
| `assets/`                  | Images, icons, and other Hugo-managed media. |
| `layouts/`                 | Overrides for Hugo Blox partials and blocks. |
| `config/_default/`         | Hugo configuration (menus, languages, params). |
| `hugoblox.yaml` / `go.mod` | Theme settings and Hugo Blox modules. |
| `package.json`             | Front-end scripts and dependencies (pnpm). |
| `content/workflow/*.mmd`   | Mermaid diagrams plus the export script. |

## Prerequisites

- Node.js ≥ 22 and [pnpm 10.14](https://pnpm.io/) for front-end tooling.
- Hugo Extended 0.150 (version pinned in `hugoblox.yaml`).
- Go ≥ 1.19 for resolving Hugo modules.
- Python ≥ 3.11 if you want to run the [Marimo](https://marimo.io/) server for interactive notebooks.

> Tip: on macOS/Linux you can install pnpm and Hugo via Homebrew (`brew install pnpm hugo`) and manage Python with `pyenv` or `uv`.

## Installation

```bash
pnpm install
```

This installs Tailwind CSS and the dependencies required by Hugo Blox (Mermaid, Tailwind plugins, etc.).

## Editing the site

1. **Pick the page to edit**
   - All pages live under `content/`. Each subfolder is a section (`courses`, `post`, `workflow`, …).
   - Pages use an `index.md` file with YAML front matter followed by Markdown content.

2. **Update metadata**
   - Example (Git course: `content/courses/git/index.md`):
     ```yaml
     ---
     title: "Git — Versioning for Researchers"
     date: "2025-10-26"
     publishDate: "2025-09-01"
     tags:
       - Git
       - Workflow
     authors:
       - admin
     ---
     ```
   - Adjust `title`, `summary`, `tags`, `authors`, `image`, etc. Hugo picks up the changes automatically.

3. **Edit the body**
   - Write standard Markdown. You can use Hugo shortcodes such as `{{< relref "courses/python1/index.md" >}}` or author mentions `{{% mention "celmo" %}}`.
   - Store images next to the page (e.g. `content/courses/git/featured.png`) and reference them through front matter or Markdown (`![caption](featured.png)`).

4. **Preview locally**
   - Run `pnpm dev` and open `http://localhost:1313`. Hugo rebuilds the page every time you save.

5. **Example: editing the Workflow page**
   - File: `content/workflow/index.md`.
   - Update the “Step 1/2/…” section to add or reorder modules.
   - Regenerate the diagram by running `content/workflow/mermaid_to-png.sh` (requires Mermaid CLI `mmdc`) to refresh `workflow.png`.

6. **Add a new page**
   ```bash
   hugo new content/courses/new-course/index.md
   ```
   - Hugo bootstraps a file with minimal front matter. Fill it in, add your content, and update menus (`config/_default/menus.yaml`) if the page should appear in navigation.

7. **Translations / multi-language**
   - The site currently targets a single language (see `config/_default/languages.yaml`). To add, for example, an English variant of a page, place an `index.en.md` alongside the default file and translate the front matter plus body.

## Run the site locally

```bash
pnpm dev
```

- Hugo serves the site on `http://localhost:1313`.
- `--disableFastRender` is enabled to avoid aggressive caching while editing.
- Tailwind assets rebuild automatically with every change.

## Create the production build

```bash
pnpm build
```

Hugo writes the static output to `public/`. This folder is what GitHub Pages/Netlify publish (`.github/workflows/hugo.yaml`, `netlify.toml`).

## Run a Marimo server

Interactive notebooks (Python exercises, demos) can be served with [Marimo](https://marimo.io/). The repo does not include notebooks yet; create a `marimo/` folder and add your `.py` notebooks (a Marimo notebook is just an annotated Python script).

1. **Prepare a Python environment**
   ```bash
   python -m venv .venv-marimo
   source .venv-marimo/bin/activate        # Windows: .venv-marimo\Scripts\activate
   pip install -U pip marimo
   ```
   > Prefer isolated tooling? Use `uv tool install marimo` or `pipx install marimo`.

2. **Create an optional sample notebook**
   ```bash
   mkdir -p marimo
   marimo new marimo/intro.py
   ```

3. **Start the server**
   ```bash
   marimo run marimo/intro.py --host 127.0.0.1 --port 2718 --reload
   ```
   - UI available at `http://127.0.0.1:2718`.
   - Use `marimo edit …` to open the built-in editor if desired.
   - `--reload` hot-reloads on save. Press `Ctrl+C` to stop.

4. **Integrate with the site**
   - Export notebooks to HTML or Markdown and place them under `content/` or `static/`.
   - For live sessions, simply link to the local Marimo URL from the relevant course page.

## Deployment

- **GitHub Pages**: `.github/workflows/hugo.yaml` installs Go, Hugo Extended, Dart Sass, and Node.js, then runs `hugo --gc --minify`.
- **Netlify**: `netlify.toml` is configured with `hugo` as the build command and `public/` as the publish directory.

Push to the `main` branch to trigger automatic publication.

## License

The project inherits the license shipped with `LICENSE.md` (Hugo Blox Academic CV starter). Update it if you add content that requires different terms.
