# Exploratory Data Analysis (EDA) Notes

Beginner-friendly notes on inspecting, cleaning, summarizing, and understanding data before deeper analysis or machine learning.

## 1. What is EDA?

**Exploratory Data Analysis (EDA)** is the process of examining and summarizing a dataset using statistics and visualizations to understand its structure, quality, patterns, relationships, and unusual values.

EDA helps answer:
- What does the dataset contain?
- How many rows and columns are present?
- Which columns are numerical or categorical?
- Are there missing or duplicate values?
- How are variables distributed?
- Are there unusual values or relationships?

EDA is more than plotting charts: it includes understanding the problem, checking data quality, asking questions, and documenting findings.

## 2. Typical EDA workflow
1. Understand the problem and dataset.
2. Load the data.
3. Inspect rows, columns, shape, and data types.
4. Check missing values and duplicates.
5. Validate values and correct data types.
6. Analyze numerical and categorical columns.
7. Investigate distributions and potential outliers.
8. Explore relationships between variables.
9. Summarize findings and limitations.
10. Prepare data for the next stage.

The process is iterative; findings may send you back to earlier steps.

## 3. Load data

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("data.csv")
# Other formats:
df = pd.read_excel("data.xlsx")
df = pd.read_json("data.json")
```

## 4. Understand the dataset

```python
df.head()              # First 5 rows
df.head(10)            # First 10 rows
df.tail()              # Last 5 rows
df.shape               # (rows, columns)
df.columns             # Column names
df.info()              # Data types and non-null counts
df.describe()          # Numeric summary
df.describe(include="all")  # Summary of all column types
df.dtypes              # Data types
df.nunique()           # Unique-value count per column
df["city"].unique()    # Unique values in one column
df["city"].value_counts()  # Category frequencies
```

Include missing values in frequency counts with `df["city"].value_counts(dropna=False)`.

## 5. Types of columns
- **Numerical:** age, salary, quantity, price.
- **Categorical:** department, city, product type.
- **Boolean:** True/False.
- **Datetime:** dates and timestamps.
- **Text:** comments and descriptions.

Convert types when appropriate:

```python
df["age"] = pd.to_numeric(df["age"], errors="coerce")
df["date"] = pd.to_datetime(df["date"], errors="coerce")
df["category"] = df["category"].astype("category")
```

`errors="coerce"` turns invalid values into missing values, so inspect how many values were affected.

## 6. Missing values

Missing values may arise because information was not collected, was unavailable, or was lost during processing.

```python
df.isnull()
df.isnull().sum()
missing_percent = (df.isnull().mean() * 100).round(2)
```

Remove missing values:

```python
df.dropna()                    # Drop rows with any missing value
df.dropna(subset=["age"])      # Drop rows missing age
df.dropna(axis=1)              # Drop columns with missing values
```

Fill values:

```python
df["age"] = df["age"].fillna(df["age"].median())
df["city"] = df["city"].fillna(df["city"].mode()[0])
```

Possible strategies:
- Numeric: mean or median, depending on distribution and outliers.
- Categorical: mode or a meaningful category such as `"Unknown"`.
- Time series: forward/backward fill when justified.
- Drop rows or columns when appropriate.

Do not fill automatically. Understand why data is missing and whether the strategy could introduce bias.

## 7. Duplicate records

```python
df.duplicated().sum()          # Count duplicate rows
df[df.duplicated()]            # Display duplicate rows
df = df.drop_duplicates()      # Remove exact duplicate rows
```

Based on selected columns:

```python
df.duplicated(subset=["customer_id"]).sum()
df = df.drop_duplicates(subset=["customer_id"], keep="first")
```

Only remove records after deciding what defines a duplicate. Repeated transactions may be valid.

## 8. Descriptive statistics

```python
df["salary"].mean()
df["salary"].median()
df["salary"].mode()
df["salary"].min()
df["salary"].max()
df["salary"].std()
df["salary"].var()
df["salary"].quantile(0.25)
df["salary"].quantile(0.75)
```

- **Mean:** arithmetic average.
- **Median:** middle value after sorting.
- **Mode:** most frequent value.
- **Range:** maximum minus minimum.
- **Variance:** average squared deviation from the mean, using population or sample convention.
- **Standard deviation:** square root of variance; spread in original units.
- **Quartiles:** divide ordered data into four parts.
- **IQR:** Q3 − Q1.

Median is less sensitive to extreme values than mean.

## 9. Univariate analysis

**Definition:** Analysis of one variable at a time.

Numerical variable:

```python
df["age"].describe()
sns.histplot(data=df, x="age", kde=True)
plt.show()

sns.boxplot(data=df, x="age")
plt.show()
```

Categorical variable:

```python
df["department"].value_counts()
sns.countplot(data=df, x="department")
plt.xticks(rotation=45)
plt.show()
```

Ask: What is typical? How spread out are values? Is the distribution skewed? Which categories are common?

## 10. Bivariate analysis

**Definition:** Analysis of the relationship between two variables.

Numerical vs numerical:

```python
sns.scatterplot(data=df, x="experience", y="salary")
plt.show()

df[["experience", "salary"]].corr()
```

Categorical vs numerical:

```python
sns.boxplot(data=df, x="department", y="salary")
plt.xticks(rotation=45)
plt.show()

df.groupby("department")["salary"].mean()
```

Categorical vs categorical:

```python
pd.crosstab(df["department"], df["gender"])

sns.countplot(data=df, x="department", hue="gender")
plt.xticks(rotation=45)
plt.show()
```

## 11. Multivariate analysis

**Definition:** Examines three or more variables together.

Correlation heatmap:

```python
numeric = df.select_dtypes(include="number")
corr = numeric.corr()
sns.heatmap(corr, annot=True, cmap="coolwarm", fmt=".2f")
plt.show()
```

Pair plot:

```python
sns.pairplot(df.select_dtypes(include="number"))
plt.show()
```

Grouped analysis:

```python
df.groupby(["department", "gender"])["salary"].mean()
```

Correlation measures association, not causation. It can be affected by outliers, confounding variables, and non-linear relationships.

## 12. Outlier detection with IQR

An **outlier** is an observation unusually far from the rest. It may be an error, a rare valid event, or a meaningful signal.

Steps:
1. Q1 = 25th percentile.
2. Q3 = 75th percentile.
3. IQR = Q3 − Q1.
4. Lower fence = Q1 − 1.5 × IQR.
5. Upper fence = Q3 + 1.5 × IQR.

```python
Q1 = df["salary"].quantile(0.25)
Q3 = df["salary"].quantile(0.75)
IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[(df["salary"] < lower) | (df["salary"] > upper)]
```

Do not automatically delete outliers. Investigate whether they are valid and whether they matter for the analysis.

## 13. Data cleaning

Standardize text:

```python
df["city"] = df["city"].str.strip().str.lower()
```

Replace inconsistent values:

```python
df["gender"] = df["gender"].replace({"M": "Male", "F": "Female"})
```

Rename columns:

```python
df = df.rename(columns={"cust_name": "customer_name"})
df.columns = df.columns.str.strip().str.lower().str.replace(" ", "_")
```

Convert data types:

```python
df["price"] = pd.to_numeric(df["price"], errors="coerce")
df["order_date"] = pd.to_datetime(df["order_date"], errors="coerce")
```

Validate ranges and categories:

```python
df[df["age"] < 0]
df[df["quantity"] < 0]
df["status"].value_counts(dropna=False)
```

Cleaning rules should be based on the meaning of the data, not just on what looks unusual.

## 14. Basic feature creation

A **feature** is an input variable used in analysis or a machine-learning model.

```python
df["total_amount"] = df["quantity"] * df["unit_price"]

df["order_date"] = pd.to_datetime(df["order_date"])
df["order_year"] = df["order_date"].dt.year
df["order_month"] = df["order_date"].dt.month
```

Create categories:

```python
df["age_group"] = pd.cut(
    df["age"],
    bins=[0, 18, 35, 60, 100],
    labels=["Under 18", "18-35", "36-60", "Above 60"]
)
```

Avoid data leakage: a feature must not use information that would be unavailable at the time a prediction is made.

## 15. Reusable EDA checklist

```python
df = pd.read_csv("data.csv")

# Inspect
print(df.head())
print(df.shape)
print(df.info())
print(df.describe(include="all"))

# Missing values and duplicates
print(df.isnull().sum())
print(df.duplicated().sum())

# Column types
numeric_cols = df.select_dtypes(include="number").columns
categorical_cols = df.select_dtypes(include=["object", "category"]).columns

# Numerical distributions
for col in numeric_cols:
    df[col].hist()
    plt.title(col)
    plt.show()

# Category frequencies
for col in categorical_cols:
    print(df[col].value_counts(dropna=False).head(10))

# Correlation
if len(numeric_cols) > 1:
    sns.heatmap(df[numeric_cols].corr(), annot=True, cmap="coolwarm")
    plt.show()
```

This is a starting template, not a substitute for questions specific to the dataset.

## 16. Mini project: Retail EDA

Use a retail dataset with fields such as customer ID, order date, city, product, quantity, and price.

Investigate:
1. Number of records and columns.
2. Missing values and duplicates.
3. Most common product categories.
4. Average order value.
5. Cities with highest sales.
6. Sales trends over time.
7. Relationship between quantity and order value.
8. Unusual prices or quantities.
9. Three useful findings and two limitations.

Example:

```python
df["sales"] = df["quantity"] * df["price"]

sales_by_city = (
    df.groupby("city")["sales"]
      .sum()
      .sort_values(ascending=False)
)
print(sales_by_city)
```

## 17. Interview questions

**What is EDA?** Examining a dataset with summaries and visualizations to understand structure, quality, patterns, and relationships.

**Why is EDA important?** It reveals data-quality problems, distributions, and relationships, and guides analysis or modeling.

**Univariate vs bivariate vs multivariate?** One variable, two variables, and three or more variables respectively.

**How do you handle missing values?** First investigate their amount and cause; then choose an appropriate removal or imputation strategy based on context.

**What is an outlier?** An unusually distant observation that may be an error or a valid rare event.

**What is the IQR method?** Potential outliers are values below Q1 − 1.5×IQR or above Q3 + 1.5×IQR.

**`isnull()` vs `dropna()`?** `isnull()` identifies missing values; `dropna()` removes rows or columns containing them.

**`describe()` vs `info()`?** `describe()` gives summary statistics; `info()` gives structure, types, and non-null counts.

**Does correlation mean causation?** No. Correlation indicates association, not proof of cause and effect.

**What comes after EDA?** Document findings, address relevant quality issues, prepare suitable features, and continue to statistical analysis or modeling.

## 18. Practice questions
1. Load a CSV and report rows and columns.
2. Inspect the first 10 records and data types.
3. Find missing-value counts and percentages.
4. Find and investigate duplicates.
5. Separate numerical and categorical columns.
6. Calculate mean, median, and standard deviation.
7. Plot a histogram and box plot for one variable.
8. Find the five most common categories.
9. Create a correlation heatmap.
10. Detect potential outliers using IQR.
11. Group by a category and calculate sum, mean, and count.
12. Write five findings and explain limitations.

## 19. Quick reference

```python
df.head()
df.shape
df.columns
df.info()
df.describe(include="all")
df.dtypes
df.nunique()
df["col"].unique()
df["col"].value_counts(dropna=False)

df.isnull().sum()
df.isnull().mean() * 100
df.dropna()
df.fillna(value)
df.duplicated().sum()
df.drop_duplicates()

df["col"].mean()
df["col"].median()
df["col"].std()
df["col"].quantile(0.25)

df.groupby("category")["value"].mean()
pd.crosstab(df["category1"], df["category2"])
df.select_dtypes(include="number").corr()

pd.to_datetime(df["date"], errors="coerce")
pd.to_numeric(df["value"], errors="coerce")
```

---
**Learning tip:** Connect every statistic or chart to a question. A good EDA report explains what the data shows and what it cannot tell you.
