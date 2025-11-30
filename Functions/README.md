# Python Functions – README

This README explains Python **functions** with definitions, syntax, types, parameters, return values, scope, lambda functions, and examples. You can upload this file directly to GitHub.

---

# 📌 What is a Function?

A **function** is a block of reusable code that performs a specific task.
Functions help make your code:

* Clean
* Reusable
* Easy to manage
* More efficient

---

# 📌 Why Use Functions?

* Avoid repeating code
* Break large programs into smaller parts
* Improve readability
* Make debugging easier

Example:

```python
def greet():
    print("Hello, Python!")

greet()
```

---

# 📌 Function Syntax

```python
def function_name(parameters):
    # function body
    return value
```

---

# 📌 Types of Functions

1. **Built-in functions** → `print()`, `len()`, `type()` etc.
2. **User-defined functions** → Functions you create.

---

# 📌 User-Defined Function Example

```python
def say_hello():
    print("Hello, Sajid!")

say_hello()
```

---

# 📌 Function With Parameters

```python
def welcome(name):
    print(f"Welcome, {name}!")

welcome("Sajid")
```

---

# 📌 Function With Two Parameters

```python
def add(a, b):
    print(a + b)

add(10, 20)
```

---

# 📌 Function With Return Value

```python
def multiply(a, b):
    return a * b

result = multiply(5, 6)
print(result)
```

---

# 📌 Default Parameters

```python
def greet(name="User"):
    print(f"Hello, {name}")

greet()
greet("Sajid")
```

---

# 📌 Keyword Arguments

```python
def student(name, age):
    print(name, age)

student(age=22, name="Sajid")
```

---

# 📌 Arbitrary Arguments (`*args`)

Used when you don’t know number of arguments.

```python
def total(*numbers):
    print(sum(numbers))

total(10, 20, 30)
```

---

# 📌 Arbitrary Keyword Arguments (`**kwargs`)

```python
def info(**data):
    print(data)

info(name="Sajid", age=22, role="DevOps")
```

---

# 📌 Lambda (Anonymous) Functions

Short one-line functions.

```python
square = lambda x: x * x
print(square(5))
```

---

# 📌 Function Scope

### Local Variable

```python
def test():
    x = 10
    print(x)

test()
```

### Global Variable

```python
x = 100

def show():
    print(x)

show()
```

---

# 📌 Nested Functions

```python
def outer():
    def inner():
        print("Inside inner function")
    inner()

outer()
```

---

# 📌 Docstring (Function Documentation)

```python
def add(a, b):
    """This function adds two numbers"""
    return a + b

print(add.__doc__)
```

---

# 📘 Summary

| Concept    | Meaning                      |
| ---------- | ---------------------------- |
| Function   | Reusable block of code       |
| Parameters | Inputs to function           |
| Return     | Sends value back             |
| *args      | Multiple arguments           |
| **kwargs   | Multiple key/value arguments |
| Lambda     | One-line function            |

---

