

# Part 1: Notes & Theory 

### 1. Introduction to Python

* **What is Python?** A high-level, interpreted, general-purpose programming language whose design philosophy emphasizes code readability through significant indentation.
* **Core Characteristics:** Dynamically-typed, garbage-collected (automatic memory management), and supports multiple paradigms (procedural, object-oriented, functional). Known as a "batteries included" language due to its comprehensive standard library.
* **History:** Created in the late 1980s by Guido van Rossum (known as the "Benevolent dictator for life"  BDFL) as a descendant of the ABC programming language. Python 3 was released in December 2008 to fix backward-incompatible flaws in Python 2 (which is no longer supported).

### 2. Execution Modes & Interpreter

* **Interactive Mode (REPL):** Read-Eval-Print Loop. Python responds to each statement immediately as you type it. Started by typing `python` in the terminal.
* **Script Mode:** Running a file containing Python statements using the interpreter.
* **The Zen of Python:** A set of 19 guiding principles written by Tim Peters for writing clean code. Triggered using `import this`.

### 3. Environment & Package Management (`pyenv` & `pip`)

* **Virtual Environment:** An isolated directory containing its own Python interpreter, libraries, and scripts, separating project dependencies from the system Python.
* **`pyenv`:** A popular tool used to manage and switch between multiple Python versions and virtual environments.
* **`pip`:** The standard package manager for installing packages from the Python Package Index (PyPI). `pip freeze > requirements.txt` allows snapshotting environment dependencies.
* **Alternative Tools / Editors:** PyCharm, Eclipse + PyDev, Sublime Text, Vim, and Jupyter Lab (great for interactive data analysis).

### 4. Syntax Rules & Identifiers

* **Identifiers:** Names for variables, functions, classes, etc. Can contain letters (`a-z`, `A-Z`), digits (`0-9`), and underscores (`_`), but **cannot** start with a digit. They are case-sensitive (`EPAM != Epam`).
* **Keywords:** Reserved words with special meanings (e.g., `if`, `else`, `while`, `def`) that cannot be used as variable names.
* **Indentation:** Python uses whitespaces (best practice: 4 spaces) to define code blocks instead of curly braces `{}`.
* **Line Continuation:** Use a backslash (`\`) or automatic grouping inside parentheses `()`, brackets `[]`, or braces `{}` to span code across multiple lines.

### 5. Variables, Mutability, & Data Types

* **Dynamic Typing:** You do not need to explicitly declare a variable's data type when assigning values. Variables are simply references to objects.
* **Numbers & Strings:** Supports integers (`int`), floating-point numbers (`float`), and strings (`str` enclosed in single, double, or triple quotes).
* **Mutability:**
* **Immutable (Unchangeable):** `int`, `float`, `string`, `tuple`. Their values cannot be modified in place.
* **Mutable (Changeable):** `list`, `dict`, `set`. Their contents can change while retaining the same memory identity.



### 6. Code Quality & PEP 8

* **PEP 8:** The official style guide document written in 2001 (by Guido van Rossum, Barry Warsaw, and Nick Coghlan) to improve code readability. Essential tools for checking compliance include `pycodestyle` and `flake8`.

---

## Part 2: Practical Examples & Code (Uygulama Kısımları)

### 1. Basic Interactive REPL / Script Commands

```python
# Printing to the console
print("Hello, World!")

# Getting input from the user
name = input("Enter your name: ")
print("Welcome,", name)

# Type conversion
age_str = input("Enter your age: ")
age_int = int(age_str)
print(f"Next year you will be {age_int + 1} years old.")

```

### 2. Identifiers, Multiple Assignment, and Deletion

```python
# Valid identifiers and case sensitivity
EPAM = "Company"
epam = "Lowercase company"
print(EPAM != epam)  # Output: True

# Multiple assignments
a = b = c = 10
x, y, z = 1, 2.5, "Python"

print(a, b, c)
print(x, y, z)

# Deleting variables
temp_var = 100
del temp_var
# print(temp_var)  # Raises NameError: name 'temp_var' is not defined

```

### 3. Strings and Quotes

```python
# Single vs double quotes
word = 'Python'
sentence = "Learning Python is fun."

# Multiline strings / Docstrings
paragraph = """This is a multiline paragraph.
It spans across multiple lines cleanly."""

# Nested quotes
quote_inside_double = "He said, 'Hello!'"
quote_inside_single = 'She replied: "Hi there!"'

print(paragraph)

```

### 4. Indentation & Multi-line Statements

```python
# Correct indentation (4 spaces)
score = 85
if score >= 50:
    print("Passed")
else:
    print("Failed")

# Multi-line statement using parentheses (preferred over backslash)
total_price = (
    100 +
    250 +
    50
)
print("Total Price:", total_price)

```

### 5. Immutability vs. Mutability Demonstration

```python
# Immutable object example (string)
x = "foo"
y = x
y += "bar"
print(x)  # Output: 'foo' (x remains unchanged because strings are immutable)

# Mutable object example (list)
list_1 = [1, 2, 3]
list_2 = list_1
list_2.append(4)
print(list_1)  # Output: [1, 2, 3, 4] (list_1 changed because lists are mutable)

```

### 6. Operators (Arithmetic, Comparison, Membership, Identity)

```python
# Arithmetic & Assignment
a, b = 10, 3
print("Addition:", a + b)       # 13
print("Exponentiation:", a ** b) # 1000

a += 5  # a becomes 15
print("Updated a:", a)

# Comparison & One-line if (Ternary Operator)
status = "Even" if a % 2 == 0 else "Odd"
print(f"15 is {status}")

# Membership Operator ('in')
text = "Python Programming"
print("Python" in text)  # True

# Identity Operators ('is' vs '==')
num1 = 500
num2 = 500
print(num1 == num2)  # True (values are equal)
print(num1 is num2)  # False (different memory locations for larger integers)

```

### 7. Conditional Statements (`if-elif-else`)

```python
x = int(input("Enter an integer: "))

if x < 0:
    print("Negative number")
elif x == 0:
    print("Zero")
elif x == 1:
    print("One")
else:
    print("Greater than one")

```