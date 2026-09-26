## 1. Global vs. Local Variables

* **Global Variables:** Defined outside any function; have a global scope and can be accessed throughout the program and inside every function.
* **Local Variables:** Defined inside a function; their scope is limited strictly to that function.

```python
total = 0  # Global variable

def sum_func(arg1, arg2):
    """Add both parameters and return them."""
    total = arg1 + arg2  # Local variable
    print("Inside the function:", total)
    return total

sum_func(10, 20)
print("Outside the function:", total)

```

**Output:**

```text
Inside the function: 30
Outside the function: 0

```

### The `global` Keyword

* Python assumes a variable is local if an assignment happens inside a function, unless it is declared using the `global` keyword.
* The `global` keyword is only needed when you want to modify or assign a global variable inside a function; it is **not** required just to read or print it.

```python
money = 2000

def add_money():
    global money
    money = money + 1
    print(money)

add_money()
print(money)

```

---

## 2. Name Resolution: The LEGB Rule

Scope determines the visibility of a variable. Python resolves names using the **LEGB** rule, which stands for the sequence of search steps:

1. **L - Local:** Names assigned in any way within a function (def or lambda).
2. **E - Enclosing:** Names in the local scope of any and all statically enclosing functions (e.g., closures/nested functions).
3. **G - Global:** Names assigned at the top-level of a module or declared global in a def.
4. **B - Built-in:** Names preassigned in the Python built-in module (e.g., `print`, `len`).

---

## 3. Anonymous Functions (`lambda`)

* Small, anonymous functions defined with the `lambda` keyword.
* Can take any number of arguments, but can **only have one expression**.

```python
# Function definition
sum_lambda = lambda a, b: a + b

# Calling the lambda function
print("sum :", sum_lambda(10, 20)) 
print("sum :", sum_lambda(20, 20))

```

---

## 4. Namespace Introspection: `globals()` and `locals()`

* **`globals()`:** Returns a dictionary containing variables defined in the global namespace.
* **`locals()`:** Returns a dictionary containing variables defined in the local namespace.

```python
>>> q = lambda: locals()
>>> q()
{}

>>> def q():
...     qwert = 1
...     print(locals())
...
>>> q()
{'qwert': 1}

```

---

## 5. Object-Oriented Programming: Classes

* **Classes:** User-defined data structures acting as blueprints for creating objects.
* **`__init__()` method:** Initializes each new instance of a class. The first parameter is always `self`, which represents the newly created object instance.

```python
class Employee:
    """Common base class for all employees"""
    empCount = 0

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
        Employee.empCount += 1

    def displayCount(self):
        print("Total Employee %d" % Employee.empCount)

    def displayEmployee(self):
        print("Name :", self.name, ", Salary:", self.salary)

# Creating instances
emp1 = Employee("Slave", 200)
emp2 = Employee("Master", 5000)

emp1.displayEmployee()
emp2.displayEmployee()
print("Total Employee %d" % Employee.empCount)

```

### Attribute Modification Built-in Functions

* `hasattr(obj, 'attr')` — Returns `True` if the attribute exists.
* `getattr(obj, 'attr')` — Returns the value of the attribute.
* `setattr(obj, 'attr', value)` — Sets or adds the attribute.
* `delattr(obj, 'attr')` — Deletes the attribute.

---

## 6. Inheritance & Method Resolution Order (MRO)

* Inheritance allows a class (child/derived class) to inherit methods and properties from another class (parent/base class).
* **MRO (Method Resolution Order):** Python looks up methods/attributes from **bottom to top and left to right**.

```python
class Base1:
    def fun(self):
        print("base1.fun")

class Base2:
    def jump(self):
        print("base2.jump")

class Child(Base1, Base2):
    def fun(self):
        print("child.fun")
        super().fun()

c = Child()
c.fun()   # child.fun -> base1.fun
c.jump()  # base2.jump

```

---

## 7. Private Variables & Name Mangling

* Python uses a convention: names prefixed with a single underscore (`_spam`) indicate non-public parts of an API.
* **Name Mangling:** Identifiers starting with at least two leading underscores and at most one trailing underscore (e.g., `__secretCount`) are automatically textually replaced with `_ClassName__secretCount` within a class definition to prevent name collisions with subclasses.

```python
class JustCounter:
    __secretCount = 0

    def count(self):
        self.__secretCount += 1
        print(self.__secretCount)

counter = JustCounter()
counter.count()  # 1
counter.count()  # 2

# print(counter.__secretCount)  # Raises AttributeError
print(counter._JustCounter__secretCount)  # 2

```

---

## 8. Magic Methods & Operator Overloading

* **Magic Methods:** Special methods starting and ending with double underscores (dunder methods). They are invoked internally by Python upon specific actions (e.g., `+` calls `__add__()`).

```python
class Vector:
    def __init__(self, a, b):
        self.a = a
        self.b = b

    def __str__(self):
        return f'Vector ({self.a}, {self.b})'

    def __add__(self, other):
        return Vector(self.a + other.a, self.b + other.b)

v1 = Vector(2, 10)
v2 = Vector(5, -2)
print(v1 + v2)  # Calls __str__ implicitly

```

---

## 9. Modules & Imports

* A module is a file containing Python code ending with `.py`. The module's name is available in the global variable `__name__`.

### Import Variants

```python
import hello
hello.print_module_name()

from hello import print_module_name
print_module_name()

import hello as bye
bye.print_module_name()

```

### The `if __name__ == "__main__"` Guard

* If a module is run directly (`python some_module.py`), `__name__` is set to `'__main__'`.
* If it is imported, `__name__` is set to the module's file name.

```python
print("Always executed")

if __name__ == "__main__":
    print("Executed when invoked directly")
else:
    print("Executed when imported")

```

### Module Search Path & Introspection

* **`sys.path`**: A list of directories where Python searches for modules during an `import`.
* **`dir(module)`**: Returns a list of names defined in a module's local scope.

---

## 10. File Handling & Directory Operations

### Opening and Reading Files

```python
# Write to file
with open("foo.txt", "w") as fo:
    fo.write("Explicit is better than implicit.\nSimple is better than complex.\n")

# Read entire file
with open("foo.txt") as fo:
    print(fo.read())

# Read line by line
with open("foo.txt") as fo:
    for line in fo:
        print(line, end="")

# Read lines into a list
with open("foo.txt") as fo:
    lines = fo.readlines()
    print(lines)

```

### File and Directory Manipulation (`os` module)

```python
import os

# Rename file
os.rename("test1.txt", "test2.txt")

# Remove file
os.remove("test2.txt")

# Directory operations
print(os.getcwd())
os.chdir("/tmp")
os.mkdir("app_dir")
os.rmdir("app_dir")

```

---

## 11. Packages, Setup, and Distribution

Packages use hierarchical file structures with `__init__.py` files to organize modules using dot notation.

### `setup.py` Example

```python
from setuptools import setup, find_packages

setup(
    name="zoo-example",
    packages=find_packages(),
    entry_points={
        "console_scripts": [
            "zoo = animals.zoo:main",
        ],
    },
    install_requires=[
        "termcolor==1.1.0",
    ],
    version="0.1",
    author="Captain Jack",
    author_email="captain_jack@gmail.com",
    description="Example of the test application",
    license="MIT"
)

```

### Building Distributions

* **Egg:** `python setup.py bdist_egg`
* **Wheel:** `python setup.py bdist_wheel`
* **Universal Wheel:** `python setup.py bdist_wheel --universal`
* **Source Archive:** `python setup.py sdist`

---

## 12. Package Management with `pip`

* **Install package:** `$ pip install <package_name>`
* **Upgrade package:** `$ pip install --upgrade <package_name>`
* **Install specific version:** `$ pip install <package_name>=='version_num'`
* **Install via criteria:** `$ pip install <package_name> >= 'version_num'`
* **Upgrade pip:** `$ pip install -U pip`
* **Local package installation:** `$ pip install .` or `$ pip install dist/zoo_example-0.1-py3-none-any.whl`
* **Uninstall package:** `$ pip uninstall zoo-example`