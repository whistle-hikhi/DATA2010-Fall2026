# Week 04 — Data Visualization

## Overview
This week's lab introduces **data visualization**: using charts and plots to explore and communicate patterns in data. You'll practice building a few common chart types in both Python (`matplotlib`/`seaborn`) and R (`ggplot2` or base R graphics), and thinking about what makes a chart clear and honest.

You may reuse the dataset you chose in [Week 2](../Week_02/Week_02.md)/[Week 3](../Week_03/Week_03.md), or pick a new one — just keep it consistent across all 5 tasks below.

## Submission Instructions
- Submit **two files**: one in **Python** (`.py` or `.ipynb`) and one in **R** (`.R` or `.Rmd`).
- Both files must solve **all 5 tasks** below, using the same dataset, and must produce/save the actual chart images (not just display them).
- Name your files clearly, e.g. `week04_yourname.py` and `week04_yourname.R`.
- Submit both files (and the exported chart images) on Canvas under the Week 4 assignment.

---

## Task 1 — A Bar Chart
Pick one categorical column from your dataset. Create a bar chart showing the count (or an aggregate, like average) of a numeric column for each category. Label the x-axis, y-axis, and give the chart a title.

## Task 2 — A Histogram
Pick one numeric column from your dataset. Create a histogram showing its distribution. Try at least two different numbers of bins and comment on how the choice of bin count changes what the histogram shows.

## Task 3 — A Scatter Plot
Pick two numeric columns from your dataset. Create a scatter plot of one against the other. Add axis labels and a title, and briefly comment (1-2 sentences) on whether you observe any relationship between the two variables.

## Task 4 — A Line Chart or Boxplot
Choose whichever fits your dataset better:
- **Line chart** — if your data has a time/date column, plot a numeric value over time.
- **Boxplot** — if it doesn't, create a boxplot of a numeric column grouped by a categorical column, to compare distributions across groups.

## Task 5 — Putting It Together: A Small Dashboard
Combine at least 3 of the charts from Tasks 1-4 into a single figure with multiple subplots/panels (`matplotlib.pyplot.subplots` in Python, `patchwork`/`gridExtra`/`par(mfrow=...)` in R). Save the combined figure as one image file (e.g. `dashboard.png`).

---

## Notes
- Refer back to the [course Readme](../Readme.md) for IDE/platform setup (Kaggle/Colab for Python, Posit Cloud/RStudio for R).
- Every chart must have a title and labeled axes — an unlabeled chart is an incomplete chart.
- Keep your code well-commented — briefly explain what each chart is meant to show.
