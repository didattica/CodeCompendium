# Come leggere un numero da tastiera in MASM e convertirlo in intero

## Introduzione

Quando leggiamo un numero da tastiera in Assembly (MASM), NON stiamo leggendo direttamente il valore numerico.

Stiamo leggendo un BYTE (8 bit) che rappresenta il codice ASCII del carattere digitato.

Questo è il punto fondamentale:
nel registro arriva sempre un valore binario a 8 bit.

Dobbiamo quindi distinguere tra:

* rappresentazione ASCII (carattere)
* valore numerico reale (numero intero)

---

# 1️⃣ Cosa significa davvero leggere un carattere

Se l’utente digita:

```
5
```

Nel registro AL non entra il numero 5.

Entra il codice ASCII di '5'.

Tabella ASCII delle cifre:

| Carattere | ASCII decimale | Binario (8 bit) |
| --------- | -------------- | --------------- |
| '0'       | 48             | 00110000        |
| '1'       | 49             | 00110001        |
| '2'       | 50             | 00110010        |
| '3'       | 51             | 00110011        |
| '4'       | 52             | 00110100        |
| '5'       | 53             | 00110101        |
| '6'       | 54             | 00110110        |
| '7'       | 55             | 00110111        |
| '8'       | 56             | 00111000        |
| '9'       | 57             | 00111001        |

Quindi se l’utente digita 5:

AL = 00110101  (53 decimale)

Non è 00000101.

---

# 2️⃣ Perché facciamo SUB AL, '0'

Il carattere '0' vale 48.

In binario:

'0' = 00110000

Se AL contiene '5':

AL = 00110101

Eseguiamo:

SUB AL, '0'

Ovvero:

00110101   (53)

* 00110000   (48)

---

00000101   (5)

Ora AL contiene 00000101.

Questo è il numero intero 5.

---

# 3️⃣ Cosa significa "conta sempre il valore binario completo a 8 bit"

Un registro a 8 bit (come AL) contiene sempre 8 bit.

Non 4.
Non 2.
Sempre 8.

Quando diciamo "5 in binario" dobbiamo scrivere:

00000101

Non semplicemente 0101.

Perché il processore lavora sempre sull’intero byte.

---

# 4️⃣ Esempio completo (DOS, interrupt 21h)

```assembly
.MODEL SMALL
.STACK 100h
.DATA

.CODE
MAIN PROC

    MOV AH, 01h      ; funzione DOS: leggere carattere
    INT 21h          ; AL = codice ASCII

    SUB AL, '0'      ; conversione ASCII → numero

    ; Ora AL contiene il valore numerico reale

    MOV AH, 4Ch
    INT 21h

MAIN ENDP
END MAIN
```

---

# 5️⃣ Cosa succede a livello binario (analisi bit per bit)

La sottrazione è un’operazione binaria eseguita dalla ALU.

La CPU non "capisce" i numeri come li intendiamo noi.
Lavora solo con sequenze di bit.

Nel caso:

00110101 - 00110000

I bit più significativi sono uguali.
La differenza avviene negli ultimi bit.

Risultato:

00000101

Questo è possibile perché i codici ASCII delle cifre sono consecutivi.

---

# 6️⃣ Perché funziona solo per cifre singole

Se l’utente digita:

25

Vengono letti due byte separati:

'2' = 00110010
'5' = 00110101

Dopo la conversione:

'2' → 00000010
'5' → 00000101

Per ottenere 25 bisogna fare:

valore = valore * 10 + nuova_cifra

In binario questo significa:

1. Moltiplicare per 10 (operazione aritmetica)
2. Sommare il nuovo valore

---

# 7️⃣ Differenza fondamentale

Carattere '5'  → 00110101  (53)
Numero 5       → 00000101  (5)

Sono due valori binari completamente diversi.

Il SUB AL, '0' serve esattamente a trasformare il primo nel secondo.

---

# 8️⃣ Riassunto concettuale

Quando leggiamo da tastiera:

• Otteniamo un BYTE ASCII
• ASCII delle cifre parte da 48
• Sottraiamo '0' per riallineare la sequenza a 0
• Il registro contiene sempre 8 bit completi
• Dopo la sottrazione abbiamo il numero reale


