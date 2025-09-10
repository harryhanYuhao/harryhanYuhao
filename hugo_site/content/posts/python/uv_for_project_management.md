---
date: '2025-05-05T15:11:48+01:00'
title: 'UV for Python Project Management'
description: 'How to make python code reliable and reproducible on all computers.'
tags: ['python']
showToc: true
TocOpen: false
hidemeta: false
comments: false
description: ""
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
---

## Issues of Reproducibility

Python is notorious for its lack of reproducibility.
(It is not the worst, the title of which shall be reserved, probably, for C++.)
Clone any python repository with more then 1000 lines of code from GitHub and try to run it on your personal computer.
The first step, which is how to execute the program, will be difficult enough.
The nightmare, however, is to make sure your system has the correct version of python, compatible versions of each python package, each C library the python package relies on, and each driver and system software C library relies on.

Python is not alone.
This is the classical problem of code distribution and package management. 

In recent years, python development team are trying to solve this problem by introducing virtual environment, `.venv`, and `pyproject.toml`. 
As of 2025 with python version 3.13, however, these measures are far from sufficient.

In the mean time, third many thiry party applications emerges, trying to solve this problem.
One of them, [uv](https://docs.astral.sh/uv/), I found superior to all others.


## UV for Python Project

Uv can create all the spoiler plates of a project for you 

```bash
uv init dummy_project --python 3.12 # using python version 3.12
```

Use `uv add` to install python packages.

```
uv add numpy pandas ipykernel
```

The first time `uv add` is executed, `uv` will create a virtual environment, `.venv/`, in the current directory with the correct python version.
If the requested python version can not be found, uv will download it automatically and keep it in a separate space without interfering with the system python binary.

Check the python versions managed by uv with `uv python list`.

The virtual environment created will be identical to the one created with `python -m venv .venv/`, except it will not have `pip`, as all installations shall be handled by `uv add`.

Run the main script with 

```bash
uv run main.py
```

After this is python development as usual.

### Note on Jupyternote book

To use jupyternote book, create a python project with steps above. 
In particular, install `ipykernel`

```
uv add ipykernel
```

Uv shall have created a virtual environment in the current directory. 

Open VSCode or Pycharm in the current directory. (You need open in the current directory else the `.venv/` directory may not be found.)
Select `.venv/` as python source in your IDE, and everything shall work as fine.
