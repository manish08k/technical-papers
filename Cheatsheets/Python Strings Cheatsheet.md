
# Python Strings Cheatsheet

## 1. Creating Strings

```python
# Single quotes
s = 'Hello'

# Double quotes
s = "Hello"

# Triple quotes
s = """Hello World"""

# Multiline string
s = '''Hello
Python
World'''

# Empty string
s = ""

# String with variables
name = "Manish"
s = f"Hello {name}"
```

## 2. Accessing Characters

```python
s = "Python"

# First character
s[0]       # P

# Last character
s[-1]      # n

# Second character
s[1]       # y

# Second last character
s[-2]      # o

# String length
len(s)     # 6
```

## 3. String Slicing

```python
s = "PythonProgramming"

s[0:6]       # Python
s[:6]        # Python
s[6:]        # Programming
s[::2]       # Every second character
s[1::2]      # Alternate characters
s[::-1]      # Reverse string
s[2:8:2]     # Characters with step 2
s[-3:]       # Last three characters
s[:-2]       # All except last two
```

Syntax:

```python
string[start:end:step]
```

## 4. String Immutability

Strings cannot be changed directly.

```python
s = "Python"

# Incorrect
# s[0] = "J"

# Correct
s = "J" + s[1:]

print(s)  # Jython
```

## 5. Changing Case

```python
s = "hello python"

s.upper()          # HELLO PYTHON
s.lower()          # hello python
s.capitalize()     # Hello python
s.title()          # Hello Python
s.swapcase()       # HELLO PYTHON
s.casefold()       # Case-insensitive form
```

## 6. Removing Spaces

```python
s = "  hello python  "

s.strip()       # Remove spaces from both ends
s.lstrip()      # Remove leading spaces
s.rstrip()      # Remove trailing spaces

# Remove specific characters from ends
s.strip("*")

# Remove newline and spaces at ends
s.strip()
```

## 7. Searching in Strings

```python
s = "hello python programming"

# Check substring
"python" in s

# Check substring absence
"java" not in s

# First occurrence
s.find("python")

# Last occurrence
s.rfind("o")

# Index of substring
s.index("python")

# Count occurrences
s.count("o")

# Find from a starting position
s.find("o", 5)

# Check prefix
s.startswith("hello")

# Check suffix
s.endswith("programming")
```

Difference:

```python
s.find("java")   # Returns -1 if missing
s.index("java")  # Raises ValueError if missing
```

## 8. Replacing Strings

```python
s = "hello python"

# Replace substring
s.replace("python", "world")

# Replace only first occurrence
s.replace("o", "0", 1)

# Replace all occurrences
s.replace("o", "0")
```

## 9. Splitting Strings

```python
s = "apple,banana,mango"

# Split by comma
s.split(",")

# Split by whitespace
"hello python world".split()

# Split only once
s.split(",", 1)

# Split from right
s.rsplit(",", 1)

# Split into lines
"hello\npython".splitlines()
```

## 10. Joining Strings

```python
words = ["Hello", "Python", "World"]

# Join using space
" ".join(words)

# Join using comma
",".join(words)

# Join using hyphen
"-".join(words)

# Join using empty string
"".join(words)
```

## 11. Checking String Content

```python
s = "Python123"

s.isalpha()       # Only alphabets
s.isdigit()       # Only digits
s.isalnum()       # Alphabets and digits
s.islower()       # All cased characters lowercase
s.isupper()       # All cased characters uppercase
s.isspace()       # Only whitespace
s.istitle()       # Title case
s.isdecimal()     # Decimal characters
s.isnumeric()     # Numeric characters
s.isidentifier()  # Valid Python identifier
s.isascii()       # ASCII characters only
```

## 12. String Formatting

```python
name = "Manish"
age = 21

# f-string
f"My name is {name} and I am {age}"

# format()
"My name is {} and I am {}".format(name, age)

# Positional formatting
"{0} is {1}".format(name, age)

# Named formatting
"{name} is {age}".format(name=name, age=age)

# Percentage formatting
"Age: %d" % age

# Number formatting
price = 1234.5678

f"{price:.2f}"      # 1234.57
f"{price:,.2f}"     # 1,234.57
```

## 13. Escape Characters

```python
# New line
s = "Hello\nWorld"

# Tab
s = "Hello\tWorld"

# Backslash
s = "C:\\Users\\Manish"

# Single quote
s = 'It\'s Python'

# Double quote
s = "He said \"Hello\""

# Carriage return
s = "Hello\rWorld"

# Raw string
s = r"C:\Users\Manish"
```

Common escape sequences:

| Escape | Meaning |
|---|---|
| `\n` | New line |
| `\t` | Tab |
| `\\` | Backslash |
| `\'` | Single quote |
| `\"` | Double quote |
| `\r` | Carriage return |
| `\b` | Backspace |
| `\0` | Null character |

## 14. String Concatenation

```python
a = "Hello"
b = "Python"

# Using +
c = a + " " + b

# Using +=
a += b

# Using join
c = " ".join([a, b])

# Using f-string
c = f"{a} {b}"
```

## 15. String Repetition

```python
s = "Python"

s * 3
# PythonPythonPython

"-" * 10
# ----------
```

## 16. Reversing a String

```python
s = "Python"

# Slicing
s[::-1]

# Using reversed()
"".join(reversed(s))

# Using loop
result = ""

for char in s:
    result = char + result
```

## 17. Iterating Through Strings

```python
s = "Python"

# Direct iteration
for char in s:
    print(char)

# Using indexes
for i in range(len(s)):
    print(s[i])

# Index and character
for i, char in enumerate(s):
    print(i, char)

# Reverse iteration
for char in reversed(s):
    print(char)
```

## 18. Character to ASCII and Unicode

```python
# Character to Unicode code point
ord("A")       # 65

# Unicode code point to character
chr(65)        # A

# Character to integer
ord("a")      # 97

# Integer to character
chr(97)       # a
```

## 19. String Comparison

```python
a = "apple"
b = "banana"

a == b
a != b
a < b
a > b

# Case-insensitive comparison
a.lower() == b.lower()

# Compare without case sensitivity
a.casefold() == b.casefold()
```

## 20. Removing Characters

```python
s = "hello world"

# Remove spaces
s.replace(" ", "")

# Remove a particular character
s.replace("l", "")

# Remove first occurrence
s.replace("l", "", 1)

# Remove prefix
s.removeprefix("hello")

# Remove suffix
s.removesuffix("world")

# Remove punctuation
import string

text = "Hello, World!"
result = text.translate(
    str.maketrans("", "", string.punctuation)
)
```

## 21. String Partitioning

```python
s = "name=Manish"

# Split into three parts
s.partition("=")

# Split from right
s.rpartition("=")

# Result
# ('name', '=', 'Manish')
```

## 22. Padding and Alignment

```python
s = "Python"

# Left alignment
s.ljust(10)

# Right alignment
s.rjust(10)

# Center alignment
s.center(10)

# Zero padding
"42".zfill(5)

# Custom fill character
s.center(10, "*")
```

## 23. Checking Prefix and Suffix

```python
s = "python.py"

s.startswith("python")
s.endswith(".py")

# Multiple prefixes
s.startswith(("java", "python"))

# Multiple suffixes
s.endswith((".py", ".txt"))
```

## 24. Converting Between Strings and Lists

```python
s = "hello"

# String to list of characters
list(s)

# List to string
chars = ["P", "y", "t", "h", "o", "n"]
"".join(chars)

# String to list of words
"hello python world".split()

# List to string with spaces
" ".join(["hello", "python"])
```

## 25. Converting Between Strings and Numbers

```python
# String to integer
int("123")

# String to float
float("12.5")

# Integer to string
str(123)

# Float to string
str(12.5)

# Binary to integer
int("1010", 2)

# Hexadecimal to integer
int("FF", 16)

# Integer to binary string
bin(10)

# Integer to hexadecimal string
hex(255)

# Integer to octal string
oct(8)
```

## 26. String Templates

```python
from string import Template

template = Template("Hello $name")

result = template.substitute(name="Manish")

# Safe substitution
result = template.safe_substitute(name="Manish")
```

## 27. Regular Expressions

```python
import re

s = "My number is 9876543210"

# Search pattern
re.search(r"\d+", s)

# Find all matches
re.findall(r"\d+", s)

# Replace matches
re.sub(r"\d+", "NUMBER", s)

# Split using pattern
re.split(r"\s+", "hello python world")

# Match from beginning
re.match(r"My", s)

# Full string match
re.fullmatch(r"\d+", "12345")

# Compile pattern
pattern = re.compile(r"\d+")
pattern.findall(s)
```

Common regex patterns:

| Pattern | Meaning |
|---|---|
| `\d` | Digit |
| `\D` | Non-digit |
| `\w` | Word character |
| `\W` | Non-word character |
| `\s` | Whitespace |
| `\S` | Non-whitespace |
| `.` | Any character except newline by default |
| `^` | Start of string |
| `$` | End of string |
| `+` | One or more |
| `*` | Zero or more |
| `?` | Zero or one |
| `{n}` | Exactly n repetitions |
| `[abc]` | Any listed character |
| `[^abc]` | Any character except listed characters |

## 28. Useful String Operations

```python
s = "hello python"

# Length
len(s)

# First character
s[0]

# Last character
s[-1]

# Reverse
s[::-1]

# Check empty
if not s:
    print("Empty")

# Check non-empty
if s:
    print("Not empty")

# Count words
len(s.split())

# Count characters excluding spaces
len(s.replace(" ", ""))

# Remove duplicate characters (preserve order)
unique = "".join(dict.fromkeys(s))

# Check palindrome
s == s[::-1]

# Convert to lowercase
s = s.lower()
```

## 29. Common LeetCode String Patterns

### Reverse String

```python
s = list("hello")

left = 0
right = len(s) - 1

while left < right:
    s[left], s[right] = s[right], s[left]
    left += 1
    right -= 1

result = "".join(s)
```

### Valid Palindrome

```python
s = "A man, a plan, a canal: Panama"

cleaned = "".join(
    char.lower()
    for char in s
    if char.isalnum()
)

result = cleaned == cleaned[::-1]
```

### Valid Anagram

```python
from collections import Counter

s = "listen"
t = "silent"

result = Counter(s) == Counter(t)
```

### First Non-Repeating Character

```python
s = "leetcode"

freq = {}

for char in s:
    freq[char] = freq.get(char, 0) + 1

for i, char in enumerate(s):
    if freq[char] == 1:
        print(i)
        break
```

### Character Frequency

```python
s = "banana"

freq = {}

for char in s:
    freq[char] = freq.get(char, 0) + 1
```

### Reverse Words

```python
s = "hello python world"

result = " ".join(s.split()[::-1])
```

### Longest Common Prefix

```python
words = ["flower", "flow", "flight"]

prefix = words[0]

for word in words[1:]:
    while not word.startswith(prefix):
        prefix = prefix[:-1]

        if not prefix:
            break
```

### Remove Duplicate Characters

```python
s = "programming"

result = "".join(dict.fromkeys(s))
```

### Check String Rotation

```python
s1 = "waterbottle"
s2 = "erbottlewat"

result = (
    len(s1) == len(s2)
    and s2 in (s1 + s1)
)
```

### Longest Substring Without Repeating Characters

```python
s = "abcabcbb"

seen = {}
left = 0
max_length = 0

for right, char in enumerate(s):
    if char in seen and seen[char] >= left:
        left = seen[char] + 1

    seen[char] = right

    max_length = max(
        max_length,
        right - left + 1
    )
```

## 30. String Time Complexity

Let `n` be the string length.

| Operation | Time Complexity |
|---|---:|
| Access by index | O(1) |
| Length | O(1) |
| Search (`in`) | O(n) |
| Find | O(n) |
| Count | O(n) |
| Equality comparison | O(n) worst case |
| Concatenation | O(n + m) |
| Slicing | O(k) |
| Reverse | O(n) |
| Replace | O(n) |
| Split | O(n) |
| Join | O(n) total output size |
| Lowercase / Uppercase | O(n) |
| Strip | O(n) |
| Sort characters | O(n log n) |

Strings are immutable, so most string operations return a new string.

## 31. Quick Reference

| Task | Python |
|---|---|
| Length | `len(s)` |
| First character | `s[0]` |
| Last character | `s[-1]` |
| Reverse | `s[::-1]` |
| Uppercase | `s.upper()` |
| Lowercase | `s.lower()` |
| Capitalize | `s.capitalize()` |
| Title case | `s.title()` |
| Remove spaces at ends | `s.strip()` |
| Replace | `s.replace(a, b)` |
| Split | `s.split()` |
| Join | `" ".join(arr)` |
| Find | `s.find(x)` |
| Index | `s.index(x)` |
| Count | `s.count(x)` |
| Starts with | `s.startswith(x)` |
| Ends with | `s.endswith(x)` |
| Check alphabet | `s.isalpha()` |
| Check digits | `s.isdigit()` |
| Check alphanumeric | `s.isalnum()` |
| Check lowercase | `s.islower()` |
| Check uppercase | `s.isupper()` |
| Check whitespace | `s.isspace()` |
| Character to integer | `ord(c)` |
| Integer to character | `chr(n)` |
| String to list | `list(s)` |
| List to string | `"".join(arr)` |
| String to integer | `int(s)` |
| Integer to string | `str(n)` |
| Remove prefix | `s.removeprefix(x)` |
| Remove suffix | `s.removesuffix(x)` |
| Format string | `f"{name}"` |
