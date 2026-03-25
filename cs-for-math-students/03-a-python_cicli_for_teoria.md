# Python – Cicli `for` e Istruzioni Condizionali: Fondamenti Teorici

> **Corso:** Informatica per Matematici  
> **Livello:** Primo anno universitario  
> **Prerequisiti:** Nozioni di base di logica e insiemistica

---

## 1. Inquadramento Matematico

### 1.1 Iterazione come formalismo matematico

Prima di scrivere codice, è utile riconoscere che i cicli informatici sono la **realizzazione computazionale di costrutti matematici ben noti**.

#### 🔷 Sommatorie e produttorie

L'espressione matematica:

$$\sum_{i=1}^{n} f(i)$$

descrive l'applicazione ripetuta di un'operazione su un indice discreto $i$ che percorre l'insieme $\{1, 2, \ldots, n\}$. Un ciclo `for` non è altro che la **traduzione algoritmica** di questa notazione: ad ogni passo $i$, si esegue un'istruzione che dipende da $i$.

Analogamente, la produttoria:

$$\prod_{i=1}^{n} f(i)$$

ha la stessa struttura iterativa: cambia solo l'operazione di accumulazione (moltiplicazione anziché addizione).

#### 🔷 Successioni definite per ricorrenza

Molte successioni matematiche sono definite **ricorsivamente**:

$$a_0 = c, \quad a_{n+1} = g(a_n)$$

Questa è esattamente la struttura di un ciclo con **accumulatore**: si parte da uno stato iniziale e si aggiorna ad ogni iterazione.

Esempio classico — i numeri di Fibonacci:

$$F_0 = 0,\quad F_1 = 1,\quad F_n = F_{n-1} + F_{n-2}$$

#### 🔷 Iterazione su insiemi finiti

In matematica, dato un insieme finito $S = \{s_1, s_2, \ldots, s_k\}$, si può definire un'operazione che percorra ogni elemento. Il ciclo `for` in Python generalizza questo concetto: itera su qualsiasi **oggetto iterabile**, che sia un intervallo discreto, una lista, una stringa, ecc.

In termini insiemistici:

$$\text{for } x \in S: \quad \text{esegui } f(x)$$

---

### 1.2 La funzione `range()` come intervallo discreto

`range(start, stop, step)` genera la sequenza:

$$\{start,\ start + step,\ start + 2 \cdot step,\ \ldots\}$$

fino al più grande elemento strettamente minore di `stop`.

In termini matematici è una **progressione aritmetica finita**:

$$a_k = start + k \cdot step, \quad k = 0, 1, \ldots, \left\lfloor \frac{stop - start - 1}{step} \right\rfloor$$

dove $\lfloor \cdot \rfloor$ è la **funzione pavimento** (floor), che restituisce la parte intera inferiore.

| Chiamata Python       | Sequenza generata          | Cardinalità                          |
|-----------------------|----------------------------|--------------------------------------|
| `range(n)`            | $0, 1, \ldots, n-1$        | $n$                                  |
| `range(a, b)`         | $a, a+1, \ldots, b-1$      | $b - a$                              |
| `range(a, b, k)`      | $a, a+k, a+2k, \ldots$     | $\lfloor (b-a-1)/k \rfloor + 1$      |

---

### 1.3 Condizioni logiche e predicati

L'istruzione `if` valuta una **proposizione logica** (un predicato) e ramifica il flusso di esecuzione in base al suo valore di verità.

In logica formale, un predicato su $\mathbb{Z}$ è una funzione:

$$P : \mathbb{Z} \to \{\text{True}, \text{False}\}$$

Ad esempio, il predicato "essere pari":

$$P_{\text{pari}}(n) \iff 2 \mid n \iff n \mod 2 = 0$$

In Python, `i % 2 == 0` è esattamente la valutazione di $P_{\text{pari}}(i)$.

L'operatore `%` (modulo) realizza la **divisione euclidea**: dato $a \in \mathbb{Z}$ e $b \in \mathbb{Z}_{>0}$, esistono unici $q, r$ tali che:

$$a = q \cdot b + r, \quad 0 \leq r < b$$

e `a % b` restituisce proprio $r$.

---

### 1.4 Complessità computazionale (cenni)

Un ciclo `for` che esegue un blocco di costo costante $O(1)$ per $n$ iterazioni ha **complessità temporale $O(n)$**: il tempo di esecuzione cresce linearmente con $n$.

Questo è il primo esempio della notazione **O-grande** (*Big-O notation*), strumento fondamentale per analizzare l'efficienza degli algoritmi.

| Struttura                        | Complessità tipica |
|----------------------------------|--------------------|
| Ciclo singolo su $n$ elementi    | $O(n)$             |
| Ciclo annidato (doppio)          | $O(n^2)$           |
| Ricerca binaria                  | $O(\log n)$        |
| Nessun ciclo (operazione diretta)| $O(1)$             |

---

## 2. Sintassi Python — Riferimento Teorico

### 2.1 Il ciclo `for`

```python
for variabile in iterabile:
    # blocco eseguito ad ogni iterazione
```

- **`variabile`**: assume il valore dell'elemento corrente ad ogni passo.
- **`iterabile`**: qualsiasi oggetto su cui sia definita un'operazione di scorrimento (lista, `range`, stringa, …).
- Il **blocco** è delimitato dall'**indentazione** (4 spazi per convenzione PEP 8).

> 📐 *Nota matematica:* l'indentazione in Python è la realizzazione sintattica del concetto di **scope** (ambito): le istruzioni indentate appartengono al corpo del ciclo, così come in una dimostrazione matematica le righe di un sotto-caso appartengono a quel ramo del ragionamento.

---

### 2.2 L'istruzione `if / elif / else`

```python
if condizione_1:
    # ramo 1
elif condizione_2:
    # ramo 2
else:
    # ramo di default
```

Questa struttura corrisponde a una **funzione a casi** (funzione definita per rami):

$$f(x) = \begin{cases} g_1(x) & \text{se } P_1(x) \\ g_2(x) & \text{se } P_2(x) \\ g_0(x) & \text{altrimenti} \end{cases}$$

---

### 2.3 Combinazione ciclo + condizione

```python
for i in range(1, n + 1):
    if P(i):
        f(i)
```

Matematicamente equivale a:

$$\sum_{\substack{i=1 \\ P(i)}}^{n} f(i)$$

ovvero: applica $f$ solo agli indici che soddisfano il predicato $P$.

---

## 3. Pattern Algoritmici Fondamentali

### 3.1 Accumulatore

Calcolare $\displaystyle\sum_{i=1}^{n} f(i)$:

```python
somma = 0                      # elemento neutro dell'addizione
for i in range(1, n + 1):
    somma = somma + f(i)       # aggiornamento stato
```

L'accumulatore mantiene lo **stato parziale** della computazione: è l'analogo informatico dell'indice di parziale somma $S_k = \sum_{i=1}^k f(i)$.

### 3.2 Contatore con predicato

Calcolare $\lvert\{i \in \{1,\ldots,n\} : P(i)\}\rvert$:

```python
count = 0
for i in range(1, n + 1):
    if P(i):
        count += 1
```

### 3.3 Ricerca di massimo/minimo

Trovare $\max\{a_1, \ldots, a_n\}$:

```python
massimo = None                 # sentinella: nessun valore ancora osservato
for x in sequenza:
    if massimo is None or x > massimo:
        massimo = x
```

Questo algoritmo è un'istanza di **scansione lineare**: complessità $O(n)$, ottimale senza ipotesi aggiuntive sull'ordinamento.

---

## 4. Proprietà Matematiche Verificabili con i Cicli

Alcune identità classiche possono essere **verificate computazionalmente** prima di essere dimostrate analiticamente:

| Identità matematica | Da verificare per $n = 1, \ldots, 10$ |
|---|---|
| $\displaystyle\sum_{i=1}^n i = \dfrac{n(n+1)}{2}$ | Somma dei primi $n$ interi |
| $\displaystyle\sum_{i=1}^n i^2 = \dfrac{n(n+1)(2n+1)}{6}$ | Somma dei quadrati |
| $\displaystyle\sum_{i=0}^{n-1} 2^i = 2^n - 1$ | Serie geometrica di ragione 2 |
| $n! = \displaystyle\prod_{i=1}^n i$ | Fattoriale |

> 💡 Verificare computazionalmente non equivale a dimostrare, ma è un potente strumento euristico per **congetturare** risultati e controllare errori.

---

## 5. Sintesi

| Concetto matematico | Costrutto Python |
|---|---|
| Progressione aritmetica finita | `range(start, stop, step)` |
| Sommatoria $\sum$ | Ciclo con accumulatore |
| Predicato $P : \mathbb{Z} \to \{\text{T,F}\}$ | Condizione `if` |
| Somma condizionata su un sottoinsieme | `for` + `if` combinati |
| Successione ricorsiva $a_{n+1} = g(a_n)$ | Aggiornamento variabile nel ciclo |
| Cardinalità di un insieme filtrato | Ciclo con contatore |

---

*Continua nel file **`python_cicli_for_esercizi.md`** con la parte pratica.*
