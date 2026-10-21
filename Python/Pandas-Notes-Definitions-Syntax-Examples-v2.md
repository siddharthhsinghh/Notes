# Pandas Notes: Definitions, Syntax, and Examples

Pandas is a Python library for working with structured data such as CSV files, Excel sheets, and database query results. Its two core data structures are **Series** (one-dimensional) and **DataFrame** (two-dimensional table).

## 1. Install and Import

```bash
pip install pandas
```

```python
import pandas as pd
```

## 2. Series and DataFrame

```python
scores = pd.Series([80, 90, 75])
data = {
    "Name": ["Asha", "Ravi", "Mina"],
    "Age": [21, 22, 20],
    "Score": [80, 90, 75]
}
df = pd.DataFrame(data)
print(df)
```

A **Series** is a labeled one-dimensional collection. A **DataFrame** is a table with rows and columns.

## 3. Read and Save Files

```python
df = pd.read_csv("students.csv")
df = pd.read_excel("students.xlsx")

df.to_csv("cleaned_students.csv", index=False)
df.to_excel("cleaned_students.xlsx", index=False)
```

For `.xlsx` support, you may need `pip install openpyxl`. `index=False` avoids writing the row index as an extra column.

## 4. Inspect Data

```python
df.head()       # first 5 rows
df.tail()       # last 5 rows
df.shape        # (rows, columns)
df.columns      # column names
df.dtypes       # column data types
df.info()       # non-null counts and memory info
df.describe()   # summary statistics for numeric columns
df.sample(3)    # 3 random rows
```

## 5. Select Columns and Rows

```python
df["Name"]                    # one column: Series
df[["Name", "Score"]]         # multiple columns: DataFrame
df.iloc[0]                    # first row by position
df.iloc[0:3, 0:2]             # first 3 rows, first 2 columns
df.loc[0, "Name"]             # row label 0, column "Name"
```

`.loc[]` selects by labels; `.iloc[]` selects by integer position. Index labels are not always the same as row positions.

## 6. Filter Rows

```python
high_scores = df[df["Score"] >= 80]
young_students = df[(df["Age"] < 22) & (df["Score"] >= 75)]
selected = df[df["Name"].isin(["Asha", "Mina"])]
```

Use `&` for AND and `|` for OR, and put each condition in parentheses.

## 7. Sort Data

```python
df.sort_values("Score")
df.sort_values("Score", ascending=False)
df.sort_values(["Age", "Score"], ascending=[True, False])
```

These return sorted DataFrames. Assign the result if you want to keep the sorting.

## 8. Add, Update, and Remove Columns

```python
df["Passed"] = df["Score"] >= 40
df["Score_plus_5"] = df["Score"] + 5
df["Score"] = df["Score"].fillna(0)
df = df.drop(columns=["Score_plus_5"])
```

Only fill missing scores with zero if zero is an appropriate interpretation for your data.

## 9. Missing Values

```python
df.isna()
df.isna().sum()                        # missing count per column
df.dropna()                            # drop rows with missing values
df.dropna(subset=["Score"])
df["Score"] = df["Score"].fillna(df["Score"].median())
```

Choose a missing-value strategy based on what the missing data means. Filling with a mean, median, zero, or label can affect analysis.

## 10. Duplicates and Text Cleaning

```python
df.duplicated()
df.drop_duplicates()
df["Name"] = df["Name"].str.strip()
df["Name"] = df["Name"].str.lower()
df = df.drop_duplicates(subset=["Name"], keep="first")
```

## 11. Change Data Types

```python
df["Age"] = pd.to_numeric(df["Age"], errors="coerce")
df["Date"] = pd.to_datetime(df["Date"], errors="coerce")
df["Name"] = df["Name"].astype("string")
```

`errors="coerce"` turns values that cannot be converted into missing values. Inspect those values afterward.

## 12. Grouping and Aggregation

```python
df.groupby("Department")["Salary"].mean()
df.groupby("Department")["Salary"].agg(["count", "mean", "max"])
df.groupby(["Department", "Role"])["Salary"].sum()
```

`groupby()` calculates summaries by category, such as average salary by department or total sales by region.

## 13. Unique Values and Counts

```python
df["Department"].value_counts()
df["Department"].unique()
df["Department"].nunique()
```

- `value_counts()` counts each value.
- `unique()` returns distinct values.
- `nunique()` counts distinct values.

## 14. Merge and Concatenate

```python
result = pd.merge(employees, departments, on="EmployeeID", how="inner")
```

Common `how` values are `"inner"`, `"left"`, `"right"`, and `"outer"`.

```python
combined_rows = pd.concat([df_january, df_february], ignore_index=True)
combined_columns = pd.concat([df_left, df_right], axis=1)
```

Use `merge()` to match rows using keys. Use `concat()` to stack or align objects along an axis. Check row counts after merging.

## 15. Apply Functions

```python
df["Name_Length"] = df["Name"].apply(len)
df["Score_Doubled"] = df["Score"].apply(lambda score: score * 2)
```

Prefer vectorized operations such as `df["Score"] * 2` when possible; they are often simpler and faster.

## 16. Dates and Times

```python
df["Date"] = pd.to_datetime(df["Date"])
df["Year"] = df["Date"].dt.year
df["Month"] = df["Date"].dt.month
df["DayName"] = df["Date"].dt.day_name()
```

The `.dt` accessor provides date/time properties for datetime-like columns.

## 17. Pivot Tables

```python
summary = pd.pivot_table(
    df,
    values="Sales",
    index="Region",
    columns="Product",
    aggfunc="sum",
    fill_value=0
)
```

Pivot tables summarize values across groups and help compare categories.

## 18. Rename Columns and Reset Index

```python
df = df.rename(columns={"old_name": "new_name"})
df = df.reset_index(drop=True)
```

`reset_index(drop=True)` creates a default integer index and discards the previous index.

## 19. Example Data-Cleaning Workflow

```python
import pandas as pd

df = pd.read_csv("sales.csv")
print(df.head())
print(df.info())
print(df.isna().sum())

df = df.drop_duplicates()
df["Date"] = pd.to_datetime(df["Date"], errors="coerce")
df["Sales"] = pd.to_numeric(df["Sales"], errors="coerce")

# Example only: choose an appropriate strategy for missing Sales.
df["Sales"] = df["Sales"].fillna(df["Sales"].median())

summary = df.groupby("Region", as_index=False)["Sales"].sum()
summary = summary.sort_values("Sales", ascending=False)
summary.to_csv("sales_by_region.csv", index=False)
```

This is a learning example, not a universal cleaning recipe. Inspect the data and decide whether dropping, filling, or correcting values is appropriate.

## 20. NumPy vs. Pandas

- **NumPy:** numerical arrays, vectorized math, matrix operations, and numerical computing.
- **Pandas:** labeled tables, CSV/Excel files, missing values, filtering, grouping, merging, and data cleaning.

Pandas uses NumPy for many numerical operations.

## 21. Common Mistakes

- Assuming `.loc` always selects by position; it uses labels.
- Forgetting parentheses around multiple filter conditions.
- Filling missing data with zero without checking whether it makes sense.
- Using `apply()` where a vectorized expression is simpler.
- Merging on the wrong key or producing unexpected duplicate rows.
- Forgetting `index=False` when exporting a clean table.

## 22. Practice Questions

1. Load a CSV and inspect its rows, columns, and data types.
2. Filter rows where a numeric column exceeds a threshold.
3. Count and handle missing values.
4. Remove duplicate records.
5. Convert a date column and extract month and year.
6. Calculate total and average sales by region.
7. Merge customer and order tables using customer ID.
8. Create a pivot table of sales by region and product.
9. Find the top five rows by a chosen metric.
10. Export a cleaned DataFrame to CSV and Excel.

## Quick Reference

| Task | Syntax |
|---|---|
| Read CSV | `pd.read_csv("file.csv")` |
| Preview | `df.head()` |
| Shape | `df.shape` |
| Select column | `df["column"]` |
| Filter | `df[df["column"] > value]` |
| Sort | `df.sort_values("column")` |
| Missing values | `df.isna().sum()` |
| Remove duplicates | `df.drop_duplicates()` |
| Group summary | `df.groupby("group")["value"].sum()` |
| Merge | `pd.merge(left, right, on="key", how="left")` |
| Convert to date | `pd.to_datetime(df["date"])` |
| Save CSV | `df.to_csv("output.csv", index=False)` |
