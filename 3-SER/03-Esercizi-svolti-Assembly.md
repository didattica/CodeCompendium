# 🖥️ Assembly x86 (EMU8086 / EMU 586)
## Esercizi svolti 

---

## ⚠️ Assunzioni valide per tutti gli esercizi

Per ogni esercizio si assume che:

- il **template Assembly sia già pronto**
- i segmenti `.DATA` e `.CODE` siano già dichiarati
- `DS` sia già inizializzato correttamente
- il programma termini con `INT 21h – AH = 4Ch`

👉 Devi scrivere **solo le poche righe richieste dall’esercizio**

---

## 🟢 Esercizio 1 – Stampare una stringa

### 📌 Traccia
Stampare a video la stringa **"Hello World!"**.

La stringa è già presente nel segmento dati:

```assembly
msg DB "Hello World!$"
````

---

### ✅ Soluzione (3 righe)

```assembly
mov dx, OFFSET msg
mov ah, 09h
int 21h
```

---

### 🧠 Spiegazione semplificata

* `OFFSET msg` → prende **l’indirizzo** della stringa
* `DX` → registro usato da DOS per sapere **dove si trova il testo**
* `AH = 09h` → servizio DOS per **stampare una stringa**
* `INT 21h` → esegue l’ordine

💡 **Idea chiave:**
👉 “DOS, vai a leggere il testo che si trova a quell’indirizzo e stampalo”

---

## 🟢 Esercizio 2 – Stampare un carattere singolo

### 📌 Traccia

Stampare a video il carattere **A**.

---

### ✅ Soluzione

```assembly
mov dl, 'A'
mov ah, 02h
int 21h
```

---

### 🧠 Spiegazione semplificata

* `DL` → contiene **il carattere da stampare**
* `AH = 02h` → servizio DOS per **stampare un solo carattere**
* `INT 21h` → stampa il carattere

💡 **Regola da ricordare:**
🧠 *Carattere → DL*
🧠 *Stampa carattere → AH = 02h*

---

## 🟢 Esercizio 3 – Stampare un carattere tramite codice ASCII

### 📌 Traccia

Stampare il carattere con codice ASCII **41h**.

---

### ✅ Soluzione

```assembly
mov dl, 41h
mov ah, 02h
int 21h
```

---

### 🧠 Spiegazione semplificata

* `41h` in ASCII corrisponde alla lettera **A**
* Il computer **non vede lettere**, ma numeri
* DOS trasforma quel numero nel carattere corretto

💡 **Idea chiave:**
👉 ASCII = tabella che associa numeri a caratteri

---

## 🟢 Esercizio 4 – Stampare due volte lo stesso carattere

### 📌 Traccia

Stampare **due volte** il carattere `*`.

---

### ✅ Soluzione

```assembly
mov dl, '*'
mov ah, 02h
int 21h
int 21h
```

---

### 🧠 Spiegazione semplificata

* Il carattere resta in `DL`
* Ogni `INT 21h` **ripete l’azione**
* Non serve ricaricare il carattere

💡 **Concetto importante:**
👉 Se i registri non cambiano, il risultato si ripete

---

## 🟢 Esercizio 5 – Stampare un carattere e andare a capo

### 📌 Traccia

Stampare il carattere **X** e poi andare a capo.

---

### ✅ Soluzione

```assembly
mov dl, 'X'
mov ah, 02h
int 21h
mov dl, 10
```

---

### 🧠 Spiegazione semplificata

* `10` → Line Feed (nuova riga)
* Serve per spostare il cursore verso il basso
* Il computer **tratta anche l’a capo come un carattere**

💡 **Promemoria:**

* 13 = ritorno carrello
* 10 = nuova riga

---

## 🟢 Esercizio 6 – Stampare una stringa su due righe

### 📌 Traccia

Stampare:

```
Ciao
Mondo
```

La stringa è già definita così:

```assembly
msg DB "Ciao",13,10,"Mondo$"
```

---

### ✅ Soluzione

```assembly
mov dx, OFFSET msg
mov ah, 09h
int 21h
```

---

### 🧠 Spiegazione semplificata

* `13,10` → simulano il tasto **Invio**
* DOS legge la stringa **fino al simbolo `$`**
* Tutto viene stampato automaticamente

💡 **Vantaggio:**
👉 Una sola stampa = più righe

---

## 🟢 Esercizio 7 – Uso dei registri

### 📌 Traccia

Caricare il valore **5** nel registro `AX`.

---

### ✅ Soluzione

```assembly
mov ax, 5
```

---

### 🧠 Spiegazione semplificata

* `AX` è un registro da **16 bit**
* Può contenere numeri
* `mov` = copia un valore in un registro

💡 **Idea chiave:**
👉 I registri sono “scatoline veloci” della CPU

---

## 🟢 Esercizio 8 – Copiare la parte bassa di AX

### 📌 Traccia

Dato che `AX = 1234h`, copiare **AL** in `BL`.

---

### ✅ Soluzione

```assembly
mov bl, al
```

---

### 🧠 Spiegazione semplificata

* `AL` → parte bassa di `AX`
* `BL` → parte bassa di `BX`
* Si copiano **8 bit**

💡 **Visualizzazione mentale:**
AX = [ AH | AL ]
BX = [ BH | BL ]

---

## 📌 Mini-riassunto finale
* **Stringhe** → `AH = 09h`
* **Caratteri singoli** → `AH = 02h`
* **Indirizzo stringa** → `DX`
* **Carattere** → `DL`
* `INT 21h` = esegue il comando
* `$` = fine stringa

