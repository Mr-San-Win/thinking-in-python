# Lesson 1 — Variables, Types, and How Python Thinks About Data

Before any syntax, one mental model you need to carry through everything:

**In Python, variables are not boxes. They are name tags.**

When you write `x = 5`, you are not putting `5` into a container called `x`. You are creating an object `5` in memory and sticking a label `x` on it.

This will matter more as we go. Keep it in the back of your mind.

---

## The Basic Types

Python has a small set of built-in types you'll use constantly:

```python
# Integer — whole numbers
age = 22

# Float — decimal numbers
gpa = 3.75

# String — text, always in quotes
name = "San"

# Boolean — True or False only
is_student = True

# NoneType — represents "nothing"
result = None
```

Nothing surprising yet. But let's look at what Python actually gives you when you create these.

---

## type() and Why It Matters

Python is **dynamically typed** — you don't declare types, Python figures them out at runtime. You can always ask Python what type something is:

```python
x = 42
print(type(x))        # <class 'int'>

name = "San"
print(type(name))     # <class 'str'>

flag = True
print(type(flag))     # <class 'bool'>

nothing = None
print(type(nothing))  # <class 'NoneType'>
```

Notice the word **class**. In Python, every value is an object — even a simple integer. `42` is an instance of the `int` class. This is different from languages like Java where `int` is a primitive. In Python, there are no primitives — everything is an object.

---

## Dynamic Typing — The Double-Edged Sword

In Java you write `int x = 5` and `x` is locked to integers forever. In Python:

```python
x = 5
print(type(x))   # <class 'int'>

x = "hello"
print(type(x))   # <class 'str'>

x = 3.14
print(type(x))   # <class 'float'>
```

The name `x` can be rebound to any type at any time. Python doesn't stop you. This is flexible but dangerous — in production code, a variable unexpectedly changing type is a common source of bugs. This is exactly why Python added **type hints** (we'll cover those later).

---

## Integers and Floats — One Trap You Need to Know Now

```python
a = 10
b = 3

print(a / b)    # 3.3333...  — always float in Python 3
print(a // b)   # 3          — floor division, drops the decimal
print(a % b)    # 1          — remainder
print(a ** b)   # 1000       — exponentiation
```

The `/` operator **always returns a float** in Python 3, even if the result is a whole number:

```python
print(10 / 2)   # 5.0  not 5
```

You've already seen this trap in Java with integer division. Python 3 flipped the default — division always gives you the true result. Use `//` when you explicitly want integer division.

---

## Strings — Just Enough For Now

Strings can use single or double quotes — Python treats them identically:

```python
a = "hello"
b = 'hello'
print(a == b)   # True
```

A few operations you'll use constantly:

```python
name = "san"

print(len(name))         # 3
print(name.upper())      # SAN
print(name.capitalize()) # San
print("an" in name)      # True
```

We have a full strings lesson coming. For now just know strings are **immutable** — you cannot change a character inside a string. You can only create a new one.

---

## Booleans and None

```python
is_ready = True
is_done = False

print(type(True))    # <class 'bool'>
print(True + 1)      # 2  — booleans are subclasses of int in Python
print(False + 1)     # 1
```

That last part surprises people. `True` is literally `1` and `False` is literally `0` under the hood. Useful occasionally, but don't abuse it.

`None` is Python's way of saying "no value here." It is its own type — `NoneType` — and there is only one `None` object in the entire Python runtime. That's why checking for it uses `is` not `==`:

```python
result = None

if result is None:
    print("nothing here")
```

---

## Practice

These are small. The goal is to confirm the basics are solid before we build on them. **Write your answers first, then run the code to check.**

---

**P1.** What does this output? Predict before running:

```python
x = 7
y = 2
print(x / y)
print(x // y)
print(x % y)
```

---

**P2.** What is the type of each of these? Answer without using `type()`:

```python
a = "3.14"
b = 3.14
c = True
d = None
e = 100
```

---

**P3.** Will this code run without error? If yes, what does it print? If no, why not?

```python
x = 10
x = "ten"
x = True
print(x)
print(type(x))
```

---

**P4.** Write from scratch — no copying from above:

- Create a variable `name` with your name as a string
- Create a variable `age` with your age as an integer
- Create a variable `height` with your height in meters as a float
- Create a variable `is_enrolled` set to `True`
- Print each variable on its own line along with its type

---

**P5.** What does this print, and why does it print that:

```python
print(True + True + False + True)
```

---

Post your answers here. Don't worry about getting everything right — I want to see how you reason, not just the final answer.