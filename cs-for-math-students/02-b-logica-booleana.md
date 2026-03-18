# 📘 Logica Booleana e Operatori Logici in Python

---

# 1. Introduzione: logica booleana

La **logica booleana** è un ramo della matematica che studia proposizioni che possono assumere solo due valori:

$$
\text{True} \quad \text{oppure} \quad \text{False}
$$

Una **proposizione** è un’affermazione che può essere vera o falsa.

Esempi:

* `5 > 3` → True
* `10 == 2` → False

---

# 2. Valori booleani in Python

In Python esiste il tipo:

```python
bool
```

con due possibili valori:

```python
True
False
```

---

## Esempi

```python
print(5 > 3)
print(10 == 2)
```

Output:

```
True
False
```

---

# 3. Predicati ed espressioni booleane

Un **predicato** è una funzione che restituisce un valore booleano:

$$
P(x): X \rightarrow {True, False}
$$

Esempio matematico:

$$
P(x) = (x > 0)
$$

In Python:

```python
x = 5
print(x > 0)
```

---

# 4. Operatori logici

Possiamo combinare più condizioni usando operatori logici.

---

## 🔹 AND (congiunzione)

$$
P \land Q
$$

È vero solo se **entrambe** le condizioni sono vere.

### Python:

```python
and
```

### Esempio:

```python
x = 5
print(x > 0 and x < 10)
```

---

## 🔹 OR (disgiunzione)

$$
P \lor Q
$$

È vero se **almeno una** delle condizioni è vera.

### Python:

```python
or
```

### Esempio:

```python
x = 15
print(x < 0 or x > 10)
```

---

## 🔹 NOT (negazione)

$$
\neg P
$$

Inverte il valore logico.

### Python:

```python
not
```

### Esempio:

```python
x = 5
print(not (x > 10))
```

---

# 5. Tabelle di verità

---

## AND

| P     | Q     | P and Q |
|-------|-------|---------|
| True  | True  | True    |
| True  | False | False   |
| False | True  | False   |
| False | False | False   |

---

## OR

| P     | Q     | P or Q |
|-------|-------|--------|
| True  | True  | True   |
| True  | False | True   |
| False | True  | True   |
| False | False | False  |

---

## NOT

| P     | not P |
|-------|-------|
| True  | False |
| False | True  |

---

# 6. Combinazione di condizioni

Possiamo costruire espressioni più complesse.

Esempio:

```python
x = 7
print((x > 0 and x < 10) or x == 20)
```

Interpretazione matematica:

$$
(0 < x < 10) \lor (x = 20)
$$

---

# 7. Esempi svolti

---

## ✅ Esempio 1 — Numero in intervallo

Verificare se un numero appartiene all’intervallo `(0, 10)`:

```python
x = 5

result = x > 0 and x < 10

print(result)
```

---

## ✅ Esempio 2 — Numero fuori intervallo

```python
x = 15

result = x < 0 or x > 10

print(result)
```

---

## ✅ Esempio 3 — Numero NON positivo

```python
x = -3

result = not (x > 0)

print(result)
```

---

# 8. Esercizi (da svolgere)

---

## 🟢 Esercizio 1 (facile)

Dato un numero `x`, verifica se:

* `x > 5` **e** `x < 20`

Stampa il risultato.

---

## 🟡 Esercizio 2 (medio)

Dato un numero `x`, verifica se:

* `x <= 0` **oppure** `x >= 100`

---

## 🔴 Esercizio 3 (più difficile)

Dato un numero `x`, verifica se appartiene all’insieme:

$$
A = { x \in \mathbb{R} \mid (x > 0 \land x < 10) \lor x = 20 }
$$

Traduci la condizione in Python e stampa il risultato booleano.

---

# 🎯 Conclusione

Abbiamo visto che:

* le espressioni booleane restituiscono `True` o `False`
* gli operatori `and`, `or`, `not` permettono di combinare condizioni
* queste strutture derivano direttamente dalla logica matematica

👉 Questo è il fondamento teorico necessario per usare:

* `if`
* `while`
* condizioni nei programmi


