# Sistema Esadecimale – Visuale

## 1. Potenze di 16

Il sistema esadecimale si basa sulle **potenze di 16**:

$16^x$

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

```diff id="hexsymbols"
0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F
```

dove $A=10$, $B=11$, $C=12$, $D=13$, $E=14$, $F=15$.

---

## 3. Conversione Decimale → Esadecimale

Metodo: **divisione ripetuta per 16**, i resti diventano le cifre esadecimali (dal basso verso l’alto).

**Esempio: 439**

```diff id="dec2hex"
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

**Esempio:** $1B7$ → `0001 1011 0111`

---

## 5. Shift in Esadecimale

Gli shift si applicano sui **bit**, come nel binario:

* `$<<1$` → shift a sinistra (moltiplica per 2)
* `$>>1$` → shift a destra (divide per 2)

**Esempio:** $1B7$ (439 decimale)

```diff id="shifthex"
Decimale: 439
Esadecimale: 1B7
Binario : 0001 1011 0111

Shift <<1: 0011 0110 1110 → 36E (878 dec)
Shift >>1: 0000 1101 1011 → DB  (219 dec)
```

---

## 6. Tabella Riassuntiva – Dec / Hex / Bin / Shift

| Dec | Hex | Binario        | <<1 | >>1 |
| --- | --- | -------------- | --- | --- |
| 10  | A   | 1010           | 14  | 5   |
| 439 | 1B7 | 0001 1011 0111 | 36E | DB  |
| 255 | FF  | 1111 1111      | 1FE | 7F  |


