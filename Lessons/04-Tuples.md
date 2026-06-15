# Lesson 4 — Tuples

Lists are one of Python's most flexible data structures. Tuples take a different approach.

A tuple is designed for data that **belongs together and shouldn't change**.

Coordinates, database records, RGB values, and multiple values returned from a function are all common examples.

---

## What Is a Tuple?

A tuple is an **ordered, immutable collection** of items.

Once created, it cannot be modified.

```python
point = (10, 20)
colors = ("red", "green", "blue")

single = (42,)   # Single-item tuple
empty = ()
```

Notice the comma:

```python
single = (42,)
```

Without the comma:

```python
single = (42)
```

Python interprets it as an integer inside parentheses, not a tuple.

The comma is what creates the tuple.

---

## Why Do Tuples Exist?

If lists can do everything tuples can do—and more—why use tuples?

### 1. They communicate intent.

A tuple says:

> "This group of values is fixed."

A list says:

> "This collection may change."

For example:

```python
user = ("San", 20, "Bangkok")
```

This represents one fixed record.

---

### 2. They can be used as dictionary keys.

Tuples are hashable.

Lists are not.

```python
location_data = {
    (40.7128, -74.0060): "New York"
}
```

This works.

However:

```python
location_data = {
    [40.7128, -74.0060]: "New York"
}
```

raises:

```text
TypeError: unhashable type: 'list'
```

---

### 3. They have a small performance advantage.

Tuples are generally:

* Faster to create
* Faster to iterate
* More memory efficient

The difference is usually small, but it matters in performance-critical code.

---

## Indexing and Slicing

Tuples behave just like strings and lists.

```python
colors = ("red", "green", "blue")

print(colors[0])      # red
print(colors[-1])     # blue
print(colors[1:])     # ('green', 'blue')
print(len(colors))    # 3
```

---

## Immutability in Practice

Tuples cannot be modified.

```python
point = (10, 20)

point[0] = 99
```

This raises:

```text
TypeError: 'tuple' object does not support item assignment
```

The tuple structure cannot change.

---

## A Common Gotcha

Immutability applies to the tuple itself—not necessarily to the objects inside it.

```python
data = ([1, 2], [3, 4])

data[0].append(99)

print(data)
```

Output:

```python
([1, 2, 99], [3, 4])
```

The tuple still contains the same two lists.

The lists themselves are mutable.

---

## Tuple Unpacking

One of the biggest advantages of tuples is unpacking.

```python
point = (10, 20)

x, y = point

print(x)   # 10
print(y)   # 20
```

---

### Returning Multiple Values

Python functions return a single object.

That object can be a tuple.

```python
def get_user():
    return ("San", 20, "Bangkok")

name, age, city = get_user()

print(name)
```

Output:

```text
San
```

You'll see this pattern frequently in Python code.

---

## Tuple vs List

| Use a Tuple When...       | Use a List When...               |
| ------------------------- | -------------------------------- |
| Data should not change    | Data may change                  |
| The structure is fixed    | Items may be added or removed    |
| Returning multiple values | Building collections dynamically |
| Using as dictionary keys  | Working with mutable sequences   |

---

# Practice

## P1. Predict the Output

Predict before running.

```python
t = (5, 10, 15, 20)

print(t[1])
print(t[-1])
print(t[1:3])
print(len(t))
```

---

## P2. Explain the Error

What happens here?

Explain **why**, using what you know about mutability.

```python
t = (1, 2, 3)

t[0] = 99
```

---

## P3. Predict the Output

Explain the behavior using the name/object model.

```python
data = ([1, 2], [3, 4])

data[0].append(99)

print(data)
```

---

## P4. Returning Multiple Values

Write a function called `get_user_info` that:

* Returns a user's name, age, and city as a tuple
* Calls the function
* Unpacks the result into three variables
* Prints each variable

---

## P5. Single-Item Tuple

What is wrong with this code?

How do you fix it?

```python
single = (42)

print(type(single))
```

---

## P6. Backend Coordinates

A backend service returns coordinates as a tuple.

Write code that:

* Stores latitude and longitude in a tuple
* Unpacks them into two variables
* Prints them exactly as:

```text
Location: lat=13.7563, lng=100.5018
```

Use Bangkok's coordinates.

---

# Coding Exercises

These exercises require you to write complete solutions.

---

## C1. Student Records

Write a function called `get_student_record` that:

* Takes a name, grade, and GPA
* Returns them as a tuple

Then write another function called `print_student_record` that:

* Accepts the tuple as a parameter
* Unpacks it inside the function
* Prints:

```text
Name: San
Grade: 2
GPA: 3.75
```

Finally:

* Call both functions together
* Do **not** store the returned tuple in a variable

Pass the output of one function directly into the other.

---

## C2. Location Summary

You have two location tuples:

```python
bangkok = (13.7563, 100.5018)
chiang_rai = (18.7883, 98.9853)
```

Write a function called `summarize_locations` that:

* Takes both tuples as parameters
* Unpacks them inside the function
* Prints:

```text
Bangkok: lat=13.7563, lng=100.5018
Chiang Rai: lat=18.7883, lng=98.9853
```

Then:

* Calculates the absolute difference between latitudes
* Calculates the absolute difference between longitudes
* Prints:

```text
Lat diff: 5.032 | Lng diff: 1.5165
```

Do not hardcode the differences.

Calculate them.

---

## C3. API Response Parser

A backend API returns user data as a tuple:

```python
response = (
    "u_1042",
    "san_win",
    "san@gmail.com",
    "backend",
    True,
    1200
)
```

The fields are:

1. `user_id`
2. `username`
3. `email`
4. `department`
5. `is_active`
6. `reputation_score`

Write a function called `parse_and_display` that:

* Takes the tuple as a parameter
* Unpacks all six fields
* Uses a **guard clause**
* If `is_active` is `False`, immediately returns
* Otherwise prints:

```text
User: san_win (u_1042)
Department: backend
Email: san@gmail.com
Reputation: 1200
Status: ACTIVE
```

Test your function twice:

* One active user
* One inactive user

Confirm the inactive user prints nothing.

---

## C4. Leaderboard Processor

You have a leaderboard stored as a list of tuples:

```python
leaderboard = [
    ("alice", 4200),
    ("san", 3875),
    ("bob", 4950),
    ("dana", 3100),
    ("mino", 4750),
]
```

Write a function called `process_leaderboard` that:

* Takes the leaderboard as a parameter
* Sorts it by score in descending order
* Does **not** modify the original list
* Prints each entry exactly as:

```text
#1 bob — 4950
#2 mino — 4750
#3 alice — 4200
#4 san — 3875
#5 dana — 3100
```

Then print:

```text
High: 4950 | Low: 3100 | Avg: 4175.00
```

Requirements:

* Do not hardcode any values
* Calculate everything from the data
* Round the average to two decimal places

**Hint:** `sorted()` can sort tuples using the `key` parameter.

---

# Reflection Questions

Think about these after completing the exercises:

* Why would you choose a tuple instead of a list?
* Why can tuples be used as dictionary keys while lists cannot?
* What does tuple unpacking make easier?
* How can a tuple still contain mutable objects?
* When might a guard clause improve readability?

---

## Before Lesson 5

For every exercise:

1. Predict what Python will do.
2. Explain why.
3. Write the code yourself.
4. Run it.
5. Compare prediction with reality.

The goal isn't just to get the right answer.

The goal is to understand **why Python behaves the way it does**.
