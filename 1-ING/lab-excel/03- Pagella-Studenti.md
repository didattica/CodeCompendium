# Verifica Pratica — Pagella Studenti con Google Sheets

## Obiettivo dell’esercitazione

Realizzare una pagella scolastica utilizzando Google Sheets oppure Microsoft Excel.

L’attività ha lo scopo di introdurre gli studenti all’uso dei fogli di calcolo attraverso:

- inserimento dati
- organizzazione tabellare
- utilizzo di formule
- calcolo automatico della media
- utilizzo della funzione logica `SE`
- formattazione del foglio

---

# Struttura del documento

Il file deve contenere:

| Riga | Contenuto |
|---|---|
| 1 | SCUOLA SECONDARIA DI PRIMO GRADO |
| 2 | Classe 1A — Pagella Studenti |
| 3 | Anno Scolastico 2025/2026 |

> [!TIP]
> Per migliorare la leggibilità si consiglia di unire le celle da A1 a I1.

---

# Struttura della tabella

Creare la seguente intestazione:

| A | B | C | D | E | F | G | H | I |
|---|---|---|---|---|---|---|---|---|
| Nome | Cognome | Italiano | Matematica | Storia | Scienze | Inglese | Media | Giudizio |

---

# Inserimento dati

Inserire almeno 10 studenti utilizzando nomi di fantasia.

Esempi:

- Gino Lasagna
- Pino Patatino
- Luca Mozzarella
- Kevin Ketchup

Per ogni studente inserire i voti delle materie.

> [!NOTE]
> I voti devono essere compresi tra 4 e 10.

---

# Calcolo della media

Nella colonna `Media` utilizzare la formula:

```excel
=AVERAGE(C6:G6)
```

Versione italiana:

```excel
=MEDIA(C6:G6)
```

La formula calcola automaticamente la media dei voti dello studente.

> [!IMPORTANT]
> Dopo aver scritto la formula nella prima riga, trascinarla verso il basso per applicarla a tutti gli studenti.

---

# Giudizio automatico con funzione SE

Nella colonna `Giudizio` utilizzare una funzione logica.

Formula in inglese:

```excel
=IF(H6>=6,"Promosso","Bocciato")
```

Formula in italiano:

```excel
=SE(H6>=6;"Promosso";"Bocciato")
```

La formula controlla se la media è maggiore o uguale a 6.

- se la condizione è vera → “Promosso”
- altrimenti → “Bocciato”

> [!WARNING]
> In Google Sheets italiano viene utilizzato il punto e virgola `;` come separatore degli argomenti.

---

# Formattazione del foglio

Applicare le seguenti modifiche grafiche:

- intestazioni in grassetto
- colori differenti per titolo e tabella
- bordi alle celle
- righe alternate colorate
- testo centrato
- larghezza colonne adeguata

> [!TIP]
> Utilizzare colori chiari e uniformi per migliorare la leggibilità del documento.

---

# Media finale della classe

Alla fine della tabella aggiungere il calcolo della media generale della classe.

Esempio:

```excel
=AVERAGE(H6:H15)
```

oppure:

```excel
=MEDIA(H6:H15)
```

---

# Utilizzo con Google Drive

## Creazione manuale

1. Aprire Google Drive
2. Selezionare “Nuovo”
3. Creare un nuovo file Google Fogli
4. Ricostruire manualmente la tabella

## Apertura di un file esistente

1. Caricare il file `.ods`
2. Aprirlo con Google Sheets

> [!CAUTION]
> Alcune formule possono cambiare tra Microsoft Excel e Google Sheets.
>
> Verificare:
>
> - utilizzo di `IF` oppure `SE`
> - separatori `,` oppure `;`

---

# Obiettivi didattici

Al termine dell’esercitazione lo studente sarà in grado di:

- creare una tabella ordinata
- utilizzare formule matematiche
- applicare funzioni logiche
- comprendere il concetto di cella e intervallo
- migliorare la presentazione grafica di un foglio di calcolo

---

# Compatibilità

- Google Sheets
- LibreOffice Calc
- Microsoft Excel
