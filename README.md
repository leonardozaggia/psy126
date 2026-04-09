<div style="padding-top:1em; padding-bottom:0.5em;">
  <img src="4.png" width="170" align="right" style="padding-left:1em;" />
</div>

<br>

$\ $

# Item Response Theory and Test Construction in Python

$\ $

This repository contains the **psy126** seminar materials for the Neurocognitive Psychology M.Sc. at the University of Oldenburg. All lectures and exercises are provided as a Jupyter Book and focus on applying Item Response Theory (IRT) and test construction techniques in **Python**.

## Topics covered

The book includes notebooks and slides on:

- Setting up your Python environment and working with Jupyter notebooks
- Data curation, manipulation and visualization with `pandas`, `numpy` and `matplotlib`
- Measurement models for **dichotomous items** (Rasch, 2‑PL, 3‑PL) using `rpy2`
- Models for **polytomous items**: Rating Scale Model, Partial Credit Model, Generalized PCM and Graded Response Model
- Concepts of **quantitative IRT**, **differential item functioning**, and **multilevel** / multidimensional modeling
- Templates for test theory reports and further resources

## Online usage (recommended)

The book is best viewed online via GitHub Pages:  [![Jupyter Book Badge](https://raw.githubusercontent.com/jupyter-book/jupyter-book/next/docs/media/images/badge.svg)](https://leonardozaggia.github.io/psy126/)

## Local usage

To build the book locally:

```batch
cd <path/to/book/>
pip install -r requirements.txt
jb build .
```

This creates HTML files in `_build/`. Open `_build/html/index.html` in your browser to browse the book. Exercise notebooks live in the `book/` folder and can be run locally or on Google Colab.

## Cloning the repository

Clone the repository if you want to keep a local copy and pull updates:

```batch
git clone https://github.com/leonardozaggia/psy126.git
```

Save your exercise solutions outside the repository to avoid overwriting them when running `git pull`.

A comprehensive tutorial on using Git in VS Code is available here: [![YouTube Badge](https://img.shields.io/badge/YouTube-red?logo=youtube&logoColor=white)](https://www.youtube.com/watch?v=i_23KUAEtUM)
