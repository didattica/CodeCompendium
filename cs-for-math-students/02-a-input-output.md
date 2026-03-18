# 📘 Input e Output in Python

## Funzioni `input()` e `print()`

---

# 1. Introduzione: funzioni in matematica e in Python

In matematica, una **funzione** è una relazione che associa a ogni elemento di un insieme (dominio) un elemento di un altro insieme (codominio):

$$
f: X \rightarrow Y
$$

Esempio:

$$
f(x) = x + 1
$$

In Python, una **funzione** è un costrutto che:

* può ricevere **parametri (input)**
* esegue un’operazione
* può produrre un **risultato (output)**

---

# 2. La funzione `print()`

## Definizione intuitiva

`print()` è una funzione che:

* prende uno o più valori
* li **mostra a schermo**

### Forma generale

```python
print(valore)
```

### Interpretazione matematica (informale)

$$
print: \text{dato} \rightarrow \text{output visibile}
$$

⚠️ Nota importante:
`print()` **non restituisce un valore utile**, ma produce un effetto (output a schermo).

---

## Esempi

```python
print(10)
print("ciao")
print(3 + 2)
```

Output:

```
10
ciao
5
```

---

# 3. La funzione `input()`

## Definizione intuitiva

`input()` è una funzione che:

* mostra un messaggio (opzionale)
* aspetta che l’utente inserisca un valore
* restituisce quel valore

### Forma generale

```python
x = input("Inserisci qualcosa: ")
```

---

## Interpretazione matematica

$$
input: \text{input utente} \rightarrow \text{stringa}
$$

⚠️ Punto fondamentale:

👉 `input()` restituisce **sempre una stringa (`str`)**

---

## Esempio

```python
x = input("Numero: ")
print(x)
print(type(x))
```

Se l’utente inserisce:

```
5
```

Output:

```
5
<class 'str'>
```

---

# 4. Composizione di funzioni

In matematica:

$$
f(g(x))
$$

In Python possiamo fare lo stesso:

```python
x = int(input("Numero: "))
```

Qui:

1. `input()` → restituisce stringa
2. `int()` → converte in intero

👉 È una **composizione di funzioni**

---

# 5. Esempi svolti

---

## ✅ Esempio 1 — Somma di due numeri

```python
a = input("Inserisci il primo numero: ")
b = input("Inserisci il secondo numero: ")

somma = int(a) + int(b)

print("La somma è:", somma)
```

---

## ✅ Esempio 2 — Nome utente

```python
nome = input("Come ti chiami? ")

print("Ciao", nome)
```

---

## ✅ Esempio 3 — Età tra 10 anni

```python
eta = input("Quanti anni hai? ")

eta_futura = int(eta) + 10

print("Tra 10 anni avrai:", eta_futura)
```

---

# 6. Osservazioni importanti

### 🔹 `input()` → sempre stringa

Serve spesso conversione:

```python
int(input())
float(input())
```

---

### 🔹 `print()` accetta più parametri

```python
print("Ciao", "Marco", 25)
```

Output:

```
Ciao Marco 25
```

---

# 7. Esercizi (da svolgere)

---

## 🟢 Esercizio 1 (facile)

Chiedi all’utente:

* nome
* cognome

Stampa:

```
Ciao <nome> <cognome>
```

---

## 🟡 Esercizio 2 (medio)

Chiedi due numeri all’utente e stampa:

* somma
* prodotto

---

## 🔴 Esercizio 3 (più difficile)

Chiedi:

* base
* altezza

Calcola e stampa l’area di un rettangolo:

$$
area = base \times altezza
$$

⚠️ Ricorda la conversione!

---

# 🎯 Conclusione

Abbiamo visto che:

* `input()` è una funzione che **restituisce un valore (stringa)**
* `print()` è una funzione che **produce output visibile**
* possiamo **comporre funzioni** come in matematica

👉 Schema fondamentale:

$$
\text{input} \rightarrow \text{elaborazione} \rightarrow \text{output}
$$

