# 🖥️ Assembly x86 – Operatori fondamentali
## mov, add, sub, int
**Spiegazione chiara di sintassi e funzionamento **

---

## 🎯 Perché questi operatori sono importanti

In Assembly **non esistono costrutti complessi** come `if`, `for`, `print`.
Tutto si riduce a **poche istruzioni base** che parlano direttamente con la CPU.

Le più usate sono:

```assembly
mov   ; copia dati
add   ; somma
sub   ; sottrazione
int   ; chiamata al sistema
````

👉 Capire **bene** queste istruzioni = capire **come ragiona il computer**

---

## 1️⃣ Istruzione `mov`

### 📌 Cosa fa (in una frase)

👉 **Copia un valore da una sorgente a una destinazione**

⚠️ Non è uno spostamento:
la sorgente **non perde** il valore.

---

### 🧠 Sintassi generale

```assembly
mov destinazione, sorgente
```

📌 Regola fondamentale:

> **NON esistono due memorie nella stessa istruzione**

✔️ Valido:

```assembly
mov ax, 5
mov ax, bx
mov dl, 'A'
```

❌ Non valido:

```assembly
mov memoria1, memoria2
```

---

### 🔧 Cosa succede a livello hardware

* La CPU:

  1. legge il valore sorgente
  2. lo copia nei circuiti interni
  3. lo scrive nella destinazione

💡 **Visualizzazione mentale**

```
SORGENTE ───▶ CPU ───▶ DESTINAZIONE
```

---

### 📦 Esempi tipici

```assembly
mov ax, 5
```

* AX contiene `0005h`
* Nessun altro registro cambia

```assembly
mov bl, al
```

* BL riceve il valore di AL
* AL resta invariato

---

### 🧠 Metafora DSA

👉 `mov` è come **fotocopiare** un foglio
L’originale resta dove si trova 📄📄

---

## 2️⃣ Istruzione `add`

### 📌 Cosa fa

👉 **Somma un valore a un registro**

Il risultato **sostituisce** il valore precedente della destinazione.

---

### 🧠 Sintassi generale

```assembly
add destinazione, sorgente
```

📌 Significato matematico:

```
destinazione = destinazione + sorgente
```

---

### 🔧 Cosa succede nella CPU

1. La CPU prende il valore della destinazione
2. Somma il valore della sorgente
3. Scrive il risultato nella destinazione
4. Aggiorna i **flag** (zero, segno, overflow…)

---

### 📦 Esempio

```assembly
mov ax, 3
add ax, 2
```

Risultato:

```
AX = 5
```

📌 AX cambia
📌 Il valore `2` non viene modificato

---

### 🧠 Effetto sui flag (senza dettagli tecnici)

* Se il risultato è **0** → flag ZERO = 1
* Se il risultato è **negativo** → flag SIGN = 1

👉 Servirà più avanti per i salti (`jmp`, `je`, ecc.)

---

### 🧠 Metafora DSA

👉 `add` è come **aggiungere monete a una scatola** 🪙
La scatola cambia contenuto

---

## 3️⃣ Istruzione `sub`

### 📌 Cosa fa

👉 **Sottrae un valore da un registro**

---

### 🧠 Sintassi generale

```assembly
sub destinazione, sorgente
```

📌 Significato matematico:

```
destinazione = destinazione - sorgente
```

---

### 🔧 Cosa succede nella CPU

1. La CPU legge la destinazione
2. Sottrae la sorgente
3. Scrive il risultato nella destinazione
4. Aggiorna i flag

---

### 📦 Esempio

```assembly
mov ax, 10
sub ax, 3
```

Risultato:

```
AX = 7
```

---

### 🧠 Caso importante

```assembly
sub ax, ax
```

Risultato:

```
AX = 0
```

👉 Metodo comune per **azzerare un registro**

---

### 🧠 Metafora DSA

👉 `sub` è come **togliere oggetti da una scatola** 📦➖

---

## 4️⃣ Istruzione `int`

### 📌 Cosa fa

👉 **Interrompe il programma e chiede un servizio al sistema**

Nel nostro caso:

* DOS
* BIOS

---

### 🧠 Sintassi

```assembly
int numero
```

Esempio:

```assembly
int 21h
```

---

### 🔧 Cosa succede davvero (hardware)

1. La CPU **ferma il programma**
2. Salva lo stato corrente
3. Salta a una **routine di sistema**
4. Esegue il servizio richiesto
5. Torna al programma

📌 Il servizio dipende dal valore in **AH**

---

### 📦 Esempio: stampa carattere

```assembly
mov dl, 'A'
mov ah, 02h
int 21h
```

* `AH = 02h` → stampa carattere
* `DL` → contiene il carattere
* `INT 21h` → DOS esegue la stampa

---

### 📦 Esempio: termina programma

```assembly
mov ax, 4Ch
int 21h
```

👉 Dice a DOS:
“Ho finito, puoi chiudere il programma”

---

### 🧠 Metafora DSA

👉 `int` è come **premere il campanello del sistema operativo** 🔔
Il programma chiede aiuto a qualcuno più potente

---

## 🔁 Confronto rapido

| Istruzione | Azione principale   | Cambia registri | Chi lavora |
| ---------- | ------------------- | --------------- | ---------- |
| mov        | copia valore        | sì              | CPU        |
| add        | somma               | sì              | CPU + ALU  |
| sub        | sottrazione         | sì              | CPU + ALU  |
| int        | chiamata al sistema | dipende         | OS / BIOS  |

---

## 🧠 Mini-riassunto finale (DSA)

* `mov` → copia dati
* `add` → somma
* `sub` → sottrae
* `int` → chiede un servizio al sistema
* Tutto passa **per i registri**
* La RAM non viene mai toccata “direttamente”
* La CPU esegue **una istruzione alla volta**


