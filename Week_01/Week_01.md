# Week 01 — Introduction to Data Science Programming

## Overview
This week's lab introduces the basics of programming for data science in **both Python and R**. The tasks are intentionally simple and focus on getting comfortable with variables, basic I/O, simple data structures, and reading a small CSV file.

A sample dataset is provided at [`data/student_scores.csv`](data/student_scores.csv) — use it for Tasks 4 and 5.

## Submission Instructions
- You must submit **two files**: one written in **Python** (`.py` or `.ipynb`) and one written in **R** (`.R` or `.Rmd`).
- Both files must solve **all 5 tasks** below.
- Name your files clearly, e.g. `week01_yourname.py` and `week01_yourname.R`.
- Submit both files on Canvas under the Week 1 assignment.

---

## Task 1 — Hello, Data Science!
Print a greeting message that includes your name, e.g. `"Hello, my name is <Your Name> and I am learning Data Science!"`.

## Task 2 — Basic Arithmetic
Create two variables `a = 15` and `b = 4`. Compute and print their sum, difference, product, quotient (division), and remainder (modulo).

## Task 3 — Working with a List/Vector
Create a list (Python) or vector (R) containing the numbers `[4, 8, 15, 16, 23, 42]`. Print:
1. The total sum of the numbers.
2. The average (mean) of the numbers.
3. The maximum and minimum values.

## Task 4 — Reading a CSV File
Load the file `data/student_scores.csv` into a data structure (a `pandas` DataFrame in Python, or a `data.frame` in R). Print:
1. The first 5 rows of the data.
2. The number of rows and columns.

## Task 5 — Simple Filtering
Using the data loaded in Task 4, filter and print only the students who scored **80 or above**. Then print how many students that is.

---

## Notes
- Feel free to use any IDE or platform mentioned in the [course Readme](../Readme.md) (Kaggle/Colab for Python, Posit Cloud/RStudio for R).
- Keep your code well-commented — briefly explain what each part does.
