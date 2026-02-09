# 🖥️ Assembly x86 – Operatori fondamentali

## Sintassi e funzionamento

In Assembly **non esistono costrutti complessi** come `if`, `for`, o `print`.
Tutto si riduce a **poche istruzioni base** che comunicano direttamente con la CPU.

Le più comuni sono:

```assembly
mov   ; copia dati
add   ; somma
sub   ; sottrazione
mul   ; moltiplicazione
div   ; divisione
cmp   ; confronto
int   ; chiamata al sistema
```

👉 Capire queste istruzioni = capire **come ragiona il computer**.

---

## 1️⃣ Istruzione `mov` – copia valori

**Tipo:** binario (richiede sorgente e destinazione)

### Sintassi

```assembly
mov destinazione, sorgente
```

### Funzionamento

* Copia il valore della **sorgente** nella **destinazione**
* La sorgente **non viene modificata**
* Non è possibile copiare direttamente da memoria a memoria

### Esempi

```assembly
mov ax, 5     ; AX = 5
mov bl, al    ; BL = valore di AL
```

💡 Metafora: come **fotocopiare un foglio** 📄. L’originale resta intatto.

---

## 2️⃣ Istruzione `add` – somma

**Tipo:** binario

### Sintassi

```assembly
add destinazione, sorgente
```

### Funzionamento

```
destinazione = destinazione + sorgente
```

* Modifica la destinazione
* Aggiorna i flag della CPU (Zero, Sign, Overflow)

### Esempio

```assembly
mov ax, 3
add ax, 2   ; AX = 5
```

💡 Metafora: come **aggiungere monete a una scatola** 🪙. La scatola cambia contenuto.

---

## 3️⃣ Istruzione `sub` – sottrazione

**Tipo:** binario

### Sintassi

```assembly
sub destinazione, sorgente
```

### Funzionamento

```
destinazione = destinazione - sorgente
```

### Esempio

```assembly
mov ax, 10
sub ax, 3   ; AX = 7
```

💡 Metafora: **togliere oggetti da una scatola** 📦➖

---

## 4️⃣ Istruzione `mul` – moltiplicazione

**Tipo:** unario (moltiplica il registro AX per il valore specificato)

### Sintassi

```assembly
mul sorgente
```

### Funzionamento

* Esegue `AX * sorgente`
* Risultato a 32 bit (per operazioni su 16 bit):

  * Parte bassa → AX
  * Parte alta → DX

### Esempio

```assembly
mov ax, 1000
mov bx, 20
mul bx   ; AX = 20000 (se supera 16 bit, DX = parte alta)
```

💡 Metafora: come **unire due pile di monete**, ma il contenitore può avere due ripiani (AX e DX).

---

## 5️⃣ Istruzione `div` – divisione

**Tipo:** unario (divide DX:AX per il valore specificato)

### Sintassi

```assembly
div sorgente
```

### Funzionamento

* Divide il **numero completo DX:AX** per la sorgente
* Risultato → AX
* Resto → DX

### Esempio

```assembly
mov ax, 20
mov dx, 0
mov bx, 3
div bx   ; AX = 6, DX = 2 (resto)
```

💡 Metafora: come **dividere una torta grande**: la fetta intera va ad AX, gli avanzi a DX.

---

## 6️⃣ Istruzione `cmp` – confronto

**Tipo:** binario

### Sintassi

```assembly
cmp destinazione, sorgente
```

### Funzionamento

* Sostanzialmente esegue `destinazione - sorgente` senza modificare nessuno dei due
* Aggiorna i flag per **salti condizionati** (`je`, `jne`, `jg`, `jl`)

### Esempio

```assembly
mov ax, 5
cmp ax, 3   ; flag Z=0, flag S=0 → AX > 3
```

💡 Metafora: come **mettere due oggetti sulla bilancia** ⚖️ senza spostarli.

---

## 7️⃣ Istruzione `int` – chiamata al sistema

**Tipo:** unario (numero di servizio)

### Sintassi

```assembly
int numero
```

### Funzionamento

* Interrompe il programma
* Salva stato corrente
* Chiama una routine di sistema
* Torna al programma dopo l’esecuzione

### Esempi

```assembly
mov dl, 'A'
mov ah, 02h
int 21h     ; stampa A
```

```assembly
mov ax, 4Ch
int 21h     ; termina programma
```

💡 Metafora: **premere il campanello del sistema operativo** 🔔

---

## 🔁 Tabella riepilogativa

| Istruzione | Azione principale   | Tipo    | Risultato principale       | Note registri |
| ---------- | ------------------- | ------- | -------------------------- | ------------- |
| mov        | copia valore        | binario | modifica destinazione      | CPU           |
| add        | somma               | binario | modifica destinazione      | CPU + ALU     |
| sub        | sottrazione         | binario | modifica destinazione      | CPU + ALU     |
| mul        | moltiplicazione     | unario  | AX/DX                      | CPU + ALU     |
| div        | divisione           | unario  | AX = quoziente, DX = resto | CPU + ALU     |
| cmp        | confronto           | binario | aggiorna flag              | CPU           |
| int        | chiamata al sistema | unario  | dipende dal servizio       | OS / BIOS     |


