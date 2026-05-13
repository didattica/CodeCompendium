# Esercitazione: Conversione Binaria → Decimale con Google Sheets

Questa esercitazione mostra come convertire un numero binario in decimale utilizzando **Google Sheets**, senza usare formule automatiche avanzate come `SUMPRODUCT()`.

L’obiettivo è comprendere chiaramente tutti i passaggi del calcolo:

1. costruzione delle potenze di 2;
2. inserimento dei bit;
3. calcolo dei prodotti;
4. somma finale dei risultati.

---

# Obiettivi

Al termine dell’attività saprai:

* costruire una tabella binaria ordinata;
* associare ogni colonna alla corretta potenza di 2;
* moltiplicare ogni bit per il proprio peso;
* utilizzare il trascinamento automatico delle formule;
* ottenere il valore decimale finale tramite somma.

> [!NOTE]
> In questa esercitazione il calcolo viene svolto **passo per passo**.
>
> Non utilizziamo `SUMPRODUCT()` perché vogliamo vedere separatamente:
>
> * le potenze;
> * i prodotti;
> * la somma finale.

---

# 1 — Preparazione della tabella

Apri un nuovo foglio Google e crea questa struttura.

---

# Riga 1 — Esponenti

Inserisci gli esponenti delle potenze di 2.

|  A  |  B  |  C  |  D  |  E  |  F  |  G  |  H  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
|  7  |  6  |  5  |  4  |  3  |  2  |  1  |  0  |

---

# Riga 2 — Potenze di 2

Nella riga successiva inserisci i valori delle potenze:

|  A  |  B  |  C  |  D  |  E  |  F  |  G  |  H  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 128 |  64 |  32 |  16 |  8  |  4  |  2  |  1  |

> [!IMPORTANT]
> Ogni numero rappresenta una potenza di 2:
>
> * 2⁷ = 128
> * 2⁶ = 64
> * 2⁵ = 32
> * 2⁴ = 16
> * …
> * 2⁰ = 1

---

# Riga 3 — Numero binario

Inserisci ora i bit del numero binario:

|  A  |  B  |  C  |  D  |  E  |  F  |  G  |  H  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
|  0  |  0  |  1  |  0  |  0  |  0  |  1  |  1  |

Il numero binario rappresentato è:

```text id="binario"
00100011
```

---

# 2 — Calcolo dei prodotti

Ora bisogna moltiplicare ogni bit per il proprio peso binario.

Crea una nuova riga sotto i bit.

---

# Prima formula

Nella cella `A4` scrivi:

```gs id="formulaA4"
=A3*A2
```

Questa formula significa:

```text id="spiegazioneA4"
bit × potenza
```

quindi:

```text id="spiegazioneA4b"
0 × 128
```

---

# Copia automatica delle formule

> [!TIP]
> Non serve scrivere manualmente una formula per ogni colonna.
>
> Dopo aver scritto la prima formula:
>
> 1. seleziona la cella `A4`;
> 2. sposta il cursore nell’angolo in basso a destra;
> 3. apparirà una piccola croce blu (`+`);
> 4. trascina verso destra fino alla colonna `H`.
>
> Google Sheets copierà automaticamente la formula aggiornando i riferimenti:
>
> * `=B3*B2`
> * `=C3*C2`
> * `=D3*D2`
> * …

> [!IMPORTANT]
> Questo comportamento utilizza i **riferimenti relativi**.
>
> Quando trascini una formula, Google Sheets modifica automaticamente lettere e numeri delle celle.

---

# Riga dei prodotti — Risultato atteso

|  A  |  B  |  C  |  D  |  E  |  F  |  G  |  H  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
|  0  |  0  |  32 |  0  |  0  |  0  |  2  |  1  |

---

# Interpretazione dei prodotti

Le uniche colonne che contribuiscono al risultato finale sono quelle in cui il bit vale `1`.

In questo esempio:

| Bit attivo | Potenza |
| ---------- | ------- |
| 1          | 32      |
| 1          | 2       |
| 1          | 1       |

> [!TIP]
> Se il bit vale `0`, il prodotto sarà sempre `0`.

---

# 3 — Somma finale

Dopo aver ottenuto tutti i prodotti, bisogna sommarli.

Nella cella finale (ad esempio `H5`) scrivi:

```gs id="sommafinale"
=SOMMA(A4:H4)
```

---

# Risultato finale

Il risultato ottenuto sarà:

```text id="risultato"
35
```

perché:

```text id="sommaesplicita"
32 + 2 + 1 = 35
```

---

# Tabella completa finale

|  A  |  B  |  C  |  D  |  E  |  F  |  G  |  H  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
|  7  |  6  |  5  |  4  |  3  |  2  |  1  |  0  |
| 128 |  64 |  32 |  16 |  8  |  4  |  2  |  1  |
|  0  |  0  |  1  |  0  |  0  |  0  |  1  |  1  |
|  0  |  0  |  32 |  0  |  0  |  0  |  2  |  1  |

Valore finale:

```text id="valorefinale"
35
```

---

# 4 — Formattazione condizionale (facoltativa)

Puoi evidenziare automaticamente i bit attivi (`1`).

## Procedura

1. Seleziona la riga dei bit (`A3:H3`)
2. Vai su:

   * **Formato → Formattazione condizionale**
3. Imposta:

   * valore uguale a `1`
   * colore verde chiaro

> [!WARNING]
> Se selezioni anche la riga delle potenze, verranno evidenziati anche i valori `1` presenti nei pesi binari.

---

# Per approfondire

Questo procedimento è il metodo reale utilizzato dai computer per interpretare i numeri binari.

Ogni bit acceso (`1`) attiva la corrispondente potenza di 2.

La somma finale delle potenze attive produce il numero decimale.

> [!IMPORTANT]
> Tutti i dati digitali nei computer vengono rappresentati tramite combinazioni di bit (`0` e `1`).

---

*Esercitazione didattica — Sistemi Numerici · Google Sheets*
