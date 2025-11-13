---
title: "Block 1: An introduction to LaTeX for Academic Writing"
date: "2025-11-26"
publishDate: "2025-09-01"
links:
  - type: site
    url: https://www.latex-project.org/
tags:
  - LaTeX
  - Academic Writing
authors:
  - admin
  - celmo
show_date: false
---

## Introduction

LaTeX is a robust typesetting system widely used for scholarly communication in the sciences, engineering, and the humanities.
This session introduces the principles and disciplined practices that enable clear, consistent, and reproducible academic writing across theses, articles, and technical reports.

{{< toc mobile_only=false is_open=true >}}

## LaTeX vs. Word in Scientific Writing

LaTeX is a markup-based system designed for long, structured, and mathematically intensive documents. It separates content from formatting, ensuring stable layout, consistent references, and excellent typography—qualities that are especially valuable in PhD theses and scientific articles.

Word offers intuitive visual editing but can become fragile as documents grow, particularly when handling equations, figures, or complex formatting. While it remains convenient for quick drafting and broad collaboration, it lacks the reproducibility and structural reliability that LaTeX provides for large scientific manuscripts.

A basic LaTeX document looks like this:

```latex
\documentclass{article}
\usepackage{amsmath}
\begin{document}
\title{An Introduction to LaTeX}
\author{Random PhD Student}
\date{\today}
\maketitle
\section{Introduction}
Wow \LaTeX is great for typesetting mathematics! 
Here is an example of Einstein's famous equation:
\begin{equation}
E = mc^2
\end{equation}
\end{document}
```

LaTeX separates content from presentation, allowing authors to focus on writing while ensuring consistent formatting.
It excels at handling complex documents with features like automatic numbering, cross-referencing, bibliographies, and high-quality typesetting of mathematics.

## Tutorial Program

By the end of the session, participants will be able to:

- Write basice documents using LaTeX and compile them to PDF.
- Structure documents using classes, packages, and a well‑defined preamble.
- Compose mathematics, use figures, create tables, and use accurate cross‑referencing.
- Manage bibliographies with BibTeX and apply journal or institutional citation styles.
- Organize long projects using modular files and coherent directory layouts.
- Compile reliably with modern engines and tools (e.g., `latexmk`) and diagnose common errors.
- Manage your supervisors.

Emphasis is placed on reproducibility, separation of content and presentation, and maintainable project structure rather than ad‑hoc formatting. 
Basic command‑line familiarity is helpful but not required.

## Prerequisites

- Students must have administrative install permissions on their computer (Windows, macOS, or Linux).
These are required to install the LaTeX toolchain and editor extensions used in the session.
- A LaTeX distribution that provides `pdflatex` and `latexmk` (e.g., TeX Live, MiKTeX, or MacTeX).
- Visual Studio Code (VS Code) as the IDE.
- Git installed is recommended for version control examples.

### Platform notes

- Windows:
  - [x] install MiKTeX and ensure `pdflatex` is available.
  - [x] Install Strawberry Perl to enable `latexmk` and confirm `perl` is on your `PATH`.
- macOS:
  - [x] install MacTeX (or TeX Live) and ensure `pdflatex`/`latexmk` are available.
- Linux:
  - [x] install TeX Live from your package manager and ensure `pdflatex`/`latexmk` are available.

### Verifications

{{% callout note %}}
To check PDFLaTeX installation, run the following commands in a terminal or command prompt: `pdflatex -v`
{{% /callout %}}

{{% callout note %}}
To check LaTeXmk installation, run the following commands in a terminal or command prompt: `latexmk -v`
{{% /callout %}}

{{% callout note %}}
On Windows, to check Perl installation (from Strawberry Perl), run the following commands in a terminal or command prompt: `perl -v`
{{% /callout %}}

<!--more-->