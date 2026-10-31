# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Course material for "Big Data Processing" (FH Kufstein Tirol, DSIA, winter semester 2026/27). It is not an application: the content is Jupyter notebooks and markdown handouts organized into `session-NN/` folders, each self-contained for one class session. There are no tests, no build, and no lint setup. Every lab notebook ends with **exam-style questions** — keep that pattern when adding or editing labs.

## Commands

```bash
source .venv/bin/activate                 # venv already exists (Python 3.12)
pip install -r requirements-local.txt     # laptop set: pandas, Polars, DuckDB, PyArrow, scikit-learn
pip install -r requirements.txt           # above + PySpark 4.0 + Delta Lake (needs Java 17+)
python get_data.py --months 2             # download NYC Yellow Taxi 2024 Parquet + zone lookup into data/
python session-04/check_env.py            # verify the environment (read-only)
```

`get_data.py` deliberately uses only the Python standard library so students can run it before any environment exists — keep it dependency-free.

## Where notebooks run

Students have three execution targets; notebooks are written for a specific one:
- **Laptop (no Java):** everything single-node — pandas/Polars/DuckDB/scikit-learn labs (session-01, session-04 Labs A–C).
- **Kaggle:** Spark notebooks (e.g. `session-04/04_spark_fundamentals_and_ml.ipynb`). Their first cell installs Java 17 + PySpark itself, since students upload them to Kaggle standalone — Spark notebooks must not assume local files beyond the dataset named at the top.
- **Dev container / Codespaces** (`.devcontainer/`): Python 3.12 + Java 17 + full `requirements.txt`; the alternative way to run Spark locally.

## Git

- Use the `gh` CLI for GitHub operations (auth, push uses its credential helper).

## Conventions

- Audience is 3rd-semester students: code in notebooks should stay simple and explainable line-by-line, pedagogy over cleverness.
- Never commit `data/`, `.venv/`, or executed notebooks with large outputs (`.gitignore` covers these — don't weaken it).
