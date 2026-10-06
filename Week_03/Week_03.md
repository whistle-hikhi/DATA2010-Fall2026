# Week 03 — Reproducible Data Science

## Overview
This week's lab focuses on **reproducibility**: making sure that anyone (including future-you) can re-run your analysis and get the exact same results. You'll practice setting random seeds, recording your environment/dependencies, organizing a project folder, and documenting your steps.

You may reuse the dataset you chose in [Week 2](../Week_02/Week_02.md), or pick a new one — just keep it consistent across all 5 tasks below.

## Submission Instructions
- Submit **two files**: one in **Python** (`.py` or `.ipynb`) and one in **R** (`.R` or `.Rmd`).
- Both files must solve **all 5 tasks** below.
- Also submit the two supporting files from Task 2 (`requirements.txt` and `session_info.R`/`renv.lock` output) alongside your code.
- Name your files clearly, e.g. `week03_yourname.py` and `week03_yourname.R`.
- Submit everything on Canvas under the Week 3 assignment.

---

## Task 1 — Setting a Random Seed
Write a short piece of code that generates 10 random numbers (e.g. from a normal or uniform distribution).
1. Set a fixed random seed (`random.seed()`/`numpy.random.seed()` in Python, `set.seed()` in R) before generating the numbers.
2. Run it twice and confirm (print + comment) that both runs produce identical output.

## Task 2 — Recording Your Environment
Reproducibility requires knowing exactly what software/library versions were used.
1. **Python:** Print your Python version and the versions of the libraries you used (e.g. `pandas`, `numpy`). Export them to a `requirements.txt` file (`pip freeze > requirements.txt`, or list them manually if using a notebook platform).
2. **R:** Run `sessionInfo()` and save the output to a text file. If you use packages, list them and their versions (`packageVersion("dplyr")`, etc.), or use `renv::snapshot()` if you have `renv` set up.

## Task 3 — Organizing a Reproducible Project Structure
Create a simple, clearly organized folder structure for your analysis, for example:
```
week03_yourname/
├── data/          # raw data file(s) (some samples)
├── scripts/       # your .py / .R script(s)
├── outputs/       # any generated results (plots, CSVs)
└── README.md      # short description of what the project does and how to run it
```
Write a short `README.md` (a few sentences) explaining: what dataset is used, what the script does, and the exact command/steps needed to reproduce your results from scratch.

## Task 4 — A Reproducible Cleaning + Analysis Script
Take the data cleaning + pipeline steps from Week 2 (or write new simple ones: load → clean missing values → compute a summary statistic) and turn them into a **single script** that can be run top-to-bottom without manual intervention.
1. The script should not depend on any interactive/manual step (e.g. no manually editing values outside the code).
2. Add comments at the top of the script stating: the input file expected, and the output produced.
3. Re-run the script from a clean environment (e.g. restart your kernel/R session) and confirm you get the same output.

## Task 5 — Documenting Assumptions and Limitations
At the end of your script (or in your README), write a short paragraph (4-6 sentences) documenting:
1. Any assumptions you made about the data (e.g. how missing values were handled, what a certain column means).
2. Any known limitations of your analysis (e.g. small sample size, data only covers a certain time period).
3. What someone would need to change if they wanted to re-run your analysis on a different dataset.

---

## Notes
- Refer back to the [course Readme](../Readme.md) for IDE/platform setup (Kaggle/Colab for Python, Posit Cloud/RStudio for R).
- The goal this week is **not** new analysis techniques — it's making sure your existing work can be trusted and repeated by someone else.
- A good rule of thumb: if you deleted all your outputs and only kept your script + data, could you regenerate everything exactly? If yes, you've succeeded this week.
