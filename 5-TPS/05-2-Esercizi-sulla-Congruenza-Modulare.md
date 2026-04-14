# 🧠 Esercizi sulla Congruenza Modulare (difficoltà crescente)

---

## 🟢 Esercizio 1 — Il resto nascosto

### 📌 Traccia
Calcola il resto delle seguenti divisioni:

1. $17 \bmod 6$
2. $29 \bmod 5$
3. $42 \bmod 8$

---

### ✅ Soluzione

1. $17 = 6 \cdot 2 + 5 \Rightarrow 17 \bmod 6 = 5$
2. $29 = 5 \cdot 5 + 4 \Rightarrow 29 \bmod 5 = 4$
3. $42 = 8 \cdot 5 + 2 \Rightarrow 42 \bmod 8 = 2$

---

## 🟢 Esercizio 2 — Sono congrui?

### 📌 Traccia
Verifica se le seguenti affermazioni sono vere:

1. $17 \equiv 5 \pmod{6}$
2. $23 \equiv 3 \pmod{10}$
3. $14 \equiv 2 \pmod{4}$

---

### ✅ Soluzione

Usiamo la definizione:  
$a \equiv b \pmod{n} \iff n \mid (a - b)$

1. $17 - 5 = 12$, $6 \mid 12$ → ✔ vero  
2. $23 - 3 = 20$, $10 \mid 20$ → ✔ vero  
3. $14 - 2 = 12$, $4 \mid 12$ → ✔ vero  

---

## 🟡 Esercizio 3 — Operazioni modulo

### 📌 Traccia
Calcola:

1. $8 + 9 \pmod{7}$
2. $6 \cdot 5 \pmod{11}$
3. $15 + 17 \pmod{10}$

---

### ✅ Soluzione

1. $8 + 9 = 17 \equiv 3 \pmod{7}$
2. $6 \cdot 5 = 30 \equiv 8 \pmod{11}$
3. $15 + 17 = 32 \equiv 2 \pmod{10}$

---

## 🟡 Esercizio 4 — Classi di equivalenza

### 📌 Traccia
Trova tutti i numeri tra 0 e 30 che sono congrui a 4 modulo 7.

---

### ✅ Soluzione

Cerchiamo numeri della forma:

$$
x \equiv 4 \pmod{7} \Rightarrow x = 4 + 7k
$$

Calcoliamo:

- $4$
- $11$
- $18$
- $25$

---

## 🟠 Esercizio 5 — Coprimi o no?

### 📌 Traccia
Determina se le seguenti coppie sono coprime:

1. $(9, 28)$  
2. $(12, 18)$  
3. $(35, 64)$  

---

### ✅ Soluzione

Calcoliamo il $\gcd$:

1. $\gcd(9,28)=1$ → ✔ coprimi  
2. $\gcd(12,18)=6$ → ✘ non coprimi  
3. $\gcd(35,64)=1$ → ✔ coprimi  

---

## 🟠 Esercizio 6 — Inverso moltiplicativo

### 📌 Traccia
Trova l’inverso di:

1. $3 \pmod{10}$  
2. $7 \pmod{26}$  

---

### ✅ Soluzione

Cerchiamo $x$ tale che:

$$
a \cdot x \equiv 1 \pmod{n}
$$

1. $3 \cdot 7 = 21 \equiv 1 \pmod{10}$ → inverso: **7**  
2. $7 \cdot 15 = 105 \equiv 1 \pmod{26}$ → inverso: **15**

---

## 🔴 Esercizio 7 — Equazione modulare

### 📌 Traccia
Risolvi:

$$
3x \equiv 1 \pmod{7}
$$

---

### ✅ Soluzione

Serve l’inverso di 3 modulo 7:

$$
3 \cdot 5 = 15 \equiv 1 \pmod{7}
$$

Quindi:

$$
x \equiv 5 \pmod{7}
$$

---

## 🔴 Esercizio 8 — Riduzione intelligente

### 📌 Traccia
Calcola:

$$
(1234 \cdot 5678) \bmod 9
$$

---

### ✅ Soluzione

Riduciamo prima:

- $1234 \equiv 1+2+3+4 = 10 \equiv 1 \pmod{9}$
- $5678 \equiv 5+6+7+8 = 26 \equiv 8 \pmod{9}$

Quindi:

$$
1 \cdot 8 = 8 \pmod{9}
$$

---

## 🔴 Esercizio 9 — Pensiero crittografico

### 📌 Traccia
Spiega perché l’equazione:

$$
ax \equiv b \pmod{n}
$$

ha soluzione **solo se** $\gcd(a,n)=1$

---

### ✅ Soluzione

Se $\gcd(a,n)=1$, allora esiste l’inverso $a^{-1}$.

Quindi possiamo scrivere:

$$
x \equiv a^{-1} \cdot b \pmod{n}
$$

Se invece $\gcd(a,n) \neq 1$, l’inverso non esiste → l’equazione può non avere soluzione.

---

## 🧠 Esercizio 10 — Mini crittografia

### 📌 Traccia
Considera il cifrario:

$$
E(x) = 5x \pmod{26}
$$

Calcola il cifrato di:

- $x = 3$
- $x = 10$

---

### ✅ Soluzione

1. $5 \cdot 3 = 15 \pmod{26}$
2. $5 \cdot 10 = 50 \equiv 24 \pmod{26}$

---

# 🚀 Conclusione

Questa progressione ti porta da:

👉 resto semplice  
👉 congruenza  
👉 operazioni  
👉 inversi  
👉 equazioni modulari  
👉 fino alla crittografia
