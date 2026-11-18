# DATA2010 — Mock Midterm Exam

**Coverage:** Weeks 1–5 (Introduction to Data Science Programming; The Data Science Lifecycle & Processing Pipelines; Reproducible Data Science; Data Visualization; Data Wrangling & Cleaning)

**Language:** All questions reference **R only**. No Python is required or expected anywhere on this exam.

**Format:** Multiple Choice (MCQ, one correct answer), Fill-in-the-Blank, and Multiple Answer (select **all** that apply).

**Total:** 100 points · 40 questions, 2.5 points each · Suggested time: 90 minutes

**Difficulty breakdown:**

| Difficulty | Points | % of Exam | Questions |
| --- | --- | --- | --- |
| Easy | 30 | 30% | Q1–Q12 |
| Medium | 40 | 40% | Q13–Q28 |
| Hard | 30 | 30% | Q29–Q40 |

**Instructions:** For MCQ, circle/select one answer. For Multiple Answer, select every correct option — partial credit given for partially correct selections. For Fill-in-the-Blank, write the missing term/function/code exactly.

---

## Easy (2.5 points each)

### Q1 — MCQ *(Week 1)*
Which of the following correctly creates a vector in R?
- A) `vector = [1, 2, 3]`
- B) `v <- c(1, 2, 3)`
- C) `v := (1, 2, 3)`
- D) `v = {1, 2, 3}`

### Q2 — Fill-in-the-Blank *(Week 1)*
The function `__________` is used in R to read a CSV file into a data frame.

### Q3 — MCQ *(Week 2)*
Which stage of the Data Science Lifecycle involves identifying missing values, duplicates, and inconsistent formats?
- A) Data Acquisition
- B) Data Understanding
- C) Data Cleaning
- D) Communication

### Q4 — Fill-in-the-Blank *(Week 3)*
The R function `__________` fixes the starting point of R's random number generator so results are identical across runs.

### Q5 — Multiple Answer *(Week 4)*
Which of the following are valid `ggplot2` geoms? (Select all that apply)
- A) `geom_bar()`
- B) `geom_histogram()`
- C) `geom_point()`
- D) `geom_sum()`

### Q6 — MCQ *(Week 5)*
Which `tidyr` function converts data from **wide** format to **long** format?
- A) `pivot_wider()`
- B) `pivot_longer()`
- C) `nest()`
- D) `unite()`

### Q7 — MCQ *(Week 1)*
Which operator is a valid alternative to `<-` for assigning a value to a variable in R?
- A) `->`
- B) `==`
- C) `!=`
- D) `%%`

### Q8 — Fill-in-the-Blank *(Week 1)*
In R, `%%` is the `__________` operator — it returns the remainder of a division.

### Q9 — MCQ *(Week 2)*
Which of the following best describes the "Communication" stage of the Data Science Lifecycle?
- A) Collecting raw data from a source
- B) Presenting results/insights to an audience via reports or visualizations
- C) Writing code to remove duplicate rows
- D) Computing summary statistics on a numeric column

### Q10 — Fill-in-the-Blank *(Week 3)*
A tool like R's `renv` is an example of a `__________` manager — it records exact package versions so an environment can be recreated later.

### Q11 — Multiple Answer *(Week 4)*
Which of the following chart types are appropriate for visualizing the **distribution of a single numeric column**? (Select all that apply)
- A) Histogram
- B) Boxplot
- C) Bar chart of category counts
- D) Scatter plot of two numeric variables

### Q12 — MCQ *(Week 5)*
Which base R function removes duplicate rows from a data frame `df`?
- A) `unique(df)`
- B) `sort(df)`
- C) `order(df)`
- D) `table(df)`

---

## Medium (2.5 points each)

### Q13 — MCQ *(Week 1)*
What is the output of `mean(c(4, 8, 15, 16, 23, 42))`?
- A) 18
- B) 16
- C) 23
- D) 108

### Q14 — Fill-in-the-Blank *(Week 2)*
Fill in the missing stage of the pipeline: Data Acquisition → `__________` → Data Cleaning → Analysis → Communication.

### Q15 — Multiple Answer *(Week 3)*
Which of the following are good reproducibility practices? (Select all that apply)
- A) Relying on randomness without setting a seed
- B) Recording package/library versions used
- C) Manually editing data values outside of your script during analysis
- D) Documenting the exact steps needed to re-run your analysis

### Q16 — MCQ *(Week 4)*
In `ggplot2`, which function is used to add axis labels and a title to a plot?
- A) `theme()`
- B) `labs()`
- C) `aes()`
- D) `scale()`

### Q17 — Fill-in-the-Blank *(Week 4)*
To combine multiple `ggplot2` charts into a single multi-panel figure, you can use the R package `__________`.

### Q18 — MCQ *(Week 5)*
Which `dplyr` function would you use to combine two data frames based on a shared key column?
- A) `mutate()`
- B) `filter()`
- C) `left_join()`
- D) `arrange()`

### Q19 — Multiple Answer *(Week 5)*
Which of the following are examples of "messy" data issues that typically need to be cleaned before analysis? (Select all that apply)
- A) Inconsistent category labels (e.g. `"Male"`, `"male"`, `"M"`)
- B) Column names with trailing whitespace
- C) A numeric column stored as a 64-bit integer
- D) Outlier values far outside a reasonable range

### Q20 — Fill-in-the-Blank *(Week 1/3)*
The command `__________` prints the R version and all loaded package versions, which is useful for recording your environment.

### Q21 — MCQ *(Week 1)*
What does `nchar("DataScience")` return in R?
- A) 10
- B) 11
- C) 12
- D) It throws an error

### Q22 — Fill-in-the-Blank *(Week 2)*
In a typical pipeline, you should always `__________` the data before you summarize or analyze it, to avoid misleading aggregates.

### Q23 — Multiple Answer *(Week 3)*
Which of the following would you include in a project's README to support reproducibility? (Select all that apply)
- A) What dataset is used
- B) The exact command/steps to re-run the analysis
- C) Your personal opinions about the dataset, unrelated to running the code
- D) Known assumptions/limitations of the analysis

### Q24 — MCQ *(Week 4)*
Which `ggplot2` component maps data columns to visual properties like x, y, or color?
- A) `geom_*()`
- B) `aes()`
- C) `theme()`
- D) `facet_wrap()`

### Q25 — Fill-in-the-Blank *(Week 4)*
The `ggplot2` function `__________()` splits a single plot into multiple small panels based on a categorical variable.

### Q26 — MCQ *(Week 5)*
Which `dplyr` verb would you use to keep only rows where `amount > 100`?
- A) `select()`
- B) `filter()`
- C) `arrange()`
- D) `rename()`

### Q27 — Fill-in-the-Blank *(Week 5)*
The `dplyr` verb `__________()` creates a new column or transforms an existing one.

### Q28 — Multiple Answer *(Week 5)*
Which of the following are valid `dplyr` join functions? (Select all that apply)
- A) `left_join()`
- B) `inner_join()`
- C) `full_join()`
- D) `cross_filter()`

---

## Hard (2.5 points each)

### Q29 — MCQ *(Week 5)*
A data frame has a column `order_date` stored as text in the format `"2024-01-15"`. Which function correctly converts it to a proper Date type?
- A) `format(order_date)`
- B) `as.Date(order_date, format = "%Y-%m-%d")`
- C) `as.numeric(order_date)`
- D) `Date(order_date)`

### Q30 — Multiple Answer *(Weeks 2/3)*
Which of the following, taken together, best describe a reproducible end-to-end pipeline? (Select all that apply)
- A) The script can be rerun top-to-bottom without manual intervention
- B) Any random processes use a fixed seed
- C) The analyst remembers the exact steps but doesn't write them down
- D) The project folder separates raw data, scripts, and outputs

### Q31 — Fill-in-the-Blank *(Week 4)*
To create a boxplot of a numeric column `y` grouped by a categorical column `x`, you would write: `ggplot(df, aes(x = x, y = y)) + __________()`.

### Q32 — MCQ *(Week 5)*
A `region` column contains `"north"`, `"North"`, and `"N"`, all meaning the same category. Which approach correctly standardizes these values using `dplyr`?
- A) `filter(region == "north")`
- B) `mutate(region = recode(tolower(region), "n" = "north"))`
- C) `arrange(region)`
- D) `select(region)`

### Q33 — Multiple Answer *(Weeks 4/5)*
Which of the following must be true before you can correctly produce a bar chart of "average sales by region" from a messy raw dataset? (Select all that apply)
- A) Missing values in the sales column have been handled
- B) The region column has been standardized to consistent category labels
- C) A random seed has been set using `set.seed()`
- D) The data has been grouped and aggregated by region

### Q34 — Fill-in-the-Blank *(Weeks 2/3)*
"If you deleted all your outputs and kept only your script and raw data, you should be able to `__________` your results exactly." (one word)

### Q35 — MCQ *(Week 5)*
You want to fill missing numeric values in a `price` column with the column's median instead of dropping the rows. Which code correctly does this in `dplyr`?
- A) `mutate(price = ifelse(is.na(price), median(price, na.rm = TRUE), price))`
- B) `filter(price != NA)`
- C) `mutate(price = mean(price))`
- D) `select(-price)`

### Q36 — Multiple Answer *(Weeks 4/5)*
Before producing a boxplot of `sales` grouped by `region`, which of the following should already be true of the data? (Select all that apply)
- A) `region` has standardized category labels (no duplicates like `"North"`/`"north"`)
- B) `sales` has been converted to the correct numeric type
- C) A `ggsave()` call has already been made
- D) Any clearly invalid outlier values have been reviewed/handled

### Q37 — Fill-in-the-Blank *(Week 3)*
To verify a script is truly reproducible, a common test is to restart your R session (clearing your environment) and run the script from a `__________` environment, confirming identical output.

### Q38 — MCQ *(Weeks 2/5)*
A dataset has one row per transaction (long format), but you need one row per customer with a separate column per month. Which operation do you need?
- A) `pivot_longer()`
- B) `pivot_wider()`
- C) `left_join()`
- D) `filter()`

### Q39 — Multiple Answer *(Weeks 2/3)*
Which of the following are true of a well-designed reproducible pipeline? (Select all that apply)
- A) It separates raw data from generated outputs
- B) It depends on files being manually edited mid-run for correct results
- C) It documents the exact dependencies/versions used
- D) It can be re-run from scratch to regenerate the same results

### Q40 — Fill-in-the-Blank *(Week 5)*
When joining `orders` with `region_lookup` and some `orders` rows have no matching region code, a `left_join()` will produce `__________` values in the new columns for those unmatched rows.

---

## Answer Key *(Instructor Use Only)*

| Q | Difficulty | Type | Answer | Notes |
| --- | --- | --- | --- | --- |
| 1 | Easy | MCQ | **B** | `<-` is R's assignment operator; `c()` constructs a vector. |
| 2 | Easy | Fill-in | **`read.csv`** (also accept `read_csv` from `readr`) | |
| 3 | Easy | MCQ | **C** | Data Cleaning is where messy/missing/duplicate issues get fixed. |
| 4 | Easy | Fill-in | **`set.seed()`** | |
| 5 | Easy | Multiple Answer | **A, B, C** | `geom_sum()` is not a real `ggplot2` function (distractor). |
| 6 | Easy | MCQ | **B** | `pivot_wider()` goes the opposite direction; `nest()`/`unite()` are unrelated. |
| 7 | Easy | MCQ | **A** | `->` is R's right-assign operator; the others are comparison/arithmetic operators. |
| 8 | Easy | Fill-in | **modulo** | |
| 9 | Easy | MCQ | **B** | Communication = presenting/reporting results, not collecting or cleaning data. |
| 10 | Easy | Fill-in | **dependency / environment / package** (accept any) | |
| 11 | Easy | Multiple Answer | **A, B** | A bar chart needs categories (not a single numeric distribution); a scatter plot needs two numeric variables. |
| 12 | Easy | MCQ | **A** | `unique(df)` returns the data frame with duplicate rows removed. |
| 13 | Medium | MCQ | **A** | Sum = 108, divided by 6 = 18. |
| 14 | Medium | Fill-in | **Data Understanding** | |
| 15 | Medium | Multiple Answer | **B, D** | A and C are anti-patterns (no seed; manual undocumented edits). |
| 16 | Medium | MCQ | **B** | `labs()` sets title/axis labels; `theme()` controls styling, `aes()` maps variables, `scale()` controls axis scaling. |
| 17 | Medium | Fill-in | **`patchwork`** (also accept `gridExtra`) | |
| 18 | Medium | MCQ | **C** | `left_join()` merges on a shared key; the others don't combine two tables. |
| 19 | Medium | Multiple Answer | **A, B, D** | A 64-bit integer column is not inherently messy (distractor C). |
| 20 | Medium | Fill-in | **`sessionInfo()`** | |
| 21 | Medium | MCQ | **B** | "DataScience" has 11 characters. |
| 22 | Medium | Fill-in | **clean** | |
| 23 | Medium | Multiple Answer | **A, B, D** | C is irrelevant/unneeded commentary for reproducing the analysis. |
| 24 | Medium | MCQ | **B** | `aes()` maps data columns to visual properties (x, y, color, etc.). |
| 25 | Medium | Fill-in | **`facet_wrap`** (also accept `facet_grid`) | |
| 26 | Medium | MCQ | **B** | `filter()` keeps rows matching a logical condition. |
| 27 | Medium | Fill-in | **`mutate`** | |
| 28 | Medium | Multiple Answer | **A, B, C** | `cross_filter()` is not a real `dplyr` function (distractor). |
| 29 | Hard | MCQ | **B** | `as.Date()` with a matching format string correctly parses the text date. |
| 30 | Hard | Multiple Answer | **A, B, D** | C describes an undocumented, non-reproducible process — incorrect. |
| 31 | Hard | Fill-in | **`geom_boxplot`** | |
| 32 | Hard | MCQ | **B** | Lowercasing then recoding standardizes all three variants to `"north"`. |
| 33 | Hard | Multiple Answer | **A, B, D** | C is a distractor: `set.seed()` is irrelevant to a deterministic aggregation with no randomness. |
| 34 | Hard | Fill-in | **reproduce** (also accept "regenerate") | |
| 35 | Hard | MCQ | **A** | Replaces only the missing values with the column's median, keeping the rest intact. |
| 36 | Hard | Multiple Answer | **A, B, D** | C is a distractor — saving the plot happens *after* creating it, not as a precondition. |
| 37 | Hard | Fill-in | **clean / fresh** (accept either) | |
| 38 | Hard | MCQ | **B** | `pivot_wider()` spreads one row-per-transaction into one row-per-customer with month columns. |
| 39 | Hard | Multiple Answer | **A, C, D** | B describes a non-reproducible manual intervention — incorrect. |
| 40 | Hard | Fill-in | **`NA`** (missing) | |
