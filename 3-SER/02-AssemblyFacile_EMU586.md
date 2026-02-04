# 🖥️ Lezione Completa di Assembly x86 (EMU 586 / EMU8086)

**Per studenti e studenti DSA – linguaggio semplice, progressivo, esempi chiari**

---

## 1️⃣ Assembly vs Assembler

### Assembly

* Linguaggio di programmazione **vicinissimo alla CPU** 🔧
* Usa **mnemonici** (parole brevi) come:

  ```assembly
  mov, add, sub, int
  ```
* **Ogni istruzione assembly corrisponde a una sola istruzione macchina**
  💡 *Metafora:* Assembly è come scrivere ricette passo passo per il tuo robot chef 🤖

### Assembler

* Programma che **traduce il codice Assembly in linguaggio macchina (numeri binari)**
* In EMU 586 l’assembler è **integrato**
  💡 *Metafora:* Assembler = traduttore simultaneo che converte le ricette in comandi che il robot capisce 📝→🤖

**Esempio semplice:**

```assembly
mov ax, 5    ; Assembly
```

Tradotto dall’assembler in codice macchina:

```
B8 05 00
```

---

## 2️⃣ Tipi di dati numerici in Assembly

In Assembly non esistono `int`, `float` o `double`.
Si lavora con **dimensioni**:

| Tipo | Dimensione | Significato              |
| ---- | ---------- | ------------------------ |
| DB   | 1 byte     | numeri 0–255 o caratteri |
| DW   | 2 byte     | numeri 0–65535           |
| DD   | 4 byte     | numeri grandi (32 bit)   |

**Esempi:**

```assembly
a DB 10       ; un byte
b DW 300      ; una word (2 byte)
c DD 100000   ; double word (4 byte)
```

💡 *Metafora:* DB, DW, DD = scatole di diverse dimensioni per contenere numeri 🎁

---

## 3️⃣ I registri del processore 8086

Registri principali (16 bit):

| Registro | Uso          |
| -------- | ------------ |
| AX       | Accumulatore |
| BX       | Base*        |
| CX       | Contatore    |
| DX       | Dati / I/O   |

*BX serve spesso come **punto di partenza per calcolare indirizzi** 🗺️

**Suddivisione in 8 bit:**

| Registro | Parte alta | Parte bassa |
| -------- | ---------- | ----------- |
| AX       | AH         | AL          |
| BX       | BH         | BL          |
| CX       | CH         | CL          |
| DX       | DH         | DL          |

**Esempio:**

```assembly
mov ax, 1234h
```

* AH = 12h
* AL = 34h

💡 *Metafora:* AX è una cassettina divisa in due scomparti: AH sopra, AL sotto 🛠️

---

## 4️⃣ Segmenti di memoria

| Segmento | Significato          |
| -------- | -------------------- |
| CS       | Codice (istruzioni)  |
| DS       | Dati                 |
| SS       | Stack                |
| ES       | Extra (uso generico) |

**Esempio:**

```assembly
mov ax, @data
mov ds, ax
```

💡 *Metafora:* “DS deve puntare al segmento dati del programma” → DS è come una mappa che indica dove trovare gli ingredienti 🍎📍

---

## 5️⃣ Skeleton di un programma Assembly

```assembly
.MODEL SMALL
.STACK 100H
DATA SEGMENT PUBLIC
DATA ENDS
CODE SEGMENT
ASSUME CS:CODE, DS:DATA
INIZIO:
    MOV AX, DATA
    MOV DS, AX
    MOV AH, 4CH
    INT 21H
CODE ENDS
END INIZIO
```

**Versione semplificata:**

```assembly
.MODEL small
.STACK 100h
.DATA
; qui vanno le variabili
.CODE
inizio:
    mov ax, @data
    mov ds, ax
    ; qui va il codice
    mov ax, 4Ch
    int 21h
END inizio
```

---

## 6️⃣ Spiegazione dello skeleton

* `.MODEL small` → programma piccolo, dati e codice in un solo segmento 🏠
* `.STACK 100h` → 256 byte per lo stack (area temporanea della CPU)
* `.DATA` → zona variabili
* `.CODE` → zona istruzioni
* `inizio:` → entry point del programma
* `mov ax, @data` → carico l’indirizzo dei dati
* `mov ds, ax` → DS punta ai dati

---

## 7️⃣ Primo programma: Hello World

```assembly
.MODEL small
.STACK 100h
.DATA
Messaggio DB "Hello World!",13,10,"$"
.CODE
inizio:
    mov ax, @data
    mov ds, ax
    mov dx, OFFSET Messaggio
    mov ah, 09h
    int 21h
    mov ax, 4Ch
    int 21h
END inizio
```

💡 *Spiegazione semplice:*

* `Messaggio DB ...` → creo una stringa
* `OFFSET Messaggio` → prendo l’indirizzo della stringa
* `mov dx, OFFSET Messaggio` → dico a DOS dove si trova
* `mov ah, 09h` → funzione DOS: stampa stringa
* `int 21h` → esegue la stampa
* `mov ax, 4Ch / int 21h` → termina il programma

**Flusso del programma (diagramma testuale):**

```
AVVIO
  |
Carico @data in AX
  |
Copio AX in DS (DS punta ai dati)
  |
Metto indirizzo stringa in DX
  |
AH = 09h (stampa stringa)
  |
INT 21h
  |
AX = 4C00h (termina)
  |
INT 21h (fine)
```

---

## 8️⃣ Interrupt DOS principali

* `int 21h` → porta per servizi DOS
* Funzioni usate:

  * AH = 09h → stampa stringa terminata da `$`
  * AH = 02h → stampa un carattere
  * AH = 4Ch → termina programma

💡 *Metafora:* int 21h = portinaio che esegue i nostri ordini verso DOS 🚪

---

## 9️⃣ Mini-riassunto per studenti con difficoltà

* **Assembly** = linguaggio
* **Assembler** = traduttore
* **Registri principali**: AX, BX, CX, DX
* AH/AL = metà alta e bassa
* Segmenti: CS, DS, SS, ES
* `.DATA` = variabili, `.CODE` = istruzioni
* `int 21h` = servizi DOS
* `4C00h` = fine programma
* EMU 586 mostra tutto in tempo reale

---

## 🔟 Esercizi base

1. Cambiare il messaggio
2. Stampare due righe
3. Stampare un carattere usando AH = 02h
4. Stampare tre caratteri uno alla volta:

   * un carattere per riga
   * tutti sulla stessa riga
   * sulla stessa riga separati da uno spazio

