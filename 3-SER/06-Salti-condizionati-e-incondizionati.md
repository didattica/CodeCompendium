# 🖥️ Assembly x86 – Salti condizionati e incondizionati (Versione schematica)

## 📌 Prerequisiti

- Registri principali: AX, BX, CX, DX  
- Flag CPU: Z (Zero), S (Sign), C (Carry), O (Overflow)  
- Concetto di **Program Counter (PC)**:
  - Il PC è un registro speciale della CPU che **indica l’indirizzo della prossima istruzione da eseguire**  
  - Ogni istruzione cambia il PC: 
    - normalmente incrementandolo alla successiva  
    - o modificandolo direttamente in caso di **salto (`jmp` o salto condizionato)**  
- Istruzioni per aggiornare flag: `cmp`, `add`, `sub`  
- Concetto di operatore:
  - `cmp` → binario (modifica solo flag, non registri)
  - `jmp` → unario (modifica PC)


---


## 1️⃣ Salti incondizionati

| Istruzione | Tipo   | Condizione | Flusso |
| ---------- | ------ | ---------- | ------ |
| jmp        | unario | sempre     | → etichetta |

💡 Flusso mentale:

```

Program Counter
│
▼
jmp etichetta
│
▼
etichetta

```

---

## 2️⃣ Salti condizionati

| Istruzione | Tipo   | Flag controllato | Signed/Unsigned | Condizione | Flusso se vero |
| ---------- | ------ | --------------- | --------------- | ---------- | -------------- |
| je / jz    | unario | Z               | entrambe         | Z=1        | → etichetta    |
| jne / jnz  | unario | Z               | entrambe         | Z=0        | → etichetta    |
| jl         | unario | S,O             | signed           | dest<src   | → etichetta    |
| jle        | unario | S,O,Z           | signed           | dest≤src  | → etichetta    |
| jg         | unario | S,O,Z           | signed           | dest>src  | → etichetta    |
| jge        | unario | S,O             | signed           | dest≥src  | → etichetta    |
| jb         | unario | C               | unsigned         | dest<src  | → etichetta    |
| jbe        | unario | C,Z             | unsigned         | dest≤src  | → etichetta    |
| ja         | unario | C,Z             | unsigned         | dest>src  | → etichetta    |
| jae        | unario | C               | unsigned         | dest≥src  | → etichetta    |

💡 Flusso mentale:

```
cmp dest, src
│
▼
Flag aggiornati → Z, S, C, O
│
▼
Salto condizionato?
├─► sì → etichetta
└─► no → istruzione successiva

````

---

## 3️⃣ Mini-flusso operativo

| Operatore | Tipo       | Flusso registri / flag | Risultato |
| ---------- | ---------- | --------------------- | ---------- |
| cmp        | binario    | dest, src → aggiornamento flag Z,S,C,O | nessun registro modificato |
| jmp        | unario     | PC → etichetta         | salto     |
| je/jne/... | unario     | Z,S,C,O → controllo    | salto condizionato |

---

## 4️⃣ Esercizi strutturati

### Esercizio 1 – Salto incondizionato
**Domanda:** Quale valore avrà AX dopo l’esecuzione?

```assembly
mov ax, 5
jmp fine
mov ax, 10   ; ignorato
fine:
````

**Risoluzione passo passo:**

```
1. mov ax,5 → AX = 5
2. jmp fine → salto immediato all’etichetta 'fine'
3. mov ax,10 → non eseguito
4. fine: → fine esecuzione
```

**Risultato:** AX = 5

---

### Esercizio 2 – Salto condizionato (uguale)

**Domanda:** CX sarà 0 o 1 dopo l’esecuzione?

```assembly
mov ax, 5
mov bx, 5
cmp ax, bx
je uguale
mov cx, 0
uguale:
mov cx, 1
```

**Risoluzione passo passo:**

```
1. mov ax,5 ; mov bx,5 → AX=5, BX=5
2. cmp ax,bx → AX-BX=0 → aggiorna flag Z=1
3. je uguale → Z=1 → salto a 'uguale'
4. mov cx,0 → ignorato
5. mov cx,1 → CX = 1
```

**Risultato:** CX = 1

---

### Esercizio 3 – Salto condizionato signed vs unsigned

**Domanda:** CX sarà 0 o 1 in ciascun caso?

**Caso signed:**

```assembly
mov ax, -3
mov bx, 2
cmp ax, bx
jl minore
mov cx, 0
minore:
mov cx, 1
```

**Risoluzione signed:**

```
1. AX=-3, BX=2
2. cmp ax,bx → aggiornamento flag S,O
3. jl minore → AX<BX (signed) → salto a 'minore'
4. mov cx,0 → ignorato
5. mov cx,1 → CX=1
```

**Risultato:** CX = 1

**Caso unsigned:**

```assembly
mov ax, 3
mov bx, 5
cmp ax, bx
jb sotto
mov cx, 0
sotto:
mov cx, 1
```

**Risoluzione unsigned:**

```
1. AX=3, BX=5
2. cmp ax,bx → aggiornamento flag C,Z
3. jb sotto → AX<BX (unsigned) → salto a 'sotto'
4. mov cx,0 → ignorato
5. mov cx,1 → CX=1
```

**Risultato:** CX = 1



Vuoi che faccia anche quella?
```
