# Python — Functions

### Esercizi con Soluzione

**Informatica per Matematici · Primo anno universitario**

**Prerequisiti:**
`python_functions_theory.md` · `for` · `if/else` · funzioni built-in

---

# 📘 Struttura

* ★★☆ MEDIO → 3 esercizi
* ★★★ CHALLENGE → 3 esercizi
* ★★★ RICORSIONE → 3 esercizi

---

# 01 · Difficoltà Media

*Funzioni, return, scope, if/else, for*

---

## 🟢 Esercizio 1.1 — Classificatore di triangoli

### ▌Traccia

Scrivi una funzione `classify_triangle(a, b, c)` che restituisce:

* `"equilateral"` → tutti i lati uguali
* `"isosceles"` → due lati uguali
* `"scalene"` → tutti diversi
* `"invalid"` → non è un triangolo

📌 Disuguaglianza triangolare:

$$
a + b > c,\quad a + c > b,\quad b + c > a
$$

---

### ▌Soluzione

```python
def classify_triangle(a, b, c):
    if a + b <= c or a + c <= b or b + c <= a:
        return "invalid"

    if a == b == c:
        return "equilateral"
    elif a == b or b == c or a == c:
        return "isosceles"
    else:
        return "scalene"
```

---

## 🟢 Esercizio 1.2 — Conta vocali e consonanti

### ▌💡 Tip

* `in` → operatore di **appartenenza**: verifica se un elemento è dentro una collezione

  ```python
  'a' in "aeiou"  # True
  ```
* `isalpha()` → **metodo delle stringhe**, non dei char (in Python i char sono stringhe di lunghezza 1)
  → restituisce `True` se il carattere è una lettera

---

### ▌Traccia

Scrivi una funzione che restituisce:

```python
(vocali, consonanti)
```

Regole:

* vocali: `aeiou`
* ignora numeri, spazi, simboli

---

### ▌Soluzione

```python
def count_vowels_consonants(text):
    vocali = "aeiou"
    n_vocali = 0
    n_consonanti = 0

    for char in text:
        if char.isalpha():
            if char.lower() in vocali:
                n_vocali += 1
            else:
                n_consonanti += 1

    return n_vocali, n_consonanti
```

---

## 🟢 Esercizio 1.3 — Numero perfetto

### ▌Traccia

Un numero è perfetto se:

$$
n = \sum_{\substack{d \mid n \ d < n}} d
$$

---

### ▌Soluzione

```python
def sum_of_divisors(n):
    total = 0
    for i in range(1, n):
        if n % i == 0:
            total += i
    return total


def is_perfect(n):
    return sum_of_divisors(n) == n
```

---

# 02 · Challenge

*Funzioni pure, composizione*

---

## 🟡 Esercizio 2.1 — Cifrario di Cesare

### ▌💡 Tip (fondamentale)

* `ord('a')` → funzione **built-in** che converte un carattere nel suo codice numerico (Unicode)

  ```python
  ord('a')  # 97
  ```
* `chr(97)` → operazione inversa (numero → carattere)

👉 Quindi lavoriamo con lettere come numeri.

---

### ▌💡 Tip matematico — Shift circolare

Non serve pensare subito ad anelli astratti 🙂

Qui è più concreto:

👉 L’alfabeto è **circolare**
dopo `z` si torna a `a`

Esempio con shift di 2:

```
y → a
z → b
```

Questo si ottiene con:

$$
(x + k) \mod 26
$$

👉 Il modulo `% 26` fa “ripartire da zero” → esattamente come un orologio.

---

### ▌Soluzione

```python
def shift_char(char, k):
    if char.islower():
        base = ord('a')
        return chr((ord(char) - base + k) % 26 + base)
    elif char.isupper():
        base = ord('A')
        return chr((ord(char) - base + k) % 26 + base)
    else:
        return char


def caesar_encrypt(text, k):
    result = ""
    for char in text:
        result += shift_char(char, k)
    return result


def caesar_decrypt(text, k):
    return caesar_encrypt(text, 26 - k)
```

---

## 🟡 Esercizio 2.2 — Run-Length Encoding

### ▌💡 Tip

* `isdigit()` → metodo delle stringhe
  → controlla se un carattere è una cifra (`0–9`)
* le stringhe sono **iterabili** → puoi scorrerle con `for`

---

### ▌Traccia

Esempio:

```
"aaabbb" → "3a3b"
```

---

### ▌Soluzione

```python
def rle_encode(text):
    if not text:
        return ""

    result = ""
    count = 1

    for i in range(1, len(text)):
        if text[i] == text[i - 1]:
            count += 1
        else:
            result += str(count) + text[i - 1]
            count = 1

    result += str(count) + text[-1]
    return result


def rle_decode(encoded):
    result = ""
    digits = ""

    for char in encoded:
        if char.isdigit():
            digits += char
        else:
            result += char * int(digits)
            digits = ""

    return result
```

---

## 🟡 Esercizio 2.3 — Numeri di Armstrong

### ▌Traccia

$$
n = \sum (\text{cifra})^{k}
$$

dove $k$ è il numero di cifre.

---

### ▌Soluzione

```python
def digit_power_sum(n):
    digits = str(n)
    k = len(digits)
    total = 0

    for char in digits:
        total += int(char) ** k

    return total


def is_armstrong(n):
    return digit_power_sum(n) == n


def armstrong_in_range(start, end):
    result = []

    for n in range(start, end + 1):
        if is_armstrong(n):
            result.append(n)

    return result
```

---

# 03 · Ricorsione

*Caso base · caso ricorsivo*

---

## 🔴 Esercizio 3.1 — Fattoriale ricorsivo

### ▌Soluzione

```python
def factorial(n):
    if n < 0:
        raise ValueError("Numero negativo")

    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)
```

---

## 🔴 Esercizio 3.2 — Somma delle cifre

### ▌💡 Tip

* `n % 10` → prende **ultima cifra**
* `n // 10` → rimuove ultima cifra

👉 È una “divisione ricorsiva” del numero.

---

### ▌Soluzione

```python
def digit_sum(n):
    if n < 10:
        return n
    else:
        return (n % 10) + digit_sum(n // 10)


def digital_root(n):
    if n < 10:
        return n
    else:
        return digital_root(digit_sum(n))
```

---

## 🔴 Esercizio 3.3 — Sequenza di Collatz

### ▌Soluzione

```python
def collatz_step(n):
    if n % 2 == 0:
        return n // 2
    else:
        return 3 * n + 1


def collatz_length(n):
    if n == 1:
        return 0
    else:
        return 1 + collatz_length(collatz_step(n))


def collatz_sequence(n):
    if n == 1:
        return [1]
    else:
        return [n] + collatz_sequence(collatz_step(n))
```

---

# 🎯 Conclusione

Questo documento mostra come:

* le **funzioni** strutturano il codice
* i **cicli** implementano iterazione
* la **ricorsione** modella definizioni matematiche

👉 La programmazione è una traduzione operativa della matematica.

