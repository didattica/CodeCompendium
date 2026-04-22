# Advanced Python Exercises — List Comprehensions

---

## Exercise 7 — Perfect numbers *(very hard)*

Find all **perfect numbers** in the range $1 \le n \le 10000$:

$$\{n \mid n = \sum_{d \mid n,\ d < n} d\}$$

A number is *perfect* if it equals the sum of its proper divisors (e.g. $6 = 1 + 2 + 3$).

---

### 💡 Tips

* Use a **nested comprehension inside** the outer one
* The inner comprehension computes the sum of divisors:
  ```python
  sum(d for d in range(1, n) if n % d == 0)
  ```
* The outer comprehension filters those `n` where the sum equals `n` itself

---

### ✅ Solution — step by step

**Step 1 — find divisors of n**

```python
[d for d in range(1, n) if n % d == 0]
```

---

**Step 2 — sum the divisors**

```python
sum(d for d in range(1, n) if n % d == 0)
```

---

**Step 3 — apply the perfect-number condition**

```python
if sum(d for d in range(1, n) if n % d == 0) == n
```

---

**Step 4 — full comprehension**

```python
perfects = [n
            for n in range(1, 10001)
            if sum(d for d in range(1, n) if n % d == 0) == n]
```

---

**Step 5 — result**

```python
print(perfects)
# [6, 28, 496, 8128]
```

---

---

## Exercise 8 — Pairs with prime sum *(very hard)*

Find all pairs $(a, b)$ such that:

$$\{(a, b) \mid 1 \le a < b \le 50,\ a + b \text{ is prime}\}$$

---

### 💡 Tips

* You need a **helper function** (or inline check) to test primality:
  ```python
  def is_prime(n):
      ...
  ```
* Use **two variables** with nested comprehensions and enforce `a < b`
* The primality check itself can be a generator expression:
  ```python
  all(n % i != 0 for i in range(2, int(n**0.5) + 1))
  ```

---

### ✅ Solution — step by step

**Step 1 — write the primality check**

```python
def is_prime(n):
    if n < 2:
        return False
    return all(n % i != 0 for i in range(2, int(n**0.5) + 1))
```

---

**Step 2 — structure the nested comprehension**

```python
for a in range(1, 51)
for b in range(1, 51)
```

---

**Step 3 — add conditions**

```python
if a < b and is_prime(a + b)
```

---

**Step 4 — full comprehension**

```python
pairs = [(a, b)
         for a in range(1, 51)
         for b in range(1, 51)
         if a < b and is_prime(a + b)]
```

---

**Step 5 — result**

```python
print(pairs[:5])
# [(1, 2), (1, 4), (1, 6), (1, 10), (1, 12), ...]
print(len(pairs))
# 302
```

---

---

## Exercise 9 — Magic square check *(very hard)*

Given a $3 \times 3$ matrix represented as a list of lists, find **all permutations** of the digits $1$–$9$ that form a valid magic square, i.e. every row, column, and diagonal sums to the same magic constant $M = 15$:

$$M = \frac{n(n^2+1)}{2} = 15$$

---

### 💡 Tips

* Use `itertools.permutations` to generate all orderings of `range(1, 10)`
* Map each permutation to a 3×3 grid (slice it into rows of 3)
* Check all rows, columns, and the two diagonals with list comprehensions:
  ```python
  all(sum(row) == 15 for row in grid)
  ```
* Collect only those permutations that satisfy **all** constraints

---

### ✅ Solution — step by step

**Step 1 — import and generate permutations**

```python
from itertools import permutations

all_perms = permutations(range(1, 10))
```

---

**Step 2 — convert a flat permutation into a 3×3 grid**

```python
grid = [p[0:3], p[3:6], p[6:9]]
```

---

**Step 3 — check rows, columns, and diagonals**

```python
def is_magic(p):
    g = [p[0:3], p[3:6], p[6:9]]
    target = 15
    rows_ok = all(sum(row) == target for row in g)
    cols_ok = all(sum(g[r][c] for r in range(3)) == target for c in range(3))
    diag_ok = (g[0][0] + g[1][1] + g[2][2] == target and
               g[0][2] + g[1][1] + g[2][0] == target)
    return rows_ok and cols_ok and diag_ok
```

---

**Step 4 — full comprehension**

```python
from itertools import permutations

magic_squares = [p
                 for p in permutations(range(1, 10))
                 if is_magic(p)]
```

---

**Step 5 — result**

```python
print(len(magic_squares))
# 8  (all 8 rotations/reflections of the unique 3×3 magic square)

for s in magic_squares[:2]:
    g = [s[0:3], s[3:6], s[6:9]]
    for row in g:
        print(row)
    print("---")
# (2, 7, 6)
# (9, 5, 1)
# (4, 3, 8)
# ---
# ...
```
