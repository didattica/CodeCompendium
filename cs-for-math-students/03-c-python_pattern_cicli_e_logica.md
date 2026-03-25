# Python – Cicli, Pattern Algoritmici e Collegamenti con la Matematica

## 📌 Obiettivo
Comprendere come i cicli `for` in Python siano collegati a concetti matematici fondamentali come:
- sommatoria
- produttoria
- conteggio (cardinalità)
- filtro logico

---

## 🧠 Concetti di base

### 🔹 Proposizione
Una proposizione è un'affermazione che può essere:
- vera
- falsa

Esempio:
- `5 > 3` → vero

---

### 🔹 Predicato
Un predicato è un'espressione con variabili:

- `x > 3`

Diventa una proposizione quando assegniamo un valore:
- `x = 5` → `5 > 3` → vero

---

### 🔹 Espressione booleana (Python)

Un’espressione che restituisce `True` o `False`:

```python
x > 3
x % 2 == 0
````

---

## 🔁 Il ciclo `for`

Il ciclo `for` permette di iterare su una sequenza di valori.

```python
for i in range(5):
    print(i)
```

---

## 🔷 Pattern fondamentali

---

### 🔍 1. Filtro (selezione)

```python
for i in range(1, 11):
    if i % 2 == 0:
        print(i)
```

📌 Idea:

* selezionare solo gli elementi che soddisfano una condizione

---

### ➕ 2. Sommatoria

```python
somma = 0

for i in range(1, 6):
    somma = somma + i
```

📌 Equivalente matematico:
[
\sum_{i=1}^{5} i
]

---

### ✖️ 3. Produttoria

```python
prodotto = 1

for i in range(1, 6):
    prodotto = prodotto * i
```

📌 Equivalente matematico:
[
\prod_{i=1}^{5} i
]

---

### 🔢 4. Contatore

```python
count = 0

for i in range(1, 11):
    if i % 2 == 0:
        count = count + 1
```

📌 Idea:

* contare quante volte una condizione è vera

---

## 🔗 Collegamento con la matematica

---

### 🔸 Cardinalità

Conta quanti elementi soddisfano una proprietà:

[
|{ x \in {1,\dots,10} \mid x \text{ è pari} }|
]

---

### 🔸 Funzione indicatrice

[
I(x) =
\begin{cases}
1 & \text{se } x \text{ soddisfa la condizione} \
0 & \text{altrimenti}
\end{cases}
]

---

### 🔸 Contatore come sommatoria

[
\sum_{x=1}^{10} I(x)
]

👉 equivalente a:

```python
if condizione:
    count += 1
```

---

## 🧠 Schema riassuntivo

| Pattern     | Codice          | Matematica                  |
| ----------- | --------------- | --------------------------- |
| Filtro      | `if`            | insieme filtrato            |
| Sommatoria  | `somma += x`    | ∑                           |
| Produttoria | `prodotto *= x` | ∏                           |
| Contatore   | `count += 1`    | cardinalità / ∑ indicatrice |

---

## 🎯 Idea chiave

Un ciclo `for` è uno strumento generale che permette di:

* filtrare
* accumulare
* contare

👉 In matematica questi concetti corrispondono a:

* insiemi
* sommatorie
* produttorie

---

## 🚀 Conclusione

Quando vedi:

* una **sommatoria** → pensa a un ciclo `for` con `+`
* una **produttoria** → pensa a un ciclo `for` con `*`
* un **conteggio** → pensa a un ciclo con `count += 1`

👉 La programmazione è il modo operativo di eseguire concetti matematici.


