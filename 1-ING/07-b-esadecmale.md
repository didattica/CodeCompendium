# Sistema Esadecimale – Visuale

## 1. Potenze di 16

Il sistema esadecimale si basa sulle **potenze di 16**:

$$
16^x
$$

Esempio:

| x | $16^x$ | Decimale |
| - | ------ | -------- |
| 0 | 1      | 1        |
| 1 | 16     | 16       |
| 2 | 256    | 256      |
| 3 | 4096   | 4096     |

---

## 2. Simboli Esadecimali

L’esadecimale usa **16 simboli**:

```text
0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F
````

dove:

$$
A=10, \quad B=11, \quad C=12, \quad D=13, \quad E=14, \quad F=15
$$

---

## 3. Conversione Decimale → Esadecimale

Metodo: **divisione ripetuta per 16**, i resti diventano le cifre esadecimali (dal basso verso l’alto).

**Esempio: 439**

```text
439 ÷ 16 = 27 resto 7
27 ÷ 16 = 1 resto 11 (B)
1 ÷ 16 = 0 resto 1
```

**Decimale 439 → Esadecimale 1B7**

---

## 4. Conversione Esadecimale → Binario

Ogni cifra esadecimale corrisponde a **4 bit**:

| Esadec | Binario |
| ------ | ------- |
| 0      | 0000    |
| 1      | 0001    |
| 2      | 0010    |
| 3      | 0011    |
| 4      | 0100    |
| 5      | 0101    |
| 6      | 0110    |
| 7      | 0111    |
| 8      | 1000    |
| 9      | 1001    |
| A      | 1010    |
| B      | 1011    |
| C      | 1100    |
| D      | 1101    |
| E      | 1110    |
| F      | 1111    |

**Esempio:**

$$
1B7_{16} \rightarrow 0001\ 1011\ 0111_2
$$

---

## 5. Shift in Esadecimale

### Shift di bit

Gli **shift di bit** si applicano sui **bit**, indipendentemente dalla base di rappresentazione:

* `$<<1$` → shift a sinistra di **1 bit**, moltiplica per 2
* `$>>1$` → shift a destra di **1 bit**, divide per 2

**Esempio con 1B7 (439 decimale):**

```text
Decimale: 439
Esadecimale: 1B7
Binario : 0001 1011 0111

Shift <<1 (1 bit): 0011 0110 1110 → 36E (878 dec)
Shift >>1 (1 bit): 0000 1101 1011 → DB  (219 dec)
```

### Shift di cifre esadecimali (×16 o ÷16)

Se vogliamo **shiftare di 1 cifra esadecimale**, spostiamo di **4 bit**:

* Moltiplicare per 16 → appendere uno 0 esadecimale a destra
* Dividere per 16 → rimuovere l’ultima cifra esadecimale

**Esempi:**

```text
B (11 dec) << 4 bit = B0 (176 dec)  ← moltiplicazione per 16
1B7 << 4 bit = 1B70 (7024 dec)
FF << 4 bit = FF0 (4080 dec)

B0 >> 4 bit = B (11 dec)           ← divisione per 16
1B70 >> 4 bit = 1B7 (439 dec)
```

---

## 6. Tabella Riassuntiva – Dec / Hex / Bin / Shift

| Dec | Hex | Binario        | <<1 bit | >>1 bit | <<4 bit | >>4 bit |
| --- | --- | -------------- | ------- | ------- | ------- | ------- |
| 10  | A   | 1010           | 14      | 5       | A0      | 0       |
| 439 | 1B7 | 0001 1011 0111 | 36E     | DB      | 1B70    | 1B7     |
| 255 | FF  | 1111 1111      | 1FE     | 7F      | FF0     | F       |

---

In questo modo:

* Gli **shift di bit** mostrano la moltiplicazione/divisione per 2.
* Gli **shift di cifra esadecimale** mostrano la moltiplicazione/divisione per 16.


