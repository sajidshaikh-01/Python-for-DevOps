# Command Line Arguments in Python

This README explains **Command Line Arguments (CLI Args)** in Python with clear examples.
These are heavily used in **DevOps, automation scripts, CI/CD tools, and administration tasks**.

---

# 📌 What Are Command Line Arguments?

Command Line Arguments are inputs passed to a Python script while running it from a terminal.

Example:

```bash
python3 script.py arg1 arg2 arg3


Example 1 — Print All Arguments
import sys
print("All arguments:", sys.argv)
print("Script name:", sys.argv[0])


Example 2 — Add Two Numbers
import sys
num1 = int(sys.argv[1])
num2 = int(sys.argv[2])
print("Sum:", num1 + num2)



| Topic          | Description                            |
| -------------- | -------------------------------------- |
| `sys.argv`     | Basic CLI args for simple scripts      |
| Indexing       | `argv[1]`, `argv[2]` etc.              |
| Error Handling | Check `len(sys.argv)`                  |
| `argparse`     | Best method for professional CLI tools |




