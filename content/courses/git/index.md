---
title: "Managing projects with Git "
# date: "2025-10-26"
publishDate: "2025-09-22"
links:
  - type: site
    url: https://github.com/pandas-dev/pandas
tags:
  - GIT
  - GIThub
authors:
  - celmo
  - admin
---

## Training Scope (4h)

### 🎯 Learning Objectives &#x1F3AF;
Understand versioning principles and adopt Git as the central tool for tracking code, data, and research documents.

> Disclaimer: 
> - This course focuses on practical Git usage for researchers. It does not cover advanced Git internals or server administration.
> - We will use VS Code's integrated Git features for ease of use, but command-line equivalents will be provided.

### 🧩 Target Skills

- Understand foundational concepts
    - What is version control ?
    - Local vs remote repositories
    - Commits, branches, merges

- Master essential Git commands using VS Code
    - Initialize a repository
    - Stage and commit changes
    - Create and switch branches
    - Push and pull from remote repositories

- Collaborate on a project (GitHub, GitLab)
    - Define remotes and clone repositories
    - Define working strategies
    - handle merge and conflicts

- Track a scientific document
    - Set up `.gitignore` for research files
    - Revert to earlier states

- Notion of advances features
    - Tags and releases
    - Pull requests
    - GitHub/Gitlab CI/CD basics
    - Git LFS for large files

- Best practices
    - Commit message conventions
    - Structuring repositories properly
    - Branching strategies (main/dev/feature)
    - Backup and recovery strategies

## Prerequisites, installation and configuration

### Prerequisites

> IMPORTANT: You need to be administrator on your computer to install Git and to run the configuration commands.

- **GitHub account:** Create an account on a Git hosting provider (GitHub, GitLab, Bitbucket)
In this course, we will use GitHub as the remote hosting provider. If you don't have an account yet, please sign up at [https://github.com/](https://github.com/) and follow the instructions provided there.

### Installation Instructions

- **Windows**
 
  Download and install Git for Windows from https://git-scm.com/download/win. Use Git Bash for command-line operations.

- **macOS**
  
  In modern macOS versions, Git is included with the Xcode Command Line Tools. Install them by running `xcode-select --install` in the terminal. Alternatively, install Git via Homebrew with `brew install git`.

- **Linux (Ubuntu/Debian)**
  
  Open a terminal and run:
  ```bash
  sudo apt update
  sudo apt install git
  ```
### Configuration Steps

In order to set up Git for the first time, you need to configure your user name and email address. Open a terminal (git-bash on Windows) and run the following commands, replacing the placeholders with your actual information:

```bash
git config --global user.name "Your Name"
git config --global user.email "my-email@mail.com"
```
Fill in your GitHub email address to link your commits to your GitHub account.
