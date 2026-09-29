# Week 02 — The Data Science Lifecycle & Processing Pipelines

## Overview
This week's lab walks through the early stages of the **Data Science Lifecycle**: obtaining data, understanding it, cleaning it, and building a simple processing pipeline. The tasks are easy and designed to get you comfortable moving data through a sequence of steps in both Python and R.

## Choosing a Dataset
You have two options:
1. **Use your own dataset** — any CSV/tabular dataset you find interesting (e.g. from Kaggle, UCI, government open data portals). It should have at least 5 columns and 100+ rows.
2. **Use the suggested dataset** — [Uber Ride Analytics Dashboard](https://www.kaggle.com/datasets/yashdevladdha/uber-ride-analytics-dashboard/data) on Kaggle.

Whichever you choose, use the **same dataset for both your Python and R submissions**.

## Submission Instructions
- Submit **two files**: one in **Python** (`.py` or `.ipynb`) and one in **R** (`.R` or `.Rmd`).
- Both files must solve **all 5 tasks** below, using the same dataset.
- Name your files clearly, e.g. `week02_yourname.py` and `week02_yourname.R`.
- Submit both files on Canvas under the Week 2 assignment.

---

## Task 1 — Data Acquisition
Download your chosen dataset and load it into your environment (`pandas.read_csv` in Python, `read.csv`/`readr::read_csv` in R). Print:
1. The shape of the dataset (number of rows and columns).
2. The column names and their data types.

## Task 2 — Data Understanding
Explore the dataset before touching it:
1. Print summary statistics for the numeric columns (`.describe()` in Python, `summary()` in R).
2. Identify and print how many missing (NA/null) values exist in each column.

## Task 3 — Data Cleaning
Build a simple cleaning step:
1. Handle missing values in at least one column (either drop the rows or fill them with a sensible value — mean, median, or a placeholder — and explain your choice in a comment).
2. Remove duplicate rows, if any, and print how many were removed.

## Task 4 — A Simple Processing Pipeline
Chain together at least 3 steps into one pipeline (a sequence of function calls or a single script section), for example:
`load data → clean data → filter rows → create a new column`.
Your new column should be derived from at least one existing column (e.g. a ratio, a category bucket, or a date part extracted from a timestamp).

## Task 5 — Summarizing the Output
Using your cleaned/processed data from Task 4:
1. Group the data by one categorical column and compute an aggregate (e.g. mean, count, or sum) for a numeric column.
2. Print the top 5 groups by that aggregate value.

---

## Notes
- Refer back to the [course Readme](../Readme.md) for IDE/platform setup (Kaggle/Colab for Python, Posit Cloud/RStudio for R).
- Keep your code well-commented — briefly explain each step of your pipeline.
- The goal this week is thinking in terms of a **pipeline** (a repeatable sequence of steps), not just writing one-off code.
