# Python — `for` Loops · Part 3
## Algorithms and Sequences — Exercises 8–11

> **Course:** Computer Science for Mathematics Students  
> **Level:** First year university  
> **Prerequisites:** `python_accumulatori_ricerca.md` (exercises 4–7)

---

## Difficulty legend

| Symbol | Level | Description |
|:---:|:---|:---|
| 🔴 | Advanced | Combines multiple patterns or requires additional reasoning |
| ⚫ | Challenge | Direct connection with university mathematics |

---

## Block 3 — Search with Early Exit

In previous exercises the loop always scanned every element. This block introduces **`break`**: once what we are looking for is found, there is no point in continuing — we exit immediately. This scheme is called *search with early exit* and can drastically reduce the number of iterations.

---

### 🔴 Exercise 8 — Prime number check

#### Statement

Given an integer $n > 1$, determine whether it is prime.

---

#### Theoretical notes

**Definition:** $n \in \mathbb{N}$ is **prime** if and only if its only positive divisors are $1$ and $n$ itself:

$$n \text{ is prime} \iff \nexists\, d \in \{2, \ldots, n-1\} : d \mid n$$

**Square-root optimisation:** if $n$ has a divisor $d > 1$, it also has the divisor $n/d$. At least one of the two is $\leq \sqrt{n}$, so it is sufficient to search for divisors up to $\lfloor\sqrt{n}\rfloor$:

$$n \text{ is prime} \iff \nexists\, d \in \{2, \ldots, \lfloor\sqrt{n}\rfloor\} : d \mid n$$

**Proof:** suppose for contradiction that every divisor $d$ of $n$ satisfies $d > \sqrt{n}$. Then $n/d < \sqrt{n}$, but $n/d$ is also a divisor of $n$ with $n/d < \sqrt{n}$, a contradiction. Therefore at least one divisor must be $\leq \sqrt{n}$.

**Impact on complexity:**

| Approach | Complexity | Example: $n = 10^6$ |
|:---|:---:|:---:|
| Search up to $n-1$ | $O(n)$ | $\sim 10^6$ iterations |
| Search up to $\lfloor\sqrt{n}\rfloor$ | $O(\sqrt{n})$ | $\sim 10^3$ iterations |

**Pattern used:** boolean flag + search with early exit (`break`).

---

#### Solution

**Basic version** — search up to $n-1$:

```python
n = int(input("Enter n: "))

is_prime = True
for d in range(2, n):
    if n % d == 0:
        is_prime = False
        break           # divisor found: no need to continue

if is_prime:
    print(f"{n} is prime")
else:
    print(f"{n} is not prime")
```

**Optimised version** — search up to $\lfloor\sqrt{n}\rfloor$:

```python
import math

n = int(input("Enter n: "))

is_prime = True
for d in range(2, int(math.sqrt(n)) + 1):
    if n % d == 0:
        is_prime = False
        break

if is_prime:
    print(f"{n} is prime")
else:
    print(f"{n} is not prime")
```

> **Why `int(math.sqrt(n)) + 1`?**  
> `range` excludes the upper bound, so `+ 1` ensures that $\lfloor\sqrt{n}\rfloor$ itself is included in the search.

---

#### Test cases

| Input $n$ | Expected output | Notes |
|:---:|:---|:---|
| `2` | `2 is prime` | Smallest prime number |
| `3` | `3 is prime` | Smallest odd prime |
| `4` | `4 is not prime` | $4 = 2 \times 2$ |
| `17` | `17 is prime` | $\lfloor\sqrt{17}\rfloor = 4$, no divisor in $\{2,3,4\}$ |
| `49` | `49 is not prime` | $49 = 7 \times 7$, found at $d = 7 = \lfloor\sqrt{49}\rfloor$ |
| `97` | `97 is prime` | Largest prime below $100$ |
| `100` | `100 is not prime` | $100 = 2 \times 50$, found immediately |

**Manual check for $n = 17$:**

$$\lfloor\sqrt{17}\rfloor = 4 \implies \text{test } d \in \{2, 3, 4\}$$

$$17 \bmod 2 = 1 \neq 0 \qquad 17 \bmod 3 = 2 \neq 0 \qquad 17 \bmod 4 = 1 \neq 0$$

No divisor found $\implies$ $17$ is prime ✓

---

### 🔴 Exercise 9 — Mathematical FizzBuzz

#### Statement

For every integer from $1$ to $30$:
- print `"Fizz"` if divisible by $3$,
- print `"Buzz"` if divisible by $5$,
- print `"FizzBuzz"` if divisible by $15$,
- otherwise print the number.

---

#### Theoretical notes

The problem classifies every integer $i \in \{1, \ldots, 30\}$ with respect to two **congruence relations** modulo $3$ and modulo $5$:

$$i \equiv 0 \pmod{3} \qquad i \equiv 0 \pmod{5}$$

This yields four disjoint classes:

| Condition | Output | Examples in $[1,30]$ |
|:---|:---:|:---|
| $3 \mid i$ and $5 \mid i$ | `FizzBuzz` | $15, 30$ |
| $3 \mid i$ and $5 \nmid i$ | `Fizz` | $3, 6, 9, 12, \ldots$ |
| $3 \nmid i$ and $5 \mid i$ | `Buzz` | $5, 10, 20, 25$ |
| $3 \nmid i$ and $5 \nmid i$ | $i$ | $1, 2, 4, 7, \ldots$ |

**Key observation:** $3 \mid i$ and $5 \mid i$ is equivalent to $\text{lcm}(3,5) \mid i$, i.e. $15 \mid i$, since $\gcd(3,5) = 1$.

**Branch ordering:** the case $15 \mid i$ must come before $3 \mid i$ and $5 \mid i$ in the code. Checking $3 \mid i$ first would cause multiples of $15$ to print only `"Fizz"` instead of `"FizzBuzz"`.

---

#### Solution

```python
for i in range(1, 31):
    if i % 15 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

---

#### Test cases

**Full output for $i \in \{1, \ldots, 30\}$:**

```
1
2
Fizz        ← 3
4
Buzz        ← 5
Fizz        ← 6
7
8
Fizz        ← 9
Buzz        ← 10
11
Fizz        ← 12
13
14
FizzBuzz    ← 15
16
17
Fizz        ← 18
19
Buzz        ← 20
Fizz        ← 21
22
23
Fizz        ← 24
Buzz        ← 25
26
Fizz        ← 27
28
29
FizzBuzz    ← 30
```

**Count verification in $[1, 30]$:**

| Category | Formula | Result |
|:---|:---|:---:|
| `FizzBuzz` (multiples of $15$) | $\lfloor 30/15 \rfloor$ | $2$ |
| `Fizz` (multiples of $3$, not $15$) | $\lfloor 30/3 \rfloor - \lfloor 30/15 \rfloor$ | $8$ |
| `Buzz` (multiples of $5$, not $15$) | $\lfloor 30/5 \rfloor - \lfloor 30/15 \rfloor$ | $4$ |
| Numbers printed | $30 - 2 - 8 - 4$ | $16$ |
| **Total** | | **30** ✓ |

---

## Block 4 — Mathematical Challenges

The following exercises directly connect programming with university mathematics results: series identities, linear recurrences, and convergence of infinite series.

---

### ⚫ Exercise 10 — Verification of the sum-of-squares identity

#### Statement

For every $N$ from $1$ to $20$, verify computationally that:

$$\sum_{i=1}^{N} i^2 = \frac{N(N+1)(2N+1)}{6}$$

---

#### Theoretical notes

**Identity:** the sum of the first $N$ squares equals:

$$\sum_{i=1}^{N} i^2 = \frac{N(N+1)(2N+1)}{6}$$

**Proof by induction:**

- *Base case:* $N = 1$ — the left-hand side is $1^2 = 1$, the right-hand side is $\frac{1 \cdot 2 \cdot 3}{6} = 1$ ✓

- *Inductive step:* assume the identity holds for $N$; prove it for $N+1$:

$$\sum_{i=1}^{N+1} i^2 = \frac{N(N+1)(2N+1)}{6} + (N+1)^2 = \frac{(N+1)(N+2)(2N+3)}{6}$$

The Python loop verifies this identity **for every value** $N \in \{1, \ldots, 20\}$, providing computational evidence (not a substitute for the formal proof, but useful for building intuition).

**Why `// 6` is exact:** one can show that $N(N+1)(2N+1)$ is always divisible by $6$ — among any three consecutive integers there is always one divisible by $2$ and one by $3$.

**Pattern used:** nested loops — the outer loop varies $N$, the inner loop computes the iterative sum.

---

#### Solution

```python
for n in range(1, 21):
    # inner loop: iterative sum of squares
    iter_sum = 0
    for i in range(1, n + 1):
        iter_sum += i ** 2

    # closed-form formula
    formula = n * (n + 1) * (2 * n + 1) // 6

    status = "✓" if iter_sum == formula else "✗"
    print(f"N={n:2d}:  iter={iter_sum:5d},  formula={formula:5d}  {status}")
```

---

#### Test cases

**Full output:**

```
N= 1:  iter=    1,  formula=    1  ✓
N= 2:  iter=    5,  formula=    5  ✓
N= 3:  iter=   14,  formula=   14  ✓
N= 4:  iter=   30,  formula=   30  ✓
N= 5:  iter=   55,  formula=   55  ✓
N= 6:  iter=   91,  formula=   91  ✓
N= 7:  iter=  140,  formula=  140  ✓
N= 8:  iter=  204,  formula=  204  ✓
N= 9:  iter=  285,  formula=  285  ✓
N=10:  iter=  385,  formula=  385  ✓
N=11:  iter=  506,  formula=  506  ✓
N=12:  iter=  650,  formula=  650  ✓
N=13:  iter=  819,  formula=  819  ✓
N=14:  iter= 1015,  formula= 1015  ✓
N=15:  iter= 1240,  formula= 1240  ✓
N=16:  iter= 1496,  formula= 1496  ✓
N=17:  iter= 1785,  formula= 1785  ✓
N=18:  iter= 2109,  formula= 2109  ✓
N=19:  iter= 2470,  formula= 2470  ✓
N=20:  iter= 2870,  formula= 2870  ✓
```

**Manual check for $N = 3$:**

$$\sum_{i=1}^{3} i^2 = 1 + 4 + 9 = 14 \qquad \frac{3 \cdot 4 \cdot 7}{6} = \frac{84}{6} = 14 \quad \checkmark$$

---

### ⚫ Exercise 11 — Fibonacci sequence

#### Statement

Print the first $n$ terms of the Fibonacci sequence:

$$F_0 = 0, \quad F_1 = 1, \quad F_k = F_{k-1} + F_{k-2} \quad (k \geq 2)$$

---

#### Theoretical notes

The Fibonacci sequence is defined by a **linear recurrence of order 2** with constant coefficients:

$$F_k = F_{k-1} + F_{k-2}$$

The first terms are:

$$0,\ 1,\ 1,\ 2,\ 3,\ 5,\ 8,\ 13,\ 21,\ 34,\ 55,\ 89,\ 144,\ \ldots$$

**Binet's formula:** there exists a closed-form expression for $F_k$:

$$F_k = \frac{\varphi^k - \psi^k}{\sqrt{5}}$$

where $\varphi = \dfrac{1+\sqrt{5}}{2} \approx 1.618$ is the **golden ratio** and $\psi = \dfrac{1-\sqrt{5}}{2} \approx -0.618$.

Since $|\psi| < 1$, the term $\psi^k \to 0$ as $k \to \infty$, so:

$$F_k \sim \frac{\varphi^k}{\sqrt{5}} \qquad (k \to \infty)$$

The sequence grows **exponentially** with base $\varphi$.

**Ratio of consecutive terms:** as $k$ increases, the ratio $F_{k+1}/F_k$ converges to the golden ratio:

$$\lim_{k \to \infty} \frac{F_{k+1}}{F_k} = \varphi = \frac{1+\sqrt{5}}{2}$$

**Implementation:** the algorithm uses two variables `a, b` representing $F_k$ and $F_{k+1}$. The **simultaneous assignment** `a, b = b, a + b` updates both using values *before* the modification, with no temporary variable needed.

**Pattern used:** two-state recurrence — double variable updated simultaneously.

---

#### Solution

```python
n = int(input("How many terms? "))

a, b = 0, 1                 # F_0, F_1
for k in range(n):
    print(f"F_{k} = {a}")
    a, b = b, a + b         # simultaneous update
```

**Variant with Binet's formula verification:**

```python
import math

n = int(input("How many terms? "))

phi = (1 + math.sqrt(5)) / 2
psi = (1 - math.sqrt(5)) / 2

a, b = 0, 1
for k in range(n):
    binet = round((phi**k - psi**k) / math.sqrt(5))
    print(f"F_{k:2d} = {a:6d}   (Binet: {binet})")
    a, b = b, a + b
```

> **Note:** `round()` is used because Binet's formula introduces floating-point errors; the rounded result always matches the exact integer value for reasonably small $k$.

---

#### Test cases

**Input `n = 10`:**

```
F_ 0 =      0   (Binet: 0)
F_ 1 =      1   (Binet: 1)
F_ 2 =      1   (Binet: 1)
F_ 3 =      2   (Binet: 2)
F_ 4 =      3   (Binet: 3)
F_ 5 =      5   (Binet: 5)
F_ 6 =      8   (Binet: 8)
F_ 7 =     13   (Binet: 13)
F_ 8 =     21   (Binet: 21)
F_ 9 =     34   (Binet: 34)
```

**Edge cases:**

| Input `n` | Behaviour |
|:---:|:---|
| `0` | No output — the loop body never executes |
| `1` | Prints only `F_0 = 0` |
| `2` | Prints `F_0 = 0` and `F_1 = 1` |

**Convergence of $F_{k+1}/F_k$ toward $\varphi$:**

| $k$ | $F_k$ | $F_{k+1}$ | $F_{k+1}/F_k$ |
|:---:|:---:|:---:|:---:|
| $5$ | $5$ | $8$ | $1.6000$ |
| $8$ | $21$ | $34$ | $1.6190$ |
| $10$ | $55$ | $89$ | $1.6182$ |
| $15$ | $610$ | $987$ | $1.61803\ldots$ |
| $\infty$ | — | — | $\varphi \approx 1.61803\ldots$ |

---

## Pattern summary — Part 3

| Pattern | Basic structure | Exercises |
|:---|:---|:---:|
| Flag + early exit | `found = False` · `if P(i): found = True; break` | 8 |
| Multiple branches (`elif`) | classification by congruence | 9 |
| Nested loops | double `for`, outer loop over $N$ | 10 |
| Two-state recurrence | `a, b = b, a + b` | 11 |

---

## Full module summary

| Part | Exercises | Main patterns |
|:---|:---:|:---|
| `python_cicli_for_esercizi_01.md` | 1–3 | Simple iteration, multiplication table |
| `python_accumulatori_ricerca.md` | 4–7 | Accumulators, counters, maximum search |
| `python_algoritmi_sequenze.md` | 8–11 | Early exit, congruences, recurrences |

---

> **Reference theory:** `python_cicli_for_teoria.md`
