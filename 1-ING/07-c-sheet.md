# Esercitazione: Costruzione di una Tabella di Verità (Logica Booleana) con Google Sheets

Questa esercitazione ti guiderà nella creazione di una tabella di verità interattiva utilizzando **Google Sheets** (il software di fogli di calcolo di Google Drive). Imparerai a utilizzare le funzioni logiche di base per automatizzare i risultati degli operatori booleani.

## Obiettivi dell'esercitazione
1.  Imparare a inserire valori booleani (VERO/FALSO).
2.  Utilizzare le funzioni `=E()`, `=O()`, `=NON()`.
3.  Applicare la formattazione condizionale per visualizzare meglio i risultati.

## Passaggi Operativi

### 1. Preparazione della Tabella
Apri un nuovo foglio Google e crea le seguenti intestazioni nelle prime celle:

| A (Input P) | B (Input Q) | C (NON P) | D (P E Q) | E (P O Q) |
| :--- | :--- | :--- | :--- | :--- |
| VERO | VERO | ... | ... | ... |
| VERO | FALSO | ... | ... | ... |
| FALSO | VERO | ... | ... | ... |
| FALSO | FALSO | ... | ... | ... |

### 2. Inserimento delle Formule
Posizionati nelle celle corrispondenti e inserisci le seguenti formule di Google Sheets:

* **Operatore NOT (NON):** Nella cella `C2`, scrivi:
    `=NON(A2)`
* **Operatore AND (E):** Nella cella `D2`, scrivi:
    `=E(A2; B2)`
* **Operatore OR (O):** Nella cella `E2`, scrivi:
    `=O(A2; B2)`

*Nota: Trascina il quadratino in basso a destra delle celle `C2`, `D2` e `E2` verso il basso per coprire tutte le righe.*

### 3. Formattazione Condizionale (Suggerita)
Per rendere la tabella più professionale:
1. Seleziona l'intervallo di dati (A2:E5).
2. Vai su **Formato** > **Formattazione condizionale**.
3. Imposta una regola: se il testo è "VERO", colora la cella di **verde chiaro**.
4. Aggiungi un'altra regola: se il testo è "FALSO", colora la cella di **rosso chiaro**.

## Risultato Atteso
Dovresti ottenere una tabella dove i valori cambiano dinamicamente. Questa è la base per comprendere i circuiti logici e la programmazione.

---
*Creato per GitHub - Esercitazione Didattica*
