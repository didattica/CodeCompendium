# Python — Lambda Functions & List Comprehensions · Exercises

## `python_lambda_listcomp_exercises.md`

> **Course:** Computer Science for Mathematics Students
> **Level:** First year university
> **Prerequisites:** `python_lambda_listcomp_theory.md`

---

## Table of contents

1. [Warm-up](#1-warm-up)
2. [Lambda functions](#2-lambda-functions)
3. [`map` and `filter`](#3-map-and-filter)
4. [List comprehensions](#4-list-comprehensions)
5. [Nested structures](#5-nested-structures)
6. [Advanced problems](#6-advanced-problems)

---

## 1. Warm-up

### Exercise 1 — squares *(very easy)*

Compute:

$${x^2 \mid x \in {1,2,3,4,5}}$$

---

### 💡 Tips

* You need to **apply a transformation** to each element
* This corresponds to:

  ```python
  [expression for x in iterable]
  ```
* The expression is `x ** 2`

---

### ✅ Solution — step by step

**Step 1 — understand the math**

We are applying:

$$x \mapsto x^2$$

to each element.

---

**Step 2 — translate to Python**

```python
numbers = [1, 2, 3, 4, 5]
```

---

**Step 3 — build the comprehension**

```python
squares = [x ** 2 for x in numbers]
```

---

**Step 4 — result**

```python
print(squares)
# [1, 4, 9, 16, 25]
```

---

## 2. Lambda functions

### Exercise 2 — define a lambda *(easy)*

Define:

$$f(x) = x^3$$

and apply it to `[1,2,3,4]`.

---

### 💡 Tips

* Lambda syntax:

  ```python
  lambda x: expression
  ```
* You can store it in a variable
* Then use `map` or a list comprehension

---

### ✅ Solution — step by step

**Step 1 — define the function**

```python
f = lambda x: x ** 3
```

---

**Step 2 — apply it**

Using list comprehension:

```python
result = [f(x) for x in [1,2,3,4]]
```

---

**Step 3 — result**

```python
print(result)
# [1, 8, 27, 64]
```

---

## 3. `map` and `filter`

### Exercise 3 — filter + transform *(medium)*

Compute:

$${x^2 \mid x \in {1,\ldots,10},\ x \text{ even}}$$

using `map` and `filter`.

---

### 💡 Tips

* Break the problem:

  1. Filter even numbers → `x % 2 == 0`
  2. Square them → `x ** 2`
* Structure:

  ```python
  map(f, filter(P, data))
  ```

---

### ✅ Solution — step by step

**Step 1 — define predicate**

```python
is_even = lambda x: x % 2 == 0
```

---

**Step 2 — define transformation**

```python
square = lambda x: x ** 2
```

---

**Step 3 — combine**

```python
result = list(map(square, filter(is_even, range(1, 11))))
```

---

**Step 4 — result**

```python
print(result)
# [4, 16, 36, 64, 100]
```

---

## 4. List comprehensions

### Exercise 4 — same problem, pythonic style *(medium)*

Rewrite Exercise 3 using a **single list comprehension**.

---

### 💡 Tips

* Combine:

  ```python
  [expression for x in iterable if condition]
  ```
* Order matters:

  * first: expression
  * then: `for`
  * then: `if`

---

### ✅ Solution — step by step

**Step 1 — identify components**

* expression → `x ** 2`
* condition → `x % 2 == 0`
* iterable → `range(1, 11)`

---

**Step 2 — build comprehension**

```python
result = [x ** 2 for x in range(1, 11) if x % 2 == 0]
```

---

**Step 3 — result**

```python
print(result)
# [4, 16, 36, 64, 100]
```

---

**Insight**

This is equivalent to:

```python
list(map(lambda x: x**2,
         filter(lambda x: x % 2 == 0, range(1, 11))))
```

but more readable.

---

## 5. Nested structures

### Exercise 5 — flatten a matrix *(hard)*

Given:

```python
matrix = [[1,2,3],
          [4,5,6],
          [7,8,9]]
```

Compute:

$${x \mid x \in matrix}$$

(flat list)

---

### 💡 Tips

* You have **two levels**:

  * rows
  * elements inside each row
* Pattern:

  ```python
  [element for row in matrix for element in row]
  ```
* The order follows nested loops

---

### ✅ Solution — step by step

**Step 1 — think as loops**

```python
flat = []
for row in matrix:
    for element in row:
        flat.append(element)
```

---

**Step 2 — convert to comprehension**

```python
flat = [element for row in matrix for element in row]
```

---

**Step 3 — result**

```python
print(flat)
# [1,2,3,4,5,6,7,8,9]
```

---

## 6. Advanced problems

### Exercise 6 — Pythagorean triples *(very hard)*

Find all:

$${(a,b,c) \mid 1 \le a < b < c \le 20,\ a^2 + b^2 = c^2}$$

---

### 💡 Tips

* You need **three variables**
* Use **nested comprehensions**
* Add a condition:

  ```python
  if a**2 + b**2 == c**2
  ```
* Enforce ordering:

  ```python
  a < b < c
  ```

---

### ✅ Solution — step by step

**Step 1 — structure**

We need:

```python
for a in ...
for b in ...
for c in ...
```

---

**Step 2 — define ranges**

```python
range(1, 21)
```

---

**Step 3 — apply condition**

```python
if a < b < c and a**2 + b**2 == c**2
```

---

**Step 4 — full comprehension**

```python
triples = [(a, b, c)
           for a in range(1, 21)
           for b in range(1, 21)
           for c in range(1, 21)
           if a < b < c and a**2 + b**2 == c**2]
```

---

**Step 5 — result**

```python
print(triples)
# [(3, 4, 5), (6, 8, 10), (5, 12, 13), ...]
```

---

## End of exercises

### What you should now be able to do

* Translate **set-builder notation → Python**
* Use:

  * `lambda`
  * `map` / `filter`
  * list comprehensions
* Recognize when each approach is appropriate
* Handle **nested structures and non-trivial conditions**

