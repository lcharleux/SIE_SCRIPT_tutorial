---
title: "Working Locally with Git"
linkTitle: "Phase 1: Local Work"
weight: 10
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

During this step, we will review the basic Git commands and make our first commits.

## Basic Commands

> Most of the commands provided here can be run using the `VS Code` graphical interface.

- Initialize Git tracking in a folder:

    ```bash
    git init
    ```

- Check the status of a repository:

    ```bash
    git status
    ```

- Add a file to tracking:

    ```bash
    git add my_file.txt
    ```

- Make a commit:

    ```bash
    git commit -m "Commit description"
    ```

- View the commit history:

    ```bash
    git log
    ```

    Or, for a more compact view:

    ```bash
    git log --pretty=oneline
    ```

- Undo your last commit:

    ```bash
    git reset --soft HEAD~1
    ```

    > You can replace `1` with a positive integer to undo as many recent commits as needed. For example, `git reset --soft HEAD~5` will undo your last 5 commits.

## Exercises

1. Create a text file and make your first commit.
2. Make several changes and create a sequence of commits.
3. Deliberately introduce an error and try to fix it.
4. Add a binary file and make a commit.
5. Exclude files from Git tracking.

    > Think about best practices.

## Notes

### Commit Messages

There are guides/conventions ([see here](https://www.conventionalcommits.org/en/v1.0.0/#specification), [or here](https://gist.github.com/qoomon/5dfcdf8eec66a051ecd85625518cfd13)) that define how commit messages should be written. This convention is more a matter of software engineering best practices.

In general, you can follow these simple guidelines:

- prefer a short message (50 characters maximum);
- provide context if needed;
- separate changes.

> Can I understand what this commit does just from its commit message?

The most common format is:

```bash
type: short summary
```

The most commonly used types are:

```yaml
add: adding a new file
feat: adding a feature
fix: bug fix
docs: documentation
refactor: change with no functional impact
test: adding/modifying tests
wip: (work in progress) dedicated to development branches
chore: changes related to your repository configuration
```

> &#x1F4A1; A good commit message goes hand in hand with a good grouping/breakdown of your changes in your commit.

Here’s a simple example: I’ve added a new section to a document: 

```yaml
feat: add new section ‘Chapter 1: Were Ross and Rachel on a break?’
```

## Best Practices

- Group changes related to the same topic or feature into a single commit.
- Always create a .gitignore file at the beginning of the project.
- Prefer committing source files rather than generated binaries.
