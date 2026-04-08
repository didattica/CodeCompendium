# Python — `for` Loops · Part 2
## Accumulators and Search — Exercises 4–7

> **Course:** Computer Science for Mathematics Students  
> **Level:** First year university  
> **Prerequisites:** `python_cicli_for_esercizi_01.md` (exercises 1–3)

---

## Difficulty legend

| Symbol | Level | Description |
|:---:|:---|:---|
| 🟡 | Medium | Requires an algorithmic pattern (accumulator, counter) |
| ⚫ | Challenge | Direct connection with university mathematics |

---

## Block 2 — Accumulator Pattern

The **accumulator pattern** is one of the fundamental algorithmic schemes.
It consists of initialising a variable with the **identity element** of an operation, then updating it at every step of the loop:

| Operation | Identity element | Initialisation |
|:---:|:---:|:---:|
| Sum | $0$ | `total = 0` |
| Product | $1$ | `product = 1` |
| Counter | $0$ | `count = 0` |

---

### 🟡 Exercise 4 — Sum of the first $N$ integers

#### Statement

Compute the sum $S = \sum_{i=1}^{N} i$ for an $N$ entered by the user.
Then verify the result using Gauss's formula.

---

#### Theoretical notes

**Gauss's formula:**

$$\sum_{i=1}^{N} i = \frac{N(N+1)}{2}$$

The elementary proof writes the sum in both forward and reverse order and adds term by term, obtaining $N$ pairs each equal to $N+1$:

$$\underbrace{1 + 2 + \cdots + N}_{S} + \underbrace{N + (N-1) + \cdots + 1}_{S} = \underbrace{(N+1)+(N+1)+\cdots+(N+1)}_{N \text{ times}}$$

$$2S = N(N+1) \implies S = \frac{N(N+1)}{2}$$

**Algorithmic complexity:**

| Approach | Complexity |
|:---|:---:|
| Iterative loop | $O(N)$ |
| Closed-form formula | $O(1)$ |

Knowing the mathematical identity makes it possible to **eliminate the loop entirely**.

**Pattern used:** additive accumulator — initialised to $0$ (identity element of addition).

---

#### Solution

```python
n = int(input("Enter N: "))

# Iterative computation — accumulator pattern
total = 0           # identity element of addition
for i in range(1, n + 1):
    total += i      # update accumulator

# Verification with Gauss's closed-form formula
gauss = n * (n + 1) // 2

print(f"Iterative sum: {total}")
print(f"Gauss formula: {gauss}")
print(f"Match: {total == gauss}")
```

---

#### Test cases

| Input $N$ | `total` | `gauss` | `Match` |
|:---:|:---:|:---:|:---:|
| `1` | `1` | `1` | `True` |
| `10` | `55` | `55` | `True` |
| `100` | `5050` | `5050` | `True` |
| `1000` | `500500` | `500500` | `True` |

**Manual check for $N = 10$:**

$$\sum_{i=1}^{10} i = 1+2+3+4+5+6+7+8+9+10 = 55 \qquad \frac{10 \cdot 11}{2} = 55 \quad \checkmark$$

---

### 🟡 Exercise 5 — Factorial

#### Statement

Compute $n! = \prod_{i=1}^{n} i$ for an $n$ entered by the user.

---

#### Theoretical notes

The factorial is defined as the **product notation**:

$$n! = \prod_{i=1}^{n} i = 1 \cdot 2 \cdot 3 \cdots n$$

with the convention $0! = 1$, which is not arbitrary: $1$ is the identity element of multiplication, just as $0$ is for addition.

**General principle:** the accumulator must always be initialised to the identity element of the operation being applied. A common mistake is to initialise to $0$ even for products, which always yields $0$ as the result.

**Notable values:**

$$5! = 120 \qquad 6! = 720 \qquad 10! = 3\,628\,800 \qquad 20! \approx 2.4 \times 10^{18}$$

**Growth rate:** the factorial grows faster than any exponential function. More precisely, **Stirling's approximation** gives the asymptotic behaviour:

$$n! \;\sim\; \sqrt{2\pi n}\left(\frac{n}{e}\right)^n \qquad (n \to \infty)$$

**Pattern used:** multiplicative accumulator — initialised to $1$ (identity element of multiplication).

---

#### Solution

```python
n = int(input("Enter n: "))

result = 1              # identity element of multiplication
for i in range(1, n + 1):
    result *= i         # update accumulator

print(f"{n}! = {result}")
```

> **Note:** Python handles arbitrarily large integers natively, so computing `100!` causes no overflow.

---

#### Test cases

| Input $n$ | Expected output | Notes |
|:---:|:---|:---|
| `0` | `0! = 1` | Convention: identity element |
| `1` | `1! = 1` | Base case |
| `5` | `5! = 120` | |
| `6` | `6! = 720` | |
| `10` | `10! = 3628800` | |
| `20` | `20! = 2432902008176640000` | No overflow in Python |

**Manual trace for $n = 4$:**

| Step | `i` | `result` before | `result` after |
|:---:|:---:|:---:|:---:|
| — | — | `1` | — |
| 1 | `1` | `1` | `1` |
| 2 | `2` | `1` | `2` |
| 3 | `3` | `2` | `6` |
| 4 | `4` | `6` | **`24`** |

$$4! = 1 \cdot 2 \cdot 3 \cdot 4 = 24 \quad \checkmark$$


# Computational Complexity of Factorial (n!)

## Overview

Computing the factorial:

```

n! = 1 × 2 × 3 × ... × n

```

is often considered an **O(n)** problem, since it requires `n-1` multiplications.

However, this analysis is incomplete from a computational perspective.

---

## Key Insight

The cost of multiplication is **not constant**.

- CPUs operate on fixed-size words (e.g., 64 bits)
- Large integers require **multiple words**
- Arithmetic on large numbers involves multiple low-level operations

---

## Cost of Multiplication

If numbers have `k` bits:

- Naive multiplication: `O(k²)`
- Fast algorithms (e.g., FFT-based): `O(k log k)`

Thus:

> The larger the numbers, the more expensive the multiplication.

---

## Growth of n!

The size of `n!` grows rapidly:

```

n! ≈ n log n  (in bits)

```

So later multiplications involve very large numbers.

---

## Sequential Approach

```

((((1×2)×3)×4)...×n)

```

### Characteristics:

- Intermediate results grow quickly
- Many operations involve:
  
```

large_number × small_number

```

- Repeatedly processing large numbers → inefficient

---

## Product Tree (Divide & Conquer)

```

(1×2×3×4) × (5×6×7×8)

```

### Strategy:

- Recursively split the range
- Multiply subproducts
- Combine results in a balanced way

### Advantages:

- Operands have **similar size**
- Fewer operations on very large numbers
- Better use of fast multiplication algorithms

---

## Why It’s Faster

Sequential approach:

- Many expensive operations on large numbers

Product tree:

- Most operations on small/medium numbers
- Only a few operations on large numbers

---

## Complexity Comparison

Let `M(k)` be the cost of multiplying `k`-bit numbers.

- Sequential:
  
```

O(n × M(n log n))

```

- Product tree:

```

O(M(n log n))

```

---

## Fundamental Limit

The output itself has size:

```

Θ(n log n) bits

```

Therefore:

> It is impossible to compute `n!` exactly in `O(log n)` time.

---

## Conclusion

- The naive algorithm is **O(n)** in number of operations
- Real cost depends on **integer size growth**
- Product tree improves performance by:
  - balancing computations
  - minimizing operations on large numbers

---

## Takeaway

> The bottleneck is not the number of multiplications,  
> but the cost of handling large integers.
```

---


---

### 🟡 Exercise 6 — Counting multiples

#### Statement

Count how many multiples of $k$ exist in the interval $[1, N]$.

---

#### Theoretical notes

**Cardinality of multiples:** the number of multiples of $k$ in $\{1, 2, \ldots, N\}$ is:

$$\left|\{i \in \{1,\ldots,N\} : k \mid i\}\right| = \left\lfloor \frac{N}{k} \right\rfloor$$

where $\lfloor \cdot \rfloor$ denotes the **floor function** (integer part).

**Modulo operator:** $i$ is a multiple of $k$ if and only if the remainder of $i \div k$ is zero:

$$k \mid i \iff i \bmod k = 0 \iff \texttt{i \% k == 0}$$

**Floor division in Python:** the `//` operator implements exactly $\lfloor \cdot \rfloor$:

$$\left\lfloor \frac{N}{k} \right\rfloor \;\longleftrightarrow\; \texttt{n // k}$$

**Pattern used:** counter with predicate — a variant of the additive accumulator where the variable is incremented by $1$ only when a condition holds.

---

#### Solution

```python
n = int(input("Enter N: "))
k = int(input("Enter k: "))

count = 0
for i in range(1, n + 1):
    if i % k == 0:          # predicate: does k divide i?
        count += 1          # increment counter

# Verification with closed-form formula
expected = n // k           # floor division = ⌊N/k⌋

print(f"Iterative count: {count}")
print(f"Formula (floor): {expected}")
```

---

#### Test cases

| Input $N$ | Input $k$ | `count` | `expected` | Multiples |
|:---:|:---:|:---:|:---:|:---|
| `10` | `2` | `5` | `5` | $2,4,6,8,10$ |
| `20` | `3` | `6` | `6` | $3,6,9,12,15,18$ |
| `100` | `7` | `14` | `14` | $7,14,\ldots,98$ |
| `7` | `7` | `1` | `1` | $7$ |
| `6` | `7` | `0` | `0` | none |

**Manual check for $N=20,\ k=3$:**

$$\lfloor 20/3 \rfloor = \lfloor 6.666\ldots \rfloor = 6 \quad \checkmark$$

---

## Block 3 — Search and Comparison

In this block we move away from accumulating a numeric value and instead **search for a special element** within a sequence. The pattern is: maintain a *current candidate* and update it whenever an element satisfying a comparison criterion is found.

---

### 🟡 Exercise 7 — Maximum of a sequence

#### Statement

Read 5 numbers entered by the user and print the maximum.

---

#### Theoretical notes

**Mathematical definition of maximum:** given a finite set $A = \{a_1, \ldots, a_n\} \subset \mathbb{R}$,

$$M = \max A \iff M \in A \;\text{ and }\; M \geq a_i \;\;\forall\, i \in \{1,\ldots,n\}$$

The algorithm translates this definition **constructively**: it scans the sequence keeping track of the maximum seen so far.

**Initialisation problem:** the initial value of the candidate cannot be an arbitrary number:
- initialising to $0$ would fail if all elements were negative
- initialising to $-\infty$ (`float('-inf')` in Python) is always correct

The most robust solution in Python is to use `None` as a **sentinel** and handle the first element specially via `current_max is None`.

**Loop invariant:** at the end of iteration $k$, the variable `current_max` holds:

$$\text{current\_max}_k = \max\{a_1, a_2, \ldots, a_k\}$$

This is an example of a *loop invariant*, a formal tool used to prove algorithm correctness.

**Complexity:** $O(n)$ — every element must be examined at least once.

---

#### Solution

```python
current_max = None      # sentinel: no maximum seen yet
for i in range(5):
    num = int(input(f"Enter number {i + 1}: "))
    if current_max is None or num > current_max:
        current_max = num   # update candidate

print(f"Maximum: {current_max}")
```

**Variant:** initialisation with $-\infty$ (useful when the numeric type is known):

```python
current_max = float('-inf')     # -∞ is less than any real number
for i in range(5):
    num = int(input(f"Enter number {i + 1}: "))
    if num > current_max:
        current_max = num

print(f"Maximum: {current_max}")
```

> **Why does this work?** Since $-\infty < a_i$ for every $a_i \in \mathbb{R}$, the first element always updates the candidate, and the loop invariant is satisfied from the very first step.

---

#### Test cases

| Input sequence | Expected output | Notes |
|:---|:---:|:---|
| `3 1 4 1 5` | `Maximum: 5` | Maximum at last position |
| `9 7 5 3 1` | `Maximum: 9` | Maximum at first position |
| `4 4 4 4 4` | `Maximum: 4` | All equal |
| `-3 -1 -4 -1 -5` | `Maximum: -1` | All negative — `0` init would fail |
| `0 0 0 0 1` | `Maximum: 1` | Single non-zero element |

**Manual trace for input `3 1 4 1 5`:**

| Step $k$ | `num` | `current_max` before | Update? | `current_max` after |
|:---:|:---:|:---:|:---:|:---:|
| 0 | `3` | `None` | ✓ | `3` |
| 1 | `1` | `3` | ✗ | `3` |
| 2 | `4` | `3` | ✓ | `4` |
| 3 | `1` | `4` | ✗ | `4` |
| 4 | `5` | `4` | ✓ | **`5`** |

---

## Pattern summary — Part 2

| Pattern | Basic structure | Identity element | Exercises |
|:---|:---|:---:|:---:|
| Additive accumulator | `total = 0` · `for ...: total += f(i)` | $0$ | 4, 6 |
| Multiplicative accumulator | `result = 1` · `for ...: result *= f(i)` | $1$ | 5 |
| Counter with predicate | `count = 0` · `if P(i): count += 1` | $0$ | 6 |
| Maximum / minimum search | sentinel + iterative comparison | $-\infty$ | 7 |

---

> **Next part:** `python_algoritmi_sequenze.md`  
> Prime numbers · Congruences · Fibonacci sequence · Leibniz series
