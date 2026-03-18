
# 📘 Strutture Condizionali: `if` / `else` in Python

---

# 1. Introduzione: condizionali e funzioni a tratti

In matematica, molte funzioni non sono descritte da un’unica formula, ma da **più espressioni definite su sottoinsiemi diversi del dominio**. Queste sono chiamate **funzioni a tratti**.

Un esempio classico è:

$$
f(x) =
\begin{cases}
x^2 & \text{se } x \geq 0 \\
-x & \text{se } x < 0
\end{cases}
$$

👉 Interpretazione:

* Se ( x ) è **maggiore o uguale a zero**, applichiamo ( x^2 )
* Se ( x ) è **negativo**, applichiamo ( -x )

---

### 🔗 Collegamento con la programmazione

In Python, non possiamo scrivere direttamente una funzione “a tratti” come in matematica.

Al suo posto utilizziamo le **strutture condizionali**, che permettono al programma di:

* **controllare una condizione**
* **scegliere quale codice eseguire**

👉 In altre parole, `if/else` è la traduzione computazionale di una funzione definita a tratti.

---

# 2. Sintassi di base

```python
if condizione:
    # eseguito se la condizione è True
else:
    # eseguito se la condizione è False
```

---

### 🧠 Cosa significa “condizione”?

Una condizione è un’espressione che restituisce un valore booleano:

* `True` (vero)
* `False` (falso)

Esempi:

```python
x > 0
x == 10
x % 2 == 0
```

---

### ⚠️ Importanza dell'indentazione

Python usa l'**indentazione (spazi)** per definire i blocchi di codice:

```python
if x > 0:
    print("positivo")   # dentro l'if
print("fine")           # fuori dall'if
```

---

# 3. Interpretazione matematica

Possiamo formalizzare un `if/else` come una funzione:

$$
f : X \rightarrow Y
$$

dove il dominio ( X ) viene **suddiviso in sottoinsiemi**.

Definiamo:

$$
X_1 = { x \in X \mid \text{condizione vera} }
$$

$$
X_2 = { x \in X \mid \text{condizione falsa} }
$$

La funzione diventa quindi:

$$
f(x) =
\begin{cases}
f_1(x) & \text{se } x \in X_1 \\
f_2(x) & \text{se } x \in X_2
\end{cases}
$$

👉 Questo è esattamente ciò che fa un `if/else`:
divide il dominio e applica **regole diverse**.

---

### 💡 Osservazione importante

In programmazione:

* la “condizione” è una **funzione booleana**

$$
c(x) : X \rightarrow {True, False}
$$

* che decide quale ramo eseguire

---

# 4. Esempi base

## ✅ Esempio 1 — Numero positivo o negativo

```python
x = int(input("Inserisci un numero: "))

if x >= 0:
    print("Numero positivo o zero")
else:
    print("Numero negativo")
```

👉 Qui stiamo implementando esattamente una funzione a tratti.

---

## ✅ Esempio 2 — Pari o dispari

```python
x = int(input("Inserisci un numero intero: "))

if x % 2 == 0:
    print("Numero pari")
else:
    print("Numero dispari")
```

---

### 🔗 Collegamento matematico

L’operatore modulo `%` implementa:

$$
x \mod 2 =
\begin{cases}
0 & \text{se } x \text{ è pari} \\
1 & \text{se } x \text{ è dispari}
\end{cases}
$$

---

## ✅ Esempio 3 — Verifica tipo e intervallo

```python
val = input("Inserisci qualcosa: ")

print("Hai inserito:", val)
print("Tipo:", type(val))

if val.isdigit() and int(val) > 10:
    print("Hai inserito un numero maggiore di 10")
else:
    print("Numero non valido o <= 10")
```

---

### 🔍 Analisi logica

La condizione:

```python
val.isdigit() and int(val) > 10
```

corrisponde a:

$$
c(x) = (\text{è numero}) \land (x > 10)
$$

👉 Uso della **logica booleana**:

* `and` → congiunzione (∧)
* `or` → disgiunzione (∨)
* `not` → negazione (¬)

---

# 5. Estensione: più di due casi (`elif`)

In matematica spesso abbiamo più di due condizioni:

$$
f(x) =
\begin{cases}
-1 & x < 0 \\
0 & x = 0 \\
1 & x > 0
\end{cases}
$$

In Python:

```python
if x < 0:
    print(-1)
elif x == 0:
    print(0)
else:
    print(1)
```

👉 `elif` permette di gestire **più partizioni del dominio**.

---

# 6. Esercizi (da svolgere)

## 🟢 Esercizio 1 (facile)

Chiedi all’utente un numero e stampa:

* “Positivo” se > 0
* “Negativo” se < 0
* “Zero” se = 0

---

## 🟡 Esercizio 2 (medio)

Chiedi un numero intero e verifica:

$$
x \mod 3 = 0
$$

Stampa:

* “Multiplo di 3”
* “Non multiplo di 3”

---

## 🟠 Esercizio 3 (medio-alto)

Dati due numeri ( a, b ), confronta:

$$
\max(a, b)
$$

Stampa:

* quale è maggiore
* oppure se sono uguali

---

## 🔴 Esercizio 4 (alto)

Definisci una funzione a tratti sull’età:

$$
f(x) =
\begin{cases}
\text{Minorenne} & x < 18 \\
\text{Adulto} & 18 \le x \le 65 \\
\text{Anziano} & x > 65
\end{cases}
$$

---

## 🟣 Esercizio 5 (avanzato)

Dati tre numeri ( a, b, c ):

* calcola:

$$
\max(a, b, c)
$$

* verifica:

$$
(a > 0) \land (b > 0) \land (c > 0)
$$

* verifica:

$$
(a \mod 2 = 0) \lor (b \mod 2 = 0) \lor (c \mod 2 = 0)
$$

---

# 🎯 Conclusione

Le strutture `if` / `else` sono fondamentali perché permettono di:

* implementare **funzioni a tratti**
* tradurre la **logica matematica in codice**
* gestire **casi diversi dello stesso problema**

👉 In sintesi:

> Programmare con `if` significa **partizionare il dominio di un problema e definire comportamenti diversi su ciascuna parte**.

<!--
Se vuoi, nel prossimo passo posso:

* trasformarlo in **slide didattiche**
* oppure aggiungere un **mini-progetto (tipo programma interattivo completo)**
* oppure renderlo ancora più “accademico” per studenti universitari-->
