# Python Notes


## 1. Python

### Definition
Python is a high-level, general-purpose programming language known for its simple and readable syntax. It is widely used in web development, automation, data analysis, machine learning, and scripting.

### Example

```python
print("Hello, World!")
```

### Output

```text
Hello, World!
```

---

# 2. Comments

### Definition
Comments are notes written inside code for humans to understand it. Python ignores comments while running the program.

### Single-line comment

### Syntax

```python
# comment
```

### Example

```python
# This prints a message
print("Hello")
```

### Multi-line comment

Python does not have a special multi-line comment syntax. Triple-quoted strings are commonly used when a block of text is not assigned to a variable.

```python
"""
This is a block
of explanatory text.
"""
```

---

# 3. Variables

### Definition
A variable is a name used to store a value.

### Syntax

```python
variable_name = value
```

### Example

```python
name = "Siddharth"
age = 22
```

Here:
- `name` stores a string.
- `age` stores an integer.

### Multiple assignment

```python
a, b = 10, 20
```

### Swapping variables

```python
a = 10
b = 20

a, b = b, a

print(a)
print(b)
```

Output:

```text
20
10
```

---

# 4. Data Types

### Definition
A data type tells Python what kind of value a variable contains.

Common Python data types:

| Type | Meaning | Example |
|---|---|---|
| `int` | Whole number | `10` |
| `float` | Decimal number | `10.5` |
| `complex` | Complex number | `2 + 3j` |
| `str` | Text | `"Python"` |
| `bool` | True/False | `True` |
| `list` | Ordered, changeable collection | `[1, 2, 3]` |
| `tuple` | Ordered, unchangeable collection | `(1, 2, 3)` |
| `set` | Unordered collection of unique values | `{1, 2, 3}` |
| `dict` | Key-value collection | `{"name": "Sam"}` |

### Example

```python
age = 22
height = 5.8
name = "Sam"
is_student = True

print(type(age))
print(type(height))
print(type(name))
print(type(is_student))
```

---

# 5. Input and Output

## `print()`

### Definition
`print()` displays information on the screen.

### Syntax

```python
print(value)
```

### Example

```python
name = "Sam"
print(name)
```

---

## `input()`

### Definition
`input()` takes input from the user. The value returned by `input()` is a string by default.

### Syntax

```python
variable = input("message")
```

### Example

```python
name = input("Enter your name: ")
print("Hello", name)
```

### Taking a number as input

```python
age = int(input("Enter your age: "))
print(age)
```

---

# 6. Type Checking

## `type()`

### Definition
`type()` tells us the data type of a value.

### Syntax

```python
type(value)
```

### Example

```python
x = 10
print(type(x))
```

Output:

```text
<class 'int'>
```

---

# 7. Type Casting

### Definition
Type casting means converting a value from one data type to another.

### Common functions

```python
int()
float()
str()
bool()
```

### Examples

```python
x = "10"

a = int(x)
b = float(x)

print(a)
print(b)
```

Output:

```text
10
10.0
```

---

# 8. Operators

### Definition
Operators are symbols or keywords used to perform operations on values.

---

## Arithmetic Operators

| Operator | Meaning | Example |
|---|---|---|
| `+` | Addition | `10 + 5` |
| `-` | Subtraction | `10 - 5` |
| `*` | Multiplication | `10 * 5` |
| `/` | Division | `10 / 5` |
| `%` | Modulus/remainder | `10 % 3` |
| `//` | Floor division | `10 // 3` |
| `**` | Exponent | `2 ** 3` |

### Example

```python
a = 10
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a % b)
print(a // b)
print(a ** b)
```

---

## Comparison Operators

### Definition
Comparison operators compare two values and return either `True` or `False`.

```python
==    # equal to
!=    # not equal to
>     # greater than
<     # less than
>=    # greater than or equal to
<=    # less than or equal to
```

### Example

```python
a = 10
b = 20

print(a == b)
print(a < b)
print(a != b)
```

---

## Assignment Operators

```python
=     # assign
+=    # add and assign
-=    # subtract and assign
*=    # multiply and assign
/=    # divide and assign
//=   # floor divide and assign
%=    # modulus and assign
**=   # exponent and assign
```

### Example

```python
x = 10
x += 5

print(x)
```

Output:

```text
15
```

---

## Logical Operators

### Definition
Logical operators are used to combine conditions.

```python
and
or
not
```

### Example

```python
age = 22

print(age > 18 and age < 30)
print(age < 18 or age > 20)
print(not(age > 18))
```

---

## Membership Operators

### Definition
Membership operators check whether a value exists inside a collection.

```python
in
not in
```

### Example

```python
numbers = [1, 2, 3, 4]

print(3 in numbers)
print(5 not in numbers)
```

---

## Identity Operators

### Definition
Identity operators check whether two variables refer to the same object.

```python
is
is not
```

### Example

```python
a = [1, 2]
b = a

print(a is b)
```

---

# 9. Conditional Statements

### Definition
Conditional statements allow a program to make decisions based on conditions.

---

## `if`

### Syntax

```python
if condition:
    statement
```

### Example

```python
age = 20

if age >= 18:
    print("Adult")
```

---

## `if-else`

### Syntax

```python
if condition:
    statement
else:
    statement
```

### Example

```python
number = 7

if number % 2 == 0:
    print("Even")
else:
    print("Odd")
```

---

## `if-elif-else`

### Syntax

```python
if condition:
    statement
elif condition:
    statement
else:
    statement
```

### Example

```python
marks = 75

if marks >= 90:
    print("A")
elif marks >= 60:
    print("B")
else:
    print("C")
```

---

## Nested `if`

### Definition
An `if` statement placed inside another `if` statement is called a nested `if`.

### Example

```python
age = 20
has_id = True

if age >= 18:
    if has_id:
        print("Allowed")
```

---

# 10. Loops

### Definition
A loop is used to execute a block of code repeatedly.

Python mainly provides:
- `for` loop
- `while` loop

---

## `for` Loop

### Definition
A `for` loop is commonly used when we want to iterate over a sequence or collection.

### Syntax

```python
for variable in sequence:
    statement
```

### Example

```python
for number in [1, 2, 3, 4]:
    print(number)
```

---

## `range()`

### Definition
`range()` generates a sequence of numbers.

### Syntax

```python
range(stop)
range(start, stop)
range(start, stop, step)
```

The `stop` value is not included.

### Examples

```python
for i in range(5):
    print(i)
```

Output:

```text
0
1
2
3
4
```

```python
for i in range(2, 10, 2):
    print(i)
```

Output:

```text
2
4
6
8
```

---

## `while` Loop

### Definition
A `while` loop repeatedly executes code as long as its condition is `True`.

### Syntax

```python
while condition:
    statement
```

### Example

```python
i = 1

while i <= 5:
    print(i)
    i += 1
```

---

## `break`

### Definition
`break` immediately stops the loop.

### Example

```python
for i in range(10):
    if i == 5:
        break
    print(i)
```

---

## `continue`

### Definition
`continue` skips the current iteration and moves to the next iteration.

### Example

```python
for i in range(5):
    if i == 2:
        continue
    print(i)
```

---

## `pass`

### Definition
`pass` does nothing. It is used as a placeholder when code is required syntactically but no action is needed yet.

### Example

```python
if True:
    pass
```

---

# 11. Strings

### Definition
A string is a sequence of characters enclosed in quotes.

### Syntax

```python
"Hello"
'Hello'
```

### Example

```python
name = "Python"
print(name)
```

---

## String Indexing

### Definition
Indexing is used to access individual characters in a string.

Python indexing starts from `0`.

```text
P y t h o n
0 1 2 3 4 5
```

### Example

```python
text = "Python"

print(text[0])
print(text[2])
```

Output:

```text
P
t
```

### Negative indexing

```python
print(text[-1])
```

Output:

```text
n
```

---

## String Slicing

### Definition
Slicing extracts a portion of a string.

### Syntax

```python
string[start:stop:step]
```

### Example

```python
text = "Python"

print(text[0:3])
print(text[::2])
print(text[::-1])
```

---

## Common String Methods

### `lower()`

```python
text = "PYTHON"
print(text.lower())
```

### `upper()`

```python
text = "python"
print(text.upper())
```

### `strip()`

Removes spaces from the beginning and end.

```python
text = "  Python  "
print(text.strip())
```

### `replace()`

```python
text = "I like Java"
print(text.replace("Java", "Python"))
```

### `split()`

Splits a string into a list.

```python
text = "Python is easy"
words = text.split()

print(words)
```

### `join()`

Joins elements into a string.

```python
words = ["Python", "is", "easy"]

result = " ".join(words)
print(result)
```

### `find()`

Returns the position of a substring.

```python
text = "Python"

print(text.find("t"))
```

### `count()`

Counts occurrences.

```python
text = "banana"

print(text.count("a"))
```

---

## String Checking Methods

```python
text.isalpha()
text.isdigit()
text.isalnum()
text.isspace()
text.islower()
text.isupper()
```

### Example

```python
text = "123"

print(text.isdigit())
```

Output:

```text
True
```

---

# 12. Lists

### Definition
A list is an ordered and changeable collection that can contain multiple values.

### Syntax

```python
list_name = [value1, value2, value3]
```

### Example

```python
numbers = [10, 20, 30, 40]

print(numbers)
```

Lists can contain different data types:

```python
data = [10, "Python", 5.5, True]
```

---

## List Indexing

```python
numbers = [10, 20, 30]

print(numbers[0])
print(numbers[-1])
```

---

## List Slicing

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[1:4])
```

---

## `append()`

### Definition
Adds one item to the end of a list.

```python
numbers = [1, 2, 3]
numbers.append(4)

print(numbers)
```

---

## `insert()`

Adds an item at a specific position.

```python
numbers = [1, 2, 3]
numbers.insert(1, 10)

print(numbers)
```

---

## `remove()`

Removes the first matching value.

```python
numbers = [1, 2, 3, 2]
numbers.remove(2)

print(numbers)
```

---

## `pop()`

Removes and returns an item.

```python
numbers = [10, 20, 30]

x = numbers.pop()

print(x)
print(numbers)
```

---

## `sort()`

Sorts a list in place.

```python
numbers = [3, 1, 2]
numbers.sort()

print(numbers)
```

---

## `reverse()`

Reverses a list in place.

```python
numbers = [1, 2, 3]
numbers.reverse()

print(numbers)
```

---

## List Comprehension

### Definition
List comprehension is a short way of creating a new list from an iterable.

### Syntax

```python
[expression for item in iterable]
```

### Example

```python
squares = [x ** 2 for x in range(5)]

print(squares)
```

Output:

```text
[0, 1, 4, 9, 16]
```

---

# 13. Tuples

### Definition
A tuple is an ordered collection that cannot normally be changed after it is created.

### Syntax

```python
tuple_name = (value1, value2, value3)
```

### Example

```python
numbers = (10, 20, 30)

print(numbers)
```

### Accessing values

```python
print(numbers[0])
```

### Tuple unpacking

```python
a, b, c = (10, 20, 30)

print(a)
print(b)
print(c)
```

---

# 14. Sets

### Definition
A set is an unordered collection of unique elements.

### Syntax

```python
set_name = {value1, value2, value3}
```

### Example

```python
numbers = {1, 2, 3, 3, 4}

print(numbers)
```

The duplicate `3` is stored only once.

### Add an element

```python
numbers.add(5)
```

### Remove an element

```python
numbers.remove(2)
```

### Common set operations

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b)   # union
print(a & b)   # intersection
print(a - b)   # difference
```

---

# 15. Dictionaries

### Definition
A dictionary stores data as **key-value pairs**.

### Syntax

```python
dictionary = {
    key: value,
    key: value
}
```

### Example

```python
student = {
    "name": "Sam",
    "age": 22,
    "course": "Python"
}

print(student["name"])
```

---

## Adding or Updating Values

```python
student["age"] = 23
student["city"] = "Pune"
```

---

## `get()`

### Definition
`get()` returns the value associated with a key.

### Syntax

```python
dictionary.get(key)
```

### Example

```python
student = {"name": "Sam"}

print(student.get("name"))
print(student.get("age"))
```

`get()` returns `None` when the key is missing unless a default value is provided.

```python
print(student.get("age", 0))
```

---

## `keys()`, `values()`, `items()`

```python
student = {
    "name": "Sam",
    "age": 22
}

print(student.keys())
print(student.values())
print(student.items())
```

---

## Looping through a Dictionary

```python
student = {
    "name": "Sam",
    "age": 22
}

for key, value in student.items():
    print(key, value)
```

---

# 16. Functions

### Definition
A function is a reusable block of code designed to perform a particular task. Functions reduce repeated code and make programs easier to understand and maintain.

### Basic Syntax

```python
def function_name(parameters):
    statements
    return value
```

- `def` defines a function.
- `parameters` are optional inputs.
- `return` is optional and sends a result back.

### Simple Function

```python
def greet():
    print("Hello")

greet()
```

### Function with Parameters

```python
def greet(name):
    print("Hello", name)

greet("Sam")
```

### Multiple Parameters and Return

```python
def add(a, b):
    return a + b

result = add(10, 20)
print(result)
```

Output:

```text
30
```

### `print()` vs `return`

`print()` displays a result, while `return` sends a result back to the calling code so it can be stored or used in another expression.

```python
def add(a, b):
    return a + b

result = add(10, 20)
```

### Default Parameters

A default parameter is used when the caller does not provide a value.

```python
def greet(name="Guest"):
    print("Hello", name)

greet()
greet("Sam")
```

### Positional Arguments

Arguments are matched with parameters according to their position.

```python
def introduce(name, age):
    print(name, age)

introduce("Sam", 22)
```

### Keyword Arguments

Arguments can be passed using parameter names.

```python
def introduce(name, age):
    print(name, age)

introduce(age=22, name="Sam")
```

### `*args`

`*args` allows a function to accept any number of positional arguments. Inside the function, `args` is a tuple.

```python
def total(*numbers):
    return sum(numbers)

print(total(10, 20, 30))
```

Output:

```text
60
```

### `**kwargs`

`**kwargs` allows a function to accept any number of keyword arguments. Inside the function, `kwargs` is a dictionary.

```python
def show_details(**details):
    print(details)

show_details(name="Sam", age=22)
```

### Recursive Functions

A recursive function calls itself. It needs a base case to stop.

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)

print(factorial(5))
```

Output:

```text
120
```

### Lambda Functions

A lambda is a small anonymous function used mainly for short expressions.

Syntax:

```python
lambda arguments: expression
```

Example:

```python
square = lambda x: x ** 2
print(square(5))
```

Output:

```text
25
```

### Functions as Arguments

Python allows functions to be passed to other functions.

```python
def square(x):
    return x ** 2

def apply_function(func, value):
    return func(value)

print(apply_function(square, 5))
```

### Docstrings

A docstring describes what a function does.

```python
def add(a, b):
    "Return the sum of two numbers."
    return a + b
```

### Type Hints

Type hints describe expected parameter and return types.

```python
def add(a: int, b: int) -> int:
    return a + b
```

Type hints improve readability and editor support, but Python does not automatically enforce them at runtime.

### Function Scope

A variable created inside a function is generally local to that function.

```python
def test():
    x = 10
    print(x)

test()
```

A variable created outside functions is generally available at the module level.

```python
x = 10

def test():
    print(x)

test()
```


### Important Points

- Use `def` to define a function.
- Functions can accept parameters.
- `return` sends a value back.
- Default parameters provide fallback values.
- `*args` collects positional arguments into a tuple.
- `**kwargs` collects keyword arguments into a dictionary.
- Functions can call other functions.
- Functions can be passed as arguments.
- Recursive functions need a stopping condition.
- Lambda functions are useful for short expressions.


# 17. Scope

### Definition
Scope determines where a variable can be accessed.

### Local variable

A variable created inside a function is generally local to that function.

```python
def test():
    x = 10
    print(x)

test()
```

### Global variable

A variable created outside functions is generally available at the module level.

```python
x = 10

def test():
    print(x)

test()
```

---

# 18. Built-in Functions

Python provides many functions that can be used directly.

### `len()`

Returns the number of items or characters.

```python
numbers = [1, 2, 3]

print(len(numbers))
```

### `max()`

Returns the largest value.

```python
numbers = [10, 20, 5]

print(max(numbers))
```

### `min()`

Returns the smallest value.

```python
print(min(numbers))
```

### `sum()`

Returns the total.

```python
print(sum(numbers))
```

### `sorted()`

Returns a new sorted list.

```python
numbers = [3, 1, 2]

result = sorted(numbers)

print(result)
```

### `abs()`

Returns the absolute value.

```python
print(abs(-10))
```

---

# 19. Useful String and Collection Problems

These are common beginner practice problems.

---

## Reverse a String

```python
text = "Python"

reverse = text[::-1]

print(reverse)
```

---

## Check Palindrome String

### Definition
A palindrome reads the same forward and backward.

```python
text = "madam"

if text == text[::-1]:
    print("Palindrome")
else:
    print("Not Palindrome")
```

---

## Count Vowels

```python
text = "python programming"
count = 0

for ch in text.lower():
    if ch in "aeiou":
        count += 1

print(count)
```

---

## Count Consonants

```python
text = "python"
count = 0

for ch in text.lower():
    if ch.isalpha() and ch not in "aeiou":
        count += 1

print(count)
```

---

## Remove Spaces

```python
text = "Python is easy"

result = text.replace(" ", "")

print(result)
```

---

## Check Anagram

### Definition
Two strings are anagrams if they contain the same characters with the same frequencies, but possibly in a different order.

```python
s1 = "listen"
s2 = "silent"

if sorted(s1) == sorted(s2):
    print("Anagram")
else:
    print("Not Anagram")
```

---

## Character Frequency

```python
text = "banana"
frequency = {}

for ch in text:
    frequency[ch] = frequency.get(ch, 0) + 1

print(frequency)
```

---

# 20. Common Number Problems

## Even or Odd

### Definition
A number is even if it is completely divisible by `2`. Otherwise, it is odd.

### Example

```python
number = 10

if number % 2 == 0:
    print("Even")
else:
    print("Odd")
```

---

## Largest of Two Numbers

```python
a = 10
b = 20

if a > b:
    print(a)
else:
    print(b)
```

---

## Largest of Three Numbers

```python
a = 10
b = 25
c = 15

if a >= b and a >= c:
    print(a)
elif b >= a and b >= c:
    print(b)
else:
    print(c)
```

---

## Factorial

### Definition
The factorial of a positive integer `n` is the product of all positive integers from `1` to `n`.

For example:

```text
5! = 5 × 4 × 3 × 2 × 1 = 120
```

### Using `for`

```python
n = 5
factorial = 1

for i in range(1, n + 1):
    factorial *= i

print(factorial)
```

### Using `while`

```python
n = 5
factorial = 1
i = 1

while i <= n:
    factorial *= i
    i += 1

print(factorial)
```

---

## Fibonacci Series

### Definition
The Fibonacci sequence is a sequence in which each number is the sum of the two previous numbers.

Example:

```text
0, 1, 1, 2, 3, 5, 8, 13
```

### Example

```python
n = 8

a = 0
b = 1

for i in range(n):
    print(a)
    a, b = b, a + b
```

---

## Prime Number

### Definition
A prime number is a number greater than `1` that has exactly two positive factors: `1` and itself.

### Example

```python
number = 17
is_prime = True

if number <= 1:
    is_prime = False
else:
    for i in range(2, number):
        if number % i == 0:
            is_prime = False
            break

if is_prime:
    print("Prime")
else:
    print("Not Prime")
```

---

## Armstrong Number

### Definition
An Armstrong number is a number that is equal to the sum of its digits raised to the power of the number of digits.

For example:

```text
153 = 1³ + 5³ + 3³
   = 1 + 125 + 27
   = 153
```

### Example

```python
number = 153
original = number
digits = len(str(number))
total = 0

while number > 0:
    digit = number % 10
    total += digit ** digits
    number //= 10

if total == original:
    print("Armstrong Number")
else:
    print("Not an Armstrong Number")
```

---

# 21. List Practice Problems

## Find Maximum

```python
numbers = [10, 25, 5, 40, 15]

largest = max(numbers)

print(largest)
```

### Without `max()`

```python
numbers = [10, 25, 5, 40, 15]

largest = numbers[0]

for number in numbers:
    if number > largest:
        largest = number

print(largest)
```

---

## Find Minimum

```python
numbers = [10, 25, 5, 40, 15]

smallest = numbers[0]

for number in numbers:
    if number < smallest:
        smallest = number

print(smallest)
```

---

## Second Largest Element

```python
numbers = [10, 25, 5, 40, 15]

unique_numbers = list(set(numbers))
unique_numbers.sort()

print(unique_numbers[-2])
```

---

## Remove Duplicates

### Using `set`

```python
numbers = [1, 2, 2, 3, 3, 4]

result = list(set(numbers))

print(result)
```

### Preserving original order

```python
numbers = [1, 2, 2, 3, 3, 4]

result = []

for number in numbers:
    if number not in result:
        result.append(number)

print(result)
```

---

## Merge Two Lists

```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]

result = list1 + list2

print(result)
```

---

# 22. Indentation

### Definition
Indentation means the spaces at the beginning of a line. Python uses indentation to define blocks of code.

### Example

```python
if 10 > 5:
    print("10 is greater")
```

The indented line belongs to the `if` block.

Incorrect:

```python
if 10 > 5:
print("10 is greater")
```

---

# 23. Identifiers

### Definition
An identifier is the name given to a variable, function, class, or other object.

### Rules

- Can contain letters, numbers, and `_`.
- Cannot start with a number.
- Cannot contain spaces.
- Cannot use Python keywords as names.
- Names are case-sensitive.

### Valid

```python
name = "Sam"
student_age = 22
age2 = 23
```

### Invalid

```python
2age = 22
student age = 22
```

---

# 24. Naming Conventions

Python commonly uses **snake_case** for variables and functions.

```python
student_name = "Sam"
total_marks = 450

def calculate_average():
    pass
```

Class names commonly use **PascalCase**:

```python
class StudentDetails:
    pass
```

---

# 25. Python Keywords

### Definition
Keywords are reserved words that have special meanings in Python.

Examples:

```text
if
else
elif
for
while
break
continue
def
return
class
try
except
import
from
True
False
None
and
or
not
in
is
```

These words should not be used as ordinary variable names.

---

# 26. `None`

### Definition
`None` represents the absence of a value.

### Example

```python
result = None

print(result)
```

Output:

```text
None
```

---

# 27. Mutable and Immutable Objects

### Definition
A mutable object can be changed after it is created.

Examples:
- `list`
- `dict`
- `set`

An immutable object cannot normally be changed after creation.

Examples:
- `int`
- `float`
- `str`
- `tuple`
- `bool`

### Example

List:

```python
numbers = [1, 2, 3]
numbers[0] = 10

print(numbers)
```

String:

```python
text = "Python"

# Individual characters cannot be directly changed.
```

---

# 28. Nested Collections

Collections can contain other collections.

### List inside a list

```python
matrix = [
    [1, 2],
    [3, 4]
]

print(matrix[0][1])
```

Output:

```text
2
```

### Dictionary containing a list

```python
student = {
    "name": "Sam",
    "marks": [80, 85, 90]
}

print(student["marks"])
```

---

# 29. Quick Syntax Reference

## Variable

```python
name = value
```

## Input

```python
value = input("Enter value: ")
```

## Type conversion

```python
int(value)
float(value)
str(value)
bool(value)
```

## Condition

```python
if condition:
    statement
elif condition:
    statement
else:
    statement
```

## For loop

```python
for item in iterable:
    statement
```

## While loop

```python
while condition:
    statement
```

## Function

```python
def function_name(parameters):
    statements
    return value
```

## List

```python
items = [1, 2, 3]
```

## Tuple

```python
items = (1, 2, 3)
```

## Set

```python
items = {1, 2, 3}
```

## Dictionary

```python
items = {
    "key": "value"
}
```

## String slicing

```python
text[start:stop:step]
```

## Dictionary access

```python
dictionary[key]
dictionary.get(key)
```

---

