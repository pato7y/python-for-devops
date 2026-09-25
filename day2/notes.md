

# Python Notes: Day 2

## 1. Loops

### while Loop

Executes a code block as long as the condition is True:

```python
i = 10
while i > 0:
    print(i)
    i -= 1

```

### for Loop

Iterates over a specific sequence or range:

```python
for i in range(10):
    print(i)

```

### One-Line Loop (List Comprehension)

```python
l = [i for i in range(10)]
print(l)  # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

```

### break Statement

Terminates the loop containing it and transfers control to the statement immediately following the loop body:

```python
for val in "string":
    if val == "i":
        break
    print(val)

print("The end")

```

**Output:**

```text
s
t
r
The end

```

### continue Statement

Skips the rest of the code inside a loop for the current iteration only. The loop does not terminate but continues with the next iteration:

```python
for val in "string":
    if val == "i":
        continue
    print(val)

print("The end")

```

**Output:**

```text
s
t
r
n
g
The end

```

### else in Loops

* **`while...else`**: The `else` clause executes when the condition becomes `False` and the loop runs normally. However, if the loop is terminated prematurely by a `break` or `return` statement, the `else` clause does not execute at all.
* **`for...else`**: The `else` clause executes at the end of the iteration when the loop finishes normally.

---

## 2. Strings

Python has three built-in numeric data types: integers, floating-point numbers, and complex numbers. Strings support indexing and slicing.

### Indexing and Slicing

* The first character has an index of `0`.
* Negative subscripts count from the end of the string (`-1` represents the last character).
* Slicing stops immediately before the second value (`[start:end]`).

```python
what = 'This parrot is dead'
what[3]     # 's'
what[0]     # 'T'
what[-1]    # 'd'
what[0:4]   # 'This'
what[5:11]  # 'parrot'
what[1:]    # 'his parrot is dead'
what[:3]    # 'Thi'
what[1:-1:2]# 'hspro sda' (Step usage)
what[::-1]  # 'daed si torrap sihT' (Reversing a string)

```

### String Formatting

```python
a, b = 1, 2
print(f"{a}+{b}={a+b}") # 1+2=3

print("String: %s integer %d" % ('str', 57)) # String: str integer 57
print('{0} and {1}'.format('minced meat', 'eggs')) # minced meat and eggs
print('This {food} — {adjective}.'.format(food='stuffing', adjective='awful'))

```

### Raw Strings

Strings prefixed with r treat backslashes `\` as literal characters, which is very useful for Windows paths and regular expression patterns:

```python
print(r'C:\\nowhere') # C:\\nowhere

```

---

## 3. Lists

A list is an ordered, flexible collection of arbitrary objects, defined by enclosing a comma-separated sequence in square brackets (`[]`).

### Characteristics and Modifications

* Lists are ordered (`[1, 2, 3, 4] == [4, 1, 3, 2]` evaluates to `False`).
* Lists can be nested to arbitrary depth.
* Lists are mutable.

```python
list1 = ['physics', 'chemistry', 1997, 2000]
list1[2] = 2001  # Update item
del list1[2]     # Delete item

```

### Essential List Methods

* `append(value)`: Appends an item to the list.
* `count(value)`: Counts occurrences of a given item.
* `extend(iterable)`: Extends the list with another list's items.
* `index(value, [start, [stop]])`: Finds the position of an item; raises `ValueError` if not found.
* `insert(index, value)`: Inserts an item into a specified position.
* `pop([index = -1])`: Retrieves and removes the last (or specified) item.
* `remove(value)`: Removes the specified item.
* `reverse()`: Reverses the items of the list in place.
* `sort(reverse=False)`: Sorts the items of the list in place.

---

## 4. Tuples (Immutable)

Tuples are ordered collections of objects, just like lists, but they are **immutable** (cannot be changed) and use parentheses `()` instead of square brackets.

```python
tup1 = ('physics', 'chemistry', 1997, 2000)
tup2 = (1, 2, 3, 4, 5)

# Direct assignment raises a TypeError:
# tup1[0] = 100 

# Concatenation is allowed:
tup3 = tup1 + tup2

```

---

## 5. Dictionaries

Dictionaries consist of a collection of key-value pairs enclosed in curly braces (`{}`).

### Update and Delete

```python
d = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}
d['Age'] = 8          # Update existing entry
d['School'] = "DPS School" # Add new entry

del d['Name']         # Remove entry with key 'Name'
d.clear()             # Remove all entries
del d                 # Delete entire dictionary

```

### Key Restrictions

* **Uniqueness:** Keys must be unique; duplicate keys overwrite previous values.
* **Immutable:** Keys must be of an immutable type (lists cannot be keys, raising `TypeError: unhashable type: 'list'`).

### Dictionary Methods and Tips

* `clear()`: Removes all items.
* `copy()`: Returns a shallow copy.
* `setdefault(key[, default])`: Returns value if key exists, otherwise inserts key with `default` and returns it.
* **Best Practice:** `d.setdefault("node", []).append("item")`


* `keys()`, `values()`, `items()`: Used to iterate through dictionary components.
* `fromkeys(iterable[, value])`: Creates a new dict with keys from an iterable.
* `get(key[, default])`: Returns value for key if present, else default.
* `pop(key[, default])`: Removes key and returns its value.
* `popitem()`: Removes and returns a `(key, value)` pair in LIFO order.
* `update(dict)`: Updates dictionary with key/value pairs from another.

---

## 6. Sets

A set is an unordered collection with no duplicate elements. It supports mathematical operations like union, intersection, difference, and symmetric difference.

```python
x = {1, 2, 3, 1, 2}
y = {2, 4, 5}

print("x & y:", x & y) # Intersection (x.intersection(y))
print("x | y:", x | y) # Union (x.union(y))
print("x - y:", x - y) # Difference (x.difference(y))
print("x ^ y:", x ^ y) # Symmetric difference

```

### `remove(elem)` vs `discard(elem)`

* `remove(elem)`: Removes the element; raises a `KeyError` if the element is not found.
* `discard(elem)`: Removes the element; does not raise an error if the element is missing.

---

## 7. Functions

### Declaration and Call

Defined using the `def` keyword. The first expression can act as a docstring. If a `return` statement is skipped, it implicitly returns `None`.

```python
def printme(str):
    """This prints a passed string."""
    print(str)

printme("EPAM is the best company!")

```

### Arguments by Reference

Passing an argument passes a reference to a variable in memory rather than a copy. For mutable objects like lists, modifications inside the function affect the original variable outside:

```python
def changeme(mylist):
    mylist.append([1,2,3,4])
    print("Inside:", mylist)

mylist = [10, 20, 30]
changeme(mylist)
# Outside the function, mylist is also modified: [10, 20, 30, [1, 2, 3, 4]]

```

### Argument Types

* **Positional:** Matched from left to right (`add(1, 2)`).
* **Keyword:** `name=value` syntax (`add(a=1, b=2)`).
* **Default Arguments:** Parameters can have default values (`def add(a, b=2):`).
* **Arbitrary Arguments (`*args`, `**kwargs`):** Captures variable numbers of positional or keyword arguments.

```python
def echo(a, b, c=3, *args, **kwargs):
    print(a, b, c, args, kwargs)

echo(1, 2, 3, 4, 5, d=6)
# Output: 1 2 3 (4, 5) {'d': 6}

```

### Input and Output (`input`, `print`)

```python
# Reading space-separated integers into a list
l = list(map(int, input('--> ').split()))

# Reading JSON data into a dictionary
import json
d = json.loads(input('Input dict:'))

```