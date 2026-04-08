# TRACCIA B — Convertire un numero a due cifre nel carattere ASCII corrispondente

## Obiettivo

Scrivere un programma Assembly 8086 che:

1. Chiede all'utente **due cifre** (0–9).
2. Converte le due cifre nel **numero intero** corrispondente (es. `'4' '8'` → 48).
3. Interpreta quel numero come **codice ASCII**.
4. Stampa il carattere corrispondente.

---

## SKELETON DA COMPLETARE

```asm
;----------------------------------------------------------
; TRACCIA B - Numero a due cifre → carattere ASCII
;----------------------------------------------------------

.model small
.stack 100h

.data
    msg1   db "Inserisci la prima cifra (0-9): $"
    msg2   db 13,10, "Inserisci la seconda cifra (0-9): $"
    msgRes db 13,10, "Il carattere ASCII corrispondente e': $"

.code
inizio:
    mov ax, @data
    mov ds, ax

    ; leggere prima cifra → BL
    ; leggere seconda cifra → BH

    ; chiama procedura e convertire BL e BH in numero a due cifre
    ; numero = BL*10 + BH

    ; interpretare il numero come codice ASCII
    ; stampare il carattere

    mov ah, 4Ch
    int 21h

end inizio
```

////////////////

# TRACCIA B — Convertire un numero a due cifre nel carattere ASCII corrispondente

## Obiettivo

Scrivere un programma Assembly 8086 che:

1. Chiede all'utente **due cifre** (0–9).
2. Converte le due cifre nel **numero intero** corrispondente (es. `'4' '8'` → 48).
3. Interpreta quel numero come **codice ASCII**.
4. Stampa il carattere corrispondente.

---

## Spiegazione della Soluzione — Analisi Approfondita

### 1. Come funziona la lettura di un carattere in DOS (INT 21h)

In Assembly 8086 su DOS, per leggere un singolo carattere dalla tastiera si usa la **INT 21h** con `AH = 01h`:

```asm
mov ah, 01h
int 21h       ; il carattere letto viene restituito in AL
```

Dopo l'interrupt, il registro `AL` (8 bit, la metà bassa di `AX`) contiene il **codice ASCII** del tasto premuto — **non il valore numerico**.

#### Esempio concreto — perché bisogna sottrarre `'0'` (48 decimale / 0x30)

Se l'utente preme il tasto `'4'`, la CPU riceve in `AL` il valore:

```
'4' in ASCII = 0x34 = 0011 0100b = 52 decimale
```

Ma noi vogliamo il valore numerico **4**, non 52. La tabella ASCII dei digit è:

| Carattere | ASCII dec | ASCII hex | Bit (8) |
|-----------|-----------|-----------|---------|
| `'0'`     | 48        | 0x30      | 0011 0000 |
| `'1'`     | 49        | 0x31      | 0011 0001 |
| `'2'`     | 50        | 0x32      | 0011 0010 |
| ...       | ...       | ...       | ... |
| `'8'`     | 56        | 0x38      | 0011 1000 |
| `'9'`     | 57        | 0x39      | 0011 1001 |

I bit 7-4 dei digit ASCII sono **sempre `0011`** (= 0x3). I bit 3-0 contengono il valore numerico effettivo. Quindi la conversione è semplicissima:

```
valore numerico = codice ASCII - 0x30
                = codice ASCII - '0'
                = codice ASCII AND 0x0F   ← alternativa bit a bit
```

In Assembly:

```asm
mov ah, 01h
int 21h          ; AL = codice ASCII della cifra
sub al, '0'      ; AL = AL - 48 → ora AL contiene il valore numerico (0–9)
mov bl, al       ; salva la prima cifra in BL
```

---

### 2. Costruire il numero intero a due cifre: `BL*10 + BH`

Una volta lette le due cifre (prima cifra in `BL`, seconda in `BH`), dobbiamo combinarle nel numero intero corrispondente secondo la formula:

```
numero = cifra_decine * 10 + cifra_unità
       = BL * 10 + BH
```

**Esempio:** cifra1 = `'4'` → BL = 4, cifra2 = `'8'` → BH = 8

```
4 * 10 + 8 = 48
```

In Assembly 8086, la moltiplicazione per 10 si esegue con `MUL` oppure, più efficientemente, con shift e addizioni. Il modo diretto:

```asm
mov al, bl       ; AL = cifra delle decine (es. 4)
mov bl, 10
mul bl           ; AX = AL * BL = 4 * 10 = 40
                 ; (MUL usa sempre AL come operando implicito,
                 ;  risultato 16 bit va in AX)
add al, bh       ; AL = 40 + 8 = 48
```

#### Cosa succede a livello di bit durante MUL

`MUL BL` esegue: `AX = AL × BL` (moltiplicazione **unsigned** 8×8 → 16 bit)

```
AL = 0000 0100b  (4)
BL = 0000 1010b  (10)
─────────────────────
AX = 0000 0000 0010 1000b = 40 = 0x28
```

Dopo `ADD AL, BH` (BH = 8 = `0000 1000b`):

```
AL = 0010 1000b  (40)
   + 0000 1000b  (8)
   ─────────────
   = 0011 0000b  (48) = 0x30
```

Notiamo un fatto interessante: **48 = 0x30 = codice ASCII di `'0'`**. Questo non è casuale — è il punto di partenza della tabella dei digit!

---

### 3. Interpretare il numero come codice ASCII e stamparlo

A questo punto `AL` contiene **48** (0x30). Dobbiamo semplicemente dire al DOS: "stampa il carattere il cui codice ASCII è 48", che è proprio `'0'`. Si usa **INT 21h con `AH = 02h`**, che vuole il carattere da stampare in `DL`:

```asm
mov dl, al       ; DL = 48 (0x30) → carattere '0'
mov ah, 02h
int 21h          ; stampa il carattere ASCII corrispondente
```

Il DOS legge `DL` come codice ASCII a 8 bit e invia il carattere al terminale.

#### Perché funziona: la simmetria ASCII

L'esercizio sfrutta un'elegante simmetria:

- L'utente digita `'4'` e `'8'` (codici ASCII 52 e 56)
- Li convertiamo in numeri 4 e 8 (sottraendo 48)
- Li combiniamo: 4×10 + 8 = **48**
- 48 è proprio il codice ASCII di **`'0'`**

Se l'utente avesse digitato `'6'` e `'5'`:
- 6×10 + 5 = **65** = `0x41` = codice ASCII di **`'A'`**

Se avesse digitato `'9'` e `'7'`:
- 9×10 + 7 = **97** = `0x61` = codice ASCII di **`'a'`**

---

### 4. Soluzione Completa Commentata

```asm
;----------------------------------------------------------
; TRACCIA B - Numero a due cifre → carattere ASCII
;----------------------------------------------------------

.model small
.stack 100h

.data
    msg1   db "Inserisci la prima cifra (0-9): $"
    msg2   db 13,10, "Inserisci la seconda cifra (0-9): $"
    msgRes db 13,10, "Il carattere ASCII corrispondente e': $"

.code
inizio:
    mov ax, @data
    mov ds, ax          ; inizializza il segmento dati

    ;--------------------------------------------------
    ; PASSO 1: stampare msg1 e leggere prima cifra → BL
    ;--------------------------------------------------
    mov ah, 09h
    lea dx, msg1
    int 21h             ; stampa "Inserisci la prima cifra..."

    mov ah, 01h
    int 21h             ; legge carattere, AL = ASCII della cifra (es. '4' = 52)
    sub al, '0'         ; converte: AL = valore numerico (es. 4)
                        ; bit: 0011 0100 - 0011 0000 = 0000 0100
    mov bl, al          ; salva la cifra delle decine in BL

    ;--------------------------------------------------
    ; PASSO 2: stampare msg2 e leggere seconda cifra → BH
    ;--------------------------------------------------
    mov ah, 09h
    lea dx, msg2
    int 21h             ; stampa "Inserisci la seconda cifra..."

    mov ah, 01h
    int 21h             ; legge carattere, AL = ASCII della cifra (es. '8' = 56)
    sub al, '0'         ; converte: AL = valore numerico (es. 8)
                        ; bit: 0011 1000 - 0011 0000 = 0000 1000
    mov bh, al          ; salva la cifra delle unità in BH

    ;--------------------------------------------------
    ; PASSO 3: calcolare BL*10 + BH
    ;--------------------------------------------------
    mov al, bl          ; AL = cifra decine (es. 4)
    mov cl, 10          ; CL = 10
    mul cl              ; AX = AL * CL (es. 4*10 = 40 = 0x28)
                        ; MUL usa AL implicito, risultato in AX
    add al, bh          ; AL = AX_low + BH (es. 40 + 8 = 48 = 0x30)
    mov bl, al          ; salva il risultato finale in BL

    ;--------------------------------------------------
    ; PASSO 4: stampare il messaggio e il carattere ASCII
    ;--------------------------------------------------
    mov ah, 09h
    lea dx, msgRes
    int 21h             ; stampa "Il carattere ASCII corrispondente e':"

    mov dl, bl          ; DL = codice ASCII da stampare (es. 48 = '0')
    mov ah, 02h
    int 21h             ; INT 21h/02h: stampa il carattere in DL

    ;--------------------------------------------------
    ; PASSO 5: uscita dal programma
    ;--------------------------------------------------
    mov ah, 4Ch
    int 21h             ; termina il processo, restituisce controllo a DOS

end inizio
```

---

### 5. Riepilogo dei Registri Usati

| Registro | Dimensione | Ruolo in questo programma |
|----------|-----------|--------------------------|
| `AX`     | 16 bit    | Usato da `MUL` per il risultato 16 bit; `AH` per i codici funzione INT 21h |
| `AL`     | 8 bit (basso di AX) | Riceve il carattere da INT 01h; operando di MUL |
| `BL`     | 8 bit (basso di BX) | Cifra delle decine, poi risultato finale |
| `BH`     | 8 bit (alto di BX)  | Cifra delle unità |
| `CL`     | 8 bit (basso di CX) | Costante 10 per la moltiplicazione |
| `DL`     | 8 bit (basso di DX) | Carattere da passare a INT 02h; indirizzo stringa per INT 09h |
| `DS`     | 16 bit (segment reg) | Punta al segmento dati `.data` |

---

### 6. Riepilogo Visivo del Flusso

```
Tastiera → INT 01h → AL = ASCII
                         │
                     sub '0'  (- 0x30)
                         │
                    AL = valore numerico
                         │
              ┌──────────┴──────────┐
           → BL (decine)        → BH (unità)
              │
           AL = BL
           MUL 10          → AX = decine * 10
           ADD AL, BH      → AL = numero finale
              │
           MOV DL, AL
           INT 02h  → stampa carattere ASCII
```

---

## SKELETON DA COMPLETARE

```asm
;----------------------------------------------------------
; TRACCIA B - Numero a due cifre → carattere ASCII
;----------------------------------------------------------

.model small
.stack 100h

.data
    msg1   db "Inserisci la prima cifra (0-9): $"
    msg2   db 13,10, "Inserisci la seconda cifra (0-9): $"
    msgRes db 13,10, "Il carattere ASCII corrispondente e': $"

.code
inizio:
    mov ax, @data
    mov ds, ax

    ; leggere prima cifra → BL
    ; leggere seconda cifra → BH

    ; chiama procedura e convertire BL e BH in numero a due cifre
    ; numero = BL*10 + BH

    ; interpretare il numero come codice ASCII
    ; stampare il carattere

    mov ah, 4Ch
    int 21h

end inizio
```
