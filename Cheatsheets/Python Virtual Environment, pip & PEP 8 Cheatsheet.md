
# Python Virtual Environment, pip & PEP 8 Cheatsheet

## 1. Python Version

```bash
# Check Python version
python --version
python3 --version

# Find Python location
which python
which python3

# Check pip version
pip --version
pip3 --version

# Python installation details
python3 -c "import sys; print(sys.executable)"
python3 -c "import sys; print(sys.version)"
```

## 2. Virtual Environment (venv)

```bash
# Create virtual environment
python3 -m venv venv

# Create with custom name
python3 -m venv myenv

# Activate on macOS / Linux
source venv/bin/activate

# Activate on Windows (CMD)
venv\Scripts\activate.bat

# Activate on Windows (PowerShell)
venv\Scripts\Activate.ps1

# Check active Python
which python

# Check active environment
echo $VIRTUAL_ENV

# Deactivate environment
deactivate
```

## 3. Virtual Environment Management

```bash
# Create environment
python3 -m venv venv

# Activate
source venv/bin/activate

# Deactivate
deactivate

# Delete environment (macOS / Linux)
rm -rf venv

# Recreate environment
python3 -m venv venv

# Create environment using a specific Python version
python3.12 -m venv venv

# List Python versions (macOS with Homebrew)
ls /opt/homebrew/bin/python*
```

## 4. pip Basics

```bash
# Check pip version
pip --version

# Install package
pip install requests

# Install specific version
pip install requests==2.32.3

# Install minimum version
pip install "requests>=2.30"

# Upgrade package
pip install --upgrade requests

# Uninstall package
pip uninstall requests

# Install multiple packages
pip install requests flask numpy pandas

# Install all packages from requirements
pip install -r requirements.txt

# Show package details
pip show requests

# List installed packages
pip list

# List outdated packages
pip list --outdated

# Check dependencies
pip check
```

## 5. pip Upgrade and Maintenance

```bash
# Upgrade pip
python -m pip install --upgrade pip

# Upgrade pip using Python 3
python3 -m pip install --upgrade pip

# Upgrade setuptools
python -m pip install --upgrade setuptools

# Upgrade wheel
python -m pip install --upgrade wheel

# Install package without cache
pip install --no-cache-dir requests

# Clear pip cache
pip cache purge

# Show pip cache location
pip cache dir
```

## 6. requirements.txt

```bash
# Save installed packages
pip freeze > requirements.txt

# Install packages from file
pip install -r requirements.txt

# Show installed packages
pip freeze

# Generate requirements file
pip freeze > requirements.txt

# Install a specific version from requirements
pip install -r requirements.txt

# Uninstall packages listed in requirements
pip uninstall -r requirements.txt -y
```

Example `requirements.txt`:

```text
requests==2.32.3
flask==3.1.0
numpy==2.2.0
pandas==2.2.3
```

## 7. Installing Packages from Different Sources

```bash
# Install from PyPI
pip install requests

# Install from GitHub
pip install git+https://github.com/user/repository.git

# Install a specific Git branch
pip install git+https://github.com/user/repository.git@main

# Install local package
pip install .

# Install local package in editable mode
pip install -e .

# Install from wheel
pip install package.whl

# Install from source archive
pip install package.tar.gz
```

## 8. pip Search and Package Information

```bash
# Show package information
pip show numpy

# List packages
pip list

# List outdated packages
pip list --outdated

# Check package dependencies
pip check

# Show installed package locations
pip show -f requests

# Export installed packages
pip freeze
```

## 9. Python Package Management Best Practices

```bash
# Create environment
python3 -m venv .venv

# Activate
source .venv/bin/activate

# Upgrade pip
python -m pip install --upgrade pip

# Install dependencies
pip install requests

# Save dependencies
pip freeze > requirements.txt

# Install dependencies on another machine
pip install -r requirements.txt

# Deactivate
deactivate
```

## 10. Virtual Environment Project Structure

```text
my_project/
│
├── .venv/
│
├── src/
│   └── main.py
│
├── tests/
│   └── test_main.py
│
├── requirements.txt
├── .gitignore
└── README.md
```

Example `.gitignore`:

```gitignore
# Virtual environments
venv/
.venv/
env/

# Python cache
__pycache__/
*.py[cod]

# Environment variables
.env

# Test and coverage
.pytest_cache/
.coverage
htmlcov/

# Build files
build/
dist/
*.egg-info/
```

---

# Python PEP 8 Cheatsheet

## 11. What is PEP 8?

PEP 8 is the official Python style guide. It defines conventions for writing readable and consistent Python code.

## 12. Indentation

```python
# Correct: 4 spaces
def greet():
    print("Hello")

# Incorrect
def greet():
  print("Hello")
```

## 13. Variable Naming

```python
# Variables: snake_case
user_name = "Manish"
total_marks = 90

# Constants: UPPER_CASE
MAX_SIZE = 100
PI = 3.14159

# Avoid
userName = "Manish"
TotalMarks = 90
```

## 14. Function Naming

```python
# Correct
def calculate_total():
    pass

def get_user_details():
    pass

# Avoid
def CalculateTotal():
    pass

def GetUserDetails():
    pass
```

## 15. Class Naming

```python
# Classes: PascalCase
class UserProfile:
    pass

class StudentDetails:
    pass
```

## 16. Module and Package Naming

```text
# Module names: lowercase
user.py
database.py
calculator.py

# Package names: lowercase
my_package/
user_management/
```

## 17. Line Length

```python
# Keep lines within 79 characters where practical

# Correct
total = calculate_total(
    price,
    quantity,
    discount
)

# Avoid very long lines
total = calculate_total(price, quantity, discount, tax, shipping, extra_charges)
```

## 18. Blank Lines

```python
import os


MAX_SIZE = 100


def calculate_total():
    return 100


def calculate_average():
    return 50


class Student:
    pass
```

- Two blank lines between top-level functions and classes.
- One blank line between methods inside a class.
- Use blank lines to separate logical sections.

## 19. Import Rules

```python
# Standard library imports
import os
import sys

# Third-party imports
import numpy as np
import pandas as pd

# Local application imports
from my_package import helper
from my_package.user import User

# Avoid wildcard imports
from module import *
```

## 20. Import Ordering

```python
# 1. Standard library
import os
import sys
from pathlib import Path

# 2. Third-party libraries
import numpy as np
import requests

# 3. Local application imports
from app.database import connect
from app.models import User
```

## 21. Spaces Around Operators

```python
# Correct
x = 10
total = price + tax
result = a * b

# Avoid
x=10
total=price+tax
result=a*b
```

## 22. Spaces in Function Arguments

```python
# Correct
def calculate(a, b):
    return a + b

result = calculate(10, 20)

# Avoid
def calculate( a,b ):
    return a+b
```

## 23. Avoid Unnecessary Spaces

```python
# Correct
arr = [1, 2, 3]
user = {"name": "Manish", "age": 21}

# Avoid
arr = [ 1,2,3 ]
user = {"name" : "Manish"}
```

## 24. String Quotes

```python
name = "Manish"
message = 'Hello World'

# Use one style consistently.
# Choose double or single quotes based on readability.
```

## 25. Comments

```python
# Calculate the total price
total = price * quantity

# Avoid unnecessary comments
x = 10  # Assign 10 to x
```

## 26. Docstrings

```python
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.

    Args:
        length: Rectangle length.
        width: Rectangle width.

    Returns:
        The calculated area.
    """
    return length * width
```

## 27. Boolean Comparisons

```python
# Correct
if is_active:
    print("Active")

if not is_active:
    print("Inactive")

if value is None:
    print("No value")

# Avoid
if is_active == True:
    print("Active")

if value == None:
    print("No value")
```

## 28. Checking Empty Collections

```python
arr = []

# Correct
if not arr:
    print("Empty")

if arr:
    print("Not empty")

# Avoid
if len(arr) == 0:
    print("Empty")
```

## 29. Exception Handling

```python
# Correct
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")

# Avoid catching every exception unnecessarily
try:
    result = 10 / 0
except:
    pass
```

## 30. Context Managers

```python
# Correct
with open("data.txt", "r") as file:
    data = file.read()

# Avoid manually managing files when not necessary
file = open("data.txt", "r")
data = file.read()
file.close()
```

## 31. List Comprehension

```python
# Correct
squares = [x * x for x in range(10)]

# Avoid unnecessary complexity
squares = []

for x in range(10):
    squares.append(x * x)
```

## 32. Avoid Mutable Default Arguments

```python
# Avoid
def add_item(item, items=[]):
    items.append(item)
    return items

# Correct
def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)
    return items
```

## 33. F-Strings

```python
name = "Manish"
age = 21

# Correct
print(f"My name is {name} and I am {age}")

# Avoid unnecessary concatenation
print("My name is " + name)
```

---

# Python Code Formatting and Linting Tools

## 34. Black

Black automatically formats Python code.

```bash
# Install
pip install black

# Format one file
black main.py

# Format entire project
black .

# Check formatting without modifying
black --check .

# Show formatting differences
black --diff main.py
```

## 35. Flake8

Flake8 checks code style and common errors.

```bash
# Install
pip install flake8

# Check one file
flake8 main.py

# Check entire project
flake8 .

# Set maximum line length
flake8 --max-line-length=79 .
```

## 36. Ruff

Ruff is a fast Python linter and formatter.

```bash
# Install
pip install ruff

# Check code
ruff check .

# Fix automatically
ruff check --fix .

# Format code
ruff format .

# Check formatting
ruff format --check .

# Check one file
ruff check main.py
```

## 37. isort

isort organizes Python imports.

```bash
# Install
pip install isort

# Sort imports in a file
isort main.py

# Sort imports in entire project
isort .

# Check imports
isort --check-only .
```

## 38. mypy

mypy checks static types.

```bash
# Install
pip install mypy

# Check one file
mypy main.py

# Check project
mypy .
```

Example:

```python
def add(a: int, b: int) -> int:
    return a + b

result = add(10, 20)
```

## 39. pytest

```bash
# Install
pip install pytest

# Run all tests
pytest

# Verbose output
pytest -v

# Run specific file
pytest test_main.py

# Run specific test
pytest test_main.py::test_add

# Stop after first failure
pytest -x

# Show print statements
pytest -s

# Run with coverage
pip install pytest-cov
pytest --cov
```

## 40. py_compile

```bash
# Compile one Python file
python -m py_compile main.py

# Compile all Python files in a directory
python -m compileall .
```

---

# Python Project Workflow

## 41. Start a New Project

```bash
# Create project folder
mkdir my_project

# Enter project folder
cd my_project

# Create virtual environment
python3 -m venv .venv

# Activate environment
source .venv/bin/activate

# Upgrade pip
python -m pip install --upgrade pip

# Install dependencies
pip install requests

# Save dependencies
pip freeze > requirements.txt

# Create Python file
touch main.py

# Run Python file
python main.py

# Deactivate environment
deactivate
```

## 42. Daily Development Workflow

```bash
# Activate environment
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Run application
python main.py

# Run tests
pytest -v

# Check linting
ruff check .

# Format code
ruff format .

# Save dependencies
pip freeze > requirements.txt

# Deactivate
deactivate
```

## 43. Common Errors and Fixes

```bash
# Error: pip command not found
python3 -m pip --version

# Error: No module named venv (Debian/Ubuntu)
sudo apt install python3-venv

# Error: Permission denied
# Prefer installing inside a virtual environment.

# Error: Module not found
python -m pip install package_name

# Check which Python is running
which python

# Check where package is installed
python -m pip show package_name

# Check active environment
echo $VIRTUAL_ENV

# Recreate broken environment
rm -rf .venv
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

---

# Quick Reference

| Task | Command |
|---|---|
| Create environment | `python3 -m venv .venv` |
| Activate (Mac/Linux) | `source .venv/bin/activate` |
| Deactivate | `deactivate` |
| Delete environment | `rm -rf .venv` |
| Check Python | `python --version` |
| Check pip | `python -m pip --version` |
| Install package | `python -m pip install package` |
| Uninstall package | `python -m pip uninstall package` |
| Upgrade pip | `python -m pip install --upgrade pip` |
| List packages | `python -m pip list` |
| Save dependencies | `python -m pip freeze > requirements.txt` |
| Install dependencies | `python -m pip install -r requirements.txt` |
| Package details | `python -m pip show package` |
| Format code | `ruff format .` |
| Lint code | `ruff check .` |
| Fix lint issues | `ruff check --fix .` |
| Run tests | `pytest -v` |
| Check types | `mypy .` |
| Sort imports | `isort .` |
| Compile code | `python -m compileall .` |
