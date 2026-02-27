

# Stack, PUSH automatici e `IRET`

Questa è la parte **più importante a livello hardware** per capire davvero cosa succede quando usi `int`.

---

## 🔹 Cos’è lo stack (in breve)

Lo **stack** è una zona di memoria usata con logica **LIFO** (Last In, First Out).

In modalità reale DOS:

* lo stack è indirizzato da **SS:SP**
* `PUSH` → decrementa `SP` e scrive
* `POP` → legge e incrementa `SP`

---

## 🔹 Cosa fa la CPU quando esegue `int 21h`

Quando la CPU esegue:

```asm
int 21h
```

NON è DOS a salvare i registri.
È la **CPU stessa**, in hardware.

La CPU esegue automaticamente:

```text
PUSH FLAGS
PUSH CS
PUSH IP
```

⚠️ L’ordine è fondamentale.

---

## 🔹 Stack prima e dopo `int`

### Prima di `int 21h`

```
SP ──► (top dello stack)
```

### Dopo `int 21h`

```
SP ──► IP   ← ultimo PUSH
        CS
        FLAGS
```

Ora la CPU:

* legge la voce 21h dalla Interrupt Vector Table
* carica il nuovo `CS:IP`
* inizia a eseguire il codice DOS

---

## 🔹 Perché si salvano anche i FLAGS

Perché l’interrupt **non deve alterare il comportamento logico del programma**.

Esempio:

* Carry Flag
* Zero Flag
* Interrupt Flag

Devono tornare **esattamente com’erano**.

---

## 🔹 Cosa fa `IRET`

Alla fine della routine DOS trovi:

```asm
IRET
```

Che equivale esattamente a:

```text
POP IP
POP CS
POP FLAGS
```

In questo ordine.

---

## 🔹 Stack dopo `IRET`

```
SP ──► (stack ripristinato)
```

La CPU riprende l’esecuzione da:

```
CS:IP   (istruzione subito dopo INT 21h)
```

Come se l’interrupt non fosse mai avvenuto.

---

## 🔹 Differenza cruciale: `CALL/RET` vs `INT/IRET`

| Meccanismo | Cosa viene salvato | Ritorno |
| ---------- | ------------------ | ------- |
| CALL       | IP (e CS se FAR)   | RET     |
| INT        | FLAGS + CS + IP    | IRET    |

⚠️ Un handler di interrupt **DEVE** usare `IRET`.

Usare `RET` corrompe lo stack.

---

## 🎯 Punto chiave da ricordare

Quando usi `int 21h`:

* non stai chiamando una funzione normale
* stai forzando un cambio di flusso gestito dalla CPU
* lo stack è il meccanismo che rende il tutto reversibile
* `IRET` è l’unico modo corretto per tornare indietro

Questo è uno dei concetti più importanti di tutto l’Assembly x86.
