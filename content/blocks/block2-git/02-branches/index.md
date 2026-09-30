---
title: "Understanding Branches"
linkTitle: "Phase 2: Branches"
weight: 20
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

By default, your commits are created on the main branch of your project, named `main` or `master`.
A branch is a pointer to a commit.
It is possible to create other branches and switch to them in order to test a feature before integrating it into your main branch, for example.

> `Git Graph` ([here](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)) is a VS Code extension that can help you better visualize your branches.

## Related Commands

- List the repository's local branches:

    ```bash
    git branch
    ```

    Variant to list all local and remote branches:

    ```bash
    git branch -a
    ```

- Switch from one branch to another:

    ```bash
    git switch your_new_branch
    ```

    **Note**: to switch to a branch, that branch must exist. You can add the `-c` option to create a new branch and switch to it:

    ```bash
    git switch -c your_new_branch
    ```

    > You can also use the commands `git checkout your_new_branch` and `git checkout -b your_new_branch` to do the same thing.

- Merge two branches:

    ```bash
    git merge your_new_branch
    ```

## Exercises

1. On the `main` branch, breaking these steps into several commits, create a text file and add a few lines to it.
2. Create a new branch, add a new line to your file, and make a commit.
3. Merge this new branch from your main branch.
4. Undo your merge.
5. Make a commit on your main branch, perform a new merge, and resolve any conflicts.

> Think about best practices.

## Questions and Notes

- How can you move between branches without necessarily having to make a commit while work is in progress?

    > git stash

- How can you copy only one file from another branch into your current branch?

    > git restore --source=<autre_branche> chemin/vers/le/fichier

    Or:

    > git checkout <autre_branche> -- chemin/vers/le/fichier

- It is possible to move between different commits:

    > git checkout <commit_sha>

## Bonus Experiments

- `git rebase` can also be used to merge two branches.
- `git cherry-pick` can be used to integrate a commit from another branch.

## Best Practices

...
