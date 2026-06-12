# Lesson 1 — Variables, Types, and How Python Thinks About Data

Before any syntax, one mental model you need to carry through everything:

**In Python, variables are not boxes. They are name tags.**

When you write `x = 5`, you are not putting `5` into a container called `x`. You are creating an object `5` in memory and sticking a label `x` on it.

Think of it like this: imagine a warehouse full of objects. A variable is just a sticky note with a name on it, attached to one of those objects. You can move the sticky note to a different object anytime — that's what reassigning a variable does.

This will matter more as we go. Keep it in the back of your mind.

---

## The Basic Types

Python has a small set of built-in types you'll use constantly:

```python
# Integer — whole numbers, no decimal point
age = 22

# Float — numbers with a decimal point
gpa = 3.75

# String — text, always wrapped in quotes
name = "San"

# Boolean — only two possible values: True or False
is_student = True

# NoneType — represents "nothing" or "no value yet"
result = None
```

Nothing surprising yet. But let's understand what Python is actually doing when you write these.

---

## type() and Why It Matters

Python is **dynamically typed** — you don't have to declare what type a variable is. Python figures it out on its own when your code runs. You can always ask Python what type something is using `type()`:

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

Notice the word **class**. In Python, every single value is an object — even a simple integer. `42` is an instance of the `int` class. This is different from languages like Java where `int` is a primitive. In Python, there are no primitives — everything is an object. This is one of the most important differences between Python and Java.

---

## Dynamic Typing — The Double-Edged Sword

In Java you write `int x = 5` and `x` is locked to integers forever. Python works completely differently:

```python
x = 5
print(type(x))   # <class 'int'>

x = "hello"
print(type(x))   # <class 'str'>

x = 3.14
print(type(x))   # <class 'float'>
```

The name `x` can be rebound to any type at any time. Python doesn't stop you. This is flexible — you write less code. But it's also dangerous. In a large program, a variable unexpectedly changing type is a very common source of bugs that are hard to find.

This is exactly why Python added **type hints** in later versions — a way to optionally say "this variable should always be an int." We'll cover those later.

---

## Integers and Floats — One Trap You Need to Know Now

```python
a = 10
b = 3

print(a / b)    # 3.3333...  — always float in Python 3
print(a // b)   # 3          — floor division, drops the decimal
print(a % b)    # 1          — remainder (modulo)
print(a ** b)   # 1000       — exponentiation (10 to the power of 3)
```

The `/` operator **always returns a float** in Python 3, even if the result is a whole number:

```python
print(10 / 2)   # 5.0  not 5
```

You've already seen the opposite trap in Java where `10 / 3` gives you `3` because both sides are integers. Python 3 flipped the default — division always gives you the mathematically correct result. Use `//` when you explicitly want integer division.

---

## Strings — Just Enough For Now

Strings are sequences of characters. You can use single or double quotes — Python treats them identically:

```python
a = "hello"
b = 'hello'
print(a == b)   # True
```

A few operations you'll use constantly:

```python
name = "san"

print(len(name))         # 3        — how many characters
print(name.upper())      # SAN      — all uppercase
print(name.capitalize()) # San      — first letter uppercase
print("an" in name)      # True     — check if something is inside
```

### f-strings — The Right Way to Format Output

One of the most useful things in Python is **f-strings**. They let you embed variables directly inside a string without awkward concatenation:

```python
name = "San"
age = 22
gpa = 3.75

# Without f-string (ugly, error-prone)
print("My name is " + name + " and I am " + str(age) + " years old")

# With f-string (clean, readable)
print(f"My name is {name} and I am {age} years old")
print(f"My GPA is {gpa:.2f}")   # .2f means 2 decimal places
```

The `f` before the opening quote tells Python this is an f-string. Anything inside `{}` gets evaluated and inserted. You will use this constantly — get comfortable with it now.

Strings are also **immutable** — you cannot change a character inside a string. You can only create a new one. For example:

```python
name = "san"
name[0] = "S"   # This will crash — strings cannot be changed in place
```

Instead you do:
```python
name = "S" + name[1:]   # Create a brand new string
```

We have a full strings lesson coming. For now just know they are immutable.

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

### None — Not Zero, Not Empty, Not False

`None` is Python's way of saying "there is no value here." It is its own type — `NoneType` — and there is only one `None` object in the entire Python runtime.

You will see `None` in real code all the time — for example, when a function finds nothing to return:

```python
def find_user(user_id):
    # imagine searching a database
    if user_id == 1:
        return "San"
    return None   # nothing found

user = find_user(99)

if user is None:
    print("User not found")
else:
    print(f"Found user: {user}")
```

Notice we check `is None`, not `== None`. That's because `None` is a singleton — there is only ever one of it in memory — and `is` checks identity, not equality. This is the correct Python style.

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

## Coding Exercises

These require you to actually write and run code. No copying — type everything yourself.

---

**E1 — Student Profile Card**

Write a program that stores the following information about a student and prints it in a clean, readable format using f-strings:

- Name (string)
- Age (integer)
- GPA (float)
- Is currently enrolled (boolean)
- Scholarship amount — set this to `None` if they have no scholarship

Your output should look something like this:
```
--- Student Profile ---
Name: San
Age: 22
GPA: 3.75
Enrolled: True
Scholarship: None
```

Then add an `if` check at the end: if the scholarship is `None`, print `"No scholarship assigned yet."` Otherwise print `"Scholarship amount: {amount}"`.

---

**E2 — Division Explorer**

Write a program that takes two numbers `a = 17` and `b = 5` and prints all of the following:

- The result of true division (`/`)
- The result of floor division (`//`)
- The remainder (`%`)
- `a` to the power of `b` (`**`)
- The type of the result of `a / b`
- The type of the result of `a // b`

Then answer in a comment: why are the types of `a / b` and `a // b` different even though both inputs are integers?

---

**E3 — Type Detective**

You are given this list of variables:

```python
a = "100"
b = 100
c = 100.0
d = True
e = None
f = "None"
g = False + False + True
```

Without running the code first, write down:
1. The type of each variable
2. Which ones would make `if variable:` evaluate to `True` (truthy values)
3. Which ones would make `if variable:` evaluate to `False` (falsy values)

Then run the code to check. For anything you got wrong, write one sentence explaining why Python behaves that way.
