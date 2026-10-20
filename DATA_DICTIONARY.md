# Derived data dictionary - v1.1

Original variables and their roles are documented in A1 and B1 of the notebook. Original columns remain in their original order at the start of each CSV.

## Netflix

| Added column | Meaning | Missing / inapplicable |
|---|---|---|
| duration_recovered | True for the three runtimes recovered from rating | No missing |
| director_missing, cast_missing, country_missing, rating_missing, date_added_missing | True when cleaned source metadata is unavailable | No missing |
| year_added, month_added | Year and month extracted from date_added | Missing when addition date is missing |
| release_decade | Floor of release_year / 10, multiplied by 10 | No missing |
| movie_minutes | Numeric movie runtime in minutes | Missing for TV shows |
| tv_seasons | Numeric season count listed for a TV show | Missing for movies |
| country_count, genre_count, cast_count | Number of nonempty unique tokens in the relevant normalized field | Missing when the source field is missing; not zero |
| release_to_add_years | year_added minus release_year, signed calendar-year difference | Missing for unknown date_added |
| release_after_addition | True for a negative signed year difference | False for an unknown addition date; use date_added_missing to distinguish |
| catalogue_lag_years | Nonnegative signed gap only | Missing for negative gap or unknown date_added |

## Supermarket

| Added column | Meaning | Missing / inapplicable |
|---|---|---|
| transaction_datetime | Transaction Date combined with Time | No missing |
| hour | Hour of transaction, 24-hour clock | No missing; observed 10-20 |
| weekday | English weekday name | No missing |
| weekday_number | Monday=0 through Sunday=6 | No missing |
| month | Actual year-month, YYYY-MM | No missing |
| total_iqr_outlier | Outside Total's Q1-1.5IQR to Q3+1.5IQR interval | No missing; nine True values retained |

Temporal features overlap their source date/time fields; use deliberate feature selection. Customer rating is the original `Customer stratification rating` field, with observed range 4-10. The one-to-one Branch/City relationship and deterministic accounting columns are documented in README.md.
