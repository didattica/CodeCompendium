# Come leggere un carattere da tastiera in MASM e convertirlo in intero

## Introduzione

Quando leggiamo un numero da tastiera in Assembly (MASM), non stiamo leggendo direttamente il valore numerico, ma il suo codice ASCII.

Ad esempio, se l'utente digita:

```
5
```

Nel registro non troveremo il numero 5, ma il valore ASCII del carattere '5', cioè 53 in decimale (35h in esadecimale).

Per ottenere il valore numerico reale dobbiamo convertire il carattere ASCII sottraendo il valore del carattere '0'.

---

# 1️⃣ Codici ASCII delle cifre

Le cifre sono consecutive nella tabella ASCII:

| Carattere | Codice ASCII (decimale) |
| --------- | ----------------------- |
| '0'       | 48                      |
| '1'       | 49                      |
| '2'       | 50                      |
| ...       | ...                     |
| '9'       | 57                      |

La cosa importante è che:

```
valore_numerico = codice_ascii - codice_ascii_di_0
```

Poiché '0' vale 48, basta fare:

```
SUB AL, '0'
```

---

# 2️⃣ Lettura di un carattere da tastiera (esempio semplice)

Esempio in ambiente DOS (interrupt 21h):

```assembly
.MODEL SMALL
.STACK 100h
.DATA

.CODE
MAIN PROC

    MOV AH, 01h      ; funzione DOS: leggere un carattere
    INT 21h          ; il carattere viene messo in AL

    ; ora AL contiene il codice ASCII

    SUB AL, '0'      ; conversione ASCII → numero

    ; ora AL contiene il valore numerico reale

    MOV AH, 4Ch
    INT 21h

MAIN ENDP
END MAIN
```

---

# 3️⃣ Cosa succede passo per passo

Supponiamo che l'utente digiti:

```
7
```

### Passaggio 1 – Dopo INT 21h

AL = 55  (perché '7' in ASCII vale 55)

### Passaggio 2 – Dopo SUB AL, '0'

AL = 55 - 48
AL = 7

Ora AL contiene il numero intero 7.

---

# 4️⃣ Perché funziona?

Perché i codici ASCII delle cifre sono consecutivi.

48  -> '0'
49  -> '1'
50  -> '2'
...
57  -> '9'

Sottraendo 48 otteniamo automaticamente il valore corretto.

---

# 5️⃣ Attenzione: funziona solo per una cifra

Questo metodo funziona solo per numeri singoli (0–9).

Se l'utente inserisce:

```
25
```

Vengono letti due caratteri separati:

'2' → 50
'5' → 53

Per ottenere 25 bisogna fare:

```
valore = valore * 10 + nuova_cifra
```

Esempio concettuale:

```
valore = 0

leggi '2'
valore = 0 * 10 + 2 = 2

leggi '5'
valore = 2 * 10 + 5 = 25
```

---

# 6️⃣ Riassunto

Quando leggiamo da tastiera:

• Otteniamo un codice ASCII
• Le cifre ASCII partono da 48
• Sottraendo '0' otteniamo il valore numerico
• Per più cifre serve moltiplicare per 10 e sommare

---

Se vuoi, posso aggiungere anche:

* esempio completo per numero a più cifre
* versione per Windows (senza interrupt DOS)
* schema grafico dei registri passo per passo
