
# Python Arrays Cheatsheet

## 1. Creating Arrays

```python
# Using list
arr = [10, 20, 30, 40, 50]

# Empty array
arr = []

# Same value repeated
arr = [0] * 5

# Using range
arr = list(range(1, 6))

# 2D array
matrix = [[1, 2, 3], [4, 5, 6]]

# Array with fixed initial values
arr = [1, 2, 3, 4, 5]
```

## 2. Accessing Elements

```python
arr = [10, 20, 30, 40, 50]

arr[0]       # First element: 10
arr[-1]      # Last element: 50
arr[-2]      # Second last: 40
arr[1]       # Element at index 1
arr[0:3]     # [10, 20, 30]
arr[:3]      # First three elements
arr[2:]      # From index 2
arr[::-1]    # Reverse array
```

## 3. Adding Elements

```python
arr = [10, 20, 30]

arr.append(40)          # Add at end
arr.insert(1, 15)       # Insert at index
arr.extend([40, 50])    # Add multiple elements

arr += [60, 70]         # Add another list
```

## 4. Removing Elements

```python
arr = [10, 20, 30, 40, 50]

arr.pop()          # Remove last element
arr.pop(1)         # Remove element at index 1
arr.remove(30)     # Remove first occurrence of value
arr.clear()        # Remove all elements

del arr[0]         # Delete element at index
del arr[1:3]       # Delete a range
```

## 5. Updating Elements

```python
arr = [10, 20, 30, 40]

arr[0] = 100       # Update element
arr[1:3] = [200, 300]
```

## 6. Searching Elements

```python
arr = [10, 20, 30, 20, 40]

20 in arr              # True
50 not in arr          # True
arr.index(20)          # First occurrence index
arr.count(20)          # Number of occurrences

# Find index safely
if 30 in arr:
    print(arr.index(30))
```

## 7. Sorting and Reversing

```python
arr = [5, 2, 8, 1, 9]

arr.sort()                 # Ascending
arr.sort(reverse=True)     # Descending

sorted(arr)                # Returns new sorted list
sorted(arr, reverse=True)

arr.reverse()              # Reverse in-place
arr[::-1]                  # Reversed copy
```

## 8. Length, Minimum, Maximum, Sum

```python
arr = [10, 20, 30, 40]

len(arr)       # 4
min(arr)       # 10
max(arr)       # 40
sum(arr)       # 100

sum(arr) / len(arr)    # Average
```

## 9. Looping Through Arrays

```python
arr = [10, 20, 30]

# Direct iteration
for x in arr:
    print(x)

# Using index
for i in range(len(arr)):
    print(arr[i])

# Index and value
for i, value in enumerate(arr):
    print(i, value)

# Reverse iteration
for x in reversed(arr):
    print(x)
```

## 10. List Comprehension

```python
arr = [1, 2, 3, 4, 5]

# Square each element
squares = [x * x for x in arr]

# Even numbers
evens = [x for x in arr if x % 2 == 0]

# Odd numbers
odds = [x for x in arr if x % 2 != 0]

# Conditional transformation
result = [x if x > 0 else 0 for x in arr]

# Nested loops
pairs = [(x, y) for x in [1, 2] for y in [3, 4]]
```

## 11. Copying Arrays

```python
arr = [1, 2, 3]

a = arr.copy()
b = arr[:]
c = list(arr)

# Shallow copy
import copy
d = copy.copy(arr)

# Deep copy for nested lists
matrix = [[1, 2], [3, 4]]
new_matrix = copy.deepcopy(matrix)
```

## 12. Combining Arrays

```python
a = [1, 2, 3]
b = [4, 5, 6]

c = a + b                 # Concatenation
a.extend(b)               # Modify a
c = [*a, *b]              # Unpacking

# Join multiple arrays
arrays = [[1, 2], [3, 4], [5, 6]]
result = [x for sub in arrays for x in sub]
```

## 13. Finding Duplicates

```python
arr = [1, 2, 2, 3, 3, 4]

# Remove duplicates
unique = list(set(arr))

# Preserve order
unique = list(dict.fromkeys(arr))

# Find duplicates
duplicates = [x for x in set(arr) if arr.count(x) > 1]
```

## 14. Frequency Counting

```python
arr = [1, 2, 2, 3, 3, 3]

# Using count
arr.count(2)

# Using dictionary
freq = {}

for x in arr:
    freq[x] = freq.get(x, 0) + 1

# Using Counter
from collections import Counter
freq = Counter(arr)

freq[2]
freq.most_common(1)
```

## 15. Useful Array Operations

```python
arr = [1, 2, 3, 4, 5]

# First element
first = arr[0]

# Last element
last = arr[-1]

# Middle element
mid = arr[len(arr) // 2]

# Swap elements
arr[0], arr[1] = arr[1], arr[0]

# Rotate left by one
arr = arr[1:] + arr[:1]

# Rotate right by one
arr = arr[-1:] + arr[:-1]

# Check empty
if not arr:
    print("Empty")

# Check non-empty
if arr:
    print("Not empty")
```

## 16. Two-Dimensional Arrays

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Access element
matrix[0][0]

# Number of rows
len(matrix)

# Number of columns
len(matrix[0])

# Iterate rows
for row in matrix:
    print(row)

# Iterate elements
for row in matrix:
    for value in row:
        print(value)

# Iterate using indexes
for i in range(len(matrix)):
    for j in range(len(matrix[0])):
        print(matrix[i][j])

# Transpose
transpose = list(zip(*matrix))

# Flatten matrix
flat = [x for row in matrix for x in row]
```

## 17. Creating 2D Arrays Correctly

```python
# Correct: independent rows
matrix = [[0] * 3 for _ in range(3)]

# Avoid: all rows refer to the same list
matrix = [[0] * 3] * 3
```

## 18. Array Slicing

```python
arr = [0, 1, 2, 3, 4, 5]

arr[1:4]       # [1, 2, 3]
arr[:3]        # [0, 1, 2]
arr[3:]        # [3, 4, 5]
arr[::2]       # [0, 2, 4]
arr[1::2]      # [1, 3, 5]
arr[::-1]      # Reverse
arr[1:5:2]     # [1, 3]

# Replace slice
arr[1:3] = [10, 20]

# Delete slice
del arr[1:3]
```

## 19. Zip and Enumerate

```python
a = [1, 2, 3]
b = [4, 5, 6]

# Pair elements
for x, y in zip(a, b):
    print(x, y)

# Index and value
for i, value in enumerate(a):
    print(i, value)

# Convert zipped values
pairs = list(zip(a, b))

# Unzip
x, y = zip(*pairs)
```

## 20. Stack Using Array

```python
stack = []

stack.append(10)     # Push
stack.append(20)
stack.append(30)

stack.pop()          # Pop
stack[-1]            # Peek
len(stack)           # Size

if stack:
    print(stack[-1])
```

## 21. Queue Using Array

```python
from collections import deque

queue = deque()

queue.append(10)       # Enqueue
queue.append(20)
queue.append(30)

queue.popleft()        # Dequeue
queue[0]               # Front
queue[-1]              # Rear
len(queue)             # Size
```

## 22. Binary Search

```python
from bisect import bisect_left, bisect_right

arr = [10, 20, 20, 30, 40, 50]

# Insert position before duplicates
bisect_left(arr, 20)

# Insert position after duplicates
bisect_right(arr, 20)

# Search element
i = bisect_left(arr, 30)

if i < len(arr) and arr[i] == 30:
    print("Found")
```

## 23. Prefix Sum

```python
arr = [1, 2, 3, 4, 5]

prefix = [0]

for x in arr:
    prefix.append(prefix[-1] + x)

# Sum from index l to r (inclusive)
l, r = 1, 3
result = prefix[r + 1] - prefix[l]
```

## 24. Sliding Window

```python
arr = [1, 2, 3, 4, 5]
k = 3

window_sum = sum(arr[:k])
max_sum = window_sum

for i in range(k, len(arr)):
    window_sum += arr[i] - arr[i - k]
    max_sum = max(max_sum, window_sum)

print(max_sum)
```

## 25. Two Pointers

```python
arr = [1, 2, 3, 4, 5]

left = 0
right = len(arr) - 1

while left < right:
    # Process elements
    left += 1
    right -= 1
```

## 26. Common Array Patterns

```python
# Find largest
largest = max(arr)

# Find smallest
smallest = min(arr)

# Second largest distinct
unique = sorted(set(arr))
second_largest = unique[-2] if len(unique) >= 2 else None

# Reverse without built-in
left, right = 0, len(arr) - 1

while left < right:
    arr[left], arr[right] = arr[right], arr[left]
    left += 1
    right -= 1

# Move zeroes to end
non_zero = [x for x in arr if x != 0]
result = non_zero + [0] * (len(arr) - len(non_zero))

# Check sorted
is_sorted = all(arr[i] <= arr[i + 1] for i in range(len(arr) - 1))

# Find missing number from 0 to n
n = len(arr)
missing = n * (n + 1) // 2 - sum(arr)
```

## 27. Python Array Module

Python lists are dynamic arrays. The `array` module provides typed arrays.

```python
from array import array

# Integer array
arr = array('i', [1, 2, 3, 4])

# Float array
floats = array('f', [1.1, 2.2, 3.3])

arr.append(5)
arr.insert(1, 10)
arr.pop()
arr.remove(3)

arr[0]
len(arr)
```

Common type codes:

```python
'i'    # Signed integer
'I'    # Unsigned integer
'f'    # Float
'd'    # Double
```

## 28. NumPy Arrays

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

# Create arrays
np.zeros(5)
np.ones(5)
np.arange(1, 6)
np.linspace(0, 10, 5)

# Dimensions and shape
arr.shape
arr.ndim
arr.size
arr.dtype

# Operations
arr + 10
arr * 2
arr.sum()
arr.mean()
arr.max()
arr.min()

# Reshape
matrix = np.arange(1, 10).reshape(3, 3)

# Indexing
arr[0]
arr[-1]
arr[1:4]

# Boolean filtering
arr[arr > 2]
```

## 29. Time Complexity

| Operation | Average Time |
|---|---:|
| Access by index | O(1) |
| Update by index | O(1) |
| Append | O(1) amortized |
| Pop last | O(1) |
| Insert at beginning | O(n) |
| Insert at middle | O(n) |
| Delete at beginning | O(n) |
| Delete at middle | O(n) |
| Search by value | O(n) |
| `in` operator | O(n) |
| `index()` | O(n) |
| `count()` | O(n) |
| Sort | O(n log n) |
| Reverse | O(n) |
| Copy | O(n) |
| Slice | O(k), where k is slice size |

## 30. Important LeetCode Patterns

```python
# Two Sum
seen = {}

for i, x in enumerate(arr):
    target = 9 - x
    if target in seen:
        print(seen[target], i)
    seen[x] = i

# Maximum subarray sum (Kadane's Algorithm)
current = best = arr[0]

for x in arr[1:]:
    current = max(x, current + x)
    best = max(best, current)

# Remove duplicates from sorted array
write = 1

for read in range(1, len(arr)):
    if arr[read] != arr[read - 1]:
        arr[write] = arr[read]
        write += 1

# Rotate array right by k
k %= len(arr)
arr = arr[-k:] + arr[:-k]

# Merge two sorted arrays
merged = []
i = j = 0

while i < len(a) and j < len(b):
    if a[i] <= b[j]:
        merged.append(a[i])
        i += 1
    else:
        merged.append(b[j])
        j += 1

merged.extend(a[i:])
merged.extend(b[j:])
```

## 31. Quick Reference

| Task | Python |
|---|---|
| Create | `arr = []` |
| Add | `arr.append(x)` |
| Add multiple | `arr.extend(other)` |
| Insert | `arr.insert(i, x)` |
| Remove value | `arr.remove(x)` |
| Remove last | `arr.pop()` |
| Remove index | `arr.pop(i)` |
| Clear | `arr.clear()` |
| Length | `len(arr)` |
| Sum | `sum(arr)` |
| Minimum | `min(arr)` |
| Maximum | `max(arr)` |
| Sort | `arr.sort()` |
| Reverse | `arr.reverse()` |
| Search | `x in arr` |
| Find index | `arr.index(x)` |
| Count | `arr.count(x)` |
| Copy | `arr.copy()` |
| Slice | `arr[start:end]` |
| Reverse copy | `arr[::-1]` |
| Sort copy | `sorted(arr)` |
| Unique | `list(set(arr))` |
| Enumerate | `enumerate(arr)` |
| Pair arrays | `zip(a, b)` |
