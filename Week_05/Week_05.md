# Week 05 — Data Wrangling & Cleaning

## Overview
This week's lab goes deeper into **data wrangling**: reshaping tables, joining data from multiple sources, and handling messy real-world formats. You'll practice these operations in both Python (`pandas`) and R (`dplyr`/`tidyr`).

You may reuse the dataset you chose in [Week 2](../Week_02/Week_02.md)/[Week 4](../Week_04/Week_04.md), or pick a new one — just keep it consistent across all 5 tasks below. For Task 3, you will need a **second** small table to join against (see Task 3 for details).

## Submission Instructions
- Submit **two files**: one in **Python** (`.py` or `.ipynb`) and one in **R** (`.R` or `.Rmd`).
- Both files must solve **all 5 tasks** below, using the same dataset.
- Name your files clearly, e.g. `week05_yourname.py` and `week05_yourname.R`.
- Submit both files on Canvas under the Week 5 assignment.

---

## Task 1 — Renaming and Re-typing Columns
Pick a dataset with at least one messy column name (extra spaces, inconsistent casing, etc.) or a column stored as the wrong type (e.g. a number stored as text, or a date stored as a string).
1. Rename at least 2 columns to clean, consistent names (e.g. `snake_case`).
2. Convert at least 1 column to its correct data type (e.g. string → number, or string → date).

## Task 2 — Reshaping Data
Take a subset of your data and reshape it:
1. If your data is in **wide** format, convert part of it to **long** format (`pandas.melt` / `tidyr::pivot_longer`).
2. Then convert it back to **wide** format (`pandas.pivot` / `tidyr::pivot_wider`).
3. Print the shape (rows × columns) at each stage and briefly comment on what changed.

## Task 3 — Joining Two Tables
Create a small second table (by hand, e.g. 5-10 rows in a dictionary/list, or a tiny CSV) that has a column in common with your main dataset — for example, a lookup table mapping a category code to a full category name, or a region to a region name.
1. Join the two tables together (`pandas.merge` / `dplyr::left_join` or similar).
2. Print the result and confirm the join worked as expected (e.g. no unexpected `NaN`/`NA` values, or explain why some exist).

## Task 4 — Handling Messy Values
Identify (or intentionally introduce, for practice) at least one of the following issues in a column, and fix it:
- Inconsistent text categories (e.g. `"Male"`, `"male"`, `"M"` all meaning the same thing).
- Outliers in a numeric column (values far outside a reasonable range).
- Extra whitespace or inconsistent formatting in string values.

Print the column before and after your fix.

## Task 5 — A Wrangling Pipeline
Chain together at least 4 of the operations above (rename → retype → reshape/join → clean messy values) into a single script/pipeline that runs from raw data to a clean final table. Print the final table's shape and the first 5 rows.

---

## Notes
- Refer back to the [course Readme](../Readme.md) for IDE/platform setup (Kaggle/Colab for Python, Posit Cloud/RStudio for R).
- Keep your code well-commented — briefly explain what each wrangling step does and why it's needed.
- The goal this week is handling data that isn't already clean — don't pick a dataset that requires no work for Tasks 1 and 4.
