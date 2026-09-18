Netflix Shows — Data Wrangling

Cleaning and preparing the Netflix Shows dataset (Kaggle, ~8,800 titles) for analysis, using a full six-stage data wrangling process: Discovery, Structuring, Cleaning, Transformation, Validation, and Publishing.

Overview

Real-world datasets are messy , missing values, inconsistent formats, and logical errors that aren't obvious at a glance. This project takes the raw Netflix titles dataset and turns it into a clean, analysis-ready CSV, while documenting every decision made along the way.

Tools: Python, pandas, Kaggle Notebooks
Dataset:[Netflix Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows) (`netflix_titles.csv`) by shivamb, via Kaggle

Process

Discovery — Loaded the raw dataset and inspected its shape, column types, and missing values with `df.info()`, `df.isnull().sum()`, and `df.duplicated().sum()`.

Structuring — Standardized column names (lowercase, underscores), converted `date_added` from text to a proper datetime column, and split `duration` into a numeric value plus a unit column (`min` or `Season(s)`).

Cleaning
- Removed exact duplicate rows and dropped the free-text `description` column (out of scope for this assignment)
- Filled missing `director` values using a director/cast pairing lookup (pairs repeating 3+ times), labeling any remaining gaps `"Not Given"`
- Filled missing `country` values using a director-to-country lookup built from known rows
- Labeled remaining missing `cast` values `"Not Given"`
- Dropped the small number of rows still missing `date_added`, `rating`, or `duration`
- Identified and removed 14 rows where `date_added` predated `release_year` — a logical inconsistency
- Checked for any titles added before 1997 (Netflix's founding year) — found none
- Sanity-checked `type` and `rating` categories for stray values

Transformation— Split the `listed_in` genre column (up to 3 comma-separated genres per title) into separate `listed_in_1`, `listed_in_2`, `listed_in_3` columns.

Validation — Verified `date_added` was a proper datetime type and `duration_value` was numeric, confirmed zero missing values remained in `director` and `country`, reset the DataFrame index, and spot-checked a random sample of rows.

Publishing — Exported the cleaned dataset to `cleaned_netflix.csv` and reloaded it to confirm the export succeeded.

Results

Filled 18 missing director values directly from repeated director/cast pairings before falling back to `"Not Given"` for the rest
Removed 14 rows where a title's `date_added` predated its own `release_year`, since there was no reliable way to correct the date
Confirmed no rows had a `date_added` before 1997, validating overall date consistency
Final dataset: **zero missing values** in `director`, `cast`, and `country`; correctly typed date and duration fields; genre data split into individual, analyzable columns

 What I would do differently

With more time, the date-inconsistency handling and director-to-country inference could both be refined further — noted in more detail in the notebook's reflection section.

Links

[Full notebook (Kaggle)](https://www.kaggle.com/code/dianahcheloti/notebook87d6905535)
Cleaned dataset: `cleaned_netflix.csv` (in this repo)
