# Convertitore Binario → Decimale con Google Sheets

## Introduzione

Questo progetto mostra come costruire un semplice convertitore di numeri binari in decimale usando **Google Sheets**.

L’idea è rappresentare un **byte** tramite 8 celle contenenti solo `0` oppure `1`.
Ogni posizione rappresenta una potenza di 2:

| Bit | Potenza |
| --- | ------- |
| 0   | 2⁰      |
| 1   | 2¹      |
| 2   | 2²      |
| ... | ...     |

Il valore decimale finale viene ottenuto sommando i valori delle celle attive (`1`).

---

## Obiettivo

Realizzare una tabella che:

* rappresenti 8 bit;
* mostri le potenze di 2;
* permetta di inserire valori binari (`0` o `1`);
* calcoli automaticamente il numero decimale.

---

## Struttura del Foglio

Creare una tabella come questa:

| A   | B  | C  | D  | E | F | G | H |
| --- | -- | -- | -- | - | - | - | - |
| 7   | 6  | 5  | 4  | 3 | 2 | 1 | 0 |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| 0   | 1  | 1  | 0  | 1 | 0 | 1 | 1 |

---

## Passo 1 — Inserire le Posizioni dei Bit

Nella prima riga inserire gli indici dei bit:

| A1 | B1 | C1 | D1 | E1 | F1 | G1 | H1 |
| -- | -- | -- | -- | -- | -- | -- | -- |
| 7  | 6  | 5  | 4  | 3  | 2  | 1  | 0  |

> [!NOTE]
> Il bit più a destra rappresenta `2⁰`.
>
> Il bit più a sinistra rappresenta `2⁷`.

---

## Passo 2 — Calcolare le Potenze di 2

Nella seconda riga calcolare automaticamente le potenze di 2.

In `A2` scrivere:

```excel
=2^A1
```

Poi trascinare la formula fino a `H2`.

Il risultato sarà:

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| --- | -- | -- | -- | - | - | - | - |

---

## Passo 3 — Inserire i Bit

Nella terza riga inserire soltanto:

* `0`
* `1`

Esempio:

| 0 | 1 | 1 | 0 | 1 | 0 | 1 | 1 |
| - | - | - | - | - | - | - | - |

> [!IMPORTANT]
> Ogni cella rappresenta un bit:
>
> * `1` → la potenza di 2 viene inclusa
> * `0` → la potenza di 2 viene ignorata

---

## Passo 4 — Calcolare il Numero Decimale

In una nuova cella inserire:

```excel
=SUMPRODUCT(A3:H3,A2:H2)
```

Questa formula:

1. moltiplica ogni bit per la sua potenza di 2;
2. somma tutti i risultati.

---

## Esempio Completo

Numero binario:

```text
01101011
```

Calcolo:

| Bit     | Valore |
| ------- | ------ |
| 0 × 128 | 0      |
| 1 × 64  | 64     |
| 1 × 32  | 32     |
| 0 × 16  | 0      |
| 1 × 8   | 8      |
| 0 × 4   | 0      |
| 1 × 2   | 2      |
| 1 × 1   | 1      |

Somma finale:

```text
64 + 32 + 8 + 2 + 1 = 107
```

Quindi:

```text
01101011₂ = 107₁₀
```

---

## Formula Matematica

La conversione da binario a decimale segue questa regola:

\sum_{i=0}^{7} b_i 2^i

dove:

* `bᵢ` è il valore del bit (`0` oppure `1`);
* `2ⁱ` è la potenza di 2 associata alla posizione.

---

## Miglioramenti Possibili

Puoi estendere il progetto aggiungendo:

* validazione dati (`solo 0 o 1`);
* colori automatici con formattazione condizionale;
* conversione inversa (decimale → binario);
* supporto a 16 bit o 32 bit;
* visualizzazione esadecimale.

> [!TIP]
> Usa colori diversi per evidenziare i bit attivi (`1`) e rendere il convertitore più leggibile.
