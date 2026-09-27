## 1. Exceptions & Error Handling

* **Exception:** An error that occurs during the execution of a program, interrupting the normal flow.
* **Exception Handler:** A piece of code that saves execution state, intercepts the error, handles it, and optionally allows the program to continue.

### Standard Exception Structure

```python
try:
    # Operations that might raise an exception
    pass
except Exception1 as exc:
    # Handle Exception1
except (Exception2, Exception3):
    # Handle Exception2 or Exception3
else:
    # Executed if no exception occurs
finally:
    # Always executed, regardless of exceptions

```

### Exception Arguments

You can capture exception details using the `as` keyword:

```python
def temp_convert(var):
    try:
        return int(var)
    except ValueError as argument:
        print("The argument does not contain numbers:", argument)

temp_convert("xyz")

```

### Raising Exceptions

Use the `raise` keyword to explicitly trigger an error:

```python
def check_level(level):
    if level < 1:
        raise Exception("Invalid level! %s" % level)

```

### Custom Exceptions

Create a custom exception by inheriting from built-in exceptions like `RuntimeError`:

```python
class NetworkError(RuntimeError):
    def __init__(self, message):
        self.message = message

try:
    raise NetworkError("Bad hostname")
except NetworkError as e:
    print(e.message)

```

---

## 2. Debugging and Logging

* **Logging:** Provides a persistent record of application flow, states, and errors. Superior to stack traces for tracking application history and performance.

### Python `logging` Module

Supports five standard log levels (from lowest to highest severity):

1. `logging.debug('message')`
2. `logging.info('message')`
3. `logging.warning('message')`
4. `logging.error('message')`
5. `logging.critical('message')`

### Configuration Example

```python
import logging

logging.basicConfig(
    filename='app.log', 
    filemode='w',
    level=logging.INFO,
    format='%(name)s - %(levelname)s - %(message)s'
)
logging.error('This will get logged to a file')

```

---

## 3. Python Debugger (PDB)

Python's built-in command-line debugger is ideal for remote or headless environments (e.g., Docker containers).

### Running PDB via Terminal

```bash
$ python -m pdb debug.py

```

### Common PDB Commands

* **`n` (next):** Execute until the next line in the current function is reached (steps over function calls).
* **`s` (step):** Execute the next line, stepping *into* called functions.
* **`p` (print):** Evaluate an expression in the current context and print its value (e.g., `(Pdb) p a, b`).
* **`c` (continue):** Resume normal execution until a breakpoint is hit.
* **`q` (quit):** Abort and exit the debugger.

### Inline Breakpoints with `pdb.set_trace()`

```python
import pdb

a = "aaa"
pdb.set_trace()  # Execution pauses here
b = "bbb"

```

---

## 4. Configuration Management with Jinja2

* **Jinja2:** A powerful Python-based templating engine used to generate dynamic configuration files across multiple servers.

### Template Tags

* `{{ var }}` : Embeds variables and prints their evaluated values.
* `{% statement %}` : Control statements (e.g., loops, `if-else`).
* `{# comment #}` : Comments describing tasks.

### Basic YAML Integration Example

```python
import yaml
from jinja2 import Template

# Load data from YAML
with open('data.yml') as data_file:
    config_data = yaml.load(data_file, Loader=yaml.FullLoader)

# Read template file
with open('vhosts.j2') as template_file:
    template_content = template_file.read()

# Render template with config data
template = Template(template_content)
vhosts_conf = template.render(config_data)

with open('vhosts.conf', 'w') as vhosts_file:
    vhosts_file.write(vhosts_conf)

```

### Jinja Control Structures in Templates

* **If-Statement:**
```jinja
{% if serveradmin %}
  ServerAdmin {{ serveradmin }}
{% endif %}

```


* **For-Loop:**
```jinja
{% for vhost in apache_vhosts %}
    <VirtualHost *:80>
        ServerName {{ vhost.servername }}
    </VirtualHost>
{% endfor %}

```



---

## 5. Python Web Application Architecture

Backend Python web apps rely on a three-tier architecture:

1. **Web Server Layer (e.g., Apache, Nginx):** Receives HTTP requests, serves static files (images, CSS), and returns responses.
2. **WSGI Server Layer (e.g., Gunicorn, uWSGI):** Web Server Gateway Interface. Bridges the gap between the web server and the application framework.
* *Benefits:* Low coupling (flexibility) and efficient request scaling.


3. **Web Application Framework Layer (e.g., Flask, Django):** Implements business logic, routing, templates, and ORM systems.

---

## 6. Flask Web Framework

* **Flask:** A lightweight, micro web application framework for Python.

### "Hello World" Example

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()

```

*Run using:* `python start.py`, then open `[http://127.0.0.1:5000/](http://127.0.0.1:5000/)` in your browser.

---

## 7. HTTP Methods & The `requests` Library

### HTTP Methods Overview

* **GET:** Requests data from a specified resource.
* **POST:** Sends data to create a resource (not idempotent).
* **PUT:** Sends data to create or update a resource (idempotent: repeating produces the same result).
* **DELETE:** Deletes a specified resource.

### Using the `requests` Library

```python
import requests

# GET request with parameters and authentication
response = requests.get(
    'https://api.github.com/user', 
    params={'key1': 'value1'},
    auth=('user', 'pass')
)

if response.status_code == 200:
    print('Success!')
    data = response.json()  # Parse JSON response body
elif response.status_code == 404:
    print('Not Found.')

```

### Parsing Nested JSON

If `j = [{"name": "cat", "items": [{"num": 1, "price": 30}, {"num": 2, "price": 50}]}]`:

```python
# How to get the price where num = 2
price = j[0]["items"][1]["price"]  # Returns 50

```