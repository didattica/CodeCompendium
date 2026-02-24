# Moltiplicazione in Esadecimale con `mul` e Shift (Continua)

In questa sezione, esploreremo come il comando `mul` gestisce l'**overflow** e il **non overflow** nel contesto di moltiplicazioni in **esadecimale**. Quando il risultato di una moltiplicazione supera la capacità di 16 bit, l'overflow viene gestito utilizzando il registro **DX** per memorizzare la parte alta del risultato.

## Overflow e Non Overflow con `mul`

### Cos'è l'Overflow in Assembly?

Quando esegui una moltiplicazione con `mul` in **assembly x86**, il risultato viene automaticamente suddiviso tra i registri **AX** (parte bassa) e **DX** (parte alta). Tuttavia, se il risultato della moltiplicazione supera i **16 bit**, si verifica un **overflow** e **DX** viene utilizzato per contenere i **16 bit superiori**.

- **Non overflow**: Il risultato è contenuto interamente in **AX** (16 bit).
- **Overflow**: Il risultato supera i 16 bit, quindi la parte alta del risultato viene memorizzata in **DX**, mentre la parte bassa rimane in **AX**.

### 1. **Caso Senza Overflow**: Risultato contenuto in AX

#### Esempio 1: Moltiplicazione senza overflow

Supponiamo di moltiplicare **AX** per **16 (0x10)**. Il risultato rientra nei 16 bit.

```asm id="dxm48g"
mov ax, 0x2000   ; AX = 0x2000 = 8192 (decimale)
mov bx, 0x10     ; BX = 0x10 = 16 (decimale)
mul bx            ; AX = AX * BX
````

##### Calcolo in esadecimale:

* **In decimale**: ( 8192 \times 16 = 131072 )
* **In esadecimale**: ( 0x2000 \times 0x10 = 0x20000 )

Poiché il risultato (`0x20000`) è maggiore di 16 bit, viene suddiviso:

```asm id="7lhtz2"
DX = 0x2       ; Parte alta del risultato
AX = 0x0000    ; Parte bassa del risultato
```

In questo caso, **AX** contiene la parte bassa del risultato, mentre **DX** contiene la parte alta. Tuttavia, poiché **DX** non è zero e la moltiplicazione non ha causato un overflow nel senso completo del termine (abbiamo una parte alta valida), il valore finale sarà **DX:AX = 0x2:0x0000**.

### 2. **Caso con Overflow**: Risultato che supera i 16 bit

#### Esempio 2: Moltiplicazione che causa overflow

Supponiamo di moltiplicare **AX = 0x8000** (32768 in decimale) per **BX = 0x2** (2 in decimale). Il risultato sarà maggiore di 16 bit, quindi si verificherà un overflow.

```asm id="hl5fmn"
mov ax, 0x8000   ; AX = 0x8000 = 32768 (decimale)
mov bx, 0x2      ; BX = 0x2 = 2 (decimale)
mul bx            ; AX = AX * BX
```

##### Calcolo in esadecimale:

* **In decimale**: ( 32768 \times 2 = 65536 )
* **In esadecimale**: ( 0x8000 \times 0x2 = 0x10000 )

Poiché il risultato (`0x10000`) è troppo grande per essere contenuto in 16 bit, il risultato viene diviso tra **DX** e **AX**:

```asm id="qz0yk2"
DX = 0x1       ; Parte alta del risultato
AX = 0x0000    ; Parte bassa del risultato
```

In questo caso, **DX** contiene la parte alta del risultato, mentre **AX** contiene la parte bassa (che in questo esempio è zero).

### 3. **Caso con Overflow Maggiore di 32 bit**

#### Esempio 3: Moltiplicazione con risultato che richiede più di 32 bit

Supponiamo di moltiplicare **AX = 0x8000** per **BX = 0x100**. Questo produrrà un risultato che richiede più di 32 bit per essere rappresentato.

```asm id="7htjc9"
mov ax, 0x8000   ; AX = 0x8000 = 32768 (decimale)
mov bx, 0x100    ; BX = 0x100 = 256 (decimale)
mul bx            ; AX = AX * BX
```

##### Calcolo in esadecimale:

* **In decimale**: ( 32768 \times 256 = 8388608 )
* **In esadecimale**: ( 0x8000 \times 0x100 = 0x800000 )

Il risultato `0x800000` è un numero a **24 bit**. Per gestirlo, il valore sarà diviso tra **DX** e **AX**:

```asm id="h56sc2"
DX = 0x8       ; Parte alta del risultato
AX = 0x0000    ; Parte bassa del risultato
```

**DX** contiene **0x8** (parte alta del risultato) e **AX** contiene **0x0000** (parte bassa).

### Overflow e `mul` – Riepilogo

* **Non overflow**: Il risultato della moltiplicazione rientra nei 16 bit e viene memorizzato interamente in **AX**.
* **Overflow**: Se il risultato supera i 16 bit, la parte alta va in **DX** e la parte bassa in **AX**. Se il risultato è maggiore di 32 bit, il valore in **DX:AX** rappresenta correttamente il risultato completo.

In tutti i casi di **overflow**, **DX** viene utilizzato per memorizzare i **16 bit più significativi**, mentre **AX** contiene i **16 bit meno significativi**.

---

## Conclusioni

Abbiamo esplorato come la moltiplicazione in **esadecimale** con il comando `mul` venga gestita sia in **situazioni di overflow** che **senza overflow**. Quando il risultato di una moltiplicazione supera i 16 bit, **DX** viene utilizzato per contenere la parte alta del risultato, mentre **AX** contiene la parte bassa.

Questa gestione è automatica e facilita l'elaborazione dei numeri grandi senza richiedere codice aggiuntivo per gestire l'overflow, rendendo l'operazione molto più efficiente in assembly.



