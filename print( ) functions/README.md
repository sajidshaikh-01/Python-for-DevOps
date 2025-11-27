# Python `print()` Function – README

This README explains the Python `print()` function with examples, formatting, escape characters, parameters, and best practices. You can directly upload this file to your GitHub.

---

## 📌 What is `print()` in Python?

The `print()` function is used to display output on the screen. It helps you show messages, variables, results of expressions, and debugging information.

---

## 📌 Basic Syntax

```python\print(object, sep=' ', end='\n', file=None, flush=False)
```

### Parameters:

* **object** → The value(s) you want to print
* **sep** → Separator between multiple values (default: space)
* **end** → What to print at the end (default: new line `\n`)
* **file** → Output stream (default: screen)
* **flush** → Force flush the stream

---

## ✅ Basic Examples

```python
print("Hello World")
print(10)
print("Python is awesome!")
```

Output:

```
Hello World
10
Python is awesome!
```

---

## ✅ Printing Multiple Values

```python
print("Name:", "Sajid", "Age:", 22)
```

Output:

```
Name: Sajid Age: 22
```

---

## ✅ Using `sep` Argument

```python
print("2025", "11", "27", sep="-")
```

Output:

```
2025-11-27
```

---

## ✅ Using `end` Argument

```python
print("Hello", end=" ")
print("World")
```

Output:

```
Hello World
```

(Default new line is replaced with space)

---

## ✅ Printing Variables

```python
name = "Sajid"
age = 22
print("Name:", name)
print("Age:", age)
```

---

## ✅ f-Strings (Recommended)

```python
name = "Sajid"
role = "DevOps Engineer"
print(f"My name is {name} and I am a {role}.")
```

---

## 📌 Escape Characters

| Escape | Meaning      |
| ------ | ------------ |
| `\n`   | New line     |
| `\t`   | Tab space    |
| `\\`   | Backslash    |
| `\"`   | Double quote |

Example:

```python
print("Hello\nWorld")
```

---

## 📌 Printing Without New Line

```python
print("Loading...", end="")
```

---

## 📌 Printing in Loops

```python
for i in range(5):
    print(i)
```

---

## 📌 Printing Lists and Dictionaries

```python
my_list = [1, 2, 3]
print(my_list)

my_dict = {"name": "Sajid", "age": 22}
print(my_dict)
```

---

## 📌 Debugging with print()

```python
x = 10
y = 20
print("x:", x, "y:", y)
```

---

## 📌 Best Practices

* Use **f-strings** for clean formatting
* Avoid too many print statements in production code
* Use `print()` mainly for learning and debugging

---

## 📘 Summary

* `print()` displays output to the screen
* Supports multiple values, formatting, and custom endings
* Useful for debugging and learning Python

---

## 📎 Example Output File Name

You can save this as:

```
README_PRINT_FUNCTION.md
```
