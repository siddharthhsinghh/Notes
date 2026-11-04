# Matplotlib & Seaborn Notes

Beginner-friendly reference for Python data visualization.

## 1. What is data visualization?
Data visualization represents data with charts and plots so that trends, comparisons, distributions, relationships, and unusual values are easier to understand.

- **Matplotlib:** foundational Python plotting library with detailed customization.
- **Seaborn:** statistical visualization library built on Matplotlib; integrates well with Pandas.

Install and import:

```bash
pip install matplotlib seaborn pandas numpy
```

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np
```

## 2. Matplotlib basics

```python
months = ["Jan", "Feb", "Mar", "Apr"]
sales = [120, 150, 135, 180]

plt.plot(months, sales, marker="o", linestyle="--", label="Sales")
plt.title("Monthly Sales")
plt.xlabel("Month")
plt.ylabel("Sales")
plt.legend()
plt.grid(True)
plt.show()
```

Common options: `color`, `marker`, `linestyle`, `linewidth`, `label`, and `alpha` (transparency).

### Figure and Axes

- **Figure:** entire canvas.
- **Axes:** an individual plotting area inside the Figure.

```python
fig, ax = plt.subplots(figsize=(8, 4))
ax.plot(months, sales, marker="o")
ax.set_title("Monthly Sales")
ax.set_xlabel("Month")
ax.set_ylabel("Sales")
ax.grid(True)
plt.tight_layout()
plt.show()
```

The object-oriented approach is useful for customization and multiple charts.

## 3. Common Matplotlib charts

### Line chart
Shows trends across an ordered variable, often time.

```python
plt.plot(months, sales, marker="o")
plt.show()
```

Use for monthly sales, temperature, or stock-price trends.

### Bar chart
Compares values across categories.

```python
products = ["A", "B", "C"]
revenue = [500, 700, 450]
plt.bar(products, revenue)
plt.xlabel("Product")
plt.ylabel("Revenue")
plt.show()
```

Horizontal version: `plt.barh(products, revenue)`. Usually start a bar chart's value axis at zero to avoid exaggerating differences.

### Scatter plot
Shows the relationship between two numerical variables. Each point is an observation.

```python
hours = [1, 2, 3, 4, 5]
marks = [40, 45, 55, 60, 72]
plt.scatter(hours, marks)
plt.xlabel("Hours studied")
plt.ylabel("Marks")
plt.show()
```

A scatter plot can reveal association, clusters, and unusual points; it does not prove causation.

### Histogram
Shows the distribution of numerical data by grouping values into bins.

```python
ages = [21, 22, 22, 23, 24, 24, 25, 26, 28, 30]
plt.hist(ages, bins=5, edgecolor="black")
plt.xlabel("Age")
plt.ylabel("Frequency")
plt.show()
```

`bins` controls the number of intervals.

### Pie chart
Shows parts of a whole. Use only for a small number of meaningful categories.

```python
labels = ["Food", "Travel", "Rent"]
values = [30, 15, 55]
plt.pie(values, labels=labels, autopct="%1.1f%%")
plt.show()
```

A bar chart is often easier for comparing category sizes.

### Box plot
Summarizes a distribution using quartiles, median, whiskers, and potential outliers.

```python
marks = [45, 50, 55, 60, 62, 65, 70, 72, 95]
plt.boxplot(marks)
plt.ylabel("Marks")
plt.show()
```

- Q1: 25th percentile; Q3: 75th percentile.
- IQR = Q3 − Q1.
- Points beyond whiskers are potential outliers, not automatically errors.

## 4. Subplots

Create multiple plots in one Figure:

```python
fig, axes = plt.subplots(1, 2, figsize=(10, 4))

axes[0].plot(months, sales)
axes[0].set_title("Sales Trend")

axes[1].bar(months, sales)
axes[1].set_title("Sales by Month")

plt.tight_layout()
plt.show()
```

`plt.subplots(rows, columns)` creates the grid. `figsize` controls dimensions.

## 5. Seaborn basics

Seaborn works with Matplotlib and is convenient for DataFrames.

```python
sns.set_theme(style="whitegrid")

df = pd.DataFrame({
    "department": ["IT", "HR", "IT", "Sales", "HR"],
    "salary": [60000, 45000, 70000, 50000, 48000],
    "experience": [2, 3, 5, 2, 4]
})
```

Common themes include `"darkgrid"`, `"whitegrid"`, `"dark"`, `"white"`, and `"ticks"`.

### Histogram and KDE

```python
sns.histplot(data=df, x="salary", kde=True)
plt.show()
```

`kde=True` overlays a smoothed density estimate.

### Count plot
Counts observations in each category.

```python
sns.countplot(data=df, x="department")
plt.show()
```

### Bar plot
Displays an aggregate numerical statistic by category (mean by default).

```python
sns.barplot(data=df, x="department", y="salary", errorbar=None)
plt.show()
```

`countplot` is for counts; `barplot` is for a numerical summary. In older Seaborn versions, `ci=None` was used instead of `errorbar=None`.

### Box plot and violin plot

```python
sns.boxplot(data=df, x="department", y="salary")
sns.violinplot(data=df, x="department", y="salary")
plt.show()
```

A violin plot adds a density shape to show the distribution.

### Scatter plot

```python
sns.scatterplot(
    data=df, x="experience", y="salary", hue="department"
)
plt.show()
```

`hue` colors observations by group.

### Pair plot

```python
penguins = sns.load_dataset("penguins")
sns.pairplot(penguins, hue="species")
plt.show()
```

Creates pairwise plots for numeric columns. Loading the sample dataset may require internet access.

### Heatmap

```python
numeric = df.select_dtypes(include="number")
sns.heatmap(numeric.corr(), annot=True, cmap="coolwarm")
plt.show()
```

A heatmap uses colors to represent matrix values. Correlation shows association, not causation.

## 6. Plotting Pandas data

```python
df = pd.read_csv("data.csv")

print(df.head())
print(df.info())
print(df.describe())

sns.histplot(data=df, x="age", kde=True)
sns.boxplot(data=df, x="department", y="salary")
sns.scatterplot(data=df, x="experience", y="salary")
plt.show()
```

Check data types and missing values before plotting.

## 7. Save a chart

```python
plt.figure(figsize=(8, 5))
plt.plot(months, sales)
plt.title("Monthly Sales")
plt.savefig("monthly_sales.png", dpi=300, bbox_inches="tight")
plt.show()
```

Calling `savefig()` before `show()` is a reliable practice.

## 8. Choosing a chart

| Goal | Chart |
|---|---|
| Trend over time | Line |
| Compare categories | Bar |
| Distribution of numeric values | Histogram |
| Relationship between two numeric variables | Scatter |
| Compare distributions / potential outliers | Box plot |
| Category frequencies | Count plot |
| Correlation matrix | Heatmap |
| Part-to-whole with few categories | Pie |

## 9. Common mistakes
1. Using a histogram for categorical data.
2. Using a line chart for unrelated categories.
3. Forgetting titles and axis labels.
4. Using too many colors or too many pie slices.
5. Treating correlation as causation.
6. Ignoring missing values or incorrect data types.
7. Removing potential outliers without investigating them.

## 10. Interview questions

**What is Matplotlib?** A Python library for creating static, animated, and interactive visualizations.

**What is Seaborn?** A statistical visualization library built on Matplotlib, with high-level functions and Pandas integration.

**Bar chart vs histogram?** A bar chart compares categories; a histogram displays the distribution of numerical data grouped into bins.

**Count plot vs bar plot?** A count plot counts category observations; a bar plot summarizes a numerical variable for each category.

**What is a heatmap?** A color-coded representation of values in a matrix, often used for correlations.

**What is a subplot?** One plotting area among multiple Axes in a Figure.

**What does `hue` do?** It separates groups using different colors.

**Does correlation imply causation?** No. Correlation measures association, not cause and effect.

## 11. Practice questions
1. Plot monthly revenue for six months using a line chart.
2. Compare sales across five products with a bar chart.
3. Plot employee ages using a histogram and change the bin count.
4. Plot study hours against exam marks using a scatter plot.
5. Compare salary distributions by department with a box plot.
6. Count customers by membership type with `countplot`.
7. Compare average salary by department with `barplot`.
8. Create a correlation heatmap for numeric columns.
9. Create two subplots in one Figure.
10. Save a chart as a high-resolution PNG.

## 12. Quick reference

```python
plt.plot(x, y)                  # Line
plt.bar(x, y)                   # Vertical bar
plt.barh(x, y)                  # Horizontal bar
plt.scatter(x, y)               # Scatter
plt.hist(data, bins=10)         # Histogram
plt.boxplot(data)               # Box plot
plt.pie(values, labels=labels)  # Pie
plt.title("Title")
plt.xlabel("X")
plt.ylabel("Y")
plt.legend()
plt.grid(True)
plt.savefig("chart.png")
plt.show()

sns.histplot(data=df, x="col")
sns.countplot(data=df, x="category")
sns.barplot(data=df, x="category", y="value")
sns.boxplot(data=df, x="category", y="value")
sns.violinplot(data=df, x="category", y="value")
sns.scatterplot(data=df, x="x", y="y", hue="group")
sns.heatmap(df.corr(numeric_only=True), annot=True)
sns.pairplot(df)
```

---
**Learning tip:** Practice each chart on a small dataset, then apply it to a real dataset.
