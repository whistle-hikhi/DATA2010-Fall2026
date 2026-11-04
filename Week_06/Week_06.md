# Week 06 — Revision (Weeks 1–5)

## Overview
This week's lab revises everything from Weeks 1–5 in one project, using **R only**. You'll take a messy dataset from raw files to a clean table, charts, and a project that anyone can re-run.

The tasks follow the order of a real analysis rather than the order of the weeks, because you need clean data before you can chart it:

| Task | Topic | Revises |
| --- | --- | --- |
| 1 | R warm-up | [Week 1](../Week_01/Week_01.md) |
| 2 | Understanding the raw data | [Week 2](../Week_02/Week_02.md) |
| 3 | Cleaning and wrangling pipeline | [Week 2](../Week_02/Week_02.md), [Week 5](../Week_05/Week_05.md) |
| 4 | Charts and a dashboard | [Week 4](../Week_04/Week_04.md) |
| 5 | Making it reproducible | [Week 3](../Week_03/Week_03.md) |

## Dataset
Everyone uses the same three files in [`data/`](data/). The data is **synthetic**: it describes a made-up ride-hailing company in Vietnam from January to June 2026.

| File | Contents |
| --- | --- |
| [`rides_raw.csv`](data/rides_raw.csv) | One row per trip, with several data quality problems for you to find and fix |
| [`vehicle_types.csv`](data/vehicle_types.csv) | Lookup table of vehicle codes, names, and seats |
| [`monthly_targets.csv`](data/monthly_targets.csv) | Target number of trips per city and month, in wide format |

Never edit these files by hand. Every fix must happen in your code.

## Submission Instructions
- This lab is **R only**. Do not submit any Python.
- Write one `.R` script (not `.Rmd`) that solves **all 5 tasks**, run from your project's root folder.
- You may use base R, `dplyr`, `tidyr`, `readr`, `ggplot2`, and `patchwork`.
- Set up this project folder before you start, and copy the three data files into `data/`:
```
week06_yourname/
├── data/          # the 3 provided CSV files, unchanged
├── scripts/       # week06_yourname.R
├── outputs/       # everything your script generates
└── README.md      # see Task 5
```
- Zip the whole folder as `week06_yourname.zip` and submit it on Canvas under the Week 6 assignment.

---

## Task 1 — R Warm-up
1. Print a greeting that includes your name.
2. A rider has `budget = 500000` VND and each trip costs `trip_cost = 45000` VND. Compute and print how many full trips they can afford and how much money is left over.
3. Create the vector `fares = c(45000, 82000, 120000, 38000, 250000, 67000)`. Print its sum, mean, maximum, and minimum.
4. Load `data/rides_raw.csv` into a data frame. Print the first 5 rows and the number of rows and columns.
5. Keep only the rows with `rating` of 4.5 or above, then print how many there are. Add a comment on whether you trust this count yet, and why.

## Task 2 — Understanding the Raw Data
Explore the data before changing anything:
1. Print the column names and their data types. Comment on which columns have the wrong type and which names are messy.
2. Print summary statistics, and print the number of missing values in each column.
3. Use `table()` or `unique()` to list the values in the city, vehicle type, and payment method columns.
4. Print how many rows are exact duplicates, and how many impossible values you can find (for example, in the summary's minimum and maximum values).

## Task 3 — Cleaning and Wrangling Pipeline
Build a pipeline from raw data to one clean table named `rides`, working in the order below so that your results match the checkpoints.

1. **Rename** the columns, in order, to: `trip_id`, `pickup_date`, `city`, `vehicle_code`, `distance_km`, `fare_vnd`, `rating`, `payment_method`.
2. **Re-type** `pickup_date` as a Date and `fare_vnd`, `distance_km`, and `rating` as numeric. Check the date format in the file first.
3. **Remove duplicates**: drop exact duplicate rows and print how many were removed.
4. **Fix messy text**, printing `table()` before and after for `city`:
   - `city` must contain only `"Hanoi"`, `"Ho Chi Minh City"`, and `"Da Nang"`.
   - `vehicle_code` must be upper case with no extra spaces.
   - `payment_method` must be lower case with no extra spaces.
5. **Remove invalid trips**: drop rows where `distance_km` is missing, not above 0, or above 100, and rows where `fare_vnd` is missing or not above 0.
6. **Handle ratings**: treat any rating outside 1–5 as missing, then fill all missing ratings with the median of the remaining ratings. In a comment, explain one risk of filling values this way.
7. **Create columns**: `month` (text such as `"2026-01"`, from `format()`) and `fare_per_km`.
8. **Join**: `left_join()` the `vehicle_types.csv` lookup table on `vehicle_code`. Print how many rows have a missing `vehicle_name`, and explain why they exist. Keep these rows.
9. **Summarize**: print the top 5 `city` and `vehicle_code` combinations by total fare revenue.
10. **Reshape and compare to targets**:
    - Use `pivot_longer()` to make `monthly_targets.csv` long, with the columns `city`, `month`, and `target_trips`.
    - Count the actual trips per `city` and `month` in `rides`, then join them to the long targets on both columns.
    - Use `pivot_wider()` to make a table of actual trips with one row per city and one column per month.
    - Print the shape at each stage. Print each city's six-month actual and target totals, then comment on which cities met their target.

Save `rides` as `outputs/rides_clean.csv`.

## Task 4 — Charts and a Dashboard
Use `rides` for every chart. Save each chart to `outputs/` with `ggsave()`.
1. **Bar chart:** average fare by vehicle code.
2. **Histogram:** `distance_km`, drawn with two different numbers of bins. Comment on what the bin count changes.
3. **Scatter plot:** `fare_vnd` against `distance_km`, colored by `vehicle_code`. Comment in 1–2 sentences on the relationship you see, including any differences between vehicle types.
4. **Line chart:** actual trips per month, with one line per city.
5. **Dashboard:** combine at least 3 of these charts into one figure with `patchwork`, and save it as `outputs/dashboard.png`.

## Task 5 — Making It Reproducible
1. **Random seed:** use `set.seed()` and `slice_sample()` to draw 20 random rows from `rides`. Do it twice with the same seed, print the result of `identical()` to confirm that the two samples match, and save one as `outputs/audit_sample.csv`.
2. **Environment:** save the output of `sessionInfo()` to `outputs/session_info.txt`.
3. **Script header:** add comments at the top of your script stating the input files, the outputs produced, and the command to run it.
4. **README:** in `README.md`, state what the dataset is, what the script does, and the exact command to reproduce your results. Also write 4–6 sentences on your assumptions, the limitations of the analysis, and what someone would change to re-run it on another dataset.
5. **Clean re-run:** delete everything in `outputs/`, then run this command from the project root:
   ```
   Rscript --vanilla scripts/week06_yourname.R
   ```
   Confirm that every output comes back, and say so in your README. Your script must not use `setwd()`, absolute file paths, or `install.packages()`.

---

## Checkpoints
Use these values to check your work. If one doesn't match, go back and find out why rather than adjusting your code to force the number.

| Task | Check | Expected |
| --- | --- | --- |
| 1 | Raw data shape | 312 rows, 8 columns |
| 1 | Rows with `rating` of 4.5 or above | 135 |
| 3.3 | Duplicates removed | 12, leaving 300 rows |
| 3.4 | Trips per city before removing invalid trips | Da Nang 37, Hanoi 151, Ho Chi Minh City 112 |
| 3.5 | Rows after removing invalid trips | 282 |
| 3.6 | Ratings to fill, and the median used | 24 ratings, median 4.4 |
| 3.8 | Final `rides` shape | 282 rows, 12 columns |
| 3.8 | Rows with a missing `vehicle_name` | 11 |
| 3.8 | Mean `fare_vnd` | About 85,511 VND |
| 3.9 | Top combination by revenue | Hanoi, `CAR4`: 5,579,000 VND |
| 3.10 | Shapes: wide, then long, then wide | 3 × 7, then 18 × 3, then 3 × 7 |
| 3.10 | Six-month actual / target trips | Hanoi 137 / 128, Ho Chi Minh City 109 / 116, Da Nang 36 / 44 |

---

## Notes
- Refer back to the [course Readme](../Readme.md) for R setup (Posit Cloud/RStudio).
- Every chart must have a title and labeled axes.
- Keep your code well-commented — briefly explain each step and why it's needed.
- A good final check: `n_distinct(rides$trip_id)` should equal `nrow(rides)`.
