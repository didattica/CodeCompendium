# 🧠 Esercizio – Funzione complessa di backoff

## Funzione

$$
T(k) = 100 \cdot 2^k + 20 \cdot k + 30 \cdot (-1)^k
$$

**Termini:**

* $100 \cdot 2^k$ → crescita esponenziale
* $20 \cdot k$ → incremento lineare
* $30 \cdot (-1)^k$ → oscillazione alternata (+/-)

---

## Richiesta

1. Calcolare $T(k)$ per $k = 0,1,2,3,4,5$
2. Compilare la tabella indicando i singoli termini e $T(k)$ finale
3. Commentare brevemente il comportamento della funzione (crescita, oscillazioni)

---

## Tabella da completare

| k | $100 \cdot 2^k$ | $20 \cdot k$ | $30 \cdot (-1)^k$ | $T(k)$ |
| - | --------------- | ------------ | ----------------- | ------ |
| 0 |                 |              |                   |        |
| 1 |                 |              |                   |        |
| 2 |                 |              |                   |        |
| 3 |                 |              |                   |        |
| 4 |                 |              |                   |        |
| 5 |                 |              |                   |        |

---

**Suggerimento:**

* Calcola prima i singoli termini, poi somma tenendo conto del segno dell’oscillazione
* $(-1)^k$ alterna **+1 e -1** ad ogni incremento di $k$

