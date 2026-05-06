# Esercitazione: Tabella di Verità (Logica Booleana) con Google Sheets

Questa esercitazione guida nella creazione di una tabella di verità interattiva utilizzando **Google Sheets**. Imparerai a usare le funzioni logiche di base per automatizzare i risultati degli operatori booleani.

---

## Obiettivi

1. Inserire valori booleani (`TRUE` / `FALSE`).
2. Utilizzare le funzioni `=NOT()`, `=AND()`, `=OR()`.
3. Applicare la formattazione condizionale per visualizzare i risultati.

> [!NOTE]
> **Lingua delle formule**
> In questa guida utilizziamo la **versione inglese** delle funzioni, quella standard e più universale.
> Se il tuo Sheets è in italiano, potresti vedere `=NON()`, `=E()`, `=O()` — funzionano allo stesso modo.

---

## 1 — Preparazione della tabella

Apri un nuovo foglio Google e inserisci queste intestazioni e valori:

| A — Input X | B — Input Y | C — NOT X | D — X AND Y | E — X OR Y |
| :---: | :---: | :---: | :---: | :---: |
| TRUE  | TRUE  | …     | …       | …      |
| TRUE  | FALSE | …     | …       | …      |
| FALSE | TRUE  | …     | …       | …      |
| FALSE | FALSE | …     | …       | …      |

> [!WARNING]
> **Convenzione sugli input**
> Le colonne A e B sono gli **input**: scrivi direttamente `TRUE` o `FALSE`.
> Google Sheets li riconosce automaticamente come valori booleani.
> Le colonne C, D, E conterranno le **formule** che calcolano i risultati — non scrivere a mano i valori!

---

## 2 — Inserimento delle formule

### Operatore NOT

> [!IMPORTANT]
> **Concetto chiave — NOT**
> `NOT X` inverte il valore di input: se X è `TRUE`, il risultato è `FALSE` e viceversa.
> Notazione logica: **¬X** oppure **X̄**
> È l'unico operatore che agisce su **un solo** input.

Nella cella **C2** scrivi:

```
=NOT(A2)
```

Sintassi: `=NOT(valore)` — accetta un solo argomento.

---

### Operatore AND

> [!IMPORTANT]
> **Concetto chiave — AND**
> `X AND Y` è `TRUE` solo se **entrambi** gli input sono `TRUE`.
> Basta un solo `FALSE` per rendere il risultato `FALSE`.
> Notazione logica: **X ∧ Y**

Nella cella **D2** scrivi:

```
=AND(A2, B2)
```

Sintassi: `=AND(valore1, valore2, …)` — accetta più argomenti.

---

### Operatore OR

> [!IMPORTANT]
> **Concetto chiave — OR**
> `X OR Y` è `TRUE` se **almeno uno** degli input è `TRUE`.
> Diventa `FALSE` solo quando *entrambi* gli input sono `FALSE`.
> Notazione logica: **X ∨ Y**

Nella cella **E2** scrivi:

```
=OR(A2, B2)
```

> [!TIP]
> **Estendere le formule velocemente**
> Dopo aver inserito le formule in riga 2, seleziona le celle `C2:E2` insieme e trascina il **quadratino blu** in basso a destra fino alla riga 5. Tutte e tre le formule si copieranno in una sola operazione, adattando automaticamente i riferimenti di riga (`A3`, `A4`, `A5`…).

---

## Risultato atteso

Dopo aver trascinato le formule, la tabella completa deve apparire così:

| X (input) | Y (input) | NOT X | X AND Y | X OR Y |
| :---: | :---: | :---: | :---: | :---: |
| TRUE  | TRUE  | FALSE | TRUE  | TRUE  |
| TRUE  | FALSE | FALSE | FALSE | TRUE  |
| FALSE | TRUE  | TRUE  | FALSE | TRUE  |
| FALSE | FALSE | TRUE  | FALSE | FALSE |

> [!CAUTION]
> **Controlla questi due casi critici prima di andare avanti:**
> - Riga 3 (X=`FALSE`, Y=`TRUE`): **NOT X = `TRUE`** — il risultato dipende solo da X, non da Y.
> - Riga 4 (X=`FALSE`, Y=`FALSE`): **X OR Y = `FALSE`** — l'unico caso in cui OR restituisce FALSE.
>
> Se i tuoi valori non corrispondono, controlla di aver trascinato correttamente le formule e che le colonne A e B contengano `TRUE`/`FALSE` e non testo libero.

---

## 3 — Formattazione condizionale (facoltativa)

1. Seleziona l'intervallo `A2:E5`.
2. Vai su **Format** → **Conditional formatting**.
3. Regola 1: se il testo è `TRUE` → colora di **verde chiaro**.
4. Regola 2: se il testo è `FALSE` → colora di **rosso chiaro**.

> [!WARNING]
> **Errore comune — Formattazione condizionale**
> Quando imposti la regola, scegli la condizione **"Text is exactly"** e digita `TRUE` (tutto maiuscolo, senza spazi).
> Se usi *"Text contains"* potresti ottenere corrispondenze indesiderate su celle che non centrano nulla.

---

## Per approfondire

Questa tabella è la base dei **circuiti logici** digitali. Gli stessi operatori NOT, AND, OR vengono implementati fisicamente con transistor nei processori. Ogni condizione `if` in un programma è, in fondo, una combinazione di questi tre operatori.

> [!NOTE]
> I tre operatori NOT, AND, OR sono chiamati **operatori logici fondamentali** perché qualsiasi altra operazione booleana (NAND, NOR, XOR…) può essere costruita combinandoli. Prova a pensare come esprimeresti **"X ma non Y"** usando solo AND e NOT.

---

*Esercitazione didattica — Logica Booleana · Google Sheets*
