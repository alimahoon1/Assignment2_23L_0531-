# Assignment 2 cleaned datasets - 23L-0531

Version: **v1.1**. Prepared: **20 October 2026** (Asia/Karachi).

Repository: https://github.com/alimahoon1/Assignment2_23L_0531-

## Versioned files

| Dataset | File | Rows | Columns |
|---|---|---:|---:|
| Netflix | `23L_0531_A2_netflix_cleaned.csv` | 8,807 | 29 |
| Supermarket Sales | `23L_0531_A2_supermarket_cleaned.csv` | 1,000 | 23 |

Use the **v1.1 tag**, not a moving branch, for Assignment 3:

- Netflix: https://raw.githubusercontent.com/alimahoon1/Assignment2_23L_0531-/v1.1/23L_0531_A2_netflix_cleaned.csv
- Supermarket: https://raw.githubusercontent.com/alimahoon1/Assignment2_23L_0531-/v1.1/23L_0531_A2_supermarket_cleaned.csv
- Version: https://github.com/alimahoon1/Assignment2_23L_0531-/tree/v1.1

`SHA256SUMS.txt` identifies the exact published bytes. Do not overwrite v1.1; publish any subsequent changes under a new tag and explain them.

## Sources and rights

Netflix: Shivam Bansal, *Netflix Movies and TV Shows*, Kaggle:
https://www.kaggle.com/datasets/shivamb/netflix-shows . The download is version 5,
last updated 27 September 2021, with 8,807 rows and 12 original columns. Kaggle metadata
declares CC0: Public Domain. Catalogue addition dates end on 25 September 2021;
these are historical metadata, not present-day availability.

Supermarket Sales: the exact instructor-provided `supermarket_Sales.csv` for CS4048,
Assignment 2, with 1,000 rows and 17 original columns. The instructor's column names
are preserved, including `Customer stratification rating`. No replacement online
version was used. Original dataset ownership remains with its authors; this README
does not assign a new licence to the instructor's data.

## Netflix cleaning

- Retained all 8,807 rows and original 12 columns; no duplicates were found.
- Stripped outer whitespace and normalized comma-separated token spacing. Removed
  empty tokens from two country cells and duplicate tokens within a cell if present;
  did not invent countries or reclassify geographical names.
- Moved three minute-valued rating entries to the missing duration field in the same
  row (`s5542`: 74 min, `s5795`: 84 min, `s5814`: 66 min). Their ratings remain unknown.
- Preserved missing director, cast, country, rating and addition dates and added
  missingness flags. Seven ratings and 831 countries remain missing after cleaning.
- Parsed addition dates; derived year/month added, release decade, separate movie
  minutes and TV seasons, country/genre/cast counts and year-level release/addition gaps.
- Kept 14 negative signed gaps and flagged them. `catalogue_lag_years` excludes these
  cases and the 10 missing dates; `release_to_add_years` preserves signed values.
- Retained unusual runtimes and season counts. The 1.5-IQR rule is descriptive, not
  sufficient proof of an error. Missing counts remain missing rather than zero.

## Supermarket cleaning

- Retained all 1,000 rows and original 17 columns. No missing values, duplicate rows,
  duplicate invoices, category inconsistencies or failed accounting identities were found.
- Parsed Date, validated/canonicalized Time to HH:MM and derived transaction_datetime,
  hour, weekday, weekday_number and month (year-month).
- Retained all nine high-total IQR flags and saved `total_iqr_outlier` for auditability.
  Every flagged total still equals Unit price x Quantity x 1.05 within floating-point tolerance.
- Retained accounting columns for provenance: cost of goods sold = price x quantity;
  tax = 5% of that cost; Total = 105% of cost; Gross income = tax. Gross margin percentage
  is constant at approximately 4.761904762. Do not treat them all as independent features.
- Branch and City have a one-to-one mapping; do not interpret their effects independently.

## Loading and missing values

These are UTF-8 CSVs. Empty fields represent missing or inapplicable values, not zero.
Dates and datetimes use ISO strings; parse `date_added`, `Date` and `transaction_datetime`
explicitly when loading. Nullable integer columns may load as float when they contain
missing values. Boolean flags use True/False. Never pool movie minutes and TV seasons.

See `DATA_DICTIONARY.md` for derived-field definitions. Analysis, plots and the report
are in the submitted notebook/PDF; this public repository publishes the data handoff.
