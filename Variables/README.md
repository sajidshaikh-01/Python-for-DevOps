# Python Variables – README

This README explains Python variables with definitions, rules, types, examples, and best practices. You can upload this file directly to your GitHub.

---

## 📌 What is a Variable?

A **variable** in Python is a name that stores a value in memory.
It acts like a container where you put data.

Example:

```python
x = 10
name = "Sajid"
```

Here:

* `x` stores **10**
* `name` stores **"Sajid"**

---

## 📌 How Variables Work

Python automatically decides the data type based on the value you assign.

Example:

```python
a = 10          # integer
b = 3.14        # float
c = "Python"    # string
```

---

## 📌 Rules for Writing Variables

| Rule                                      | Example              |
| ----------------------------------------- | -------------------- |
| Must start with a letter or underscore    | `name`, `_value`     |
| Cannot start with a number                | ❌ `1name`            |
| Can contain letters, numbers, underscores | `first_name`, `age1` |
| Case sensitive                            | `Name` ≠ `name`      |
| Cannot use keywords                       | ❌ `class = 10`       |

---

## 📌 Good Variable Names

```python
age = 25
user_name = "Sajid"
total_amount = 5000
```

Bad examples:

```python
a = 25       # Not meaningful
x1 = 100     # Confusing name
```

---

## 📌 Assigning Multiple Variables

### ✔ Same Value to Multiple Variables

```python
a = b = c = 10
```

### ✔ Multiple Values to Multiple Variables

```python
name, age, country = "Sajid", 22, "India"
```

---

## 📌 Changing (Updating) Variables

```python
x = 10
x = 20   # updated value
```

---

## 📌 Types of Variables

Python has three main categories:

### 1️⃣ Numeric Variables

```python
x = 10          # int
y = 3.14        # float
z = 3 + 4j      # complex
```

### 2️⃣ String Variables

```python
name = "Sajid"
```

### 3️⃣ Boolean Variables

```python
is_active = True
```

---

## 📌 Checking Variable Type

Use `type()` function:

```python
x = 10
print(type(x))
```

Output:

```
<class 'int'>
```

---

## 📌 Variable Casting (Converting Types)

```python
x = int(5.9)      # 5
y = float(10)     # 10.0
z = str(100)      # "100"
```

---

## 📌 Example Program

```python
name = "Sajid"
age = 22
is_devops = True

print(f"Name: {name}")
print(f"Age: {age}")
print(f"DevOps Engineer: {is_devops}")
```

---

## 📌 Best Practices

* Use meaningful names
* Use lowercase with underscores → `snake_case`
* Avoid single-letter names except in loops
* Never use Python keywords

---

## 📘 Summary

| Topic                 | Description                      |
| --------------------- | -------------------------------- |
| Variable              | Container for storing data       |
| No declaration needed | Python auto-detects type         |
| Can reassign          | Variables can be updated anytime |
| Use `type()`          | To check data type               |
| Follow naming rules   | Use meaningful names             |

---

## 📎 Output File Name

```
README_VARIABLES.md
```

