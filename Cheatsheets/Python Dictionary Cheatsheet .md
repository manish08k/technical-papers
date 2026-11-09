
# Python Dictionary Cheatsheet

## 1. Creating Dictionaries

```python
# Empty dictionary
d = {}

# Dictionary with values
student = {
    "name": "Manish",
    "age": 21,
    "branch": "CSE"
}

# Using dict()
d = dict(name="Manish", age=21)

# From list of tuples
d = dict([("a", 1), ("b", 2)])

# Using fromkeys()
d = dict.fromkeys(["a", "b", "c"], 0)

# Dictionary comprehension
squares = {x: x * x for x in range(1, 6)}
```

## 2. Accessing Values

```python
student = {"name": "Manish", "age": 21}

# Access using key
student["name"]

# Access safely
student.get("name")

# Default value if key doesn't exist
student.get("city", "Unknown")

# Access all keys
student.keys()

# Access all values
student.values()

# Access key-value pairs
student.items()
```

## 3. Adding Elements

```python
d = {"a": 1, "b": 2}

# Add new key-value pair
d["c"] = 3

# Add multiple elements
d.update({"d": 4, "e": 5})

# Add using assignment expression
d |= {"f": 6}
```

## 4. Updating Elements

```python
d = {"name": "Manish", "age": 21}

# Update existing value
d["age"] = 22

# Update multiple values
d.update({"age": 23, "city": "Bangalore"})

# Set value only if key is missing
d.setdefault("country", "India")
```

## 5. Removing Elements

```python
d = {"a": 1, "b": 2, "c": 3}

# Remove using key
del d["a"]

# Remove and return value
d.pop("b")

# Remove with default if key is missing
d.pop("x", None)

# Remove last inserted item
d.popitem()

# Remove all elements
d.clear()
```

## 6. Checking Keys

```python
d = {"name": "Manish", "age": 21}

# Check if key exists
"name" in d

# Check if key doesn't exist
"city" not in d

# Check dictionary is empty
if not d:
    print("Empty")

# Check dictionary is not empty
if d:
    print("Not empty")
```

## 7. Looping Through Dictionaries

```python
d = {"a": 1, "b": 2, "c": 3}

# Loop through keys
for key in d:
    print(key)

# Loop through values
for value in d.values():
    print(value)

# Loop through keys and values
for key, value in d.items():
    print(key, value)

# Loop through keys explicitly
for key in d.keys():
    print(key)
```

## 8. Dictionary Length

```python
d = {"a": 1, "b": 2, "c": 3}

# Number of key-value pairs
len(d)

# Check empty
len(d) == 0

# Check non-empty
len(d) > 0
```

## 9. Copying Dictionaries

```python
d = {"a": 1, "b": 2}

# Shallow copy
a = d.copy()

# Using dict()
b = dict(d)

# Using copy module
import copy

c = copy.copy(d)

# Deep copy for nested dictionaries
nested = {"user": {"name": "Manish"}}
new_dict = copy.deepcopy(nested)
```

## 10. Merging Dictionaries

```python
a = {"x": 1, "y": 2}
b = {"z": 3, "w": 4}

# Using update()
a.update(b)

# Using | operator (Python 3.9+)
c = a | b

# Using unpacking
c = {**a, **b}

# Merge and update in-place
a |= b
```

## 11. Dictionary Comprehension

```python
# Create dictionary
squares = {x: x * x for x in range(1, 6)}

# Filter values
even = {x: x for x in range(10) if x % 2 == 0}

# Convert list to dictionary
arr = [10, 20, 30]
d = {i: value for i, value in enumerate(arr)}

# Swap keys and values
d = {"a": 1, "b": 2}
swapped = {value: key for key, value in d.items()}

# Convert values
d = {"a": 1, "b": 2}
result = {key: value * 2 for key, value in d.items()}
```

## 12. Getting Default Values

```python
d = {"a": 10}

# Returns value if key exists
d.get("a")

# Returns default if key is missing
d.get("b", 0)

# Insert default only if missing
d.setdefault("b", 0)
```

## 13. Sorting Dictionaries

```python
d = {"c": 3, "a": 1, "b": 2}

# Sort by keys
sorted(d)

# Sort by keys and create dictionary
sorted_dict = dict(sorted(d.items()))

# Sort by values
sorted_dict = dict(
    sorted(d.items(), key=lambda item: item[1])
)

# Sort descending by values
sorted_dict = dict(
    sorted(d.items(), key=lambda item: item[1], reverse=True)
)
```

## 14. Finding Minimum and Maximum

```python
d = {"a": 10, "b": 30, "c": 20}

# Minimum key
min(d)

# Maximum key
max(d)

# Minimum value
min(d.values())

# Maximum value
max(d.values())

# Key with minimum value
min(d, key=d.get)

# Key with maximum value
max(d, key=d.get)

# Sum of values
sum(d.values())
```

## 15. Dictionary with Lists

```python
d = {
    "names": ["Manish", "Rahul"],
    "marks": [90, 85]
}

# Access list
d["names"]

# Add element
d["names"].append("John")

# Access nested element
d["names"][0]

# Update nested element
d["marks"][0] = 95
```

## 16. Nested Dictionaries

```python
students = {
    "student1": {
        "name": "Manish",
        "age": 21
    },
    "student2": {
        "name": "Rahul",
        "age": 22
    }
}

# Access nested value
students["student1"]["name"]

# Update nested value
students["student1"]["age"] = 22

# Add nested key
students["student1"]["city"] = "Bangalore"

# Loop nested dictionary
for student, details in students.items():
    print(student)
    for key, value in details.items():
        print(key, value)
```

## 17. Frequency Counting

```python
arr = [1, 2, 2, 3, 3, 3]

# Using dictionary
freq = {}

for x in arr:
    freq[x] = freq.get(x, 0) + 1

# Result: {1: 1, 2: 2, 3: 3}

# Using Counter
from collections import Counter

freq = Counter(arr)

# Count specific element
freq[2]

# Most common element
freq.most_common(1)

# All frequencies
freq.items()
```

## 18. Grouping Elements

```python
words = ["apple", "ant", "banana", "ball", "cat"]

groups = {}

for word in words:
    key = word[0]
    groups.setdefault(key, []).append(word)

# Result:
# {
#     'a': ['apple', 'ant'],
#     'b': ['banana', 'ball'],
#     'c': ['cat']
# }
```

## 19. defaultdict

```python
from collections import defaultdict

# Default integer value
freq = defaultdict(int)

freq["apple"] += 1

# Default list
groups = defaultdict(list)

groups["fruit"].append("apple")

# Default set
unique = defaultdict(set)

unique["numbers"].add(10)
```

## 20. Counter

```python
from collections import Counter

arr = [1, 2, 2, 3, 3, 3]

# Create frequency dictionary
freq = Counter(arr)

# Access count
freq[2]

# Most common elements
freq.most_common(2)

# Add counters
a = Counter([1, 1, 2])
b = Counter([1, 2, 2])

a + b

# Subtract counters
a - b

# Total count
freq.total()
```

## 21. Dictionary Views

```python
d = {"a": 1, "b": 2, "c": 3}

# Keys view
keys = d.keys()

# Values view
values = d.values()

# Items view
items = d.items()

# Convert to lists
list(d.keys())
list(d.values())
list(d.items())

# Check key in dictionary
"a" in d.keys()
```

## 22. Dictionary Unpacking

```python
a = {"x": 1, "y": 2}
b = {"z": 3}

# Unpack dictionaries
c = {**a, **b}

# Function argument unpacking
def display(name, age):
    print(name, age)

person = {"name": "Manish", "age": 21}

display(**person)
```

## 23. Converting Between Lists and Dictionaries

```python
# List of keys and values
keys = ["a", "b", "c"]
values = [10, 20, 30]

# Using zip
d = dict(zip(keys, values))

# Dictionary to list of keys
keys = list(d.keys())

# Dictionary to list of values
values = list(d.values())

# Dictionary to list of tuples
items = list(d.items())

# List of tuples to dictionary
d = dict([("a", 1), ("b", 2)])
```

## 24. Handling Missing Keys

```python
d = {"a": 10}

# Using get()
value = d.get("b", 0)

# Using setdefault()
d.setdefault("b", 0)

# Using membership check
if "b" in d:
    print(d["b"])
else:
    print("Not found")

# Using try-except
try:
    print(d["c"])
except KeyError:
    print("Key not found")
```

## 25. Dictionary Equality

```python
a = {"x": 1, "y": 2}
b = {"y": 2, "x": 1}

# Compare dictionaries
a == b       # True
a != b       # False

# Check same keys
a.keys() == b.keys()

# Check same values
a.values() == b.values()
```

## 26. Useful Dictionary Patterns

```python
# Get value with default
value = d.get("key", 0)

# Increment frequency
freq[x] = freq.get(x, 0) + 1

# Add item to dictionary
d[key] = value

# Update if key exists
if key in d:
    d[key] = new_value

# Remove key safely
d.pop(key, None)

# Find key with maximum value
max_key = max(d, key=d.get)

# Find key with minimum value
min_key = min(d, key=d.get)

# Swap keys and values
reversed_dict = {v: k for k, v in d.items()}

# Remove duplicate values (preserve first key)
unique = {}
for key, value in d.items():
    if value not in unique.values():
        unique[key] = value
```

## 27. Common LeetCode Patterns

```python
# Two Sum
nums = [2, 7, 11, 15]
target = 9

seen = {}

for i, num in enumerate(nums):
    complement = target - num

    if complement in seen:
        print([seen[complement], i])
        break

    seen[num] = i


# First non-repeating character
s = "leetcode"

freq = {}

for char in s:
    freq[char] = freq.get(char, 0) + 1

for i, char in enumerate(s):
    if freq[char] == 1:
        print(i)
        break


# Check anagrams
s = "listen"
t = "silent"

from collections import Counter

result = Counter(s) == Counter(t)


# Group anagrams
words = ["eat", "tea", "tan", "ate", "nat", "bat"]

groups = {}

for word in words:
    key = tuple(sorted(word))
    groups.setdefault(key, []).append(word)

result = list(groups.values())


# Find duplicates
nums = [1, 2, 3, 2, 4, 3]

seen = set()
duplicates = set()

for num in nums:
    if num in seen:
        duplicates.add(num)
    seen.add(num)


# Majority element
nums = [2, 2, 1, 1, 2, 2, 2]

freq = {}

for num in nums:
    freq[num] = freq.get(num, 0) + 1

majority = max(freq, key=freq.get)


# Top K frequent elements
nums = [1, 1, 1, 2, 2, 3]

freq = Counter(nums)

top_k = freq.most_common(2)


# Intersection of two arrays
a = [1, 2, 2, 3]
b = [2, 2, 4]

result = list((Counter(a) & Counter(b)).elements())
```

## 28. Dictionary Time Complexity

| Operation | Average Time |
|---|---:|
| Access by key | O(1) |
| Insert key-value | O(1) |
| Update value | O(1) |
| Delete key | O(1) |
| Search key | O(1) |
| `key in dict` | O(1) |
| `get()` | O(1) |
| `pop()` | O(1) |
| `keys()` | O(1) |
| `values()` | O(1) |
| `items()` | O(1) |
| Copy dictionary | O(n) |
| Iterate dictionary | O(n) |
| Sort dictionary | O(n log n) |

*Average-case complexities; worst-case lookup can be O(n).*

## 29. Quick Reference

| Task | Python |
|---|---|
| Create | `d = {}` |
| Add | `d[key] = value` |
| Access | `d[key]` |
| Safe access | `d.get(key, default)` |
| Update | `d.update(other)` |
| Delete | `del d[key]` |
| Remove and return | `d.pop(key)` |
| Remove last item | `d.popitem()` |
| Clear | `d.clear()` |
| Check key | `key in d` |
| Length | `len(d)` |
| Get keys | `d.keys()` |
| Get values | `d.values()` |
| Get pairs | `d.items()` |
| Copy | `d.copy()` |
| Sort keys | `sorted(d)` |
| Sort by values | `sorted(d.items(), key=lambda x: x[1])` |
| Merge | `d1 \| d2` |
| Frequency | `Counter(arr)` |
| Default dictionary | `defaultdict(int)` |
| Dictionary comprehension | `{k: v for k, v in items}` |
| Key with max value | `max(d, key=d.get)` |
| Key with min value | `min(d, key=d.get)` |
