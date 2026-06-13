I actually think Lesson 2 is the point where readers should stop just predicting outputs and start **writing small pieces of code**. Backend engineers manipulate strings constantly.

I would keep your original P1–P5 and add **three coding exercises** that feel realistic.

---

# Lesson 2 — Strings

## Review of Lesson 1

A quick review before moving on:

* **P1** — Perfect. You know the division operators.
* **P2** — Correct. Remember Python's exact type names: `str`, `float`, `bool`, `NoneType`, and `int`.
* **P3** — Correct. Python allows rebinding names to different types because of dynamic typing.
* **P4** — Correct, although the exercise asked you to print both the values and their types. Reading requirements carefully is a real engineering skill.
* **P5** — Correct. `True` behaves like `1` and `False` behaves like `0`.

### One Small Engineering Habit

Use realistic test data.

For example:

```python
height = 3.8
```

This is valid Python, but unrealistic. Backend systems often fail at the boundaries of valid input. Using plausible values helps reveal problems earlier.

---

## Why Strings Matter

Strings are one of the most important data types in backend engineering.

Almost everything entering your application arrives as text:

* Request bodies
* Query parameters
* Form inputs
* JSON fields
* Email addresses
* Authentication tokens

Being comfortable with strings is essential.

---

## Creating Strings

```python
# Single or double quotes — identical behavior
a = 'hello'
b = "hello"

# Triple quotes — for multi-line strings
message = """
Dear San,
Your application was received.
"""

# Checking length
print(len("hello"))   # 5
```

---

## String Indexing

Strings are sequences. Every character has a position starting at 0:

```
 S  a  n
 0  1  2
-3 -2 -1
```

```python
name = "San"

print(name[0])    # S
print(name[1])    # a
print(name[-1])   # n
print(name[-2])   # a
```

Negative indexing is something Python does that Java doesn't. `-1` is always the last element.

---

## Slicing

You can extract a portion of a string using `[start:end]`.

The `start` is inclusive and the `end` is exclusive.

```python
text = "backend"

print(text[0:4])    # back
print(text[4:])     # end
print(text[:4])     # back
print(text[-3:])    # end
print(text[::-1])   # dnekcab
```

`[::-1]` uses a step of `-1`, meaning "walk backwards".

---

## String Methods

```python
email = "  San@Example.COM  "

print(email.strip())          # "San@Example.COM"
print(email.strip().lower())  # "san@example.com"
print(email.strip().upper())  # "SAN@EXAMPLE.COM"

text = "hello world"

print(text.replace("world", "backend"))
print(text.split(" "))
print(text.startswith("hello"))
print(text.endswith("world"))
print("world" in text)
```

Methods can be chained:

```python
email.strip().lower()
```

The result of one method becomes the input for the next.

---

## Mental Model: `split()`

`split()` does **not** modify the original string.

It creates a **new list**.

Original:

```python
"one,two,three,four"
```

After:

```python
["one", "two", "three", "four"]
```

The string stays the same.

The list is new.

---

## String Formatting — Three Ways

```python
name = "San"
age = 23

print("Hello %s, you are %d years old" % (name, age))

print("Hello {}, you are {} years old".format(name, age))

print(f"Hello {name}, you are {age} years old")
```

Modern Python prefers **f-strings**.

```python
price = 49.99
quantity = 3

print(f"Total: {price * quantity}")
print(f"Total: {price * quantity:.2f}")
print(f"Name: {name.upper()}")
```

---

## Strings Are Immutable

You cannot change a character in a string.

```python
name = "San"
name[0] = "s"
```

This produces:

```python
TypeError
```

String methods return new strings instead.

```python
name = "San"
lower_name = name.lower()

print(name)
print(lower_name)
```

Output:

```text
San
san
```

---

# Practice

## P1. Predict the output.

```python
text = "Python"

print(text[1])
print(text[-2])
print(text[1:4])
print(text[::-1])
```

---

## P2.

Given:

```python
raw_input = "   Hello, World!   "
```

Using only string methods, produce:

```text
hello, world!
```

Do it in one line.

---

## P3.

A user submits:

```python
"  USER@GMAIL.COM  "
```

Write code that:

* Strips whitespace
* Converts to lowercase
* Checks if it ends with `"@gmail.com"`
* Prints `"Valid Gmail"` or `"Not Gmail"`

---

## P4. Predict the output and explain why.

```python
a = "hello"
b = a

a = a.upper()

print(a)
print(b)
print(a is b)
```

---

## P5. What does this print?

```python
text = "one,two,three,four"

parts = text.split(",")

print(parts[0])
print(parts[-1])
print(len(parts))
```

---

# Coding Exercises

These require you to write code from scratch.

---

## C1. Username Generator

Write a program that takes a user's full name and generates a username.

Example:

```python
full_name = "   San Win   "
```

Output:

```text
san_win_oo
```

Requirements:

* Remove extra whitespace.
* Convert everything to lowercase.
* Replace spaces with underscores.
* Print the final username.

---

## C2. Password Strength Checker

Given:

```python
password = input("Enter password: ")
```

Print:

```text
Strong Password
```

if the password:

* Has at least 8 characters.
* Contains at least one digit.

Otherwise print:

```text
Weak Password
```

**Hint:** You may need a loop and the string method `isdigit()`.

---

## C3. Log Parser

Backend services often store logs like this:

```python
log = "ERROR:Database connection failed"
```

Write code that splits the log into:

```text
Level: ERROR
Message: Database connection failed
```

Requirements:

* Use `split()`.
* Print using f-strings.

---

# Reflection Questions

After completing the exercises, think about these:

* Why does `text[::-1]` work?
* Why does `lower()` not change the original string?
* When would `split()` be useful in backend development?
* Which string methods do you think you'll use most often, and why?

---

### Before Lesson 3

For every prediction exercise:

1. Predict the output.
2. Explain your reasoning.
3. Run the code.
4. Compare the result with your prediction.
5. Ask yourself why you were right or wrong.

That gap between prediction and reality is where understanding grows.
