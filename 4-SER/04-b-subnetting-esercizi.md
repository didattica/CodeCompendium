# Subnetting Avanzato – Esercizi (Livello Crescente)

Formato:
- 📌 Traccia
- ❓ Domande
- ✅ Risoluzione completa (approccio matematico + binario)

Gli esercizi sono organizzati a coppie simili.

---

# 🟢 LIVELLO 1 – Base (Divisione diretta)

---

## 🔹 Esercizio 1

### 📌 Traccia

Rete: 192.168.10.0/24  
Dividere in 2 sottoreti.

### ❓ Domande

1. Nuovo CIDR?
2. Subnet mask?
3. Numero host per subnet?
4. Elenco delle sottoreti (network + broadcast)?

---

### ✅ Risoluzione

Servono almeno 2 subnet:

```

2^n ≥ 2
2^1 = 2

```

👉 n = 1

Nuovo CIDR:

```

/24 + 1 = /25

```

Mask:

```

255.255.255.128

```

Host rimasti:

```

8 - 1 = 7 bit

```

Indirizzi per subnet:

```

2^7 = 128
Host = 128 - 2 = 126

```

Incremento:

```

256 - 128 = 128

```

Subnet:

| Subnet | Network | Broadcast |
|--------|----------|------------|
| 1 | 192.168.10.0 | 192.168.10.127 |
| 2 | 192.168.10.128 | 192.168.10.255 |

---

## 🔹 Esercizio 2

### 📌 Traccia

Rete: 10.0.0.0/24  
Dividere in 2 sottoreti.

### ❓ Domande

Stesse dell’esercizio 1.

---

### ✅ Risoluzione

Identica struttura matematica:

n = 1  
Nuovo CIDR = /25  
Host per subnet = 126  
Incremento = 128  

Subnet:

- 10.0.0.0 – 10.0.0.127  
- 10.0.0.128 – 10.0.0.255  

---

# 🟡 LIVELLO 2 – 4 sottoreti

---

## 🔹 Esercizio 3

### 📌 Traccia

Rete: 192.168.1.0/24  
Dividere in 4 sottoreti.

---

### ✅ Risoluzione

```

2^n ≥ 4
2^2 = 4

```

n = 2

Nuovo CIDR:

```

/26

```

Host bit:

```

8 - 2 = 6

```

Indirizzi:

```

2^6 = 64
Host = 62

```

Incremento:

```

256 - 192 = 64

```

Subnet:

0, 64, 128, 192

---

## 🔹 Esercizio 4

### 📌 Traccia

Rete: 172.16.5.0/24  
Dividere in 4 sottoreti.

---

### ✅ Risoluzione

Stessa matematica:

Nuovo CIDR:

```

/26

```

Incremento = 64

Subnet:

- 172.16.5.0
- 172.16.5.64
- 172.16.5.128
- 172.16.5.192

---

# 🟠 LIVELLO 3 – 8 sottoreti

---

## 🔹 Esercizio 5

### 📌 Traccia

Rete: 192.168.50.0/24  
Dividere in 8 sottoreti.

---

### ✅ Risoluzione

```

2^n ≥ 8
2^3 = 8

```

n = 3

Nuovo CIDR:

```

/27

```

Host bit:

```

8 - 3 = 5

```

Indirizzi per subnet:

```

2^5 = 32
Host = 30

```

Incremento:

```

256 - 224 = 32

```

Subnet ogni 32.

---

## 🔹 Esercizio 6

### 📌 Traccia

Rete: 10.1.20.0/24  
Dividere in 8 sottoreti.

---

### ✅ Risoluzione

Identica struttura:

CIDR = /27  
Incremento = 32  
Host per subnet = 30  

Subnet:

0, 32, 64, 96, 128, 160, 192, 224

---

# 🔴 LIVELLO 4 – Richiesta numero minimo host

---

## 🔹 Esercizio 7

### 📌 Traccia

Rete: 192.168.1.0/24  
Creare sottoreti che supportino almeno 50 host ciascuna.

---

### ❓ Domanda

Quale CIDR scegliere?

---

### ✅ Risoluzione

Cerchiamo bit host tali che:

```

2^h - 2 ≥ 50

```

Proviamo:

```

2^5 - 2 = 30 → insufficiente
2^6 - 2 = 62 → sufficiente

```

👉 h = 6

Nuovo CIDR:

```

32 - 6 = /26

```

Incremento:

```

64

```

Numero subnet:

```

2^(8-6) = 4

```

---

## 🔹 Esercizio 8

### 📌 Traccia

Rete: 172.16.0.0/24  
Servono sottoreti da almeno 100 host.

---

### ✅ Risoluzione

```

2^h - 2 ≥ 100

```

Proviamo:

```

2^6 - 2 = 62 → insufficiente
2^7 - 2 = 126 → sufficiente

```

👉 h = 7

CIDR:

```

32 - 7 = /25

```

Incremento:

```

128

```

Numero subnet:

```

2^(8-7) = 2

```

---

# 🔵 LIVELLO 5 – Multi-ottetto (più complesso)

---

## 🔹 Esercizio 9

### 📌 Traccia

Rete: 10.0.0.0/16  
Dividere in 16 sottoreti.

---

### ✅ Risoluzione

```

2^n ≥ 16
2^4 = 16

```

n = 4

Nuovo CIDR:

```

/16 + 4 = /20

```

Host bit:

```

16 - 4 = 12

```

Indirizzi per subnet:

```

2^12 = 4096
Host = 4094

```

Mask:

```

255.255.240.0

```

Incremento terzo ottetto:

```

256 - 240 = 16

```

Subnet:

10.0.0.0  
10.0.16.0  
10.0.32.0  
...  
10.0.240.0  

---

## 🔹 Esercizio 10

### 📌 Traccia

Rete: 172.16.0.0/16  
Servono almeno 1000 host per sottorete.

---

### ✅ Risoluzione

Cerchiamo h:

```

2^h - 2 ≥ 1000

```

Proviamo:

```

2^9 - 2 = 510 → insufficiente
2^10 - 2 = 1022 → sufficiente

```

👉 h = 10

CIDR:

```

32 - 10 = /22

```

Nuovo CIDR totale:

```

/16 → /22

```

Bit presi:

```

22 - 16 = 6

```

Numero subnet:

```

2^6 = 64

```

Mask:

```

255.255.252.0

```

Incremento:

```

256 - 252 = 4

```

Subnet ogni 4 nel terzo ottetto:

172.16.0.0  
172.16.4.0  
172.16.8.0  
...

---

# 📌 Conclusione

Subnetting avanzato =

- Potenze di 2
- Calcolo esponenziale
- Analisi binaria
- Partizionamento matematico dello spazio IP

Struttura mentale:

```

Richiesta → calcolo potenze → scelta bit → nuovo CIDR → incremento → elenco subnet
```


<!--
Se vuoi, prossimo step:

👉 Solo esercizi “da esame universitario” molto complessi  

oppure  
👉 VLSM completo con progettazione di rete reale
-->
