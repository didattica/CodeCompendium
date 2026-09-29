# Il sistema binario

## 1. Che cos'è un sistema di numerazione?

Un **sistema di numerazione** è un insieme di simboli e regole utilizzato per rappresentare i numeri.

I simboli utilizzati per scrivere i numeri sono chiamati **cifre**.

Il sistema che utilizziamo normalmente è il **sistema decimale**, detto anche **sistema in base 10**.

Utilizza 10 cifre:

```text
0 1 2 3 4 5 6 7 8 9
```

Il **sistema binario** è invece un sistema di numerazione **in base 2**.

Utilizza solamente due cifre:

```text
0 1
```

---

# 2. Sistemi di numerazione posizionali

Il sistema decimale e il sistema binario sono **sistemi di numerazione posizionali**.

In un sistema posizionale, il valore di una cifra dipende:

1. dal valore della cifra;
2. dalla posizione che essa occupa nel numero.

Consideriamo il numero decimale:

```text
352
```

Possiamo scriverlo come:

$$
352 = 3\cdot10^2 + 5\cdot10^1 + 2\cdot10^0
$$

cioè:

$$
352 = 300+50+2
$$

Nel sistema decimale, quindi, ogni posizione corrisponde a una **potenza di 10**.

---

# 3. Il sistema binario

Nel sistema binario avviene la stessa cosa, ma ogni posizione corrisponde a una **potenza di 2**.

Consideriamo:

```text
1011₂
```

Le posizioni rappresentano:

```text
2³   2²   2¹   2⁰
 8    4    2    1
-----------------
 1    0    1    1
```

Quindi:

$$
1011_2 =
1\cdot2^3+
0\cdot2^2+
1\cdot2^1+
1\cdot2^0
$$

$$
=8+0+2+1
$$

$$
=11_{10}
$$

Il pedice indica la **base**:

- $1011_2$ → numero scritto in base 2;
- $1011_{10}$ → numero scritto in base 10.

**Attenzione:** la stessa sequenza di cifre può rappresentare valori diversi a seconda della base.

---

# 4. Le potenze di 2

Per lavorare con i numeri binari è importante conoscere le prime potenze di 2.

| Potenza | Valore |
|--------:|-------:|
| $2^0$ | 1 |
| $2^1$ | 2 |
| $2^2$ | 4 |
| $2^3$ | 8 |
| $2^4$ | 16 |
| $2^5$ | 32 |
| $2^6$ | 64 |
| $2^7$ | 128 |
| $2^8$ | 256 |
| $2^9$ | 512 |
| $2^{10}$ | 1024 |

Osserviamo:

| Decimale | Binario |
|---------:|--------:|
| 1 | `1` |
| 2 | `10` |
| 4 | `100` |
| 8 | `1000` |
| 16 | `10000` |
| 32 | `100000` |
| 64 | `1000000` |
| 128 | `10000000` |

Una potenza di 2, scritta in binario, è rappresentata da:

```text
1 seguito da una serie di 0
```

Ad esempio:

$$
2^5=32=100000_2
$$

---

# 5. Il bit

La parola **bit** deriva dall'espressione inglese:

> **binary digit** = cifra binaria

Un bit può assumere solamente due valori:

```text
0
1
```

Il **bit è l'unità fondamentale dell'informazione digitale**.

Un bit permette di distinguere tra due possibili stati.

Per esempio:

```text
0 → falso
1 → vero
```

oppure, in maniera semplificata:

```text
0 → spento
1 → acceso
```

Nei circuiti elettronici i due valori possono essere rappresentati mediante due differenti livelli di tensione.

**Importante:** `0` e `1` non significano necessariamente "spento" e "acceso". Sono due simboli utilizzati per rappresentare **due stati distinti**.

---

# 6. Dal bit al byte

Un singolo bit permette di rappresentare due possibilità:

$$
2^1=2
$$

Con due bit abbiamo:

```text
00
01
10
11
```

quindi:

$$
2^2=4
$$

possibili combinazioni.

In generale, con **n bit** possiamo rappresentare:

$$
\boxed{2^n}
$$

combinazioni differenti.

| Numero di bit | Combinazioni |
|--------------:|-------------:|
| 1 | $2^1=2$ |
| 2 | $2^2=4$ |
| 3 | $2^3=8$ |
| 4 | $2^4=16$ |
| 8 | $2^8=256$ |

Un gruppo di **8 bit** viene chiamato **byte**.

```text
1 byte = 8 bit
```

Esempio di byte:

```text
01001101
```

Con 8 bit possiamo rappresentare:

$$
2^8=256
$$

combinazioni differenti.

Se utilizziamo queste combinazioni per rappresentare numeri interi **senza segno**, possiamo rappresentare i numeri:

```text
da 0 a 255
```

Infatti:

$$
2^8-1=255
$$

---

# 7. Perché i computer usano il sistema binario?

I computer sono costruiti utilizzando circuiti elettronici.

Un circuito elettronico può distinguere in maniera affidabile tra due stati fisici differenti.

In maniera semplificata possiamo pensare a:

```text
stato basso → 0
stato alto  → 1
```

Per questo motivo il sistema binario è particolarmente adatto alla rappresentazione delle informazioni nei computer.

Numeri, testi, immagini, suoni, video e programmi possono essere rappresentati mediante sequenze di bit.

---

# 8. Conversione da binario a decimale

Per convertire un numero binario in decimale dobbiamo considerare il **peso** di ogni posizione.

Ogni posizione corrisponde a una potenza di 2.

## Esempio: `1101₂`

```text
          2³   2²   2¹   2⁰
           8    4    2    1
         -------------------
           1    1    0    1
```

Quindi:

$$
1101_2 =
1\cdot8+
1\cdot4+
0\cdot2+
1\cdot1
$$

$$
=8+4+1
$$

$$
=13
$$

Quindi:

$$
\boxed{1101_2=13_{10}}
$$

---

## Altro esempio: `10110₂`

```text
2⁴   2³   2²   2¹   2⁰
16    8    4    2    1
------------------------
 1    0    1    1    0
```

Consideriamo solamente le posizioni nelle quali compare `1`:

$$
16+4+2=22
$$

Quindi:

$$
\boxed{10110_2=22_{10}}
$$

---

# 9. Conversione da decimale a binario

Per convertire un numero decimale in binario possiamo **scriverlo come somma di potenze di 2**.

Questa è l'idea fondamentale:

> Ogni `1` indica che quella potenza di 2 è presente nella somma.  
> Ogni `0` indica che quella potenza di 2 non è presente.

## Esempio: 19

Vogliamo rappresentare:

$$
19_{10}
$$

Consideriamo le potenze di 2:

```text
16   8   4   2   1
```

Cerchiamo quali dobbiamo sommare per ottenere 19:

$$
19=16+2+1
$$

cioè:

$$
19=2^4+2^1+2^0
$$

Le potenze $2^4$, $2^1$ e $2^0$ sono presenti.

Le potenze $2^3$ e $2^2$ non sono presenti.

```text
2⁴   2³   2²   2¹   2⁰
16    8    4    2    1
------------------------
 1    0    0    1    1
```

Quindi:

$$
\boxed{19_{10}=10011_2}
$$

---

# 10. Altro esempio: 13 → binario

Vogliamo rappresentare:

$$
13_{10}
$$

Cerchiamo una somma di potenze di 2:

$$
13=8+4+1
$$

cioè:

$$
13=2^3+2^2+2^0
$$

Costruiamo il numero:

```text
2³   2²   2¹   2⁰
 8    4    2    1
------------------
 1    1    0    1
```

Quindi:

$$
\boxed{13_{10}=1101_2}
$$

---

# 11. Altro esempio: 22 → binario

Scriviamo 22 come somma di potenze di 2:

$$
22=16+4+2
$$

cioè:

$$
22=2^4+2^2+2^1
$$

```text
2⁴   2³   2²   2¹   2⁰
16    8    4    2    1
------------------------
 1    0    1    1    0
```

Quindi:

$$
\boxed{22_{10}=10110_2}
$$

---

# 12. Alcuni numeri da conoscere

| Decimale | Binario |
|---------:|--------:|
| 0 | `0` |
| 1 | `1` |
| 2 | `10` |
| 3 | `11` |
| 4 | `100` |
| 5 | `101` |
| 6 | `110` |
| 7 | `111` |
| 8 | `1000` |
| 9 | `1001` |
| 10 | `1010` |
| 11 | `1011` |
| 12 | `1100` |
| 13 | `1101` |
| 14 | `1110` |
| 15 | `1111` |
| 16 | `10000` |

Osserviamo:

```text
1111₂  = 15
10000₂ = 16
```

Con 4 bit possiamo rappresentare 16 combinazioni:

$$
2^4=16
$$

Se rappresentiamo numeri interi senza segno, queste combinazioni corrispondono ai valori da 0 a 15.

Il valore massimo è quindi:

$$
2^4-1=15
$$

In generale, con **n bit**, il massimo numero intero senza segno rappresentabile è:

$$
\boxed{2^n-1}
$$

---

# 13. MSB e LSB

In un numero binario possiamo distinguere:

- **MSB – Most Significant Bit** → bit più significativo;
- **LSB – Least Significant Bit** → bit meno significativo.

Consideriamo:

```text
1 0 1 1 0 1
↑         ↑
MSB      LSB
```

Il bit più a sinistra ha il **peso maggiore**.

Il bit più a destra ha il **peso minore**:

$$
2^0=1
$$

---

# 14. Numeri pari e dispari

Il bit meno significativo permette immediatamente di capire se un numero binario è pari o dispari.

Se il numero termina con:

```text
0 → numero pari
1 → numero dispari
```

Esempi:

```text
1010₂ = 10 → pari
1100₂ = 12 → pari

1011₂ = 11 → dispari
1101₂ = 13 → dispari
```

Questo accade perché tutte le potenze di 2, tranne $2^0$, sono numeri pari.

---

# 15. Shift dei bit

Lo **shift** consiste nello spostamento dei bit.

## Shift a sinistra

Lo shift a sinistra di una posizione si indica spesso:

```text
<< 1
```

Esempio:

```text
3 = 11₂

11 << 1

110₂ = 6
```

Quindi:

$$
3\cdot2=6
$$

Per numeri interi non negativi, ignorando eventuali limiti del numero di bit:

> Uno shift a sinistra di una posizione equivale a moltiplicare per 2.

Uno shift di due posizioni:

```text
<< 2
```

equivale a moltiplicare per:

$$
2^2=4
$$

---

# 16. Shift a destra

Consideriamo:

```text
12 = 1100₂
```

Spostiamo tutti i bit di una posizione verso destra:

```text
1100 >> 1 = 110
```

e:

$$
110_2=6
$$

Quindi:

$$
12/2=6
$$

Per numeri interi positivi, uno shift a destra di una posizione corrisponde a una **divisione intera per 2**.

---

# 17. Tabella riassuntiva degli shift

| Decimale | Binario | `<< 1` | Valore | `>> 1` | Valore |
|---------:|--------:|-------:|-------:|-------:|-------:|
| 5 | `101` | `1010` | 10 | `10` | 2 |
| 12 | `1100` | `11000` | 24 | `110` | 6 |
| 7 | `111` | `1110` | 14 | `11` | 3 |
| 20 | `10100` | `101000` | 40 | `1010` | 10 |

---

# 18. Esercizi – Binario → Decimale

Converti i seguenti numeri binari in decimale:

1. `10₂`
2. `101₂`
3. `111₂`
4. `1000₂`
5. `1010₂`
6. `1101₂`
7. `1111₂`
8. `10000₂`
9. `10101₂`
10. `11010₂`

---

# 19. Esercizi – Decimale → Binario

Scrivi ogni numero come **somma di potenze di 2** e poi ricava la rappresentazione binaria.

1. $3_{10}$
2. $6_{10}$
3. $9_{10}$
4. $14_{10}$
5. $17_{10}$
6. $21_{10}$
7. $25_{10}$
8. $31_{10}$

### Esempio di svolgimento

Per 21:

$$
21=16+4+1
$$

$$
21=2^4+2^2+2^0
$$

quindi:

```text
16   8   4   2   1
 1   0   1   0   1
```

e quindi:

$$
21_{10}=10101_2
$$

---

# 20. Esercizi – Completa la tabella

| Decimale | Binario |
|---------:|:-------:|
| 5 | ? |
| ? | `1001` |
| 12 | ? |
| ? | `1111` |
| 18 | ? |
| ? | `10101` |
| 32 | ? |

---

# 21. Esercizi di ragionamento

## Esercizio 1

Qual è il massimo numero intero senza segno rappresentabile con:

- 3 bit?
- 4 bit?
- 5 bit?
- 8 bit?

Ricorda:

$$
\text{massimo}=2^n-1
$$

## Esercizio 2

Quante combinazioni differenti possiamo rappresentare con:

- 2 bit?
- 4 bit?
- 8 bit?
- 10 bit?

Ricorda:

$$
\text{combinazioni}=2^n
$$

## Esercizio 3

Senza convertire completamente in decimale, stabilisci quali numeri sono pari e quali dispari:

```text
10101
11010
11111
10000
10110
```

## Esercizio 4

Completa mentalmente:

```text
101₂ << 1 = ?
101₂ << 2 = ?

1100₂ >> 1 = ?
1100₂ >> 2 = ?
```

---

# 22. Domande di verifica

1. Che cos'è un sistema di numerazione?
2. Che cosa significa sistema posizionale?
3. Che cosa significa dire che il sistema binario è in base 2?
4. Che cosa significa **bit**?
5. Quali valori può assumere un bit?
6. Che cos'è un byte?
7. Quanti bit contiene un byte?
8. Quante combinazioni possiamo rappresentare con 8 bit?
9. Qual è il massimo intero senza segno rappresentabile con 8 bit?
10. Che cosa significa MSB?
11. Che cosa significa LSB?
12. Come possiamo riconoscere immediatamente un numero binario pari?
13. Come si converte un numero binario in decimale?
14. Come possiamo convertire un numero decimale in binario utilizzando le potenze di 2?
15. Che effetto ha uno shift a sinistra?
16. Che effetto ha uno shift a destra?

---

# 23. Soluzioni degli esercizi

## Binario → Decimale

| Binario | Decimale |
|--------:|---------:|
| `10` | 2 |
| `101` | 5 |
| `111` | 7 |
| `1000` | 8 |
| `1010` | 10 |
| `1101` | 13 |
| `1111` | 15 |
| `10000` | 16 |
| `10101` | 21 |
| `11010` | 26 |

## Decimale → Binario

| Decimale | Somma di potenze di 2 | Binario |
|---------:|-----------------------|--------:|
| 3 | $2+1$ | `11` |
| 6 | $4+2$ | `110` |
| 9 | $8+1$ | `1001` |
| 14 | $8+4+2$ | `1110` |
| 17 | $16+1$ | `10001` |
| 21 | $16+4+1$ | `10101` |
| 25 | $16+8+1$ | `11001` |
| 31 | $16+8+4+2+1$ | `11111` |

---

# 24. Glossario – Definizioni da ricordare

Queste sono le principali definizioni da conoscere e ricordare.

## Base

La **base** di un sistema di numerazione indica il numero di cifre differenti utilizzate dal sistema.

Il sistema decimale ha base 10 e utilizza dieci cifre (`0`–`9`).

Il sistema binario ha base 2 e utilizza due cifre (`0` e `1`).

---

## Bit

Il **bit** (*binary digit*, "cifra binaria") è l'unità fondamentale dell'informazione digitale.

Un bit può assumere solamente due valori:

```text
0 oppure 1
```

---

## Byte

Il **byte** è un gruppo formato da **8 bit**.

```text
1 byte = 8 bit
```

Un byte può assumere:

$$
2^8=256
$$

configurazioni differenti.

---

## Cifra

Una **cifra** è un simbolo utilizzato per rappresentare un numero all'interno di un sistema di numerazione.

Nel sistema decimale le cifre sono:

```text
0 1 2 3 4 5 6 7 8 9
```

Nel sistema binario sono:

```text
0 1
```

---

## LSB – Least Significant Bit

Il **LSB** (*Least Significant Bit*) è il bit meno significativo di un numero binario.

È il bit più a destra e, per un numero intero, ha peso:

$$
2^0=1
$$

---

## MSB – Most Significant Bit

Il **MSB** (*Most Significant Bit*) è il bit più significativo di un numero binario.

È il bit più a sinistra e rappresenta la posizione con il peso maggiore.

---

## Peso

Il **peso** di una cifra è il valore associato alla posizione che essa occupa in un sistema posizionale.

Nel sistema binario i pesi sono potenze di 2:

$$
2^0,\ 2^1,\ 2^2,\ 2^3,\ldots
$$

cioè:

```text
1, 2, 4, 8, 16, 32, 64, ...
```

---

## Sistema binario

Il **sistema binario** è un sistema di numerazione posizionale in **base 2** che utilizza solamente le cifre `0` e `1`.

Ogni posizione ha un peso corrispondente a una potenza di 2.

---

## Sistema decimale

Il **sistema decimale** è un sistema di numerazione posizionale in **base 10** che utilizza le dieci cifre da `0` a `9`.

Ogni posizione ha un peso corrispondente a una potenza di 10.

---

## Sistema di numerazione

Un **sistema di numerazione** è un insieme di simboli e regole utilizzato per rappresentare i numeri.

---

## Sistema posizionale

Un **sistema di numerazione posizionale** è un sistema nel quale il valore di una cifra dipende sia dalla cifra stessa sia dalla posizione che essa occupa nel numero.

---

## Shift

Lo **shift** è un'operazione che sposta i bit di un numero verso sinistra o verso destra.

Per numeri interi non negativi:

- uno shift a sinistra di una posizione corrisponde a una moltiplicazione per 2;
- uno shift a destra di una posizione corrisponde a una divisione intera per 2.

---

# 25. Formule da ricordare

### Numero di combinazioni rappresentabili con n bit

$$
\boxed{2^n}
$$

### Massimo intero senza segno rappresentabile con n bit

$$
\boxed{2^n-1}
$$

### Valore di un numero binario

Se un numero binario è:

$$
b_n b_{n-1}\ldots b_2b_1b_0
$$

il suo valore è:

$$
\boxed{
b_n2^n+b_{n-1}2^{n-1}+\cdots+b_22^2+b_12^1+b_02^0
}
$$

dove ogni bit $b_i$ può assumere solamente il valore:

$$
0 \quad \text{oppure} \quad 1
$$
