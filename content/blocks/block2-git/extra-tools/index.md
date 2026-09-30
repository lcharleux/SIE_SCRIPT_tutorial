---
title: "Extra Tools"
linkTitle: "Extra Tools"
weight: 40
type: docs
date: "2026-05-04"
publishDate: "2026-01-01"
tags:
  - Git
  - GitHub
authors:
  - celmo
  - admin
show_date: true
---

## Pre-commit

[Pre-commit](https://pre-commit.com/) is a small utility that automates actions in your repository before making a commit.
For example, it can be used to run checks, standardize code style, or prevent overly large files from being committed.


> Requirements:
>
> To use it, you will need a working Python installation.
> We strongly recommend installing your Python environment via `miniforge`. A guide is available on this [GitHub](https://github.com/conda-forge/miniforge) page.

You can install pre-commit in your Python environment with the following command:

```bash
pip install pre-commit
```

Pre-commit works by using a configuration file named `.pre-commit-config.yaml`, which must be located at the root of your Git repository (at the same level as the `.git` file).

Here is a minimal example of this type of configuration file:

```yaml
# .pre-commit-config.yaml
repos:
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v3.2.0
    hooks:
    -   id: trailing-whitespace
    -   id: end-of-file-fixer
    -   id: check-yaml
    -   id: check-added-large-files
```

You will then need to apply this configuration to your repository by running the following command:

```bash
pre-commit install
```

## The CI/CD Pipeline

Code hosting platforms such as GitHub and GitLab provide automation systems called CI/CD pipelines.

A pipeline is a sequence of actions that are automatically executed when an event occurs in your repository (for example, a `push` or a `pull request`).

These actions can be used to:

* run tests automatically
* compile code (or a LaTeX document)
* generate files called artifacts (for example, a PDF)
* deploy an application or a website

> The goal is to automatically check that the project works and produce results without manual intervention.

**Note**: These services often have limits on free accounts (compute time, number of minutes, etc.).

On GitHub, these automations are called **GitHub Actions**. They are configured using `.yml` files placed in the repository's `.github/workflows/` folder.

Here is an example of a file named `latex.yml` that compiles a LaTeX document on each `push` or `pull request`, then publishes the PDF as a downloadable artifact:

```yaml
# latex.yml
name: Build LaTeX PDF

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

permissions:
  contents: read

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Compile LaTeX document
        uses: xu-cheng/latex-action@v3
        with:
          root_file: main.tex

      - name: Upload PDF artifact
        uses: actions/upload-artifact@v4
        with:
          name: compiled-pdf
          path: main.pdf
```

An implementation of this example is available in this [repository](https://github.com/SCRIPT-SIE-2026/SCRIPT_SIE_2026_05_04_Git_CICD).
