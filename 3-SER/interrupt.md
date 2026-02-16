# Interrupt `int` in Assembly (x86)  
## Focus: `int 21h` (DOS)

---

# 1. Cos’è una `int`

L’istruzione:

```asm
int N
````

genera un **interrupt software**.

La CPU:

1. Salva FLAGS
2. Salva CS
3. Salva IP
4. Salta alla routine associata al numero N
5. Esegue il servizio
6. Torna con `iret`

Nel caso di:

```asm
int 21h
```

si richiama un servizio del **DOS**.

---

# 2. Selezione del Servizio

Il servizio viene scelto tramite il registro:

```
AH
```

Schema generale:

```asm
mov ah, <numero_servizio>
int 21h
```

Altri registri possono essere usati per passare parametri (DL, DX, AL, ecc.).

---

# 3. Terminare il Programma – `AH = 4Ch`

Servizio moderno e corretto per terminare un programma DOS:

```
AH = 4Ch
```

Esempio minimale:

```asm
mov ah, 4Ch      ; funzione terminate process
int 21h
```

### Il registro AL è obbligatorio?

Tecnicamente:

```
AL = exit code
```

Se non inizializzi AL, il programma termina comunque,
ma il codice di uscita sarà imprevedibile (conterrà il valore precedente).

👉 Buona pratica:

```asm
mov ah, 4Ch
mov al, 00h      ; codice di uscita = 0 (successo)
int 21h
```

Non è obbligatorio per il funzionamento,
ma è **corretto e consigliato** inizializzarlo.

---

# 4. Stampare un Carattere – `AH = 02h`

Servizio:

```
AH = 02h
DL = carattere ASCII
```

Esempio:

```asm
mov ah, 02h      ; funzione stampa carattere
mov dl, 'A'      ; codice ASCII di A
int 21h
```

Il DOS legge:

* AH → quale funzione
* DL → quale carattere stampare

---

# 5. Stampare il Numero 5

## Problema fondamentale

Numero 5 in binario:

```
00000101b = 05h
```

ASCII '5':

```
35h
```

Relazione:

```
ASCII = numero + 30h
```

---

# 6. Esempio Completo (MODEL SMALL)

```asm
.model small
.stack 100h
.data

.code
main:

    mov ax, @data
    mov ds, ax            ; inizializza segmento dati

    mov al, 5             ; valore numerico 5
    add al, 30h           ; conversione ASCII (5 → '5')

    mov dl, al            ; DL = carattere da stampare
    mov ah, 02h           ; funzione stampa carattere
    int 21h               ; chiamata al DOS

    mov ah, 4Ch           ; funzione terminate process
    mov al, 00h           ; codice di uscita = 0
    int 21h               ; ritorna al sistema operativo

end main
```

---

# 7. Analisi Dettagliata

### Inizializzazione DS

```asm
mov ax, @data
mov ds, ax
```

Serve per far puntare DS al segmento dati corretto.

---

### Caricare il numero

```asm
mov al, 5
```

AL = 05h (valore numerico puro, NON stampabile)

---

### Conversione ASCII

```asm
add al, 30h    ; conversione ASCII
```

05h + 30h = 35h → ora AL contiene il codice ASCII di '5'.

---

### Preparare la stampa

```asm
mov dl, al     ; il carattere va in DL
mov ah, 02h    ; selezione funzione stampa
int 21h        ; esegue il servizio DOS
```

---

### Terminazione

```asm
mov ah, 4Ch    ; funzione terminazione
mov al, 00h    ; exit code 0 (buona pratica)
int 21h
```

Se si omette:

```asm
mov al, 00h
```

Il programma termina comunque,
ma il codice di ritorno sarà indefinito.

---

# 8. Versione Ancora Più Essenziale

```asm
.model small
.stack 100h
.data

.code
main:

    mov ax, @data
    mov ds, ax

    mov al, 5
    add al, 30h        ; conversione ASCII

    mov dl, al
    mov ah, 02h
    int 21h

    mov ah, 4Ch
    int 21h            ; termina (AL non inizializzato)

end main
```

Funziona, ma non è formalmente pulita.

---

# 9. Concetti Fondamentali

* `int 21h` è una chiamata ai servizi DOS
* AH seleziona la funzione
* DL contiene il carattere da stampare
* Per stampare numeri → serve conversione ASCII
* `AH = 4Ch` termina il programma
* `AL` contiene il codice di uscita (consigliato inizializzarlo)

<!--
Nel prossimo documento possiamo approfondire:

* stampa numeri multi-cifra con divisione
* lettura input da tastiera (`AH = 01h`)
* differenza tra `int 10h` (BIOS) e `int 21h` (DOS)
* funzionamento interno dell'Interrupt Vector Table
-->

