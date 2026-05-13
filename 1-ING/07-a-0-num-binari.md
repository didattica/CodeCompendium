# Numeri Binari – Visuale

## 1. Potenze di 2

Il sistema binario si basa sulle **potenze di 2**:

[
2^x
]

Esempio:

| x | (2^x) | Binario |
| - | ----- | ------- |
| 0 | 1     | 1       |
| 1 | 2     | 10      |
| 2 | 4     | 100     |
| 3 | 8     | 1000    |
| 4 | 16    | 10000   |

---

## 2. Conversione Decimale → Binario

Metodo: somma di potenze di 2.

**Esempio: 19**

1. Trova le potenze di 2 ≤ 19 → 16, 8, 4, 2, 1
2. Somma: 19 = 16 + 2 + 1
3. Binario: `10011`

```diff
2^4  2^3  2^2  2^1  2^0
+1    0    0    1    1
```

### Altri esempi

| Dec | Binario |
| --- | ------- |
| 5   | 101     |
| 12  | 1100    |
| 7   | 111     |
| 20  | 10100   |

---

## 3. Shift dei Bit

Lo **shift** sposta i bit e corrisponde a moltiplicazione/divisione per 2.

### Shift a sinistra (`<< 1`)

```diff
Decimale: 3
Binario :  11
Shift <<1:110  (3*2 = 6)
```

### Shift a destra (`>> 1`)

```diff
Decimale: 6
Binario : 110
Shift >>1: 11  (6/2 = 3)
```

---

## 4. Tabella Riassuntiva

| Dec | Bin   | <<1    | >>1  |
| --- | ----- | ------ | ---- |
| 5   | 101   | 1010   | 10   |
| 12  | 1100  | 11000  | 110  |
| 7   | 111   | 1110   | 11   |
| 20  | 10100 | 101000 | 1010 |

---

## 5. Esempio Passo-Passo: 13 → Binario

**Decimale:** 13

1. Potenze di 2 ≤ 13 → 8, 4, 2, 1
2. Somma per ottenere 13 → 8 + 4 + 1
3. Scrivi binario:

```diff
2^3  2^2  2^1  2^0
+1    1    0    1
```


