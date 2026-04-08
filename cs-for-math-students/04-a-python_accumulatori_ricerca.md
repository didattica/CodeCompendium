# Python — Cicli `for` · Parte 2
## Accumulatori e Ricerca — Esercizi 4–7

> **Corso:** Informatica per Matematici  
> **Livello:** Primo anno universitario  
> **Prerequisiti:** `python_cicli_for_esercizi_01.md` (esercizi 1–3)

---

## Legenda difficoltà

| Simbolo | Livello | Descrizione |
|:---:|:---|:---|
| 🟡 | Medio | Richiede un pattern algoritmico (accumulatore, contatore) |
| ⚫ | Challenge | Collegamento esplicito con matematica universitaria |

---

## Blocco 2 — Pattern Accumulatore

Il **pattern accumulatore** è uno degli schemi algoritmici fondamentali.
Consiste nell'inizializzare una variabile con l'**elemento neutro** di un'operazione, per poi aggiornarla ad ogni passo del ciclo:

| Operazione | Elemento neutro | Inizializzazione |
|:---:|:---:|:---:|
| Somma | $0$ | `s = 0` |
| Prodotto | $1$ | `p = 1` |
| Contatore | $0$ | `c = 0` |

---

### 🟡 Esercizio 4 — Somma dei primi $N$ interi

#### Traccia

Calcola la somma $S = \sum_{i=1}^{N} i$ per un $N$ inserito dall'utente.
Verifica poi il risultato con la formula di Gauss.

---

#### Considerazioni teoriche

**Formula di Gauss:**

$$\sum_{i=1}^{N} i = \frac{N(N+1)}{2}$$

La dimostrazione elementare si basa sull'osservazione che scrivendo la somma in ordine diretto e inverso e sommando termine a termine si ottengono sempre $N$ coppie di valore $N+1$:

$$\underbrace{1 + 2 + \cdots + N}_{S} + \underbrace{N + (N-1) + \cdots + 1}_{S} = \underbrace{(N+1)+(N+1)+\cdots+(N+1)}_{N \text{ volte}}$$

$$2S = N(N+1) \implies S = \frac{N(N+1)}{2}$$

**Complessità algoritmica:**

| Approccio | Complessità |
|:---|:---:|
| Ciclo iterativo | $O(N)$ |
| Formula chiusa | $O(1)$ |

Conoscere l'identità matematica permette di **eliminare il ciclo del tutto**.

**Pattern usato:** accumulatore additivo — inizializzazione a $0$ (elemento neutro della somma).

---

#### Soluzione

```python
n = int(input("Inserisci N: "))

# Calcolo iterativo — pattern accumulatore
somma = 0          # elemento neutro della somma
for i in range(1, n + 1):
    somma += i     # aggiornamento accumulatore

# Verifica con formula chiusa di Gauss
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

---

### 🟡 Esercizio 5 — Fattoriale

#### Traccia

Calcola $n! = \prod_{i=1}^{n} i$ per un $n$ dato in input.

---

#### Considerazioni teoriche

Il fattoriale è definito come la **produttoria**:

$$n! = \prod_{i=1}^{n} i = 1 \cdot 2 \cdot 3 \cdots n$$

con la convenzione $0! = 1$, che non è arbitraria: $1$ è l'elemento neutro del prodotto, esattamente come $0$ lo è per la somma.

**Principio generale:** l'inizializzazione dell'accumulatore deve sempre essere l'elemento neutro dell'operazione. Un errore comune è inizializzare a $0$ anche per i prodotti, ottenendo sempre $0$ come risultato.

**Valori notevoli:**

$$5! = 120 \qquad 6! = 720 \qquad 10! = 3\,628\,800 \qquad 20! \approx 2.4 \times 10^{18}$$

**Crescita:** il fattoriale cresce più velocemente di qualsiasi esponenziale. Più precisamente, la **formula di Stirling** fornisce l'approssimazione asintotica:

$$n! \;\sim\; \sqrt{2\pi n}\left(\frac{n}{e}\right)^n \qquad (n \to \infty)$$

**Pattern usato:** accumulatore moltiplicativo — inizializzazione a $1$ (elemento neutro del prodotto).

---

#### Soluzione

```python
n = int(input("Inserisci n: "))

fattoriale = 1          # elemento neutro del prodotto
for i in range(1, n + 1):
    fattoriale *= i     # aggiornamento accumulatore

print(f"{n}! = {fattoriale}")
```

**Output per $n = 6$:**

```
6! = 720
```

> **Nota:** Python gestisce nativamente interi di dimensione arbitraria, quindi `100!` è calcolabile senza overflow.

---

### 🟡 Esercizio 6 — Contare i multipli

#### Traccia

Conta quanti multipli di $k$ esistono nell'intervallo $[1, N]$.

---

#### Considerazioni teoriche

**Cardinalità dei multipli:** il numero di multipli di $k$ nell'insieme $\{1, 2, \ldots, N\}$ è:

$$\left|\{i \in \{1,\ldots,N\} : k \mid i\}\right| = \left\lfloor \frac{N}{k} \right\rfloor$$

dove $\lfloor \cdot \rfloor$ è la **funzione pavimento** (parte intera inferiore).

**Operatore modulo:** $i$ è multiplo di $k$ se e solo se il resto della divisione $i \div k$ è zero:

$$k \mid i \iff i \bmod k = 0 \iff \texttt{i \% k == 0}$$

**Floor division in Python:** l'operatore `//` realizza esattamente $\lfloor \cdot \rfloor$:

$$\left\lfloor \frac{N}{k} \right\rfloor \;\longleftrightarrow\; \texttt{n // k}$$

**Pattern usato:** contatore con predicato — variante dell'accumulatore additivo dove si incrementa di $1$ solo quando una condizione è verificata.

---

#### Soluzione

```python
n = int(input("Inserisci N: "))
k = int(input("Inserisci k: "))

count = 0
for i in range(1, n + 1):
    if i % k == 0:      # predicato: k divide i?
        count += 1      # incremento contatore

# Verifica con formula matematica
formula = n // k        # floor division = ⌊N/k⌋

print(f"Contatore iterativo: {count}")
print(f"Formula (floor):     {formula}")
```

**Output per $N = 20,\ k = 3$:**

```
Contatore iterativo: 6
Formula (floor):     6
```

> I 6 multipli di $3$ in $[1,20]$ sono: $3, 6, 9, 12, 15, 18$.  
> Verifica: $\lfloor 20/3 \rfloor = \lfloor 6.666\ldots \rfloor = 6$ ✓

---

## Blocco 3 — Ricerca e Confronto

In questo blocco si abbandona l'idea di accumulare un valore numerico e si passa a **ricercare un elemento speciale** all'interno di una sequenza. Il pattern è: mantenere un *candidato corrente* e aggiornarlo ogni volta che si incontra un elemento che soddisfa un criterio di confronto.

---

### 🟡 Esercizio 7 — Massimo di una sequenza

#### Traccia

Leggi 5 numeri inseriti dall'utente e stampa il massimo della sequenza.

---

#### Considerazioni teoriche

**Definizione matematica di massimo:** dato un insieme finito $A = \{a_1, \ldots, a_n\} \subset \mathbb{R}$,

$$M = \max A \iff M \in A \;\text{ e }\; M \geq a_i \;\;\forall\, i \in \{1,\ldots,n\}$$

L'algoritmo traduce questa definizione in modo **costruttivo**: si scandisce la sequenza mantenendo il massimo visto fino al passo corrente.

**Problema dell'inizializzazione:** il valore iniziale del candidato non può essere un numero arbitrario:
- inizializzare a $0$ fallirebbe se tutti gli elementi fossero negativi
- inizializzare a $-\infty$ ($\texttt{float('-inf')}$ in Python) è corretto ma poco esplicito

La soluzione più robusta in Python è usare `None` come **sentinella** e gestire il primo elemento in modo speciale con `massimo is None`.

**Invariante di ciclo:** al termine dell'iterazione $k$, la variabile `massimo` contiene:

$$\text{massimo}_k = \max\{a_1, a_2, \ldots, a_k\}$$

Questo è un esempio di *loop invariant*, uno strumento formale per dimostrare la correttezza degli algoritmi.

**Complessità:** $O(n)$ — è necessario esaminare ogni elemento almeno una volta.

---

#### Soluzione

```python
massimo = None          # sentinella: nessun massimo visto ancora
for i in range(5):
    num = int(input(f"Inserisci il numero {i+1}: "))
    if massimo is None or num > massimo:
        massimo = num   # aggiorna il candidato

print(f"Massimo: {massimo}")
```

**Variante:** inizializzazione con $-\infty$ (utile quando si conosce il tipo numerico):

```python
massimo = float('-inf')     # -∞ è minore di qualsiasi numero reale
for i in range(5):
    num = int(input(f"Inserisci il numero {i+1}: "))
    if num > massimo:
        massimo = num

print(f"Massimo: {massimo}")
```

> **Perché funziona?** Poiché $-\infty < a_i$ per ogni $a_i \in \mathbb{R}$, il primo elemento aggiorna sempre il candidato, e l'invariante di ciclo è soddisfatto fin dal primo passo.

---

## Riepilogo pattern — Parte 2

| Pattern | Struttura base | Elemento neutro | Esercizi |
|:---|:---|:---:|:---:|
| Accumulatore additivo | `s = 0` · `for ...: s += f(i)` | $0$ | 4, 6 |
| Accumulatore moltiplicativo | `p = 1` · `for ...: p *= f(i)` | $1$ | 5 |
| Contatore con predicato | `c = 0` · `if P(i): c += 1` | $0$ | 6 |
| Ricerca massimo / minimo | sentinella + confronto iterativo | $-\infty$ | 7 |

---

> **Prossima parte:** `python_algoritmi_sequenze.md`  
> Numeri primi · Congruenze · Successione di Fibonacci · Serie di Leibniz
