---

## 0. Prerequisiti matematici — Ripasso rapido

Questa sezione riassume i concetti matematici essenziali per comprendere la crittografia.

---

### 0.1 Insiemi e notazione

- $\mathbb{Z}$: insieme dei numeri interi (..., -2, -1, 0, 1, 2, ...)
- $\mathbb{N}^+$: numeri naturali positivi (1, 2, 3, ...)

Se scriviamo:
$$a \in \mathbb{Z}$$
significa:
👉 “a appartiene all’insieme degli interi”

---

### 0.2 Divisibilità

Scriviamo:
$$n \mid a$$

e si legge:
👉 
"$n$ divide $a$"

Significa che esiste un intero $k$ tale che:
$$a = n \cdot k$$

**Esempi:**
- $2 \mid 10$ (vero, perché $10 = 2 \cdot 5$)
- $3 \mid 10$ (falso)

---

### ⚠️ Attenzione ai simboli

- $a / b$ → **divisione** (operazione)
- $a \mid b$ → **divisibilità** (proprietà)

---

### 0.3 Massimo comun divisore

Il massimo comun divisore tra $a$ e $b$ si indica con:
$$\gcd(a, b)$$

👉 è il più grande numero che divide sia $a$ che $b$

**Esempio:**
$$\gcd(12, 18) = 6$$

---

### 0.4 Numeri coprimi

Due numeri si dicono **coprimi** se:
$$\gcd(a, b) = 1$$

👉 Non hanno divisori comuni (tranne 1)

**Esempio:**
- $7$ e $26$ sono coprimi
- $6$ e $9$ NON sono coprimi

---

### 0.5 Congruenza modulo $n$

Scriviamo:
$$a \equiv b \pmod{n}$$

e si legge:
👉 “ $a$ è congruo a $b$ modulo $n$”

Definizione:
$$a \equiv b \pmod{n} \iff n \mid (a - b)$$

👉 In parole semplici:
> $a$ e $b$ hanno lo stesso resto nella divisione per $n$

**Esempio:**
$$17 \equiv 5 \pmod{6}$$

perché:
$$17 - 5 = 12 \quad \text{e} \quad 6 \mid 12$$

---

### 0.6 Operazioni modulo $n$

Quando lavoriamo “modulo $n$”, i risultati vengono sempre riportati tra $0$ e $n-1$.

**Esempi:**
$$17 \bmod 6 = 5$$
$$8 + 7 \equiv 15 \equiv 3 \pmod{6}$$

---

### 0.7 Inverso moltiplicativo

Un numero $a$ ha un inverso modulo $n$ se esiste un numero $a^{-1}$ tale che:
$$a \cdot a^{-1} \equiv 1 \pmod{n}$$

👉 Questo succede **solo se**:
$$\gcd(a, n) = 1$$

**Esempio in $\mathbb{Z}_{26}$:**
$$3 \cdot 9 = 27 \equiv 1 \pmod{26}$$

quindi:
$$3^{-1} \equiv 9 \pmod{26}$$

---

### 0.8 Perché è importante?

Questi concetti sono fondamentali perché:

- la crittografia lavora con numeri modulo $n$
- molti algoritmi (RSA, Diffie-Hellman) usano:
  - congruenze
  - inversi
  - numeri coprimi

👉 Senza questi strumenti, la crittografia moderna non esisterebbe.
