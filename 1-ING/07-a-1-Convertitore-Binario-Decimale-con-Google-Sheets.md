# Esercitazione: Conversione Binaria → Decimale con Google Sheets

Questa esercitazione guida nella costruzione di una tabella che converte un numero binario in decimale utilizzando **Google Sheets**.

L’obiettivo è eseguire il calcolo in modo esplicito:

1. identificare i pesi delle potenze di 2;
2. moltiplicare ogni bit per il proprio peso;
3. sommare i prodotti ottenuti;
4. automatizzare la copia delle formule tramite trascinamento.

---

# Obiettivi

Al termine dell’esercitazione saprai:

* rappresentare un numero binario in tabella;
* associare ogni colonna alla corretta potenza di 2;
* calcolare i prodotti singolarmente;
* utilizzare il trascinamento automatico delle formule;
* ottenere il valore decimale finale tramite somma.

> [!NOTE]
> In questa attività **non** utilizziamo formule avanzate come `SUMPRODUCT()`.
>
> Lo scopo è comprendere chiaramente ogni fase del procedimento:
>
> 1. bit;
> 2. peso;
> 3. prodotto;
> 4. somma finale.

---

# 1 — Preparazione della tabella

Apri un nuovo foglio Google e inserisci la seguente struttura.

---

## Riga degli esponenti

|  A  |  B  |  C  |  D  |  E  |  F  |  G  |  H  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
|  7  |  6  |  5  |  4  |  3  |  2  |  1  |  0  |

---

## Riga dei pesi binari

Nella riga successiva inserisci:

|  A  |  B  |  C  |  D  |  E  |  F  |  G  |  H  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 128 |  64 |  32 |  16 |  8  |  4  |  2  |  1  |

> [!IMPORTANT]
> Ogni valore rappresenta una potenza di 2:
>
> * 2⁷ = 128
> * 2⁶ = 64
> * 2⁵ = 32
> * …
> * 2⁰ = 1

---

## Riga dei bit

Inserisci ora i bit del numero binario:

|  A  |  B  |  C  |  D  |  E  |  F  |  G  |  H  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
|  0  |  0  |  1  |  0  |  0  |  0  |  1  |  1  |

Questo numero binario è:

```text id="binario1"
00100011
```

---

# 2 — Calcolo dei prodotti

Sotto la riga dei bit crea una nuova riga dedicata ai prodotti.

Ogni colonna deve moltiplicare:

```text id="formula-base"
bit × peso
```

---

## Inserimento della prima formula

Nella cella `A4` scrivi:

```gs id="prodottoA"
=A3*A2
```

Questa formula moltiplica:

* il bit presente in `A3`
* per il peso presente in `A2`

---

## Copia automatica delle formule

> [!TIP]
> **Non serve scrivere manualmente una formula per ogni colonna**
>
> Dopo aver inserito la formula nella prima cella:
>
> 1. seleziona la cella `A4`;
> 2. sposta il cursore nell’angolo in basso a destra della cella;
> 3. comparirà una piccola **croce blu** (`+`);
> 4. trascina verso destra fino alla colonna `H`.
>
> Google Sheets copierà automaticamente la formula adattando i riferimenti:
>
> * `=B3*B2`
> * `=C3*C2`
> * `=D3*D2`
> * …

> [!IMPORTANT]
> Questo meccanismo si chiama **riferimento relativo**.
>
> Quando trascini una formula, Google Sheets aggiorna automaticamente lettere e numeri delle celle.

---

# Risultato atteso dei prodotti

|  A  |  B  |  C  |  D  |  E  |  F  |  G  |  H  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
|  0  |  0  |  32 |  0  |  0  |  0  |  2  |  1  |

> [!TIP]
> Quando il bit vale `0`, anche il prodotto vale `0`.
>
> Solo le colonne con bit uguale a `1` contribuiscono al risultato finale.

---

# 3 — Somma finale dei prodotti

Nella cella finale (ad esempio `H5`) inserisci:

```gs id="sommafinale"
=SOMMA(A4:H4)
```

Il risultato ottenuto sarà:

```text id="risultato35"
35
```

---

# Interpretazione del risultato

Il numero binario:

```text id="numero-binario"
00100011
```

corrisponde al numero decimale:

```text id="numero-decimale"
35
```

perché:

```text id="somma35"
32 + 2 + 1 = 35
```

---

# Schema completo finale

|  A  |  B  |  C  |  D  |  E  |  F  |  G  |  H  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
|  7  |  6  |  5  |  4  |  3  |  2  |  1  |  0  |
| 128 |  64 |  32 |  16 |  8  |  4  |  2  |  1  |
|  0  |  0  |  1  |  0  |  0  |  0  |  1  |  1  |
|  0  |  0  |  32 |  0  |  0  |  0  |  2  |  1  |

Valore finale:

```text id="finale35"
35
```

---

# 4 — Formattazione condizionale (facoltativa)

Puoi evidenziare automaticamente i bit attivi (`1`) con una formattazione condizionale.

## Procedura

1. Seleziona la riga dei bit (`A3:H3`)
2. Vai su:

   * **Formato → Formattazione condizionale**
3. Imposta:

   * valore uguale a `1`
   * colore verde chiaro

> [!WARNING]
> Assicurati di selezionare solo la riga dei bit.
>
> Se includi anche la riga dei pesi, verranno colorati anche i valori `1` presenti nei pesi binari.

---

# Per approfondire

Questo metodo è esattamente il procedimento utilizzato internamente dai computer per interpretare i numeri binari.

Ogni bit attivo (`1`) “accende” il corrispondente peso della potenza di 2.

La somma finale dei pesi attivi produce il valore decimale.

> [!IMPORTANT]
> Questo esercizio introduce il principio fondamentale della rappresentazione binaria:
>
> ogni numero è una combinazione di potenze di 2.

---

*Esercitazione didattica — Sistemi Numerici · Google Sheets*
