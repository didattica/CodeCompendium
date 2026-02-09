
# 🖥️ Assembly x86 – Registro CX e istruzione LOOP

## 📌 Prerequisiti

- Registri principali: AX, BX, CX, DX  
- Flag CPU: Z, S, C, O  
- Concetto di **Program Counter (PC)**:
  - Indica **l’indirizzo della prossima istruzione** da eseguire  
  - Salti e `loop` modificano il PC per cambiare il flusso del programma  
- Concetto di **operatore binario/unario**:
  - `loop` → unario (opera su un solo indirizzo/etichetta)  
- Concetto di **registro contatore**:
  - CX viene usato come **contatore automatico** per cicli  
  - Ogni `loop` decrementa CX e decide se saltare  

---

## 1️⃣ Registro CX come contatore

- CX è un **registro a 16 bit**  
- Utilizzato tipicamente nei cicli **per contare le iterazioni**  
- Non influisce su flag di CPU (a differenza di `cmp` o `add`)  
- Funzionamento:  

```

CX = N   ; numero di ripetizioni
loop etichetta
decrementa CX
se CX != 0 → salto a etichetta
se CX = 0 → continua con istruzione successiva

```

💡 Metafora: CX è come un **timer automatico o una clessidra** ⏳  
> “Ripeti il blocco finché la clessidra non è vuota”

---

## 2️⃣ Istruzione LOOP

| Istruzione | Tipo   | Condizione | Registri modificati | Flusso |
| ---------- | ------ | ---------- | ----------------- | ------ |
| loop etichetta | unario | CX ≠ 0 → salto | CX ↓ di 1 | → etichetta se CX≠0, altrimenti istruzione successiva |

💡 Flusso mentale:

```

inizio ciclo:
...istruzioni...
loop ciclo
│
▼
CX = CX - 1
│
├─► CX ≠ 0 → salto a ciclo
└─► CX = 0 → continua istruzione successiva

````

---

## 3️⃣ Mini-flusso operativo con LOOP

| Operatore | Tipo       | Flusso registri / flag | Risultato |
| ---------- | ---------- | --------------------- | ---------- |
| loop      | unario     | CX → decrementato     | salto condizionato basato su CX |

---

## 4️⃣ Esercizi strutturati

### Esercizio 1 – ciclo semplice
**Domanda:** Quali valori assumerà AX durante l’esecuzione?

```assembly
mov cx, 3
mov ax, 0
ciclo:
    add ax, 2
    loop ciclo
````

**Risoluzione passo passo:**

```
1. mov cx,3 → CX=3
2. mov ax,0 → AX=0
3. ciclo:
    add ax,2 → AX=0+2=2
    loop ciclo → CX=3-1=2 → CX≠0 → salto a ciclo

4. ciclo:
    add ax,2 → AX=2+2=4
    loop ciclo → CX=2-1=1 → CX≠0 → salto a ciclo

5. ciclo:
    add ax,2 → AX=4+2=6
    loop ciclo → CX=1-1=0 → CX=0 → non salta

Fine ciclo → AX=6, CX=0
```

---

### Esercizio 2 – ciclo con decremento e somma

**Domanda:** Dopo l’esecuzione, quali valori avranno AX e CX?

```assembly
mov cx, 4
mov ax, 1
ciclo2:
    add ax,1
    loop ciclo2
```

**Risoluzione passo passo:**

```
1. CX=4, AX=1
2. Iterazione 1: AX=1+1=2, CX=4-1=3 → salto
3. Iterazione 2: AX=2+1=3, CX=3-1=2 → salto
4. Iterazione 3: AX=3+1=4, CX=2-1=1 → salto
5. Iterazione 4: AX=4+1=5, CX=1-1=0 → fine ciclo

Risultato finale: AX=5, CX=0
```

💡 Metafora: **CX è la clessidra che conta le ripetizioni**, AX è la scatola in cui accumulo oggetti 🪙

---

### Esercizio 3 – ciclo e salto condizionato combinato

**Domanda:** Quale istruzione sarà eseguita per ultima?

```assembly
mov cx,2
mov ax,0
ciclo3:
    add ax,3
    cmp ax,3
    je fine
    loop ciclo3
fine:
```

**Risoluzione passo passo:**

```
1. CX=2, AX=0
2. Iterazione 1:
    add ax,3 → AX=3
    cmp ax,3 → Z=1
    je fine → salto a fine
CX rimane 2 (non decrementato perché loop non eseguito)

Fine → AX=3
```

💡 Nota: **`loop` non viene eseguito se salto condizionato interrompe il flusso**

---

**Riepilogo metaforico:**

* CX = contatore/clessidra ⏳
* `loop` = “ripeti il blocco finché CX non è zero”
* `add`/`cmp` = azioni nel ciclo, aggiornano registro o flag
* Salti condizionati (`je`, `jl`, ...) e `loop` = strumenti per controllare il flusso


