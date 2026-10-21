# NumPy Notes: Definitions, Syntax, and Examples

NumPy is a Python library for numerical computing. Its main data structure is the multidimensional `ndarray`, which supports efficient mathematical operations on arrays.

## 1. Install and Import

```bash
pip install numpy
```

```python
import numpy as np
```

## 2. Create Arrays

```python
a = np.array([10, 20, 30])
matrix = np.array([[1, 2, 3], [4, 5, 6]])
zeros = np.zeros(3)
ones = np.ones((2, 3))
sequence = np.arange(0, 10, 2)  # [0, 2, 4, 6, 8]
spaced = np.linspace(0, 1, 5)
```

- `np.array()` creates an array.
- `np.zeros(shape)` and `np.ones(shape)` create zeros or ones.
- `np.arange(start, stop, step)` excludes the stop value.
- `np.linspace(start, stop, num)` creates a specified number of evenly spaced values.

## 3. Attributes

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr.ndim)   # 2 dimensions
print(arr.shape)  # (2, 3)
print(arr.size)   # 6 elements
print(arr.dtype)  # element data type
```

## 4. Indexing and Slicing

```python
arr = np.array([10, 20, 30, 40, 50])
print(arr[0])      # 10
print(arr[-1])     # 50
print(arr[1:4])    # [20 30 40]

m = np.array([[1, 2, 3], [4, 5, 6]])
print(m[0, 1])     # 2
print(m[:, 0])     # first column: [1 4]
print(m[1, :])     # second row: [4 5 6]
```

Indexes start at zero; slice end positions are excluded.

## 5. Vectorized Operations and Broadcasting

```python
a = np.array([1, 2, 3])
b = np.array([10, 20, 30])
print(a + b)   # [11 22 33]
print(a * 2)   # [2 4 6]
print(a ** 2)  # [1 4 9]
print(a + 5)   # [6 7 8]
```

**Vectorization** applies an operation to an entire array without an explicit Python loop. **Broadcasting** allows operations between compatible shapes, such as an array and a scalar.

## 6. Reshape and Transpose

```python
arr = np.arange(1, 7)
m = arr.reshape(2, 3)
print(m)
print(m.T)  # transpose: rows and columns switch
```

The new shape must contain the same total number of elements.

## 7. Statistics and Aggregation

```python
data = np.array([10, 20, 30, 40])
print(np.sum(data))     # 100
print(np.mean(data))    # 25.0
print(np.median(data))  # 25.0
print(np.min(data))     # 10
print(np.max(data))     # 40
print(np.std(data))     # standard deviation
print(np.var(data))     # variance
```

For a 2D array, `axis=0` reduces down rows and `axis=1` reduces across columns:

```python
m = np.array([[1, 2, 3], [4, 5, 6]])
print(np.sum(m, axis=0))  # column totals: [5 7 9]
print(np.sum(m, axis=1))  # row totals: [6 15]
```

## 8. Boolean Filtering

```python
scores = np.array([45, 72, 88, 60, 95])
print(scores[scores >= 70])  # [72 88 95]
print(scores[(scores >= 60) & (scores < 90)])
```

Use `&` for AND and `|` for OR, with each comparison in parentheses. Do not use Python's `and` or `or` with an array mask.

## 9. Useful Functions

```python
arr = np.array([3, 1, 3, 2, 1])
print(np.unique(arr))       # [1 2 3]
print(np.sort(arr))         # sorted copy
print(np.argmax(arr))       # index of maximum
print(np.argmin(arr))       # index of minimum
print(np.where(arr > 1, 1, 0))
```

`argmax` and `argmin` return indexes, not the maximum/minimum values.

## 10. Random Numbers

```python
rng = np.random.default_rng(42)
print(rng.integers(1, 10, size=5))  # integers 1 through 9
print(rng.random(3))                # floats in [0, 1)
```

A fixed seed helps make random results reproducible.

## 11. Dot Product and Matrix Multiplication

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
print(np.dot(a, b))  # 32
print(a @ b)         # 32
```

For matrix multiplication, the number of columns in the first matrix must equal the number of rows in the second.

## 12. Views, Copies, and NaN

```python
arr = np.array([1, 2, 3])
view = arr[1:]
view[0] = 99
print(arr)  # [1 99 3]: the slice is a view here

copy_arr = arr.copy()
copy_arr[0] = 500
print(arr)       # unchanged by editing copy_arr
print(copy_arr)
```

A view shares underlying data; a copy has independent data. Use `.copy()` when you need independent data.

```python
values = np.array([10.0, np.nan, 30.0])
print(np.isnan(values))
print(np.nanmean(values))  # 20.0; ignores NaN
```

## 13. NumPy in Data Analysis

NumPy is useful for numerical calculations, arrays and matrices, statistics, image processing, and preparing numerical data for machine learning.

## 14. Common Mistakes

- Assuming `np.arange()` includes its stop value.
- Forgetting that indexing starts at zero.
- Using `and` / `or` instead of `&` / `|` in array filters.
- Combining arrays with incompatible shapes.
- Confusing `argmax()`'s index with the maximum value.
- Accidentally modifying a view when a copy was needed.

## 15. Practice Questions

1. Create an array from 1 to 20.
2. Find an array's mean, median, minimum, and maximum.
3. Filter values greater than 50.
4. Reshape 12 values into a 3-by-4 matrix.
5. Calculate row and column totals.
6. Find indexes of minimum and maximum values.
7. Normalize an array by subtracting its mean and dividing by its standard deviation.
8. Find the dot product of two arrays.

## Quick Reference

| Task | Syntax |
|---|---|
| Create array | `np.array([...])` |
| Zeros / ones | `np.zeros(shape)`, `np.ones(shape)` |
| Range | `np.arange(start, stop, step)` |
| Shape | `arr.shape` |
| Reshape | `arr.reshape(rows, columns)` |
| Mean / sum | `np.mean(arr)`, `np.sum(arr)` |
| Filter | `arr[arr > value]` |
| Unique values | `np.unique(arr)` |
| Matrix multiplication | `a @ b` |
| Copy | `arr.copy()` |
