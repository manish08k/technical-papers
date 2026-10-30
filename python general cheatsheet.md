
# Python General Cheatsheet

## 1. PYTHON VERSION & HELP

```bash
python --version
python3 --version
python --help
python3 --help
python -c "print('Hello World')"
python3 -c "print('Hello World')"
which python
which python3
python3 -m pydoc MODULE
```

## 2. PYTHON INTERPRETER

```bash
python
python3
python3 -i FILE.py
python3 -c "print(10 + 20)"
python3 -m MODULE
python3 FILE.py
python3 -u FILE.py
python3 -O FILE.py
python3 -B FILE.py
```

## 3. VARIABLES & DATA TYPES

```python
name = "Manish"
age = 21
height = 170.5
is_student = True

x = 10
y = 20

print(type(name))
print(type(age))
print(type(height))
print(type(is_student))

print(id(x))
print(isinstance(age, int))
print(isinstance(name, str))
```

## 4. TYPE CONVERSION

```python
int("10")
float("10.5")
str(100)
bool(1)

list((1, 2, 3))
tuple([1, 2, 3])
set([1, 2, 2, 3])
dict([("a", 1), ("b", 2)])

ord("A")
chr(65)
bin(10)
oct(10)
hex(10)

abs(-10)
round(10.567, 2)
```

## 5. INPUT & OUTPUT

```python
name = input("Enter name: ")
age = int(input("Enter age: "))

print("Hello", name)
print(f"Name: {name}, Age: {age}")

print("Python", "Java", sep=", ")
print("Hello", end=" ")
print("World")

print("Hello\nWorld")
print("Hello\tWorld")

print("Value: {}".format(100))
print("Name: %s" % name)
```

## 6. OPERATORS

```python
# Arithmetic
a + b
a - b
a * b
a / b
a // b
a % b
a ** b

# Comparison
a == b
a != b
a > b
a < b
a >= b
a <= b

# Logical
a and b
a or b
not a

# Assignment
a = 10
a += 5
a -= 5
a *= 2
a /= 2
a //= 2
a %= 2
a **= 2

# Bitwise
a & b
a | b
a ^ b
~a
a << 1
a >> 1

# Membership
"a" in "apple"
10 in [10, 20]

# Identity
a is b
a is not b
```

## 7. CONDITIONAL STATEMENTS

```python
if condition:
    pass

if condition:
    print("True")
else:
    print("False")

if condition1:
    pass
elif condition2:
    pass
else:
    pass

result = "Pass" if marks >= 40 else "Fail"

match value:
    case 1:
        print("One")
    case 2:
        print("Two")
    case _:
        print("Default")
```

## 8. LOOPS

```python
for i in range(10):
    print(i)

for i in range(1, 10):
    print(i)

for i in range(1, 10, 2):
    print(i)

while condition:
    pass

for item in iterable:
    print(item)

break
continue
pass

for i in range(5):
    if i == 3:
        break
else:
    print("Completed")

for i in range(5):
    print(i)
else:
    print("Loop completed")
```

## 9. RANGE & ENUMERATE

```python
range(10)
range(1, 10)
range(1, 10, 2)

list(range(5))
list(range(1, 11))

enumerate(["a", "b", "c"])
list(enumerate(["a", "b", "c"]))

for index, value in enumerate(["a", "b", "c"]):
    print(index, value)

for index, value in enumerate(["a", "b"], start=1):
    print(index, value)
```

## 10. STRINGS

```python
s = "Hello Python"

len(s)
s.upper()
s.lower()
s.title()
s.capitalize()
s.swapcase()

s.strip()
s.lstrip()
s.rstrip()

s.replace("Python", "Java")
s.split()
s.split(" ")
" ".join(["Hello", "World"])

s.find("Python")
s.index("Python")
s.count("l")

s.startswith("Hello")
s.endswith("Python")

s.isalpha()
s.isdigit()
s.isalnum()
s.isspace()
s.islower()
s.isupper()
s.istitle()

s.center(20)
s.ljust(20)
s.rjust(20)
s.zfill(10)

s[::-1]
s[0]
s[-1]
s[0:5]
s[::2]

"Python" in s
```

## 11. STRING FORMATTING

```python
name = "Manish"
age = 21

f"Name: {name}"
f"Age: {age}"

"Name: {}".format(name)
"Age: {}".format(age)

"Name: %s" % name
"Age: %d" % age

f"{10:.2f}"
f"{1000000:,}"
f"{0.75:.1%}"
f"{name:>20}"
f"{name:<20}"
f"{name:^20}"
```

## 12. LISTS

```python
arr = [10, 20, 30, 40]

arr.append(50)
arr.extend([60, 70])
arr.insert(1, 15)

arr.remove(20)
arr.pop()
arr.pop(0)
arr.clear()

arr.index(30)
arr.count(10)

arr.sort()
arr.sort(reverse=True)
arr.reverse()

sorted(arr)
sorted(arr, reverse=True)

len(arr)
min(arr)
max(arr)
sum(arr)

arr.copy()
arr[:]
arr[0]
arr[-1]
arr[1:3]
arr[::-1]

10 in arr
```

## 13. LIST COMPREHENSION

```python
[x for x in range(10)]

[x for x in range(10) if x % 2 == 0]

[x * x for x in range(10)]

[x.upper() for x in ["a", "b", "c"]]

[x if x > 0 else 0 for x in [-1, 2, -3, 4]]

[(x, y) for x in range(3) for y in range(3)]

[x for row in matrix for x in row]
```

## 14. TUPLES

```python
t = (10, 20, 30)

t[0]
t[-1]
t[1:3]

len(t)
min(t)
max(t)
sum(t)

t.count(10)
t.index(20)

tuple([1, 2, 3])
list(t)

a, b, c = t
```

## 15. SETS

```python
s = {1, 2, 3}

s.add(4)
s.update([5, 6])

s.remove(2)
s.discard(10)
s.pop()
s.clear()

len(s)

a = {1, 2, 3}
b = {3, 4, 5}

a.union(b)
a.intersection(b)
a.difference(b)
a.symmetric_difference(b)

a | b
a & b
a - b
a ^ b

a.issubset(b)
a.issuperset(b)
a.isdisjoint(b)

frozenset([1, 2, 3])
```

## 16. DICTIONARIES

```python
d = {"name": "Manish", "age": 21}

d["name"]
d.get("name")
d.get("city", "Unknown")

d.keys()
d.values()
d.items()

d["city"] = "Bangalore"
d.update({"age": 22})

d.setdefault("country", "India")

d.pop("age")
d.popitem()
d.clear()

del d["name"]

"name" in d
len(d)

d.copy()
dict.fromkeys(["a", "b"], 0)

for key, value in d.items():
    print(key, value)
```

## 17. DICTIONARY COMPREHENSION

```python
{x: x * x for x in range(5)}

{x: x for x in range(10) if x % 2 == 0}

{k: v for k, v in pairs}

{value: index for index, value in enumerate(arr)}
```

## 18. FUNCTIONS

```python
def greet():
    print("Hello")

greet()

def add(a, b):
    return a + b

result = add(10, 20)

def greet(name="User"):
    print("Hello", name)

def calculate(*args):
    return sum(args)

def display(**kwargs):
    print(kwargs)

def function(a, b, /):
    pass

def function(*, a, b):
    pass

def function(a, b, /, c, *, d):
    pass

lambda x: x * 2

square = lambda x: x * x
```

## 19. ARGUMENTS

```python
# Positional arguments
def add(a, b):
    return a + b

add(10, 20)

# Keyword arguments
add(a=10, b=20)

# Default arguments
def greet(name="User"):
    return name

# Variable positional arguments
def total(*args):
    return sum(args)

# Variable keyword arguments
def details(**kwargs):
    return kwargs

# Unpacking
numbers = [10, 20]
add(*numbers)

data = {"a": 10, "b": 20}
add(**data)
```

## 20. LAMBDA, MAP, FILTER & REDUCE

```python
square = lambda x: x * x

map(lambda x: x * 2, [1, 2, 3])

list(map(lambda x: x * 2, [1, 2, 3]))

filter(lambda x: x > 5, [1, 6, 8, 2])

list(filter(lambda x: x > 5, [1, 6, 8, 2]))

from functools import reduce

reduce(lambda a, b: a + b, [1, 2, 3, 4])

reduce(lambda a, b: a * b, [1, 2, 3, 4])
```

## 21. RECURSION

```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

def countdown(n):
    if n == 0:
        return
    print(n)
    countdown(n - 1)
```

## 22. ITERATORS

```python
iter([1, 2, 3])

it = iter([1, 2, 3])

next(it)
next(it)
next(it)

next(it, None)

for item in iter([1, 2, 3]):
    print(item)

iter("Python")
iter(range(5))
```

## 23. GENERATORS

```python
def generate():
    yield 1
    yield 2
    yield 3

gen = generate()

next(gen)
next(gen)

list(generate())

def numbers(n):
    for i in range(n):
        yield i

(x * x for x in range(10))
```

## 24. DECORATORS

```python
def decorator(func):
    def wrapper(*args, **kwargs):
        print("Before")
        result = func(*args, **kwargs)
        print("After")
        return result
    return wrapper

@decorator
def greet():
    print("Hello")

greet()
```

## 25. CLOSURES

```python
def outer():
    message = "Hello"

    def inner():
        print(message)

    return inner

func = outer()
func()
```

## 26. SCOPE & VARIABLES

```python
x = 10

def function():
    global x
    x = 20

def outer():
    x = 10

    def inner():
        nonlocal x
        x = 20

    inner()
    return x
```

## 27. OOP – CLASSES & OBJECTS

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print(self.name, self.age)

p = Person("Manish", 21)
p.display()
```

## 28. INHERITANCE

```python
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    def bark(self):
        print("Bark")

d = Dog()
d.speak()
d.bark()
```

## 29. POLYMORPHISM

```python
class Dog:
    def speak(self):
        print("Bark")

class Cat:
    def speak(self):
        print("Meow")

for animal in [Dog(), Cat()]:
    animal.speak()
```

## 30. ENCAPSULATION

```python
class Bank:
    def __init__(self):
        self.name = "Manish"
        self._balance = 1000
        self.__pin = 1234

    def get_balance(self):
        return self._balance

b = Bank()
print(b.name)
print(b.get_balance())
```

## 31. ABSTRACTION

```python
from abc import ABC, abstractmethod

class Shape(ABC):

    @abstractmethod
    def area(self):
        pass

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side ** 2

s = Square(5)
print(s.area())
```

## 32. CLASS & STATIC METHODS

```python
class Example:

    count = 0

    def instance_method(self):
        return self

    @classmethod
    def class_method(cls):
        return cls.count

    @staticmethod
    def static_method():
        return "Hello"
```

## 33. SPECIAL / DUNDER METHODS

```python
__init__
__str__
__repr__
__len__
__iter__
__next__
__getitem__
__setitem__
__delitem__
__contains__
__call__
__add__
__sub__
__mul__
__eq__
__lt__
__gt__
__enter__
__exit__
```

## 34. PROPERTY & ATTRIBUTES

```python
class Person:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        self._age = value

    @age.deleter
    def age(self):
        del self._age
```

## 35. EXCEPTION HANDLING

```python
try:
    x = 10 / 0

except ZeroDivisionError:
    print("Cannot divide by zero")

except ValueError:
    print("Invalid value")

except Exception as e:
    print(e)

else:
    print("No exception")

finally:
    print("Always executed")
```

## 36. RAISE & CUSTOM EXCEPTIONS

```python
raise ValueError("Invalid value")

raise TypeError("Wrong type")

raise RuntimeError("Runtime error")

class CustomError(Exception):
    pass

raise CustomError("Something went wrong")

assert 10 > 5
assert age >= 18, "Age must be 18 or above"
```

## 37. FILE HANDLING

```python
file = open("data.txt", "r")
content = file.read()
file.close()

file = open("data.txt", "w")
file.write("Hello Python")
file.close()

file = open("data.txt", "a")
file.write("\nNew line")
file.close()

file = open("data.txt", "r")
file.readline()
file.readlines()
file.close()
```

## 38. FILE HANDLING WITH WITH

```python
with open("data.txt", "r") as file:
    content = file.read()

with open("data.txt", "w") as file:
    file.write("Hello")

with open("data.txt", "a") as file:
    file.write("\nNew line")

with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())
```

## 39. FILE MODES

```python
"r"   # Read
"w"   # Write
"a"   # Append
"x"   # Create
"b"   # Binary
"t"   # Text
"r+"  # Read and write
"w+"  # Write and read
"a+"  # Append and read
"rb"  # Read binary
"wb"  # Write binary
```

## 40. OS & FILE SYSTEM

```python
import os

os.getcwd()
os.chdir("DIRECTORY")
os.listdir()
os.mkdir("folder")
os.makedirs("parent/child", exist_ok=True)
os.rmdir("folder")
os.remove("file.txt")
os.rename("old.txt", "new.txt")
os.path.exists("file.txt")
os.path.isfile("file.txt")
os.path.isdir("folder")
os.path.join("folder", "file.txt")
os.path.abspath("file.txt")
os.path.basename("/home/user/file.txt")
os.path.dirname("/home/user/file.txt")
os.path.getsize("file.txt")
os.environ.get("PATH")
os.walk(".")
```

## 41. PATHLIB

```python
from pathlib import Path

p = Path("data.txt")

p.exists()
p.is_file()
p.is_dir()
p.name
p.stem
p.suffix
p.parent
p.resolve()

p.read_text()
p.write_text("Hello")

p.unlink()
p.rename("new.txt")

Path("folder").mkdir(exist_ok=True)
Path("folder").rmdir()

list(Path(".").iterdir())
list(Path(".").glob("*.py"))
list(Path(".").rglob("*.py"))
```

## 42. JSON

```python
import json

data = {"name": "Manish", "age": 21}

json.dumps(data)
json.dumps(data, indent=4)

json.loads('{"name": "Manish"}')

with open("data.json", "w") as file:
    json.dump(data, file, indent=4)

with open("data.json", "r") as file:
    data = json.load(file)
```

## 43. CSV

```python
import csv

with open("data.csv", "r") as file:
    reader = csv.reader(file)

    for row in reader:
        print(row)

with open("data.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Age"])
    writer.writerow(["Manish", 21])

with open("data.csv", "r") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row)
```

## 44. PICKLE

```python
import pickle

data = {"name": "Manish"}

with open("data.pkl", "wb") as file:
    pickle.dump(data, file)

with open("data.pkl", "rb") as file:
    data = pickle.load(file)
```

## 45. REGULAR EXPRESSIONS

```python
import re

re.search("pattern", text)
re.match("pattern", text)
re.fullmatch("pattern", text)
re.findall("pattern", text)
re.finditer("pattern", text)
re.split(",", text)
re.sub("old", "new", text)
re.subn("old", "new", text)

re.compile("pattern")
re.escape("a.b")

re.search(r"\d+", text)
re.search(r"\w+", text)
re.search(r"\s+", text)

re.IGNORECASE
re.MULTILINE
re.DOTALL
```

## 46. COLLECTIONS MODULE

```python
from collections import Counter
from collections import defaultdict
from collections import deque
from collections import OrderedDict
from collections import namedtuple
from collections import ChainMap

Counter([1, 2, 2, 3])
Counter("banana")

defaultdict(int)
defaultdict(list)

d = deque([1, 2, 3])
d.append(4)
d.appendleft(0)
d.pop()
d.popleft()
d.rotate(1)

Person = namedtuple("Person", ["name", "age"])
p = Person("Manish", 21)
```

## 47. ITERTOOLS

```python
import itertools

itertools.count()
itertools.count(1, 2)

itertools.cycle([1, 2, 3])
itertools.repeat(10, 3)

itertools.chain([1, 2], [3, 4])
itertools.product([1, 2], [3, 4])
itertools.permutations([1, 2, 3])
itertools.combinations([1, 2, 3], 2)

itertools.accumulate([1, 2, 3, 4])
itertools.groupby([1, 1, 2, 2, 3])
itertools.islice(range(10), 2, 8)
itertools.zip_longest([1, 2], [3, 4, 5])
```

## 48. FUNCTOOLS

```python
from functools import reduce
from functools import partial
from functools import lru_cache
from functools import cache
from functools import wraps
from functools import total_ordering

reduce(lambda a, b: a + b, [1, 2, 3])

double = partial(lambda x, y: x * y, 2)
double(5)

@lru_cache(maxsize=None)
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

fibonacci.cache_info()
fibonacci.cache_clear()
```

## 49. MATH MODULE

```python
import math

math.sqrt(25)
math.pow(2, 3)
math.ceil(4.2)
math.floor(4.8)
math.trunc(4.8)
math.factorial(5)
math.gcd(12, 18)
math.lcm(12, 18)
math.fabs(-10)
math.isqrt(25)

math.pi
math.e
math.inf
math.nan

math.sin(0)
math.cos(0)
math.tan(0)
math.radians(90)
math.degrees(math.pi)
math.log(10)
math.log10(100)
math.exp(2)
```

## 50. RANDOM MODULE

```python
import random

random.random()
random.randint(1, 10)
random.randrange(1, 10)
random.uniform(1, 10)

random.choice([1, 2, 3])
random.choices([1, 2, 3], k=2)
random.sample([1, 2, 3, 4], 2)

arr = [1, 2, 3, 4]
random.shuffle(arr)

random.seed(42)
```

## 51. DATETIME

```python
from datetime import datetime, date, time, timedelta

datetime.now()
datetime.today()
date.today()

datetime.now().year
datetime.now().month
datetime.now().day
datetime.now().hour
datetime.now().minute
datetime.now().second

datetime.now().strftime("%Y-%m-%d")
datetime.now().strftime("%H:%M:%S")

datetime.strptime("2026-10-30", "%Y-%m-%d")

timedelta(days=7)
timedelta(hours=2)

date.today() + timedelta(days=7)
date.today() - timedelta(days=7)
```

## 52. TIME MODULE

```python
import time

time.time()
time.ctime()
time.sleep(2)
time.localtime()
time.gmtime()
time.strftime("%Y-%m-%d", time.localtime())
time.perf_counter()
time.monotonic()
```

## 53. ENUM

```python
from enum import Enum, IntEnum

class Status(Enum):
    PENDING = 1
    SUCCESS = 2
    FAILED = 3

print(Status.SUCCESS)
print(Status.SUCCESS.value)
print(Status.SUCCESS.name)

class Number(IntEnum):
    ONE = 1
    TWO = 2
```

## 54. DATACLASSES

```python
from dataclasses import dataclass, field

@dataclass
class Person:
    name: str
    age: int
    skills: list = field(default_factory=list)

p = Person("Manish", 21)
print(p)
```

## 55. TYPE HINTS

```python
name: str = "Manish"
age: int = 21
price: float = 10.5
active: bool = True

def add(a: int, b: int) -> int:
    return a + b

from typing import Optional, Union, Any, Callable

def get_name() -> Optional[str]:
    return None

def process(value: Union[int, str]) -> Any:
    return value

from typing import List, Dict, Tuple, Set

numbers: List[int] = [1, 2, 3]
users: Dict[str, int] = {"Manish": 21}
point: Tuple[int, int] = (10, 20)
values: Set[int] = {1, 2, 3}
```

## 56. CONTEXT MANAGERS

```python
with open("file.txt") as file:
    data = file.read()

from contextlib import contextmanager

@contextmanager
def manager():
    print("Enter")
    try:
        yield
    finally:
        print("Exit")

with manager():
    print("Inside")
```

## 57. MULTITHREADING

```python
import threading

def task():
    print("Running")

t = threading.Thread(target=task)
t.start()
t.join()

threading.current_thread()
threading.active_count()

lock = threading.Lock()

with lock:
    print("Locked section")
```

## 58. MULTIPROCESSING

```python
from multiprocessing import Process

def task():
    print("Process running")

if __name__ == "__main__":
    p = Process(target=task)
    p.start()
    p.join()
```

## 59. CONCURRENT FUTURES

```python
from concurrent.futures import ThreadPoolExecutor
from concurrent.futures import ProcessPoolExecutor

def task(n):
    return n * n

with ThreadPoolExecutor(max_workers=4) as executor:
    results = executor.map(task, range(10))

    print(list(results))

with ProcessPoolExecutor(max_workers=4) as executor:
    results = executor.map(task, range(10))

    print(list(results))
```

## 60. ASYNCIO

```python
import asyncio

async def task():
    print("Start")
    await asyncio.sleep(1)
    print("End")

async def main():
    await task()

asyncio.run(main())

asyncio.create_task(task())
await asyncio.gather(task(), task())
await asyncio.sleep(1)
```

## 61. SUBPROCESS

```python
import subprocess

subprocess.run(["ls", "-l"])
subprocess.run(["pwd"])

result = subprocess.run(
    ["python3", "--version"],
    capture_output=True,
    text=True
)

print(result.stdout)
print(result.stderr)
print(result.returncode)

subprocess.check_output(["ls"], text=True)

subprocess.Popen(["python3", "script.py"])
```

## 62. SYS MODULE

```python
import sys

sys.argv
sys.path
sys.version
sys.platform
sys.executable
sys.exit()
sys.maxsize
sys.stdin
sys.stdout
sys.stderr
```

## 63. IMPORTS & MODULES

```python
import math
import os

from math import sqrt
from math import *

import module as alias

__name__
__file__
__package__

if __name__ == "__main__":
    main()
```

## 64. PYTHON PACKAGE MANAGEMENT

```bash
python3 -m pip --version
python3 -m pip install PACKAGE
python3 -m pip uninstall PACKAGE
python3 -m pip list
python3 -m pip freeze
python3 -m pip freeze > requirements.txt
python3 -m pip install -r requirements.txt
python3 -m pip show PACKAGE
python3 -m pip check
python3 -m pip cache info
python3 -m pip cache purge
```

## 65. VIRTUAL ENVIRONMENTS

```bash
python3 -m venv venv
python3 -m venv .venv

source venv/bin/activate
source .venv/bin/activate

deactivate

python -m pip install PACKAGE
python -m pip freeze > requirements.txt
python -m pip install -r requirements.txt

rm -rf venv
```

## 66. PYTHON PROJECT STRUCTURE

```text
project/
│
├── src/
│   └── package/
│       ├── __init__.py
│       └── main.py
│
├── tests/
│   └── test_main.py
│
├── venv/
├── .gitignore
├── README.md
├── requirements.txt
└── pyproject.toml
```

## 67. UNIT TESTING

```python
import unittest

def add(a, b):
    return a + b

class TestMath(unittest.TestCase):

    def test_add(self):
        self.assertEqual(add(2, 3), 5)

    def test_true(self):
        self.assertTrue(True)

    def test_false(self):
        self.assertFalse(False)

    def test_none(self):
        self.assertIsNone(None)

if __name__ == "__main__":
    unittest.main()
```

## 68. PYTEST

```python
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5

def test_equal():
    assert 10 == 10

def test_true():
    assert True
```

```bash
pip install pytest
pytest
pytest -v
pytest -q
pytest -x
pytest -k "test_add"
pytest test_file.py
pytest --collect-only
pytest --cov=src
```

## 69. DEBUGGING

```python
print("Debug")

breakpoint()

import pdb
pdb.set_trace()

assert value == expected

try:
    pass
except Exception as e:
    print(repr(e))
```

```bash
python3 -m pdb FILE.py
python3 -X dev FILE.py
```

## 70. LOGGING

```python
import logging

logging.basicConfig(level=logging.DEBUG)

logging.debug("Debug message")
logging.info("Information")
logging.warning("Warning")
logging.error("Error")
logging.critical("Critical")

logging.basicConfig(
    filename="app.log",
    level=logging.INFO,
    format="%(asctime)s %(levelname)s %(message)s"
)
```

## 71. PROFILING & PERFORMANCE

```python
import timeit

timeit.timeit("sum(range(100))", number=1000)

import cProfile

cProfile.run("sum(range(100000))")
```

```bash
python3 -m cProfile FILE.py
python3 -m timeit "sum(range(100))"
```

## 72. MEMORY MANAGEMENT

```python
import gc
import sys
import tracemalloc

sys.getsizeof([1, 2, 3])

gc.collect()
gc.get_count()
gc.get_stats()

tracemalloc.start()

snapshot = tracemalloc.take_snapshot()
print(snapshot.statistics("lineno"))
```

## 73. HASHING

```python
import hashlib

hashlib.md5(b"hello").hexdigest()
hashlib.sha1(b"hello").hexdigest()
hashlib.sha256(b"hello").hexdigest()
hashlib.sha512(b"hello").hexdigest()

password = b"password"
salt = b"random_salt"

import hashlib

hashlib.pbkdf2_hmac(
    "sha256",
    password,
    salt,
    100000
)
```

## 74. BASE64

```python
import base64

encoded = base64.b64encode(b"Hello")
decoded = base64.b64decode(encoded)

print(encoded)
print(decoded)
```

## 75. SOCKET PROGRAMMING

```python
import socket

socket.gethostname()
socket.gethostbyname("google.com")

s = socket.socket(
    socket.AF_INET,
    socket.SOCK_STREAM
)

s.connect(("example.com", 80))
s.close()
```

## 76. HTTP REQUESTS

```python
import urllib.request

response = urllib.request.urlopen("https://example.com")
print(response.status)
print(response.read())
```

```python
import requests

response = requests.get("https://example.com")

response.status_code
response.text
response.json()
response.headers

requests.post(URL, json=DATA)
requests.put(URL, json=DATA)
requests.patch(URL, json=DATA)
requests.delete(URL)

requests.get(URL, timeout=10)
```

## 77. SQLITE DATABASE

```python
import sqlite3

conn = sqlite3.connect("database.db")

cursor = conn.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY,
    name TEXT
)
""")

cursor.execute(
    "INSERT INTO users (name) VALUES (?)",
    ("Manish",)
)

cursor.execute("SELECT * FROM users")

rows = cursor.fetchall()

conn.commit()
conn.close()
```

## 78. ENVIRONMENT VARIABLES & DOTENV

```python
import os

os.environ.get("API_KEY")
os.getenv("DATABASE_URL")

os.environ["APP_ENV"] = "development"
```

```bash
pip install python-dotenv
```

```python
from dotenv import load_dotenv
import os

load_dotenv()

API_KEY = os.getenv("API_KEY")
```

## 79. PANDAS

```python
import pandas as pd

df = pd.read_csv("data.csv")
df = pd.read_json("data.json")
df = pd.read_excel("data.xlsx")

df.head()
df.tail()
df.info()
df.describe()
df.shape
df.columns
df.dtypes
df.index

df["column"]
df[["col1", "col2"]]

df.loc[0]
df.iloc[0]

df.isnull()
df.isnull().sum()
df.dropna()
df.fillna(0)
df.drop_duplicates()

df.sort_values("column")
df.groupby("column").sum()
df.value_counts()

df.to_csv("output.csv", index=False)
df.to_json("output.json")
df.to_excel("output.xlsx", index=False)
```

## 80. NUMPY

```python
import numpy as np

arr = np.array([1, 2, 3])
np.zeros(5)
np.ones(5)
np.arange(0, 10)
np.linspace(0, 1, 5)
np.eye(3)

arr.shape
arr.ndim
arr.size
arr.dtype

np.reshape(arr, (3, 1))
np.sort(arr)
np.unique(arr)

np.sum(arr)
np.mean(arr)
np.median(arr)
np.std(arr)
np.var(arr)
np.min(arr)
np.max(arr)

np.concatenate([arr, arr])
np.vstack([arr, arr])
np.hstack([arr, arr])

np.random.randint(1, 10, size=5)
np.random.rand(3, 3)
```

## 81. JSON & API PROJECT UTILITIES

```python
import json

json.dumps(DATA)
json.loads(JSON_STRING)

with open("data.json", "w") as f:
    json.dump(DATA, f, indent=4)

with open("data.json") as f:
    data = json.load(f)
```

## 82. COMMON BUILT-IN FUNCTIONS

```python
print()
input()
len()
type()
id()
isinstance()
issubclass()

int()
float()
str()
bool()
list()
tuple()
set()
dict()

range()
enumerate()
zip()
map()
filter()
sorted()
reversed()

sum()
min()
max()
abs()
round()
pow()
divmod()

all()
any()

iter()
next()
callable()
getattr()
setattr()
hasattr()
delattr()

repr()
format()
hash()
help()
dir()
vars()
globals()
locals()
```

## 83. IMPORTANT PYTHON KEYWORDS

```python
False
None
True
and
as
assert
async
await
break
class
continue
def
del
elif
else
except
finally
for
from
global
if
import
in
is
lambda
nonlocal
not
or
pass
raise
return
try
while
with
yield
match
case
```

## 84. PYTHON SHORTCUTS & IDIOMS

```python
# Swap variables
a, b = b, a

# Multiple assignment
a, b, c = 1, 2, 3

# Unpacking
first, *middle, last = [1, 2, 3, 4, 5]

# Reverse a list
arr[::-1]

# Reverse a string
text[::-1]

# Remove duplicates while preserving order
list(dict.fromkeys(arr))

# Merge dictionaries
merged = {**dict1, **dict2}

# Merge dictionaries (Python 3.9+)
merged = dict1 | dict2

# Safe dictionary access
value = data.get("key", default)

# Swap dictionary keys and values
inverted = {v: k for k, v in data.items()}

# Check empty collection
if not arr:
    print("Empty")

# Get first and last elements
first, last = arr[0], arr[-1]

# Zip two lists
pairs = list(zip(a, b))

# Enumerate with index
for i, value in enumerate(arr):
    print(i, value)

# Sort by key
sorted(data, key=lambda x: x[1])

# Any condition
any(x > 10 for x in arr)

# All conditions
all(x > 0 for x in arr)
```

## 85. IMPORTANT PYTHON CONCEPTS TO MASTER

- [ ] Variables and data types
- [ ] Mutable and immutable objects
- [ ] List, tuple, set and dictionary
- [ ] String operations and slicing
- [ ] Conditional statements
- [ ] Loops and nested loops
- [ ] List and dictionary comprehensions
- [ ] Functions and arguments
- [ ] `*args` and `**kwargs`
- [ ] Lambda, map, filter and reduce
- [ ] Recursion
- [ ] Iterators and generators
- [ ] Decorators and closures
- [ ] Scope: local, global and nonlocal
- [ ] OOP: classes and objects
- [ ] Inheritance and polymorphism
- [ ] Encapsulation and abstraction
- [ ] Method overriding and overloading concepts
- [ ] Dunder methods
- [ ] Exception handling
- [ ] File handling
- [ ] Modules and packages
- [ ] Virtual environments
- [ ] Itertools and collections
- [ ] Regular expressions
- [ ] JSON and CSV
- [ ] Memory management
- [ ] Shallow copy and deep copy
- [ ] Multithreading and multiprocessing
- [ ] GIL (Global Interpreter Lock)
- [ ] Asyncio and asynchronous programming
- [ ] Context managers
- [ ] Type hints
- [ ] Dataclasses
- [ ] Unit testing and Pytest
- [ ] Logging and debugging
- [ ] Profiling and optimization
- [ ] Database connectivity
- [ ] API requests
- [ ] Python packaging

## 86. PYTHON CLI COMMANDS

```bash
# Check Python version
python3 --version

# Run Python file
python3 main.py

# Interactive interpreter
python3

# Create virtual environment
python3 -m venv venv

# Activate virtual environment (macOS/Linux)
source venv/bin/activate

# Deactivate environment
deactivate

# Install package
pip install PACKAGE

# Uninstall package
pip uninstall PACKAGE

# List packages
pip list

# Export dependencies
pip freeze > requirements.txt

# Install dependencies
pip install -r requirements.txt

# Run module
python3 -m MODULE

# Run tests
pytest

# Run unittest
python3 -m unittest

# Compile Python file
python3 -m py_compile main.py

# Generate bytecode
python3 -m compileall .

# Start Python HTTP server
python3 -m http.server 8000

# Run debugger
python3 -m pdb main.py

# Show installed packages
python3 -m pip list
```

## 87. DANGEROUS OPERATIONS

**Warning:** These operations can delete data, overwrite files or execute untrusted code.

```python
import os
import shutil

# Delete a file
os.remove("file.txt")

# Delete an empty directory
os.rmdir("folder")

# Delete directory recursively
shutil.rmtree("folder")

# Overwrite a file
open("file.txt", "w").close()

# Execute system command
os.system("COMMAND")
```

Avoid running untrusted code using `eval()`, `exec()`, `pickle.load()` or shell commands.
