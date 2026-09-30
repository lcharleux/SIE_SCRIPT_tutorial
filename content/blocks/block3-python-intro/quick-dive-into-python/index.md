---
title: "A Quick Dive into Python"
linkTitle: "Quick Dive"
weight: 10
type: docs
date: "2026-05-22"
publishDate: "2026-01-01"
tags:
  - Python
  - Jupyter
authors:
  - admin
  - celmo
show_date: true
---

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

    Hello, Researcher!
