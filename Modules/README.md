# Python Modules – README
---

# 📌 What is a Module?

A **module** in Python is simply a file that contains Python code (functions, variables, classes).

A module = `filename.py`

Example:

```
math.py
os.py
my_module.py
```

---

# 📌 Why Use Modules?

Modules help you:

* Organize code
* Reuse functions
* Avoid writing code again
* Keep project clean and readable

---

# 📌 Types of Modules

1. **Built-in Modules** (already provided by Python)

   * `math`
   * `os`
   * `random`
   * `datetime`

2. **User-Defined Modules** (you create your own `.py` files)

3. **Third-Party Modules** (installed using pip)

   * `numpy`
   * `requests`
   * `pandas`

---

# 📌 Importing a Module

## ✔ Basic import

```python
import math
print(math.sqrt(25))
```

---

## ✔ Import with alias

```python
import math as m
print(m.pi)
```

---

## ✔ Import only specific functions

```python
from math import sqrt, pi
print(sqrt(16))
print(pi)
```

---

## ✔ Import all functions (not recommended)

```python
from math import *
```

---

# 📌 Built-in Module Examples

## 1️⃣ `math` Module

```python
import math
print(math.factorial(5))
print(math.pi)
print(math.sin(0))
```

## 2️⃣ `random` Module

```python
import random
print(random.randint(1, 10))
print(random.choice([10, 20, 30]))
```

## 3️⃣ `datetime` Module

```python
from datetime import datetime
now = datetime.now()
print(now)
```

## 4️⃣ `os` Module

```python
import os
print(os.getcwd())   # current directory
os.mkdir("test_folder")
```

---

# 📌 Creating Your Own Module

Create a file named **my_module.py**:

```python
# my_module.py

def greet(name):
    print(f"Hello {name}")

x = 100
```

Use it in another file:

```python
import my_module

my_module.greet("Sajid")
print(my_module.x)
```

---

# 📌 `__name__ == "__main__"`

Used to run code only when file is executed directly.

```python
def add(a, b):
    return a + b

if __name__ == "__main__":
    print(add(5, 3))
```

---

# 📌 Installing Third-Party Modules

Use pip:

```bash
pip install requests
```

Example:

```python
import requests
response = requests.get("https://google.com")
print(response.status_code)
```

---

# 📘 Summary

| Topic                | Description                    |
| -------------------- | ------------------------------ |
| Module               | A Python file containing code  |
| import               | Used to load modules           |
| Built-in modules     | Provided by Python             |
| User-defined modules | You create your own `.py` file |
| Third-party          | Installed using pip            |

---

## 📎 Suggested File Name

```
READ
```
