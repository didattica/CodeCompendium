
# Operatore `cmp` (Assembly)

## 1. Introduzione

L’istruzione `cmp` (compare) è utilizzata in Assembly per confrontare due operandi.  
Dal punto di vista logico, esegue una **sottrazione implicita**:

```

cmp A, B

```

equivale a:

```

A - B

```

⚠️ **Importante:** il risultato NON viene salvato.  
Vengono invece aggiornati i **flag nel registro FLAGS/EFLAGS/RFLAGS**.

L’istruzione `cmp` è quasi sempre seguita da un salto condizionato (`je`, `jne`, `jg`, `jl`, ecc.).

---

# 2. Segmento documento CMP (cenno)

A livello documentale, `cmp` è classificata come:

- Istruzione aritmetico-logica
- Non distruttiva (non modifica gli operandi)
- Impatta esclusivamente sui flag

In questo documento ci concentriamo soprattutto sull’effetto sui **flag** e sulla gestione dei salti.

---

# 3. Registro dei Flag (EFLAGS / RFLAGS)

Dopo `cmp`, vengono aggiornati principalmente:

| Flag | Nome | Significato |
|------|------|-------------|
| ZF | Zero Flag | Risultato = 0 |
| SF | Sign Flag | Risultato negativo |
| OF | Overflow Flag | Overflow aritmetico con segno |
| CF | Carry Flag | Prestito nella sottrazione (unsigned) |
| PF | Parity Flag | Parità dei bit |
| AF | Auxiliary Flag | Riporto intermedio (raro uso pratico) |

---

# 4. Logica Interna di CMP

```

cmp A, B

```

Internamente:

```

temp = A - B

````

I flag vengono impostati in base a `temp`.

---

# 5. Caso 1: Risultato ZERO

Esempio:

```asm
mov eax, 5
cmp eax, 5
````

Calcolo interno:

```
5 - 5 = 0
```

Flag risultanti:

* ZF = 1
* SF = 0
* OF = 0
* CF = 0

Salto tipico:

```asm
je etichetta
```

---

Altro esempio:

```asm
cmp 100, 100
```

Stesso effetto: ZF = 1.

---

# 6. Caso 2: Risultato POSITIVO

Esempio:

```asm
mov eax, 10
cmp eax, 4
```

Calcolo:

```
10 - 4 = 6
```

Flag:

* ZF = 0
* SF = 0
* OF = 0
* CF = 0

Interpretazione:

* Confronto signed → maggiore
* Confronto unsigned → maggiore

Salti compatibili:

```asm
jg etichetta    ; signed >
ja etichetta    ; unsigned >
```

---

# 7. Caso 3: Risultato NEGATIVO (signed)

Esempio:

```asm
mov eax, 3
cmp eax, 7
```

Calcolo:

```
3 - 7 = -4
```

Flag:

* ZF = 0
* SF = 1
* OF = 0
* CF = 1   (borrow nella sottrazione unsigned)

Interpretazione:

* Signed → minore
* Unsigned → minore (per via di CF)

Salti:

```asm
jl etichetta    ; signed <
jb etichetta    ; unsigned <
```

---

# 8. Focus su OF (Overflow Flag)

L’Overflow avviene SOLO in aritmetica con segno.

Esempio 8 bit:

```
127 - (-1)
```

In 8 bit signed:

```
127 - (-1) = 128
```

Ma 128 non è rappresentabile in 8 bit signed
Range: -128 → 127

Risultato effettivo: -128 (wrap)

OF = 1

Esempio Assembly:

```asm
mov al, 127
cmp al, -1
```

Risultato interno: 128 (overflow signed)

Flag:

* OF = 1
* SF = 1
* ZF = 0

---

# 9. Focus su CF (Carry Flag)

CF è rilevante nei confronti **unsigned**.

Esempio:

```asm
mov eax, 2
cmp eax, 5
```

```
2 - 5
```

Unsigned → serve prestito
CF = 1

Se:

```asm
mov eax, 10
cmp eax, 3
```

CF = 0

---

# 10. Differenza Signed vs Unsigned

CMP è la stessa istruzione.
Cambia il salto condizionato usato dopo.

### Signed

| Istruzione | Significato |
| ---------- | ----------- |
| jl         | <           |
| jg         | >           |
| jle        | <=          |
| jge        | >=          |

Usano: SF e OF

---

### Unsigned

| Istruzione | Significato |
| ---------- | ----------- |
| jb         | <           |
| ja         | >           |
| jbe        | <=          |
| jae        | >=          |

Usano: CF e ZF

---

# 11. Esempi Completi

## Esempio A

```asm
mov eax, 8
cmp eax, 8
je uguale
```

Risultato: ZF = 1

---

## Esempio B

```asm
mov eax, -3
cmp eax, 2
jl minore
```

Calcolo:

```
-3 - 2 = -5
```

SF = 1
OF = 0
JL verifica: SF ≠ OF → salto

---

## Esempio C (overflow signed)

```asm
mov al, -128
cmp al, 1
```

```
-128 - 1 = -129
```

In 8 bit diventa 127

OF = 1

---

## Esempio D (unsigned grande)

```asm
mov eax, 0FFFFFFFFh
cmp eax, 1
```

Unsigned:

```
4294967295 - 1 = 4294967294
```

CF = 0
JA → vero

Signed invece:

```
-1 - 1 = -2
```

Interpretazione completamente diversa.

---

# 12. Riassunto Finale

`cmp`:

* Non modifica i registri
* Simula una sottrazione
* Aggiorna i flag
* È sempre seguita da salto condizionato

Valore risultato implicito:

| Caso            | ZF | SF      | OF | CF      |
| --------------- | -- | ------- | -- | ------- |
| A = B           | 1  | 0       | 0  | 0       |
| A > B           | 0  | 0       | 0  | 0       |
| A < B           | 0  | 1       | 0  | 1       |
| Overflow signed | 0  | dipende | 1  | dipende |

---

# 13. Concetto chiave

`cmp` non decide nulla.
Sono i **flag** a decidere.

La scelta tra confronto signed e unsigned dipende esclusivamente dal salto che usi dopo.
