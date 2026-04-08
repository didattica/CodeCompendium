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



