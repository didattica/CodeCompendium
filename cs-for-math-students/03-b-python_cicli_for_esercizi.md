# Python – Cicli `for` e Istruzioni Condizionali: Esercizi Svolti

> **Corso:** Informatica per Matematici  
> **Livello:** Primo anno universitario  
> **Riferimento teorico:** `python_cicli_for_teoria.md`

---

## Legenda difficoltà

| Simbolo | Livello | Descrizione |
|---|---|---|
| 🟢 | Facile | Applicazione diretta della sintassi base |
| 🟡 | Medio | Richiede un pattern algoritmico (accumulatore, contatore) |
| 🔴 | Avanzato | Combina più pattern o richiede ragionamento aggiuntivo |
| ⚫ | Challenge | Collegamento esplicito con matematica universitaria |

---

## Blocco 1 — Iterazione di base

---

### 🟢 Esercizio 1 — Stampa sequenziale

**Traccia:** Stampa i numeri interi da 1 a 10, uno per riga.

**Concetto matematico:** Enumerazione dell'insieme $\{1, 2, \ldots, 10\}$.

**Soluzione:**

```python
for i in range(1, 11):
    print(i)
```

**Output atteso:**
```
1
2
3
...
10
```

**Commento:** `range(1, 11)` genera la sequenza $\{1, 2, \ldots, 10\}$ — ricorda che l'estremo superiore è **escluso**.

---

### 🟢 Esercizio 2 — Stampa numeri pari

**Traccia:** Stampa solo i numeri pari compresi tra 1 e 20.

**Concetto matematico:** Enumerazione del sottoinsieme $\{i \in \{1,\ldots,20\} : 2 \mid i\}$.

**Soluzione (con `if`):**

```python
for i in range(1, 21):
    if i % 2 == 0:
        print(i)
```

**Soluzione alternativa (con `step`):**

```python
for i in range(2, 21, 2):
    print(i)
```

**Commento:** La seconda soluzione è più efficiente: non valuta il predicato ad ogni passo, ma costruisce direttamente la sottosequenza. Corrisponde a iterare sulla progressione aritmetica $2, 4, 6, \ldots, 20$.

---

### 🟢 Esercizio 3 — Tabellina

**Traccia:** Stampa la tabellina del numero $n$ (scelto dall'utente) da 1 a 10.

**Soluzione:**

```python
n = int(input("Inserisci un numero: "))
for i in range(1, 11):
    print(f"{n} x {i} = {n * i}")
```

**Output per $n = 7$:**
```
7 x 1 = 7
7 x 2 = 14
...
7 x 10 = 70
```

**Commento:** Stiamo calcolando i valori della funzione lineare $f(i) = n \cdot i$ per $i = 1, \ldots, 10$.

---

## Blocco 2 — Pattern accumulatore

---

### 🟡 Esercizio 4 — Somma dei primi N interi

**Traccia:** Calcola la somma $S = \sum_{i=1}^{N} i$ per un $N$ inserito dall'utente. Verifica poi il risultato con la formula di Gauss.

**Concetto matematico:** Formula di Gauss: $\displaystyle\sum_{i=1}^{N} i = \dfrac{N(N+1)}{2}$

**Soluzione:**

```python
n = int(input("Inserisci N: "))

# Calcolo iterativo
somma = 0
for i in range(1, n + 1):
    somma += i

# Verifica con formula chiusa
formula = n * (n + 1) // 2

print(f"Somma iterativa:  {somma}")
print(f"Formula di Gauss: {formula}")
print(f"Coincidono: {somma == formula}")
```

**Output per $N = 100$:**
```
Somma iterativa:  5050
Formula di Gauss: 5050
Coincidono: True
```

**Commento:** Questo esercizio mostra come un algoritmo $O(n)$ (il ciclo) possa essere sostituito da un'operazione $O(1)$ (la formula chiusa). Nella pratica, conoscere l'identità matematica consente di **ottimizzare** il codice.

---

### 🟡 Esercizio 5 — Fattoriale

**Traccia:** Calcola $n! = \prod_{i=1}^{n} i$ per un $n$ dato.

**Concetto matematico:** Produttoria; per convenzione $0! = 1$ (elemento neutro della moltiplicazione).

**Soluzione:**

```python
n = int(input("Inserisci n: "))

fattoriale = 1              # elemento neutro del prodotto
for i in range(1, n + 1):
    fattoriale *= i

print(f"{n}! = {fattoriale}")
```

**Output per $n = 6$:**
```
6! = 720
```

**Commento:** L'accumulatore è inizializzato a 1 (non a 0!) perché 1 è l'**elemento neutro** del prodotto. In generale, l'inizializzazione dell'accumulatore deve essere l'elemento neutro dell'operazione che si intende applicare.

---

### 🟡 Esercizio 6 — Contare i multipli

**Traccia:** Conta quanti multipli di $k$ esistono nell'intervallo $[1, N]$.

**Concetto matematico:** $\lvert\{i \in \{1,\ldots,N\} : k \mid i\}\rvert = \lfloor N/k \rfloor$

**Soluzione:**

```python
n = int(input("Inserisci N: "))
k = int(input("Inserisci k: "))

count = 0
for i in range(1, n + 1):
    if i % k == 0:
        count += 1

# Verifica con formula
formula = n // k

print(f"Contatore iterativo: {count}")
print(f"Formula (floor):     {formula}")
```

**Commento:** Ancora una volta, il ciclo verifica una formula matematica. L'operatore `//` in Python è la **divisione intera** (floor division), che realizza esattamente $\lfloor N/k \rfloor$.

---

## Blocco 3 — Ricerca e confronto

---

### 🟡 Esercizio 7 — Massimo di una sequenza

**Traccia:** Leggi 5 numeri inseriti dall'utente e stampa il massimo.

**Soluzione:**

```python
massimo = None
for i in range(5):
    num = int(input(f"Inserisci il numero {i+1}: "))
    if massimo is None or num > massimo:
        massimo = num

print(f"Massimo: {massimo}")
```

**Commento:** La sentinella `None` evita di dover scegliere un valore iniziale arbitrario (es. 0 fallirebbe se tutti i numeri fossero negativi). L'algoritmo implementa la definizione matematica di massimo: $M = \max\{a_1, \ldots, a_n\}$ è l'unico elemento tale che $M \geq a_i$ per ogni $i$.

---

### 🔴 Esercizio 8 — Verifica numero primo

**Traccia:** Dato un intero $n > 1$, determina se è primo.

**Concetto matematico:** $n$ è primo se e solo se $\nexists\ d \in \{2, \ldots, n-1\} : d \mid n$.  
Ottimizzazione: è sufficiente controllare fino a $\lfloor\sqrt{n}\rfloor$.

**Soluzione base:**

```python
n = int(input("Inserisci n: "))

è_primo = True
for d in range(2, n):
    if n % d == 0:
        è_primo = False
        break           # uscita anticipata: trovato un divisore

if è_primo:
    print(f"{n} è primo")
else:
    print(f"{n} non è primo")
```

**Soluzione ottimizzata (con $\sqrt{n}$):**

```python
import math

n = int(input("Inserisci n: "))

è_primo = True
for d in range(2, int(math.sqrt(n)) + 1):
    if n % d == 0:
        è_primo = False
        break

if è_primo:
    print(f"{n} è primo")
else:
    print(f"{n} non è primo")
```

**Commento:** La complessità scende da $O(n)$ a $O(\sqrt{n})$: un miglioramento significativo per $n$ grande. Il `break` implementa la **ricerca con uscita anticipata**, comune in molti algoritmi.

---

### 🔴 Esercizio 9 — FizzBuzz matematico

**Traccia:** Per ogni intero da 1 a 30:
- stampa `"Fizz"` se divisibile per 3,
- stampa `"Buzz"` se divisibile per 5,
- stampa `"FizzBuzz"` se divisibile per 15,
- altrimenti stampa il numero.

**Concetto matematico:** Classificazione di $\mathbb{Z}$ rispetto a due relazioni di congruenza: $i \equiv 0 \pmod{3}$ e $i \equiv 0 \pmod{5}$.

**Soluzione:**

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

**Commento:** L'ordine dei rami è cruciale: il caso $15 \mid i$ deve precedere i casi $3 \mid i$ e $5 \mid i$, altrimenti verrebbe intercettato prima.

---

## Blocco 4 — Challenge matematici

---

### ⚫ Esercizio 10 — Verifica identità di Gauss (somma dei quadrati)

**Traccia:** Per ogni $N$ da 1 a 20, verifica computazionalmente che:

$$\sum_{i=1}^{N} i^2 = \frac{N(N+1)(2N+1)}{6}$$

**Soluzione:**

```python
for n in range(1, 21):
    somma_iter = 0
    for i in range(1, n + 1):
        somma_iter += i ** 2
    
    formula = n * (n + 1) * (2 * n + 1) // 6
    
    check = "✓" if somma_iter == formula else "✗"
    print(f"N={n:2d}: iterativa={somma_iter:4d}, formula={formula:4d}  {check}")
```

**Output (parziale):**
```
N= 1: iterativa=   1, formula=   1  ✓
N= 2: iterativa=   5, formula=   5  ✓
N= 5: iterativa=  55, formula=  55  ✓
N=10: iterativa= 385, formula= 385  ✓
```

---

### ⚫ Esercizio 11 — Successione di Fibonacci

**Traccia:** Stampa i primi $n$ termini della successione di Fibonacci:
$F_0 = 0,\ F_1 = 1,\ F_k = F_{k-1} + F_{k-2}$.

**Concetto matematico:** Successione definita per ricorrenza lineare di ordine 2.

**Soluzione:**

```python
n = int(input("Quanti termini? "))

a, b = 0, 1
for k in range(n):
    print(f"F_{k} = {a}")
    a, b = b, a + b
```

**Output per $n = 8$:**
```
F_0 = 0
F_1 = 1
F_2 = 1
F_3 = 2
F_4 = 3
F_5 = 5
F_6 = 8
F_7 = 13
```

**Commento:** L'assegnazione simultanea `a, b = b, a + b` è idiomatica in Python e aggiorna entrambe le variabili usando i valori **prima** della modifica, evitando la necessità di una variabile temporanea.

---

### ⚫ Esercizio 12 — Stima di π con serie di Leibniz

**Traccia:** Usa la serie di Leibniz per approssimare $\pi$:

$$\pi = 4 \sum_{k=0}^{\infty} \frac{(-1)^k}{2k+1} = 4\left(1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \cdots\right)$$

Calcola la somma parziale per $N = 1000, 10000, 100000$ termini e confronta con `math.pi`.

**Soluzione:**

```python
import math

for n in [1000, 10000, 100000]:
    stima = 0
    for k in range(n):
        stima += ((-1) ** k) / (2 * k + 1)
    stima *= 4
    errore = abs(stima - math.pi)
    print(f"N={n:7d}: π ≈ {stima:.8f}  errore = {errore:.2e}")
```

**Output atteso:**
```
N=   1000: π ≈ 3.14059265  errore = 1.00e-03
N=  10000: π ≈ 3.14149265  errore = 1.00e-04
N= 100000: π ≈ 3.14158265  errore = 1.00e-05
```

**Commento:** La serie di Leibniz converge **lentamente** (errore $\sim 1/N$). È un bellissimo esempio di come matematica e programmazione si incontrino: si può osservare computazionalmente la **convergenza** di una serie infinita e misurarne la velocità.

---

## Riepilogo pattern

| Pattern | Struttura base | Esercizi |
|---|---|---|
| Iterazione semplice | `for i in range(...)` | 1, 2, 3 |
| Accumulatore additivo | `s = 0; for ...: s += f(i)` | 4, 6 |
| Accumulatore moltiplicativo | `p = 1; for ...: p *= f(i)` | 5 |
| Contatore con predicato | `c = 0; if P(i): c += 1` | 6 |
| Ricerca massimo/minimo | Sentinella + confronto | 7 |
| Uscita anticipata (`break`) | Ricerca con predicato | 8 |
| Rami multipli (`elif`) | Classificazione | 9 |
| Cicli annidati | Doppio `for` | 10, 12 |
| Ricorrenza a due stati | Doppia variabile | 11 |

---

*Riferimento teorico: **`python_cicli_for_teoria.md`***
