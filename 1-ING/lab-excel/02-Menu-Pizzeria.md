# 🍕 Verifica Pratica — Menu Pizzeria
### Esercitazione su Excel / Google Sheets per classi prime

> **Obiettivo:** imparare a inserire dati in un foglio di calcolo, usare formule di base (moltiplicazione, somma) e applicare la logica condizionale con la funzione **SE**.

---

## 📋 Struttura del file

Il file è diviso in **4 sezioni progressive**, ognuna più difficile della precedente.

| Sezione | Argomento | Competenza richiesta |
|---------|-----------|----------------------|
| 1 | Menu della pizzeria | Inserimento dati manuale |
| 2 | Ordine cliente | Moltiplicazione `=A*B` |
| 3 | Riepilogo calcoli | Somma `=SUM()` |
| 4 | Sconto automatico | Condizione `=IF()` |

---

## ✏️ Sezione 1 — Menu della Pizzeria

Gli studenti compilano manualmente una tabella con almeno **8 pizze** e **5 bevande**.

**Layout colonne:**

```
A             | B          | C  | D  | E             | F              | G  | H
Nome Pizza    | Prezzo (€) | —  | —  | Nome Bevanda  | Prezzo (€)     | —  | —
```

> [!NOTE]
> Le colonne C, D, G, H sono spazi vuoti per separare visivamente le due metà della tabella. Non contengono dati.

**Dati di esempio:**

| Nome Pizza | Prezzo | | | Nome Bevanda | Prezzo |
|---|---|---|---|---|---|
| Margherita | € 7,50 | | | Acqua | € 1,50 |
| Diavola | € 8,50 | | | Coca Cola | € 2,50 |
| Capricciosa | € 9,00 | | | Fanta | € 2,50 |
| Marinara | € 6,50 | | | Sprite | € 2,50 |
| Quattro Formaggi | € 9,50 | | | Tè Freddo | € 2,00 |
| Vegetariana | € 8,00 | | | | |
| Napoli | € 8,00 | | | | |
| Boscaiola | € 9,00 | | | | |

> [!TIP]
> I prezzi delle pizze e delle bevande di questa sezione saranno **copiati a mano** nella Sezione 2. Questo aiuta gli studenti a capire il collegamento tra menu e ordine — prima di imparare i riferimenti di cella.

---

## 🛒 Sezione 2 — Ordine Cliente

Gli studenti inseriscono un ordine fittizio e calcolano i subtotali riga per riga.

**Layout colonne:**

```
A           | B    | C               | D               | E            | F    | G               | H
Nome Pizza  | Qtà  | Prezzo Unit.(€) | Totale Pizza(€) | Nome Bevanda | Qtà  | Prezzo Unit.(€) | Totale Bev.(€)
```

### 🔢 Formula: Moltiplicazione `=B*C`

La prima formula che gli studenti devono scrivere è il **totale per riga**: quantità moltiplicata per il prezzo unitario.

```excel
=B2*C2
```

> [!IMPORTANT]
> Questa è la formula più importante dell'esercizio. Gli studenti devono capire che il foglio di calcolo **non fa i conti da solo**: bisogna dire esplicitamente al programma cosa moltiplicare.
>
> La stessa logica vale per le bevande nella colonna H:
> ```excel
> =F2*G2
> ```

**Esempio ordine compilato:**

| Nome Pizza | Qtà | Prezzo | **Totale** | Nome Bevanda | Qtà | Prezzo | **Totale** |
|---|---|---|---|---|---|---|---|
| Margherita | 2 | € 7,50 | **€ 15,00** | Coca Cola | 2 | € 2,50 | **€ 5,00** |
| Diavola | 1 | € 8,50 | **€ 8,50** | Acqua | 1 | € 1,50 | **€ 1,50** |
| Capricciosa | 3 | € 9,00 | **€ 27,00** | Fanta | 3 | € 2,50 | **€ 7,50** |
| Quattro Formaggi | 1 | € 9,50 | **€ 9,50** | Tè Freddo | 2 | € 2,00 | **€ 4,00** |
| Boscaiola | 2 | € 9,00 | **€ 18,00** | Sprite | 1 | € 2,50 | **€ 2,50** |
| | | **Totale Pizze** | **€ 78,00** | | | **Totale Bevande** | **€ 20,50** |

La riga dei totali usa la funzione **SUM** (vedi Sezione 3).

---

## 🧮 Sezione 3 — Riepilogo Calcoli

### 🔢 Formula: Somma `=SUM()`

Dopo aver calcolato i totali riga, gli studenti sommano tutti i valori della colonna D (pizze) e della colonna H (bevande).

```excel
=SUM(D2:D6)
```

> [!NOTE]
> `SUM(D2:D6)` significa: *"somma tutti i valori dalla cella D2 fino alla cella D6"*.  
> Il simbolo `:` indica un **intervallo** di celle consecutive.

**Struttura della sezione:**

```
Totale Pizze    →  =SUM(D2:D6)
Totale Bevande  →  =SUM(H2:H6)
Totale Ordine   →  =E27+E28        ← somma dei due totali precedenti
```

> [!TIP]
> Per il **Totale Ordine** si può usare sia `=SUM(E27:E28)` che `=E27+E28`. Entrambe le formule sono corrette. Vale la pena mostrare entrambe agli studenti per far capire che ci sono sempre più modi per arrivare allo stesso risultato.

---

## 💸 Sezione 4 — Sconto Automatico con la funzione SE

Questa è la sezione più avanzata. Gli studenti applicano uno **sconto del 10%** solo se il totale supera i 100 €.

### 🔢 Formula: Condizione `=IF()` / `=SE()`

> [!IMPORTANT]
> La funzione `SE` (in italiano) o `IF` (in inglese) è una delle più usate nei fogli di calcolo. Permette al programma di **prendere una decisione** in base a una condizione.
>
> **Sintassi:**
> ```excel
> =IF(condizione; valore_se_VERO; valore_se_FALSO)
> ```
> oppure in italiano:
> ```excel
> =SE(condizione; valore_se_VERO; valore_se_FALSO)
> ```

**Applicazione all'esercizio:**

```excel
=IF(E34>100; E34*10%; 0)
```

Si legge così:
- **SE** il totale in E34 è maggiore di 100
- **ALLORA** calcola il 10% del totale (`E34*10%`)
- **ALTRIMENTI** lo sconto è 0

```excel
Totale Finale   →  =E29            ← riprende il totale dalla sezione 3
Sconto          →  =IF(E34>100, E34*10%, 0)
Totale Scontato →  =E34-E35        ← totale finale meno lo sconto
```

> [!WARNING]
> Attenzione alla compatibilità tra Excel e Google Sheets:
> - **Google Sheets** usa il punto e virgola come separatore: `=SE(E34>100; E34*10%; 0)`
> - **Excel in italiano** usa il punto e virgola: `=SE(E34>100; E34*10%; 0)`
> - **Excel in inglese** usa la virgola: `=IF(E34>100, E34*10%, 0)`
>
> Se la formula dà errore, prova a cambiare il separatore.

**Esempio con totale > 100 €:**

```
Totale Finale     €  98,50
Sconto            €   0,00   ← nessuno sconto (totale < 100)
Totale Scontato   €  98,50
```

```
Totale Finale     € 110,00
Sconto            €  11,00   ← 10% applicato (totale > 100)
Totale Scontato   €  99,00
```

---

## 📐 Riepilogo formule usate

| Formula | Sintassi | Descrizione |
|---------|----------|-------------|
| Moltiplicazione | `=B2*C2` | Moltiplica il valore di B2 per C2 |
| Somma intervallo | `=SUM(D2:D6)` | Somma tutte le celle da D2 a D6 |
| Somma celle | `=E27+E28` | Somma due celle specifiche |
| Condizione | `=IF(E34>100, E34*10%, 0)` | Se vero → 10%, altrimenti → 0 |
| Riferimento | `=E29` | Riprende il valore di un'altra cella |

> [!NOTE]
> Le formule si scrivono sempre partendo dal simbolo `=`. Senza il simbolo uguale, Excel e Google Sheets trattano il contenuto come testo normale e **non calcolano nulla**.

---

## 🎯 Obiettivi didattici

Al termine dell'esercitazione lo studente sarà in grado di:

- [x] Inserire dati in un foglio di calcolo in modo ordinato
- [x] Scrivere una formula di moltiplicazione tra due celle
- [x] Usare `SUM()` per sommare un intervallo di celle
- [x] Capire la differenza tra dato inserito a mano e valore calcolato da formula
- [x] Applicare la funzione `IF` / `SE` con una condizione semplice

---

## 📁 File allegati

| File | Descrizione |
|------|-------------|
| `verifica_pizzeria_TEMPLATE.xlsx` | Template vuoto da distribuire agli studenti |
| `verifica_pizzeria_SOLUZIONE.xlsx` | Versione completa con tutti i dati e le formule corrette |

---

*Compatibile con Microsoft Excel e Google Sheets — livello: prima superiore*
