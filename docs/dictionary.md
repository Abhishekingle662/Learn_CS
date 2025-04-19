# 🧠 Understanding Python Dictionaries

Python dictionaries are a fundamental and powerful data structure that allows you to store and manipulate data using key-value pairs.

## 📘 What Is a Python Dictionary?

A dictionary in Python is a mutable, unordered collection of items. Each item consists of a key and its associated value. Keys must be unique and immutable (like strings, numbers, or tuples), while values can be of any data type.

Think of a real-world dictionary: you look up a word (the key) to find its definition (the value). Similarly, in Python:

```python
my_dict = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}
```

Here, `"name"`, `"age"`, and `"city"` are keys, and their corresponding values are `"Alice"`, `30`, and `"New York"`.

## 🛠️ Creating Dictionaries

### 1. Using Curly Braces `{}`
```python
person = {"name": "Bob", "age": 25}
```

### 2. Using the `dict()` Constructor
```python
person = dict(name="Bob", age=25)
```

### 3. Creating an Empty Dictionary
```python
empty_dict = {}
# or
empty_dict = dict()
```

## 🔍 Accessing and Modifying Items

### Accessing Values
```python
print(person["name"])  # Outputs: Bob
```

### Adding or Updating Items
```python
person["city"] = "Los Angeles"  # Adds a new key-value pair
person["age"] = 26              # Updates the existing value
```

### Removing Items
```python
del person["age"]               # Removes the key 'age'
city = person.pop("city")       # Removes 'city' and returns its value
```

## 🔄 Iterating Through a Dictionary

### Iterating Over Keys
```python
for key in person:
    print(key)
```

### Iterating Over Values
```python
for value in person.values():
    print(value)
```

### Iterating Over Key-Value Pairs
```python
for key, value in person.items():
    print(f"{key}: {value}")
```

## 🧰 Useful Dictionary Methods

- `get(key, default)` – Returns the value for `key` if `key` is in the dictionary; otherwise, returns `default`.
- `keys()` – Returns a view object of all keys.
- `values()` – Returns a view object of all values.
- `items()` – Returns a view object of all key-value pairs.
- `update(other_dict)` – Updates the dictionary with key-value pairs from `other_dict`.
- `clear()` – Removes all items from the dictionary.

## 🧠 Dictionary Comprehensions

Dictionary comprehensions provide a concise way to create dictionaries:

```python
squares = {x: x**2 for x in range(5)}
print(squares)  # Outputs: {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

You can also add conditions:

```python
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}
```

## 🧪 Practical Example

Let's say you have a list of fruits and their quantities:

```python
fruits = [("apple", 2), ("banana", 3), ("orange", 1)]
fruit_dict = dict(fruits)
print(fruit_dict)
```

This will output:

```python
{'apple': 2, 'banana': 3, 'orange': 1}
```

## 📚 Further Learning

- [Dictionaries in Python](https://realpython.com/python-dicts/?utm_source=chatgpt.com)
- [Python Dictionaries: A Comprehensive Tutorial (with 52 Code Examples)](https://www.dataquest.io/blog/python-dictionaries/?utm_source=chatgpt.com)
- [Python Dictionary Comprehensions: How and When to Use Them](https://realpython.com/python-dictionary-comprehension/?utm_source=chatgpt.com)
- [Python Tutorial for Beginners 5: Dictionaries](https://www.youtube.com/watch?v=daefaLgNkw0&utm_source=chatgpt.com)

---

## 🧠 Advanced Python Dictionary Techniques in LeetCode

Python dictionaries are versatile tools in solving complex algorithmic problems. Below are advanced techniques and patterns demonstrating their power:

### 1. Hash Maps for Constant-Time Lookups

**Problem:** Two Sum  
**Concept:** Use a dictionary to store elements and their indices for O(1) lookups.

```python
def two_sum(nums, target):
    num_map = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in num_map:
            return [num_map[complement], i]
        num_map[num] = i
```

### 2. Counting Frequencies with `collections.Counter`

**Problem:** Uncommon Words from Two Sentences  
**Concept:** Utilize `Counter` to count word frequencies efficiently.

```python
from collections import Counter

def uncommon_from_sentences(s1, s2):
    count = Counter((s1 + " " + s2).split())
    return [word for word in count if count[word] == 1]
```

### 3. Grouping Anagrams

**Problem:** Group Anagrams  
**Concept:** Use a dictionary with sorted word tuples as keys to group anagrams.

```python
from collections import defaultdict

def group_anagrams(strs):
    anagrams = defaultdict(list)
    for word in strs:
        key = tuple(sorted(word))
        anagrams[key].append(word)
    return list(anagrams.values())
```

### 4. Sliding Window with Hash Maps

**Problem:** Longest Substring Without Repeating Characters  
**Concept:** Maintain a sliding window and use a dictionary to track characters' indices.

```python
def length_of_longest_substring(s):
    char_index = {}
    left = max_length = 0
    for right, char in enumerate(s):
        if char in char_index and char_index[char] >= left:
            left = char_index[char] + 1
        char_index[char] = right
        max_length = max(max_length, right - left + 1)
    return max_length
```

### 5. Topological Sorting with Dictionaries

**Problem:** Alien Dictionary  
**Concept:** Build adjacency lists and in-degree counts using dictionaries for topological sorting.

```python
from collections import defaultdict, deque

def alien_order(words):
    adj = defaultdict(set)
    in_degree = {char: 0 for word in words for char in word}
    
    for first, second in zip(words, words[1:]):
        for c1, c2 in zip(first, second):
            if c1 != c2:
                if c2 not in adj[c1]:
                    adj[c1].add(c2)
                    in_degree[c2] += 1
                break
        else:
            if len(second) < len(first):
                return ""
    
    queue = deque([c for c in in_degree if in_degree[c] == 0])
    order = []
    while queue:
        c = queue.popleft()
        order.append(c)
        for neighbor in adj[c]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    
    return "".join(order) if len(order) == len(in_degree) else ""
```

### 6. Dynamic Programming with Memoization

**Problem:** Word Break  
**Concept:** Use a dictionary to memoize results of subproblems to avoid redundant computations.

```python
def word_break(s, word_dict):
    memo = {}
    
    def can_break(start):
        if start == len(s):
            return True
        if start in memo:
            return memo[start]
        for end in range(start + 1, len(s) + 1):
            if s[start:end] in word_dict and can_break(end):
                memo[start] = True
                return True
        memo[start] = False
        return False
    
    return can_break(0)
```