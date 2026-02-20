
# L’operatore `CMP` nell’Assembly 8086

L’istruzione **`CMP`** (compare = confronta) serve per confrontare due valori.

⚠️ Importante:
`CMP` **non modifica i valori**, ma aggiorna solo i **flag** del processore, che poi vengono usati per fare salti condizionali (`JE`, `JG`, `JL`, ecc.).

---

## 🔹 Come funziona

L’istruzione:

```
CMP A, B
```

fa internamente questa operazione:

```
A - B
```

👉 Ma **senza salvare il risultato**.

Serve solo per capire:

* se A = B
* se A > B
* se A < B

Il risultato viene indicato attraverso i **flag**.

---

## 🔹 Flag modificati

Dopo un `CMP`, il processore aggiorna:

| Flag               | Significato                         |
| ------------------ | ----------------------------------- |
| ZF (Zero Flag)     | = 1 → i valori sono uguali          |
| CF (Carry Flag)    | = 1 → A < B (numeri senza segno)    |
| SF (Sign Flag)     | indica se il risultato è negativo   |
| OF (Overflow Flag) | segnala errori nei numeri con segno |

---

## 🔹 Esempio

```
MOV AX, 5
CMP AX, 3
```

Il processore calcola:

```
5 - 3 = 2
```

Non salva 2, ma imposta i flag:

* ZF = 0 → non sono uguali
* CF = 0 → AX non è minore
  → quindi AX > 3

---

## 🔹 Uso con i salti

Dopo `CMP`, si usano i salti condizionali.

### Uguali

```
CMP AX, BX
JE uguali
```

Salta se AX = BX

---

### Maggiore

```
CMP AX, BX
JG maggiore
```

Salta se AX > BX (numeri con segno)

---

### Minore

```
CMP AX, BX
JL minore
```

Salta se AX < BX (numeri con segno)

---

## 🔹 Riassunto semplice

👉 `CMP` confronta due valori
👉 non cambia i registri
👉 aggiorna i flag
👉 permette di prendere decisioni con i salti


