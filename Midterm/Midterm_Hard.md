# DATA2010 — Midterm Exam (Hard Version)

**Coverage:** Weeks 1–5 (Introduction to Data Science Programming; The Data Science Lifecycle & Processing Pipelines; Reproducible Data Science; Data Visualization; Data Wrangling & Cleaning)

**Language:** All questions reference **R only**. No Python is required or expected anywhere on this exam.

**Format:** Multiple Choice (MCQ, one correct answer), Fill-in-the-Blank, and Multiple Answer (select **all** that apply).

**Total:** 100 points · 40 questions, 2.5 points each · Suggested time: 90 minutes

**Difficulty breakdown:**


| Difficulty | Points | % of Exam | Questions |
| ---------- | ------ | --------- | --------- |
| Easy       | 30     | 30%       | Q1–Q12    |
| Medium     | 40     | 40%       | Q13–Q28   |
| Hard       | 30     | 30%       | Q29–Q40   |


**Instructions:** For MCQ, circle/select one answer. For Multiple Answer, select every correct option — partial credit given for partially correct selections. For Fill-in-the-Blank, write the missing term/function/code exactly. Many questions require predicting the output or behavior of R code — read each snippet carefully.

---



## Easy (2.5 points each)



### Q1 — MCQ *(Week 1)*

**What is the result of** `sum(1:5) %% 4` **in R?**

- A) 3
- B) 0
- C) 1
- D) 4



### Q2 — Fill-in-the-Blank *(Week 1)*

The function `__________()` returns the number of elements in a vector (e.g. `length(c(1, 2, 3))` returns `3`).

### Q3 — MCQ *(Week 2)*

An analyst has just acquired a raw dataset and, before any cleaning, checks column types, counts missing values, and inspects summary statistics. Which lifecycle stage is this?

- A) Data Acquisition
- B) Data Understanding
- C) Data Cleaning
- D) Communication



### Q4 — Fill-in-the-Blank *(Week 3)*

The command `renv::__________()` restores a project's recorded package versions from a lockfile.

### Q5 — Multiple Answer *(Week 4)*

Which of the following are TRUE about `ggplot2` layers? (Select all that apply)

- A) Layers are added using `+`
- B) `geom_point()` requires both `x` and `y` mapped to variables to draw a scatter plot
- C) `labs()` must be called before any `geom_*()` call or the plot will fail
- D) Multiple geoms can be layered on the same plot (e.g. points plus a smoothed line)



### Q6 — MCQ *(Week 5)*

Which pair of `tidyr` functions are opposites of each other?

- A) `mutate()` / `filter()`
- B) `pivot_longer()` / `pivot_wider()`
- C) `select()` / `arrange()`
- D) `rename()` / `recode()`



### Q7 — MCQ *(Week 1)*

What does `class(1L)` return in R?

- A) `"numeric"`
- B) `"integer"`
- C) `"double"`
- D) `"character"`



### Q8 — Fill-in-the-Blank *(Week 1)*

The operator `__________` tests for exact equality between two values (e.g. `5 == 5` returns `TRUE`).

### Q9 — MCQ *(Week 2)*

A pipeline computes the total sales per category **before** removing duplicate transaction rows. What is the most likely consequence?

- A) No effect — aggregation automatically ignores duplicates
- B) The totals may be inflated, since duplicated rows get counted more than once
- C) R throws an error when summarizing data with duplicates
- D) The duplicate rows are automatically dropped during aggregation



### Q10 — Fill-in-the-Blank *(Week 3)*

To verify reproducibility after restarting your session, your script must run entirely from the `__________` data file(s) alone — never from values re-typed by hand.

### Q11 — Multiple Answer *(Week 4)*

Which of the following would make a chart more effective for comparing sales across 5 regions? (Select all that apply)

- A) Sorting bars by value rather than alphabetically
- B) Adding clear axis labels and a title
- C) Assigning each bar a new random color every time the script runs
- D) Using consistent, meaningful colors across related charts



### Q12 — MCQ *(Week 5)*

A `price` column was read in as character type (e.g. `"19.99"`) instead of numeric. Which function correctly converts it?

- A) `as.character(price)`
- B) `as.numeric(price)`
- C) `toString(price)`
- D) `factor(price)`

---



## Medium (2.5 points each)



### Q13 — MCQ *(Week 1)*

What is the output of `paste("Week", 1:3)` in R?

- A) `"Week1" "Week2" "Week3"`
- B) `"Week 1" "Week 2" "Week 3"`
- C) `"Week" "1" "2" "3"`
- D) An error — `paste()` cannot be vectorized over a numeric range



### Q14 — Fill-in-the-Blank *(Week 2)*

Summarizing raw survey responses by average rating per product, without first removing duplicate/test submissions, violates the principle of always `__________` data before aggregating it.

### Q15 — Multiple Answer *(Week 3)*

Which of the following steps would make an analysis **not** reproducible? (Select all that apply)

- A) Not setting a seed before a random sampling step
- B) Hardcoding a file path that only exists on your own computer
- C) Recording package versions in a `sessionInfo()` printout
- D) Manually deleting a few "bad" rows in a spreadsheet before loading the data into R, without documenting it



### Q16 — MCQ *(Week 4)*

You run `ggplot(df, aes(x = category, y = value)) + geom_col()`, where `value` is already a pre-computed, aggregated numeric column. What does this produce?

- A) A scatter plot
- B) A bar chart whose bar heights equal `value` directly, with no further aggregation
- C) A histogram with automatic binning
- D) A boxplot grouped by category



### Q17 — Fill-in-the-Blank *(Week 4)*

`geom_bar()` aggregates data by **counting** rows per category by default, whereas `geom___________()` plots a y-value you have already computed, without further aggregation.

### Q18 — MCQ *(Week 5)*

You run `inner_join(orders, region_lookup, by = "region")` and the result has **fewer** rows than `orders`. What does this most likely indicate?

- A) `region_lookup` has duplicate keys
- B) Some rows in `orders` have a `region` value with no match in `region_lookup`
- C) `inner_join()` always reduces row count, regardless of matches
- D) The join failed silently and returned an empty data frame



### Q19 — Multiple Answer *(Week 5)*

Which of the following correctly describe `left_join(a, b, by = "key")`? (Select all that apply)

- A) Every row of `a` is kept in the result, even if there is no match in `b`
- B) Rows in `b` with no match in `a` are kept, with `NA` for `a`'s columns
- C) If a key in `a` matches multiple rows in `b`, the result can have more rows than `a`
- D) Columns from `b` are added to the matching rows of `a`



### Q20 — Fill-in-the-Blank *(Week 1/3)*

Running the same script twice and getting different results from a `sample()` call with no fixed seed means the analysis is not `__________`.

### Q21 — MCQ *(Week 1)*

What is the class of the result of `5 / 2` in R?

- A) `"integer"`
- B) `"numeric"`
- C) `"character"`
- D) `"logical"`



### Q22 — Fill-in-the-Blank *(Week 2)*

A pipeline step that converts raw timestamps into separate year/month/day columns, performed before any visualization is created, belongs to the `__________` stage of the lifecycle.

### Q23 — Multiple Answer *(Week 3)*

Which of the following belong in a reproducible project's documentation? (Select all that apply)

- A) The exact R package versions used
- B) A note on what each raw data column means
- C) Unrelated personal notes copied in from a different course
- D) The steps needed to regenerate every output file from the raw data



### Q24 — MCQ *(Week 4)*

Which chart is most appropriate for showing how one company's monthly revenue changed over 2 years?

- A) A bar chart grouped by company
- B) A line chart with month on the x-axis
- C) A boxplot of revenue grouped by company
- D) A scatter plot of revenue vs. an unrelated numeric column



### Q25 — Fill-in-the-Blank *(Week 4)*

In `ggplot2`, mapping a third variable to point color in a scatter plot is done inside `__________()`, e.g. `aes(x = a, y = b, color = c)`.

### Q26 — MCQ *(Week 5)*

Which code correctly keeps only the rows where `category` is **not** missing?

- A) `filter(df, category == NA)`
- B) `filter(df, !is.na(category))`
- C) `filter(df, is.na(category))`
- D) `select(df, -category)`



### Q27 — Fill-in-the-Blank *(Week 5)*

Testing `x == NA` in R always returns `__________`, regardless of the value of `x` — you must use `is.na()` instead.

### Q28 — Multiple Answer *(Week 5)*

Which of these correctly identify/count duplicate rows in a data frame `df`? (Select all that apply)

- A) `sum(duplicated(df))`
- B) `nrow(df) - nrow(unique(df))`
- C) `sum(is.na(df))`
- D) `df %>% count(across(everything())) %>% filter(n > 1)`

---



## Hard (2.5 points each)



### Q29 — MCQ *(Week 5)*

A `region` column contains the values `"north"`, `"North"`, `" North"` (leading space), and `"N"` — all meaning the same region. Which single line of code standardizes **all** of these to `"north"`?

- A) `mutate(region = tolower(region))`
- B) `mutate(region = recode(trimws(tolower(region)), "n" = "north"))`
- C) `mutate(region = trimws(region))`
- D) `mutate(region = toupper(region))`



### Q30 — Multiple Answer *(Weeks 2/3)*

A teammate claims their pipeline is "fully reproducible." Which of the following observations would **disprove** that claim? (Select all that apply)

- A) Running the script twice on the same machine gives identical output both times
- B) The script contains a `sample()` call with no `set.seed()` anywhere before it
- C) The script's first line is `setwd("C:/Users/Alice/Desktop/project")`
- D) The script's README lists the exact package versions used



### Q31 — Fill-in-the-Blank *(Week 4)*

When a bar chart's y-axis does not start at 0, it can visually `__________` the true magnitude of the differences between bars — a well-known visualization pitfall.

### Q32 — MCQ *(Week 5)*

You run `df %>% group_by(region) %>% summarize(avg_sales = mean(sales))`, and `sales` contains some unhandled `NA` values. What happens to `avg_sales` for a region with at least one `NA`?

- A) It is computed automatically ignoring the `NA`
- B) It is `NA`, unless `na.rm = TRUE` is passed inside `mean()`
- C) That region's row is silently dropped from the output
- D) R throws an error and the script stops

### Q33 — Multiple Answer *(Weeks 4/5)*

A scatter plot of `price` vs. `sales` shows one point far from all the others. Which of the following are reasonable next steps before deciding how to handle it? (Select all that apply)

- A) Check whether it's a data entry error (e.g. an extra zero)
- B) Delete it immediately without checking, since outliers are always errors
- C) Check whether it represents a real, valid extreme case (e.g. a bulk order)
- D) Consider whether conclusions change if it's included vs. excluded



### Q34 — Fill-in-the-Blank *(Weeks 2/3)*

A pipeline is considered reproducible only if it produces the `__________` output every time it is re-run on the same, unmodified input data.

### Q35 — MCQ *(Week 5)*

A data frame `df` has columns `id, jan, feb, mar` (one row per `id`, one column per month). Which code correctly reshapes it into long format with columns `id, month, value`?

- A) `pivot_wider(df, names_from = month, values_from = value)`
- B) `pivot_longer(df, cols = c(jan, feb, mar), names_to = "month", values_to = "value")`
- C) `pivot_longer(df, cols = id, names_to = "month", values_to = "value")`
- D) `spread(df, month, value)`



### Q36 — Multiple Answer *(Week 3)*

Which of the following would most likely **break** the reproducibility of a previously-working script? (Select all that apply)

- A) Upgrading a key package to a new major version without re-testing the script
- B) Pinning package versions with `renv::snapshot()`
- C) Relying on today's date (`Sys.Date()`) inside a calculation without documenting it
- D) Running the exact same script on the exact same data on a different, identically-configured machine



### Q37 — Fill-in-the-Blank *(Week 4)*

Faceting a plot by a categorical variable with `facet_wrap(~region)` creates one `__________` per unique value of `region`, all sharing the same axis scales by default.

### Q38 — MCQ *(Weeks 2/5)*

A dataset has one row per transaction. To compute "total revenue per customer per month," which sequence of operations is correct?

- A) `pivot_wider()` → `filter()` → `arrange()`
- B) `mutate()` (extract month) → `group_by(customer, month)` → `summarize(total = sum(revenue))`
- C) `select()` → `rename()` → `pivot_longer()`
- D) `arrange()` → `distinct()` → `left_join()`



### Q39 — Multiple Answer *(Weeks 2/3)*

Which of the following are true about the relationship between the Data Science Lifecycle and reproducibility? (Select all that apply)

- A) Reproducibility practices (seeds, environment recording, documentation) should be applied throughout the lifecycle, not just at the end
- B) A pipeline can produce a final report without being reproducible
- C) Cleaning steps never need to be documented, since they're "obvious" from reading the code
- D) Visualization code should still be re-runnable from raw data to final chart without manual steps



### Q40 — Fill-in-the-Blank *(Week 5)*

After joining `orders` with `region_lookup` using `left_join()`, several rows show `NA` in the new `region_name` column. The most likely cause is that the `region` value in those rows has no matching `__________` in `region_lookup`.

---



## Answer Key *(Instructor Use Only)*


| Q   | Difficulty | Type            | Answer                                               | Notes                                                                                                                                              |
| --- | ---------- | --------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Easy       | MCQ             | **A**                                                | `1+2+3+4+5=15`; `15 %% 4 = 3`.                                                                                                                     |
| 2   | Easy       | Fill-in         | `length`                                             |                                                                                                                                                    |
| 3   | Easy       | MCQ             | **B**                                                | Inspecting types/missingness/summary stats is Data Understanding, before cleaning begins.                                                          |
| 4   | Easy       | Fill-in         | `restore` (`renv::restore()`)                        |                                                                                                                                                    |
| 5   | Easy       | Multiple Answer | **A, B, D**                                          | C is false — `labs()` has no required position relative to `geom_*()`.                                                                             |
| 6   | Easy       | MCQ             | **B**                                                | `pivot_longer()`/`pivot_wider()` are inverse reshaping operations.                                                                                 |
| 7   | Easy       | MCQ             | **B**                                                | The `L` suffix forces an integer literal in R.                                                                                                     |
| 8   | Easy       | Fill-in         | `==`                                                 |                                                                                                                                                    |
| 9   | Easy       | MCQ             | **B**                                                | Summing/averaging before dedup double-counts duplicated rows, inflating totals.                                                                    |
| 10  | Easy       | Fill-in         | **raw**                                              |                                                                                                                                                    |
| 11  | Easy       | Multiple Answer | **A, B, D**                                          | C is an anti-pattern — random colors break consistency and reproducibility of the figure.                                                          |
| 12  | Easy       | MCQ             | **B**                                                | `as.numeric()` converts a numeric-looking string to a true numeric type.                                                                           |
| 13  | Medium     | MCQ             | **B**                                                | `paste()` vectorizes and inserts a space separator by default.                                                                                     |
| 14  | Medium     | Fill-in         | **cleaning**                                         |                                                                                                                                                    |
| 15  | Medium     | Multiple Answer | **A, B, D**                                          | C is a good practice, not a problem — distractor.                                                                                                  |
| 16  | Medium     | MCQ             | **B**                                                | `geom_col()` uses the y-value as-is; it does not count/aggregate like `geom_bar()`.                                                                |
| 17  | Medium     | Fill-in         | `col`                                                |                                                                                                                                                    |
| 18  | Medium     | MCQ             | **B**                                                | `inner_join()` drops `orders` rows whose `region` has no match in the lookup table.                                                                |
| 19  | Medium     | Multiple Answer | **A, C, D**                                          | B is false — that describes `right_join()`/`full_join()` behavior, not `left_join()` (trap).                                                       |
| 20  | Medium     | Fill-in         | **reproducible**                                     |                                                                                                                                                    |
| 21  | Medium     | MCQ             | **B**                                                | R's `/` always returns a double/numeric, even for integer operands.                                                                                |
| 22  | Medium     | Fill-in         | **Cleaning** (accept "Data Preparation"/"Wrangling") |                                                                                                                                                    |
| 23  | Medium     | Multiple Answer | **A, B, D**                                          | C is irrelevant to reproducing *this* analysis — distractor.                                                                                       |
| 24  | Medium     | MCQ             | **B**                                                | A line chart over time is the standard choice for a trend in one series.                                                                           |
| 25  | Medium     | Fill-in         | `aes`                                                |                                                                                                                                                    |
| 26  | Medium     | MCQ             | **B**                                                | `!is.na(category)` correctly excludes missing values; `== NA` never works (trap in A).                                                             |
| 27  | Medium     | Fill-in         | `NA`                                                 |                                                                                                                                                    |
| 28  | Medium     | Multiple Answer | **A, B, D**                                          | C counts missing values, not duplicates — distractor.                                                                                              |
| 29  | Hard       | MCQ             | **B**                                                | Needs both `trimws()` (whitespace) and `tolower()`+`recode()` (case/abbreviation) to catch every variant; A/C/D each fix only part of the problem. |
| 30  | Hard       | Multiple Answer | **B, C**                                             | B breaks determinism; C breaks portability (hardcoded personal path). A and D are signs of good, not broken, reproducibility.                      |
| 31  | Hard       | Fill-in         | **exaggerate** (accept "distort"/"mislead")          |                                                                                                                                                    |
| 32  | Hard       | MCQ             | **B**                                                | `mean()` propagates `NA` unless `na.rm = TRUE` is set; it is not dropped or ignored automatically.                                                 |
| 33  | Hard       | Multiple Answer | **A, C, D**                                          | B is the trap — outliers must be investigated, not auto-deleted.                                                                                   |
| 34  | Hard       | Fill-in         | **identical** (accept "same")                        |                                                                                                                                                    |
| 35  | Hard       | MCQ             | **B**                                                | `pivot_longer()` on the month columns (`jan, feb, mar`) reshapes wide → long correctly.                                                            |
| 36  | Hard       | Multiple Answer | **A, C**                                             | B improves reproducibility (distractor); D alone, on a matching environment, does not break it.                                                    |
| 37  | Hard       | Fill-in         | **panel** (accept "subplot")                         |                                                                                                                                                    |
| 38  | Hard       | MCQ             | **B**                                                | Extract month, group by customer+month, then sum revenue — the correct wrangling → aggregation order.                                              |
| 39  | Hard       | Multiple Answer | **A, B, D**                                          | C is false — undocumented cleaning steps are a common, serious reproducibility gap (trap).                                                         |
| 40  | Hard       | Fill-in         | **key** (accept "code"/"value")                      |                                                                                                                                                    |


