
# Python – Cicli Base (for) e If

## 📌 Obiettivo della lezione
Imparare a:
- utilizzare i cicli `for`
- usare `range()`
- combinare cicli con `if/else`
- risolvere semplici problemi iterativi

---

## 🧠 Introduzione teorica

### Perché servono i cicli?

Spesso abbiamo bisogno di ripetere un'operazione più volte.

Esempio senza ciclo:

```python
print("Ciao")
print("Ciao")
print("Ciao")
print("Ciao")
````

Questo approccio è:

* ripetitivo
* poco efficiente
* difficile da modificare

Con un ciclo:

```python
for i in range(4):
    print("Ciao")
```

👉 Il codice è più pulito e scalabile.

---

## 🔁 Il ciclo `for`

### Sintassi base

```python
for variabile in range(n):
    # istruzioni
```

---

### 📌 `range()`

* `range(n)` → da 0 a n-1
* `range(start, end)` → da start a end-1
* `range(start, end, step)` → con passo

---

## ✅ Esempi svolti

### 🔹 Esempio 1 – Stampare numeri da 0 a 4

```python
for i in range(5):
    print(i)
```

---

### 🔹 Esempio 2 – Stampare numeri da 1 a 5

```python
for i in range(1, 6):
    print(i)
```

---

### 🔹 Esempio 3 – Somma dei numeri da 1 a N

```python
n = 5
somma = 0

for i in range(1, n + 1):
    somma = somma + i

print(somma)
```

---

### 🔹 Esempio 4 – Numeri pari

```python
for i in range(1, 11):
    if i % 2 == 0:
        print(i)
```

👉 `%` è l'operatore modulo (resto della divisione)

---

### 🔹 Esempio 5 – Tabellina

```python
n = 3

for i in range(1, 11):
    print(n, "x", i, "=", n * i)
```

---

## 🧪 Esercizi

---

### 🟢 Esercizio 1 (facile)

**Traccia:**
Stampa i numeri da 1 a 10.

**Soluzione:**

```python
for i in range(1, 11):
    print(i)
```

---

### 🟢 Esercizio 2 (facile)

**Traccia:**
Stampa solo i numeri pari da 1 a 20.

**Soluzione:**

```python
for i in range(1, 21):
    if i % 2 == 0:
        print(i)
```

---

### 🟡 Esercizio 3 (medio)

**Traccia:**
Calcola la somma dei numeri da 1 a N (N scelto dall'utente).

**Soluzione:**

```python
n = int(input("Inserisci un numero: "))
somma = 0

for i in range(1, n + 1):
    somma = somma + i

print("Somma:", somma)
```

---

### 🟡 Esercizio 4 (medio)

**Traccia:**
Stampa tutti i multipli di 3 tra 1 e 30.

**Soluzione:**

```python
for i in range(1, 31):
    if i % 3 == 0:
        print(i)
```

---

### 🔴 Esercizio 5 (medio-avanzato)

**Traccia:**
Conta quanti numeri pari ci sono tra 1 e N.

**Soluzione:**

```python
n = int(input("Inserisci un numero: "))
count = 0

for i in range(1, n + 1):
    if i % 2 == 0:
        count = count + 1

print("Numeri pari:", count)
```

---

### 🔴 Esercizio 6 (avanzato)

**Traccia:**
Trova il numero massimo tra 5 numeri inseriti dall’utente.

**Soluzione:**

```python
max_num = None

for i in range(5):
    num = int(input("Inserisci un numero: "))
    
    if max_num is None or num > max_num:
        max_num = num

print("Massimo:", max_num)
```

---

## 🎯 Conclusione

In questa lezione hai imparato:

* a usare i cicli `for`
* a controllare le iterazioni con `range()`
* a combinare cicli e condizioni (`if`)


