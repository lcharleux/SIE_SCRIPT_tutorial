---
title: "Block 3:  Introduction to Scientific Python"
date: "2025-10-26"
publishDate: "2025-09-01"
links:
  - type: site
    url: https://www.python.org/
tags:
  - Python
  - Git
  - Jupyter
authors:
  - admin
---

{{% callout note %}}

It is better if you have attended blocks 1 and 2 before starting this one.

{{% /callout %}}

## Introduction

You didn’t start a PhD to spend your days copying-pasting in Excel or manually renaming 200 files. You started it to do science — and Python is the tool that lets you focus on thinking, not clicking.

What you’ll learn in Block 3 is:

- Core Python syntax: variables, types, and control flow
- Essential data structures: lists, dicts, sets, and arrays
- Working in notebooks and scripts (Jupyter vs. `.py`)
- Reading/writing files and simple automation
- Plotting basics with Matplotlib
- First steps with NumPy and pandas/polars for data tasks

No coding background? No problem. We start from zero and build up the skills every researcher wishes they’d learned earlier.

Python isn’t just for programmers — it’s the Swiss army knife of modern research. Let’s make it your secret weapon.

### A quick dive into Python

Python is a high-level, interpreted programming language known for its readability and versatility. It’s widely used in scientific computing, data analysis, machine learning, web development, and automation.
Is is easy to learn for beginners yet powerful enough for experts, making it a popular choice across various domains.

```python
# Variables and types
name = "Researcher"
age = 30
is_student = False  
height = 1.75  # in meters
# Control flow
if age < 18:
    status = "Minor"
else:
    status = "Adult"
# Data structures
scores = [85, 90, 78, 92]  # List
profile = {"name": name, "age": age, "status": status}  # Dict
unique_ids = {101, 102, 103}  # Set
import numpy as np
data = np.array([1, 2, 3, 4, 5])
# Functions
def greet(person):
    return f"Hello, {person}!"
print(greet(name))
```

Many interactive examples are available as Jupyter Notebooks on our teaching website [Positron](https://symmehub.github.io/positron/intro.html).

## Tutorial program

By the end of the session, participants will be able to:

- Write basic Python scripts and Jupyter notebooks for data analysis.
- Use core Python data structures and control flow to manipulate data.
- Create basic plots using Matplotlib to visualize data.
- Perform data manipulation tasks using NumPy and pandas/polars.

## Prerequisites

- Students **must come with a laptop with administrative install permissions** and a compatible OS (Windows, macOS, or Linux).
- Install MiniForge, VSCode and GIT using our site [Positron](https://symmehub.github.io/positron/setup/setup.html) instructions.










<!--more-->
