# Lesson 5 — Dictionaries

If lists are the most common way to work with sequences of data, dictionaries are the most common way to work with **structured data**.

Almost everything in backend engineering maps to a dictionary at some level:

* HTTP request bodies
* JSON API responses
* Database records
* Configuration settings
* Session data
* Caches

Learning dictionaries well will pay off throughout your backend journey.

---

# What Is a Dictionary?

A dictionary is a collection of **key-value pairs**.

Each key maps to a value.

```python
user = {
    "id": 1042,
    "username": "san_win",
    "email": "san@gmail.com",
    "is_active": True
}
```

Here:

| Key           | Value             |
| ------------- | ----------------- |
| `"id"`        | `1042`            |
| `"username"`  | `"san_win"`       |
| `"email"`     | `"san@gmail.com"` |
| `"is_active"` | `True`            |

Unlike lists:

* Lists use positions (indexes).
* Dictionaries use names (keys).

---

# Why Dictionaries Exist

Lists work well for ordered collections.

However, they become difficult to understand when representing structured data.

```python
# Which index is the email?
user = [1042, "san_win", "san@gmail.com", True]

print(user[2])
```

This works, but it isn't obvious.

Compare that to:

```python
user = {
    "id": 1042,
    "username": "san_win",
    "email": "san@gmail.com"
}

print(user["email"])
```

The meaning is immediately clear.

Dictionaries are self-documenting.

---

# Fast Lookups

Dictionaries are also extremely efficient.

Looking up a value by key is generally:

```text
O(1)
```

or **constant time**.

This means that, on average, retrieving a value remains fast regardless of dictionary size.

Python achieves this using a data structure called a **hash table**.

You don't need to understand hash tables deeply yet, but remember:

> Dictionaries trade ordering by position for extremely fast lookups by key.

---

# Creating and Accessing Dictionaries

```python
user = {
    "id": 1042,
    "username": "san_win",
    "email": "san@gmail.com",
    "is_active": True
}
```

Access values using keys:

```python
print(user["username"])
```

Output:

```text
san_win
```

---

## Safe Access with `.get()`

```python
print(user.get("email"))
print(user.get("age"))
print(user.get("age", 0))
```

Output:

```text
san@gmail.com
None
0
```

---

## `[]` vs `.get()`

These behave differently.

### Using brackets

```python
user["age"]
```

Raises:

```text
KeyError
```

if the key does not exist.

---

### Using `.get()`

```python
user.get("age")
```

Returns:

```python
None
```

instead of crashing.

Or:

```python
user.get("age", 0)
```

returns a default value.

In production backend code, `.get()` is often safer when dealing with optional data.

---

# Modifying Dictionaries

```python
user = {
    "username": "san_win",
    "score": 100
}
```

---

## Adding a Key

```python
user["email"] = "san@gmail.com"
```

---

## Updating a Value

```python
user["score"] = 200
```

---

## Removing a Key

```python
del user["email"]
```

---

## Removing and Returning

```python
score = user.pop("score")

print(score)
print(user)
```

Output:

```text
200
{'username': 'san_win'}
```

---

# Essential Dictionary Methods

```python
config = {
    "host": "localhost",
    "port": 5432,
    "db": "myapp"
}
```

---

## Keys

```python
print(config.keys())
```

---

## Values

```python
print(config.values())
```

---

## Items

```python
print(config.items())
```

Output resembles:

```text
dict_items([
    ('host', 'localhost'),
    ('port', 5432),
    ('db', 'myapp')
])
```

---

## Membership

```python
print("port" in config)
print("password" in config)
```

Output:

```text
True
False
```

Notice:

> The `in` operator checks keys, not values.

---

# Iterating Through Dictionaries

The most common pattern is:

```python
for key, value in config.items():
    print(f"{key}: {value}")
```

Output:

```text
host: localhost
port: 5432
db: myapp
```

You'll use this constantly.

---

# Nested Dictionaries

Real backend data is rarely flat.

Dictionaries often contain other dictionaries and lists.

```python
user = {
    "id": 1,
    "username": "san_win",
    "address": {
        "city": "Bangkok",
        "country": "Thailand",
        "zip": "10900"
    },
    "scores": [88, 92, 75]
}
```

Access nested values:

```python
print(user["address"]["city"])
print(user["scores"][0])
```

Output:

```text
Bangkok
88
```

---

# Merging Dictionaries

Combining dictionaries is common.

```python
defaults = {
    "theme": "dark",
    "language": "en",
    "timeout": 30
}

user_prefs = {
    "theme": "light",
    "language": "th"
}
```

Merge them:

```python
merged = {
    **defaults,
    **user_prefs
}

print(merged)
```

Output:

```python
{
    'theme': 'light',
    'language': 'th',
    'timeout': 30
}
```

Keys on the right override keys on the left.

You'll use this pattern frequently in configuration systems.

---

# Practice

## P1. Predict the Output

```python
data = {"x": 10, "y": 20, "z": 30}

print(data["x"])
print(data.get("w"))
print(data.get("w", 99))
print("y" in data)

data["x"] = 999

print(data)
```

---

## P2. Explain the Error

Predict what happens.

Then explain why.

```python
data = {
    "name": "San"
}

print(data["age"])
```

---

## P3. Nested Dictionaries

Given:

```python
server = {
    "host": "prod-01",
    "specs": {
        "cpu": 8,
        "ram": 32,
        "storage": ["/dev/sda", "/dev/sdb"]
    },
    "tags": ["production", "backend", "primary"]
}
```

Without modifying the dictionary definition:

Write code that:

* Prints the host name
* Prints the RAM
* Prints the second storage device
* Prints the last tag
* Adds `"region"` with value `"ap-southeast-1"`
* Adds `"gpu"` with value `0` inside `"specs"`
* Prints the updated dictionary

---

# Coding Exercises

These are closer to real backend problems.

---

## C1. User Session Manager

Write a function called `manage_session`.

Input:

```python
events = [
    ("login", "alice"),
    ("login", "bob"),
    ("login", "san"),
    ("logout", "bob"),
    ("login", "dana"),
    ("logout", "alice"),
    ("login", "bob"),
]
```

Requirements:

* Maintain a dictionary.
* Keys are usernames.
* Values are active session counts.
* `"login"` increases the count.
* `"logout"` decreases the count.
* Never allow the count to go below zero.

After processing all events, print:

```text
Active sessions:
dana: 1
san: 1
bob: 1
```

Order does not matter.

---

## C2. Configuration Validator

Write a function called `validate_config`.

Requirements:

* Takes a configuration dictionary.
* Takes a list of required keys.
* Finds missing keys.
* Finds keys with invalid values.

Invalid values are:

* `None`
* Empty strings (`""`)

Return:

```python
(missing_keys, invalid_keys)
```

Then print:

```text
Config Validation Report
Missing keys: [...]
Invalid values: [...]
```

Test with:

```python
config = {
    "host": "",
    "port": 5432,
    "db": "myapp",
    "password": "secret"
}

required = [
    "host",
    "port",
    "db",
    "password",
    "timeout"
]
```

---

## C3. Inventory Tracker

You receive inventory updates:

```python
updates = [
    ("keyboard", 50),
    ("mouse", 30),
    ("keyboard", -10),
    ("monitor", 20),
    ("mouse", -5),
    ("keyboard", -8),
    ("monitor", -25),
    ("mouse", 10),
]
```

Write a function called `process_inventory`.

Requirements:

### Build Inventory

Create a dictionary representing inventory levels.

---

### Out-of-Stock Warnings

Print warnings for items with quantity less than or equal to zero.

Example:

```text
WARNING: monitor is out of stock (quantity: -5)
```

---

### Current Inventory

Print items with positive stock.

Sort alphabetically.

Example:

```text
Current inventory:
keyboard: 32
mouse: 35
```

---

### Total Stock

Print:

```text
Total units in stock: 67
```

Calculate everything from the data.

Do not hardcode values.

---

# Challenge — Frequency Counter

One of the most common dictionary patterns is counting.

Given:

```python
words = [
    "python",
    "backend",
    "python",
    "api",
    "backend",
    "python",
    "fastapi"
]
```

Write code that:

* Counts how many times each word appears
* Stores the results in a dictionary
* Prints:

```text
python: 3
backend: 2
api: 1
fastapi: 1
```

Do not use external libraries.

---

# Reflection Questions

Think about these after finishing the lesson:

* Why are dictionaries often better than lists for structured data?
* When should you use `.get()` instead of `[]`?
* Why are dictionary lookups fast?
* What does `in` check when used with dictionaries?
* Why are nested dictionaries so common in backend systems?

---

## Before Lesson 6

For every exercise:

1. Predict what Python will do.
2. Explain why.
3. Write the code yourself.
4. Run it.
5. Compare prediction with reality.

The goal isn't just to get the correct answer.

The goal is to understand how Python organizes and retrieves structured data—because dictionaries are everywhere in backend engineering.
