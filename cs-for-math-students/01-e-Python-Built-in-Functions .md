
# Python Built-in Functions  
## Mathematical Foundations and Functional Programming Concepts

## Overview

Python provides a rich set of **built-in functions** that are immediately available without importing external modules.

Examples include:

- `print()`
- `type()`
- `len()`
- `abs()`
- `sum()`
- `max()`
- `map()`
- `filter()`

These functions represent fundamental computational tools. Many of them correspond closely to the **mathematical concept of a function**, while others perform operations with **side effects**.

Understanding this connection helps bridge the gap between:

- **mathematical reasoning**
- **computational thinking**
- **programming practice**

---

# 1. Mathematical Definition of a Function

In mathematics, a **function** is a mapping between two sets.

Formal notation:

```

f : A → B

```

where

- **A** = domain
- **B** = codomain
- each element of A corresponds to **exactly one element of B**

Example:

```

f(x) = x²

```

If

```

x = 3

```

then

```

f(3) = 9

```

Graphically:

```

Domain      Function        Codomain
x   ─────── f ───────►    f(x)

```

Example mapping:

```

1 → 1
2 → 4
3 → 9

````

Thus a function is a **rule transforming inputs into outputs**.

---

# 2. Functions in Python

Python functions follow a similar conceptual model.

General structure:

```python
result = function(argument)
````

Example:

```python
abs(-5)
```

Output:

```
5
```

Mathematically:

```
f(x) = |x|
```

Therefore, a Python function may be interpreted as a **computational implementation of a mathematical mapping**.

---

# 3. Built-in Functions

Python includes many **built-in functions** available globally.

Example:

```python
print("Hello")
```

No import is required.

List them:

```python
dir(__builtins__)
```

Official documentation:

[https://docs.python.org/3/library/functions.html](https://docs.python.org/3/library/functions.html)

---

# 4. Functions as Mathematical Mappings

Many Python functions correspond directly to mathematical operations.

| Python Function | Mathematical Interpretation |
| --------------- | --------------------------- |
| `abs(x)`        | absolute value              |
| `len(S)`        | cardinality of a set        |
| `sum(S)`        | summation                   |
| `max(S)`        | supremum                    |

Example:

```python
sum([1,2,3])
```

Output:

```
6
```

Mathematically:

```
Σ xi
```

---

# 5. Example Built-in Functions

## `print()`

Displays information on the console.

```python
print("Hello")
```

Output:

```
Hello
```

Unlike mathematical functions, `print()` produces a **side effect** rather than a value.

---

## `type()`

Returns the **type of an object**.

```python
a = 2
type(a)
```

Output:

```
<class 'int'>
```

Mathematical interpretation:

```
type : Objects → Classes
```

Example:

```
type(2) → int
type(3.14) → float
type("abc") → str
```

---

## `len()`

Returns the number of elements.

```python
len("hello")
```

Output:

```
5
```

Mathematical equivalent:

```
len : Collection → ℕ
```

This corresponds to the **cardinality of a set**.

---

# 6. Pure Functions vs Side Effects

In mathematics, functions are **pure**.

```
f(x) → y
```

Properties:

* deterministic
* no external state
* same input → same output

Example:

```
f(x) = x²
```

In programming, functions may also produce **side effects**.

Example:

```python
print(x)
```

Effects may include:

* writing to the console
* modifying variables
* interacting with files

Thus we distinguish:

### Pure Functions

Examples:

```
abs()
len()
sum()
max()
```

### Functions with Side Effects

Examples:

```
print()
input()
open()
```

---

# 7. Functions as First-Class Objects

In Python, **functions are first-class objects**.

This means they can be:

* assigned to variables
* passed as arguments
* returned from functions

Example:

```python
def square(x):
    return x*x

f = square

f(3)
```

Output:

```
9
```

Thus:

```
function → object
```

This idea is central in **functional programming**.

---

# 8. Lambda Functions

Python supports **anonymous functions** using `lambda`.

Example:

```python
f = lambda x: x**2
```

Usage:

```python
f(4)
```

Output:

```
16
```

Equivalent mathematical notation:

```
f(x) = x²
```

Lambda expressions originate from **Lambda Calculus**, a formal system introduced by **Alonzo Church** in the 1930s.

---

# 9. Functional Programming Tools

Python includes built-in tools inspired by functional programming.

## `map()`

Applies a function to each element.

```python
list(map(lambda x: x**2, [1,2,3]))
```

Output:

```
[1,4,9]
```

Mathematical interpretation:

```
map(f, S) = { f(x) | x ∈ S }
```

---

## `filter()`

Selects elements satisfying a condition.

```python
list(filter(lambda x: x%2==0, [1,2,3,4]))
```

Output:

```
[2,4]
```

Mathematical interpretation:

```
{ x ∈ S | P(x) }
```

---

## `reduce()`

Performs cumulative operations.

```python
from functools import reduce

reduce(lambda a,b: a+b, [1,2,3,4])
```

Output:

```
10
```

Equivalent to:

```
1 + 2 + 3 + 4
```

---

# 10. Everything is an Object

A fundamental principle of Python:

> **Everything is an object**

Example:

```python
type(2)
```

Output:

```
<class 'int'>
```

Classes themselves also have types:

```python
type(int)
```

Output:

```
<class 'type'>
```

Even more interesting:

```python
type(type)
```

Output:

```
<class 'type'>
```

This means that:

```
type : Class → Metaclass
```

`type` is therefore the **metaclass of all Python classes**.

---

# 11. Conceptual Diagram

Mathematics:

```
x ∈ Domain
      │
      ▼
   Function
      │
      ▼
y ∈ Codomain
```

Python:

```
object
   │
   ▼
function()
   │
   ▼
result
```

Functional programming:

```
function → object → argument of another function
```

---

# Conclusion

Python built-in functions provide powerful computational abstractions.

Many correspond directly to **mathematical functions**, while others perform **side effects necessary for interaction with the real world**.

Understanding these ideas connects:

* mathematics
* computer science
* programming practice

---

# References

Python Documentation
[https://docs.python.org/3/library/functions.html](https://docs.python.org/3/library/functions.html)

Abelson & Sussman
Structure and Interpretation of Computer Programs

Alonzo Church
Lambda Calculus


