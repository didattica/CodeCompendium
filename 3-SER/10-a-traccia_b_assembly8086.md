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
