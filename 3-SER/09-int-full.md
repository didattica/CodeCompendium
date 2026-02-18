# Interrupt `int` in Assembly (x86)

## Focus: `int 21h` (DOS)

---

# 1️⃣ Cos’è una `int`

L’istruzione:

```asm
int N
```

genera un **interrupt software**.

## 🔹 Cosa fa la CPU

Quando esegue:

```asm
int 21h
```

La CPU:

1. Salva `FLAGS`
2. Salva `CS`
3. Salva `IP`
4. Consulta la **Interrupt Vector Table (IVT)**
5. Salta alla routine associata
6. Esegue il servizio
7. Torna con `iret`

---

# 2️⃣ Schema del flusso

```
Programma
   │
   │ int 21h
   ▼
CPU
   │
   ▼
Interrupt Vector Table (0000:0000)
   │
   ▼
DOS (routine servizio)
   │
   ▼
IRET
   │
   ▼
Ritorno al programma
```

---

# 3️⃣ Struttura Generale di `int 21h`

Schema base:

```asm
mov ah, numero_funzione
; eventuali parametri in altri registri
int 21h
```

📌 Il registro **AH** seleziona il servizio.

Altri registri (AL, DL, DX, ecc.) contengono parametri.

---

# 4️⃣ Tabella Servizi Principali – `int 21h`

| Funzione                  | AH  | Parametri                                | Output          |
| ------------------------- | --- | ---------------------------------------- | --------------- |
| Terminare programma       | 4Ch | AL = exit code                           | ritorno al DOS  |
| Stampare carattere        | 02h | DL = carattere ASCII                     | —               |
| Stampare stringa          | 09h | DS:DX = indirizzo stringa `$`-terminated | —               |
| Input carattere (echo)    | 01h | —                                        | AL = carattere  |
| Input carattere (no echo) | 08h | —                                        | AL = carattere  |
| Input stringa             | 0Ah | DS:DX = buffer                           | buffer riempito |

---

# 5️⃣ Terminare il Programma – AH = 4Ch

```asm
mov ah, 4Ch
mov al, 00h   ; codice uscita
int 21h
```

📌 `AL` contiene l’**exit code**
Se non inizializzato → valore indefinito.

---

# 6️⃣ Stampare un Carattere – AH = 02h

```asm
mov ah, 02h
mov dl, 'A'
int 21h
```

Schema:

```
AH = 02h
DL = codice ASCII
```

---

# 7️⃣ Stampare una Stringa – AH = 09h

⚠️ La stringa deve terminare con `$`

```asm
.data
msg db "Ciao mondo$"

.code
mov dx, offset msg
mov ah, 09h
int 21h
```

Schema:

```
AH = 09h
DS:DX = indirizzo stringa
terminatore = $
```

---

# 8️⃣ Input da Tastiera

---

## 🔹 Leggere un carattere (con echo)

```asm
mov ah, 01h
int 21h
```

Risultato:

```
AL = carattere ASCII
```

Il carattere viene mostrato a schermo.

---

## 🔹 Leggere un carattere (senza echo)

```asm
mov ah, 08h
int 21h
```

Non viene visualizzato.

---

## 🔹 Leggere una stringa – AH = 0Ah

Richiede un buffer strutturato:

```asm
.data
buffer db 20        ; lunghezza massima
       db ?         ; numero caratteri letti
       db 20 dup(?) ; spazio per input
```

Uso:

```asm
mov dx, offset buffer
mov ah, 0Ah
int 21h
```

Struttura buffer:

| Byte | Contenuto              |
| ---- | ---------------------- |
| 0    | Lunghezza massima      |
| 1    | Numero caratteri letti |
| 2+   | Dati inseriti          |

---

# 9️⃣ Differenza Concettuale

Non stai chiamando funzioni "normali".

Stai usando:

```
Interrupt Software
```

Il DOS fornisce servizi tramite:

```
int 21h
```

È l’equivalente di una:

```
API del sistema operativo DOS
```

---

# 🔟 Schema Completo a Livello Hardware

```
[Programma Assembly]
        │
        │  mov ah, XX
        │  int 21h
        ▼
[CPU]
        │ salva FLAGS
        │ salva CS
        │ salva IP
        ▼
[Interrupt Vector Table]
        │ legge vettore 21h
        ▼
[DOS - Routine Servizio]
        │ esegue funzione richiesta
        ▼
[IRET]
        │ ripristina IP
        │ ripristina CS
        │ ripristina FLAGS
        ▼
[Ritorno al Programma]
```

---

# 🔹 Concetti Fondamentali

* `int` = interrupt software
* `int 21h` = servizi DOS
* `AH` seleziona la funzione
* Altri registri passano parametri
* Il ritorno avviene tramite `IRET`
* È un meccanismo a basso livello gestito dalla CPU

---
<!--
Se vuoi, nel prossimo passo posso aggiungere anche:

* Differenza tra interrupt hardware e software
* Struttura reale della Interrupt Vector Table
* Confronto con le system call moderne

Dimmi tu 😊-->
