---
title: "Bash to PowerShell Cheatsheet"
date: "2026-05-12"
weight: 80
type: docs
authors:
  - celmo
  - admin
tags:
  - Bash
  - PowerShell
  - Cheatsheet
show_date: true
---

## Variables and Environment

| Bash | PowerShell | Description |
|---|---|---|
| `$HOME` | `$HOME` | User home directory |
| `$USER` | `$env:USERNAME` | Current username |
| `$PATH` | `$env:PATH` | PATH environment variable |
| `export VAR=value` | `$env:VAR="value"` | Define environment variable |
| `unset VAR` | `Remove-Item Env:VAR` | Remove environment variable |
| `echo $VAR` | `echo $env:VAR` | Read environment variable |

---

## Current Directory

| Bash | PowerShell | Description |
|---|---|---|
| `pwd` | `pwd` | Print current directory |
| `$(pwd)` | `${PWD}` | Current directory object/string |
| `cd folder` | `cd folder` | Change directory |
| `cd ..` | `cd ..` | Parent directory |
| `ls` | `ls` | List files |
| `ls -la` | `ls -Force` | Show hidden files |

---

## File Operations

| Bash | PowerShell | Description |
|---|---|---|
| `cp file1 file2` | `Copy-Item file1 file2` | Copy file |
| `mv file1 file2` | `Move-Item file1 file2` | Move/Rename file |
| `rm file` | `Remove-Item file` | Remove file |
| `rm -rf folder` | `Remove-Item folder -Recurse -Force` | Remove directory recursively |
| `mkdir folder` | `New-Item -ItemType Directory folder` | Create directory |
| `touch file.txt` | `New-Item file.txt` | Create empty file |
| `cat file.txt` | `Get-Content file.txt` | Display file content |

---

## Pipes and Redirection

| Bash | PowerShell | Description |
|---|---|---|
| `command > file.txt` | `command > file.txt` | Redirect output |
| `command >> file.txt` | `command >> file.txt` | Append output |
| `command1 \| command2` | `command1 \| command2` | Pipe output |
| `grep "text"` | `Select-String "text"` | Search text |
| `find . -name "*.py"` | `Get-ChildItem -Recurse -Filter "*.py"` | Find files |

---

## Process Management

| Bash | PowerShell | Description |
|---|---|---|
| `ps` | `Get-Process` | List processes |
| `kill PID` | `Stop-Process -Id PID` | Kill process |
| `top` | `Get-Process` | Monitor processes |
| `clear` | `Clear-Host` | Clear terminal |

---

## Docker Examples

| Bash | PowerShell |
|---|---|
| `docker run -v $(pwd):/app image` | `docker run -v ${PWD}:/app image` |
| `docker run -v $(pwd)/data:/data image` | `docker run -v ${PWD}/data:/data image` |
| `docker build -t myimage .` | `docker build -t myimage .` |
| `docker compose up` | `docker compose up` |

---

## Command Substitution

| Bash | PowerShell |
|---|---|
| `$(pwd)` | `${PWD}` |
| `$(whoami)` | `$(whoami)` |
| `$(date)` | `Get-Date` |

---

## Conditional Operators

| Bash | PowerShell |
|---|---|
| `&&` | `; if ($?) { ... }` |
| `\|\|` | `; if (-not $?) { ... }` |

---

## Useful Notes

- PowerShell uses objects internally, not plain text.
- Many Linux commands (`ls`, `cat`, `pwd`) are aliases in PowerShell.
- Environment variables are accessed through `$env:`.
- `${PWD}` is often required instead of `$(pwd)` in Docker commands under PowerShell.