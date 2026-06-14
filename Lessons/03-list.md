# Lesson 3 — Lists

If strings are the most common type for data coming **into** your backend, lists are the most common type for data moving **through** it.

Collections of users, database query results, items in an order, API responses—almost everything in backend work is a sequence of things.

---

# What Is a List?

A list is an **ordered, mutable collection** of items.

Unlike strings:

* Lists can be changed after creation.
* Lists can grow or shrink dynamically.

Unlike Java arrays:

* Lists can hold mixed types.
* Lists don't require a fixed size.

```python
# A list of integers
scores = [95, 87, 92, 78]

# A list of strings
names = ["Alice", "Bob", "San"]

# Mixed types
mixed = [1, "hello", True, 3.14]

# Empty list
empty = []
```

Although Python allows mixed types, good backend code usually doesn't.

You'll commonly see:

* List of users
* List of strings
* List of dictionaries
* List of database records

Mixed-type lists are often a code smell.

---

# Indexing and Slicing

Lists work just like strings.

```python
names = ["Alice", "Bob", "San", "Dana"]
#          0        1      2      3
#         -4       -3     -2     -1

print(names[0])     # Alice
print(names[-1])    # Dana
print(names[1:3])   # ["Bob", "San"]
```

Remember:

* Start is inclusive.
* End is exclusive.

---

# Mutability — The Biggest Difference

Strings are immutable.

Lists are mutable.

```python
names = ["Alice", "Bob", "San"]

names[1] = "Charlie"

print(names)
```

Output:

```text
['Alice', 'Charlie', 'San']
```

The list object itself changed.

No new list was created.

---

# Common List Methods

These are the methods you'll use constantly.

```python
users = ["Alice", "Bob"]

# Adding items
users.append("San")
users.insert(0, "Admin")

print(users)
```

Output:

```text
['Admin', 'Alice', 'Bob', 'San']
```

---

## Removing Items

```python
users.remove("Bob")

popped = users.pop()

popped_at = users.pop(0)
```

Difference:

* `remove(value)` → removes by value
* `pop()` → removes by index and returns the item

---

## Membership

```python
print("Alice" in users)
```

Output:

```text
True
```

---

## Length

```python
print(len(users))
```

---

## Sorting

```python
numbers = [3, 1, 4, 1, 5, 9]

numbers.sort()

print(numbers)
```

Output:

```text
[1, 1, 3, 4, 5, 9]
```

---

## `sort()` vs `sorted()`

This distinction matters.

```python
numbers = [3, 1, 4]

numbers.sort()

print(numbers)
```

The original list changes.

---

```python
numbers = [3, 1, 4]

result = sorted(numbers)

print(numbers)
print(result)
```

Output:

```text
[3, 1, 4]
[1, 3, 4]
```

`sorted()` creates a new list.

The original stays unchanged.

---

# Mental Model

Python often gives you two choices:

**Modify the existing object**

or

**Create a new object.**

Knowing which one you're using prevents many bugs.

---

# Iterating Over Lists

Most of the time:

```python
names = ["Alice", "Bob", "San"]

for name in names:
    print(name)
```

---

## Getting the Index

```python
for index, name in enumerate(names):
    print(index, name)
```

Output:

```text
0 Alice
1 Bob
2 San
```

Use `enumerate()`.

Avoid this unless necessary:

```python
for i in range(len(names)):
    ...
```

That's usually carrying over Java habits.

---

# Practice

## P1. Predict the Output

```python
items = [10, 20, 30, 40, 50]

print(items[1])
print(items[-2])
print(items[1:4])

items[0] = 99

print(items)
```

---

## P2. Manipulating Lists

Start with:

```python
users = ["Alice", "Bob", "Charlie"]
```

Write code that:

* Adds `"Dana"` to the end
* Adds `"Admin"` at the beginning
* Removes `"Bob"`
* Prints the final list

---

## P3. Memory and References

Predict the output and explain what happens.

```python
a = [1, 2, 3]

b = a

a.append(4)

print(b)
```

Use the name/object model from Lesson 1.

---

## P4. Working With Scores

```python
scores = [88, 72, 95, 61, 84]
```

Write code that:

* Prints the highest score
* Prints the lowest score
* Prints the total number of scores
* Prints the scores in ascending order without modifying the original list

**Hint:** `max()`, `min()`, `len()`, and `sorted()`.

---

## P5. Explain the Difference

```python
numbers = [3, 1, 2]

# Option A
numbers.sort()

# Option B
result = sorted(numbers)
```

Explain:

* What happens to `numbers`
* What happens to `result`
* Which one changes the original list

---

# Coding Exercises

These are closer to real backend work.

---

## C1. User Registration Queue

Start with:

```python
users = ["Alice", "Bob"]
```

Write code that:

* Adds `"Charlie"` and `"Dana"` to the queue
* Removes the first user who has been processed
* Prints the processed user
* Prints the remaining queue

---

## C2. Shopping Cart

Start with:

```python
cart = ["Laptop", "Mouse", "Keyboard"]
```

Write code that:

* Adds `"Monitor"`
* Removes `"Mouse"`
* Checks whether `"Keyboard"` is still in the cart
* Prints the final cart

---

## C3. Student Scores Analyzer

Given:

```python
scores = [78, 92, 85, 67, 95, 88]
```

Write code that:

* Prints the highest score
* Prints the lowest score
* Prints the average score
* Prints the sorted scores without modifying the original list

---

## C4. Backend Log Filter

Backend logs often arrive as lists:

```python
logs = [
    "INFO:Server started",
    "ERROR:Database failed",
    "INFO:User logged in",
    "ERROR:Invalid token"
]
```

Write code that prints only the log messages containing:

```text
ERROR
```

Expected output:

```text
ERROR:Database failed
ERROR:Invalid token
```

---

# Challenge

## CH1. The Shared List Bug

Predict the output before running.

```python
a = ["Python", "Java"]
b = a

b.remove("Java")
b.append("Go")

print(a)
print(b)
print(a is b)
```

Explain the behavior using the name/object model.

---

# Reflection Questions

After completing this lesson, think about these:

* Why are lists called mutable?
* When should you use `sorted()` instead of `sort()`?
* Why can shared references become dangerous in backend applications?
* Why is `enumerate()` preferred over `range(len(...))` in Python?

---

## Before Lesson 4

For every exercise:

1. Predict the outcome.
2. Explain your reasoning.
3. Write the code yourself.
4. Run it.
5. Compare prediction vs reality.

Understanding grows in the gap between what you expected Python to do and what it actually did.

---
