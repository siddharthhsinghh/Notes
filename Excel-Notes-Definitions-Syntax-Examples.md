# Excel Notes – Definitions, Functions, Syntax & Examples

These notes are a beginner-friendly reference for learning Microsoft Excel. Each topic includes a simple definition, examples, and practical formulas.

---

## 1. What is Excel?

**Definition:** Microsoft Excel is a spreadsheet application used to store, organize, calculate, analyze, and visualize data.

Common uses:
- Data entry
- Calculations
- Data cleaning
- Data analysis
- Reporting
- Charts and dashboards
- Sorting and filtering

---

## 2. Workbook and Worksheet

**Workbook:** An Excel file that can contain one or more worksheets.

Example:
```text
Sales_Report.xlsx
```

**Worksheet:** A single spreadsheet inside a workbook.

```text
Workbook
├── Sheet1
├── Sheet2
└── Sheet3
```

---

## 3. Rows, Columns and Cells

**Row:** Runs horizontally and is identified by numbers such as 1, 2, 3.

**Column:** Runs vertically and is identified by letters such as A, B, C.

**Cell:** The intersection of a row and column.

Example:

```text
A1
```

means column A, row 1.

---

## 4. Cell Reference

A cell reference identifies the location of a cell.

Examples:

```text
A1
B5
C10
```

If A1 contains 100:

```excel
=A1
```

returns 100.

---

## 5. Range

A **range** is a group of cells.

```text
A1:A10
```

means A1 through A10.

```text
A1:C10
```

represents a rectangular range.

---

## 6. Data Types

Excel cells can contain:
- Text
- Numbers
- Dates
- Times
- TRUE/FALSE
- Formulas

Example:

```text
Name        Age       Date
Siddharth   25        04/09/2026
```

---

## 7. Formula

A **formula** is an expression used to perform a calculation.

Most formulas begin with `=`.

```excel
=A1+B1
```

If A1 is 10 and B1 is 20, the result is 30.

---

## 8. Arithmetic Operators

| Operator | Meaning | Example |
|---|---|---|
| `+` | Addition | `=A1+B1` |
| `-` | Subtraction | `=A1-B1` |
| `*` | Multiplication | `=A1*B1` |
| `/` | Division | `=A1/B1` |
| `^` | Exponent | `=A1^2` |
| `%` | Percentage | `=A1*10%` |

---

## 9. SUM

**Definition:** Adds numbers.

**Syntax:**
```excel
=SUM(range)
```

**Example:**
```excel
=SUM(A1:A10)
```

Adds all numeric values in A1:A10.

---

## 10. AVERAGE

**Definition:** Calculates the arithmetic mean.

```excel
=AVERAGE(B2:B10)
```

---

## 11. MIN and MAX

**MIN** returns the smallest numeric value.

```excel
=MIN(B2:B10)
```

**MAX** returns the largest numeric value.

```excel
=MAX(B2:B10)
```

---

## 12. COUNT, COUNTA and COUNTBLANK

**COUNT:** Counts cells containing numbers.

```excel
=COUNT(A1:A10)
```

**COUNTA:** Counts non-empty cells.

```excel
=COUNTA(A1:A10)
```

**COUNTBLANK:** Counts blank cells.

```excel
=COUNTBLANK(A1:A10)
```

---

## 13. IF

**Definition:** Checks a condition and returns one result if TRUE and another if FALSE.

**Syntax:**
```excel
=IF(condition, value_if_true, value_if_false)
```

**Example:**
```excel
=IF(B2>=50,"Pass","Fail")
```

---

## 14. AND, OR and NOT

**AND:** TRUE only when all conditions are TRUE.

```excel
=AND(B2>=50,C2>=50)
```

**OR:** TRUE when at least one condition is TRUE.

```excel
=OR(B2>=50,C2>=50)
```

**NOT:** Reverses a logical result.

```excel
=NOT(B2>=50)
```

Combined with IF:

```excel
=IF(AND(B2>=50,C2>=50),"Pass","Fail")
```

---

## 15. Nested IF and IFS

A **nested IF** places one IF inside another.

```excel
=IF(B2>=90,"A",IF(B2>=75,"B",IF(B2>=50,"C","F")))
```

`IFS` checks multiple conditions more directly:

```excel
=IFS(
B2>=90,"A",
B2>=75,"B",
B2>=50,"C",
B2<50,"F"
)
```

Availability of `IFS` depends on the Excel version.

---

## 16. Relative, Absolute and Mixed References

**Relative reference:** Changes when copied.

```excel
=A2+B2
```

Copied one row down:

```excel
=A3+B3
```

**Absolute reference:** Remains fixed.

```excel
=$A$1
```

**Mixed reference:** Locks either the column or row.

```excel
=$A1
=A$1
```

---

## 17. Autofill

**Definition:** Autofill copies formulas, values, or patterns into adjacent cells.

If B2 contains:

```excel
=A2*2
```

copying it downward automatically changes the row reference.

---

## 18. Sorting and Filtering

**Sorting:** Rearranges data, for example from smallest to largest or A to Z.

**Filtering:** Displays only rows that meet selected conditions without normally deleting the other rows.

Example filter:

```text
Region = North
```

---

## 19. Excel Tables

An **Excel Table** converts a data range into a structured table with features such as filtering, sorting, automatic expansion, and structured references.

Shortcut:

```text
Ctrl + T
```

Example columns:

```text
Employee | Department | Salary
```

---

## 20. Structured References

Structured references use table and column names.

Example:

```excel
=SUM(Sales[Amount])
```

Here `Sales` is the table name and `Amount` is the column name.

---

## 21. SUMIF and SUMIFS

**SUMIF:** Adds values meeting one condition.

```excel
=SUMIF(A2:A10,"North",C2:C10)
```

**SUMIFS:** Adds values meeting multiple conditions.

```excel
=SUMIFS(D2:D100,A2:A100,"North",B2:B100,"Laptop")
```

---

## 22. COUNTIF and COUNTIFS

**COUNTIF:** Counts values meeting one condition.

```excel
=COUNTIF(A2:A100,"North")
```

**COUNTIFS:** Counts values meeting multiple conditions.

```excel
=COUNTIFS(A2:A100,"North",B2:B100,"Laptop")
```

---

## 23. AVERAGEIF and AVERAGEIFS

**AVERAGEIF:**
```excel
=AVERAGEIF(A2:A100,"North",C2:C100)
```

**AVERAGEIFS:**
```excel
=AVERAGEIFS(D2:D100,A2:A100,"North",B2:B100,"Laptop")
```

---

## 24. Text Functions

### LEFT
Extracts characters from the beginning.

```excel
=LEFT(A2,3)
```

### RIGHT
Extracts characters from the end.

```excel
=RIGHT(A2,3)
```

### MID
Extracts characters from a specified position.

```excel
=MID(A2,2,3)
```

### LEN
Returns the number of characters.

```excel
=LEN(A2)
```

### TRIM
Removes extra spaces.

```excel
=TRIM(A2)
```

### UPPER
Converts text to uppercase.

```excel
=UPPER(A2)
```

### LOWER
Converts text to lowercase.

```excel
=LOWER(A2)
```

### PROPER
Capitalizes the first letter of each word.

```excel
=PROPER(A2)
```

### SUBSTITUTE
Replaces specific text.

```excel
=SUBSTITUTE(A2,"Delhi","Mumbai")
```

---

## 25. CONCAT and TEXTJOIN

**CONCAT:** Combines text.

```excel
=CONCAT(A2," ",B2)
```

**TEXTJOIN:** Combines text using a delimiter.

```excel
=TEXTJOIN(", ",TRUE,A2:A5)
```

`TEXTJOIN` can also ignore empty cells when its second argument is TRUE.

---

## 26. FIND and SEARCH

**FIND:** Finds the position of text and is case-sensitive.

```excel
=FIND("@",A2)
```

**SEARCH:** Finds text and is not case-sensitive.

```excel
=SEARCH("python",A2)
```

---

## 27. TEXT Function

**Definition:** Formats a number or date as text.

```excel
=TEXT(A2,"0.00")
```

Date example:

```excel
=TEXT(A2,"dd-mm-yyyy")
```

---

## 28. TODAY and NOW

`TODAY()` returns the current date.

```excel
=TODAY()
```

`NOW()` returns the current date and time.

```excel
=NOW()
```

---

## 29. IFERROR

**Definition:** Returns an alternative value when a formula produces an error.

**Syntax:**
```excel
=IFERROR(value, value_if_error)
```

**Example:**
```excel
=IFERROR(A2/B2,0)
```

---

## 30. VLOOKUP

**Definition:** Searches for a value in the first column of a table/range and returns a value from another column in the same row.

**Syntax:**
```excel
=VLOOKUP(lookup_value, table_array, col_index_num, [range_lookup])
```

**Example:**
```excel
=VLOOKUP(E2,A2:C10,3,FALSE)
```

For an exact match, `FALSE` (or `0`) is commonly used.

---

## 31. HLOOKUP

**Definition:** Searches for a value in the first row of a range and returns a value from a specified row.

```excel
=HLOOKUP(B1,A1:F5,4,FALSE)
```

---

## 32. XLOOKUP

**Definition:** A modern lookup function that searches one range and returns a corresponding value from another range.

**Syntax:**
```excel
=XLOOKUP(lookup_value, lookup_array, return_array)
```

**Example:**
```excel
=XLOOKUP(E2,A2:A10,C2:C10,"Not Found")
```

Advantages include:
- Can look left or right
- Uses separate lookup and return ranges
- Does not require a column index number
- Can specify a not-found result

Availability depends on the Excel version.

---

## 33. INDEX and MATCH

**INDEX:** Returns a value from a specified position.

```excel
=INDEX(C2:C10,3)
```

**MATCH:** Returns the position of a value.

```excel
=MATCH(E2,A2:A10,0)
```

**INDEX + MATCH:**

```excel
=INDEX(C2:C10,MATCH(E2,A2:A10,0))
```

The formula finds E2 in A2:A10 and returns the corresponding value from C2:C10.

---

## 34. PivotTable

A **PivotTable** is used to summarize and analyze large amounts of data quickly.

Example source:

```text
Date | Region | Product | Sales
```

A PivotTable can produce:

```text
Region | Total Sales
North  | 150000
South  | 125000
West   | 180000
```

Common PivotTable areas:

- **Rows** → categories shown as rows
- **Columns** → categories shown as columns
- **Values** → calculations such as Sum or Count
- **Filters** → filters the PivotTable

---

## 35. Charts

Charts are visual representations of data.

Common types:

- **Column/Bar chart** → compare categories
- **Line chart** → show trends over time
- **Pie chart** → show parts of a whole when categories are limited
- **Scatter chart** → examine relationships between numerical variables
- **Area chart** → show trends and magnitude over time

---

## 36. Conditional Formatting

**Definition:** Automatically changes the appearance of cells based on values or conditions.

Examples:
- Highlight values greater than 100
- Highlight duplicates
- Color scales
- Data bars
- Top/bottom values

---

## 37. Data Validation

**Definition:** Controls what users can enter into a cell.

Examples:
- Dropdown lists
- Whole numbers only
- Dates within a range
- Text length restrictions

A dropdown could contain:

```text
Python
SQL
Excel
Power BI
```

---

## 38. Remove Duplicates

**Remove Duplicates** identifies repeated records and removes duplicate entries from the selected data.

Before using it, make sure you understand which columns define a duplicate.

---

## 39. Find and Replace

Find and Replace searches for specific content and can replace it.

Shortcut:

```text
Ctrl + H
```

Example:

```text
Delhi → Mumbai
```

---

## 40. Freeze Panes

**Definition:** Keeps selected rows or columns visible while scrolling.

This is especially useful for keeping column headers visible in large datasets.

---

## 41. Text to Columns

**Definition:** Splits data from one column into multiple columns using a delimiter or fixed width.

Example:

```text
Siddharth,Singh,India
```

can become:

```text
Siddharth | Singh | India
```

using comma as the delimiter.

---

## 42. Flash Fill

**Definition:** Detects a pattern from examples and fills remaining values automatically.

Example:

```text
Siddharth Singh
Rahul Kumar
```

can be transformed into first names:

```text
Siddharth
Rahul
```

---

## 43. Named Range

A **named range** gives a meaningful name to a cell or range.

Instead of:

```excel
=SUM(B2:B100)
```

you can name the range `Sales` and use:

```excel
=SUM(Sales)
```

---

## 44. Excel Errors

| Error | Meaning |
|---|---|
| `#DIV/0!` | Division by zero or blank denominator |
| `#N/A` | Value is not available/found |
| `#VALUE!` | Incorrect type of value or argument |
| `#REF!` | Invalid cell reference |
| `#NAME?` | Excel does not recognize a name or function |
| `#NUM!` | Invalid numeric result or argument |
| `#SPILL!` | A dynamic array formula cannot spill into required cells |
| `#CALC!` | Calculation-related error |

---

## 45. Data Cleaning in Excel

**Definition:** Data cleaning means preparing raw data so it is consistent and usable for analysis.

Common tasks:
- Remove duplicates
- Remove unnecessary spaces
- Standardize text
- Handle missing values
- Correct data types
- Split columns
- Standardize dates
- Check inconsistent categories

Useful functions/tools:

```excel
=TRIM(A2)
=UPPER(A2)
=LOWER(A2)
=PROPER(A2)
=IFERROR(...)
```

Other tools include:
- Find and Replace
- Text to Columns
- Remove Duplicates
- Flash Fill
- Power Query

---

## 46. Power Query

**Definition:** Power Query is an Excel tool for importing, transforming, and preparing data.

It can:
- Import data from files
- Combine datasets
- Remove columns
- Filter rows
- Change data types
- Split columns
- Remove duplicates
- Merge tables
- Append tables
- Automate repeatable data-cleaning steps

Typical workflow:

```text
Get Data
   ↓
Transform Data
   ↓
Clean Data
   ↓
Load Data
```

---

## 47. Power Pivot

**Definition:** Power Pivot is used for working with larger datasets and creating data models.

It supports:
- Relationships between tables
- Data models
- Measures
- DAX calculations

---

## 48. DAX

**Definition:** DAX (Data Analysis Expressions) is a formula language used with Power Pivot and Power BI.

Example:

```text
Total Sales = SUM(Sales[Amount])
```

DAX is different from normal Excel worksheet formulas and is mainly used for data models and analytical calculations.

---

## 49. Basic Excel Data Analysis Workflow

A practical workflow is:

```text
1. Import / enter data
        ↓
2. Inspect the data
        ↓
3. Clean the data
        ↓
4. Format data as a table
        ↓
5. Filter / sort
        ↓
6. Use formulas
        ↓
7. Create PivotTables
        ↓
8. Create charts
        ↓
9. Build a report or dashboard
```

---

## 50. Common Excel Practice Problems

### Calculate total sales

```excel
=SUM(D2:D100)
```

### Calculate average sales

```excel
=AVERAGE(D2:D100)
```

### Find highest sale

```excel
=MAX(D2:D100)
```

### Find lowest sale

```excel
=MIN(D2:D100)
```

### Count sales records

```excel
=COUNT(D2:D100)
```

### Count sales from North

```excel
=COUNTIF(B2:B100,"North")
```

### Total sales from North

```excel
=SUMIF(B2:B100,"North",D2:D100)
```

### Total laptop sales from North

```excel
=SUMIFS(D2:D100,B2:B100,"North",C2:C100,"Laptop")
```

### Mark employees as eligible

```excel
=IF(D2>=50000,"Eligible","Not Eligible")
```

### Look up an employee's department

```excel
=XLOOKUP(G2,A2:A100,C2:C100,"Not Found")
```

---

## 51. Useful Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl + C` | Copy |
| `Ctrl + V` | Paste |
| `Ctrl + X` | Cut |
| `Ctrl + Z` | Undo |
| `Ctrl + Y` | Redo |
| `Ctrl + S` | Save |
| `Ctrl + F` | Find |
| `Ctrl + H` | Find and Replace |
| `Ctrl + T` | Create Table |
| `Ctrl + 1` | Format Cells |
| `Ctrl + Arrow Key` | Move to edge of a data region |
| `Ctrl + Shift + Arrow Key` | Select to edge of a data region |
| `F2` | Edit active cell |
| `Alt + =` | AutoSum |
| `Ctrl + ;` | Enter current date |

---

## 52. Important Excel Concepts to Remember

- A workbook can contain multiple worksheets.
- A cell is identified by a column letter and row number.
- A range contains multiple cells.
- Formulas normally begin with `=`.
- Relative references change when copied.
- Absolute references use `$` to remain fixed.
- `IF` is used for conditional logic.
- `SUMIF` and `SUMIFS` perform conditional sums.
- `COUNTIF` and `COUNTIFS` count based on conditions.
- `XLOOKUP`, `VLOOKUP`, `INDEX`, and `MATCH` are used for lookups.
- PivotTables summarize data efficiently.
- Charts help communicate patterns visually.
- Conditional Formatting highlights important values.
- Data Validation helps control data entry.
- Power Query is useful for repeatable data transformation.
- Power Pivot and DAX are useful for data modeling and advanced analysis.

**Learn → Practice → Analyze → Improve**
