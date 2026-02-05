# 📂 Raccolta esercizi avanzati – IP, Subnet e CIDR

---

## 🧮 Esercizio 5 – Network e broadcast con CIDR

### 🧾 Traccia

Dato l’indirizzo:

* IP: **192.168.10.77/26**

Calcolare:

1. Network address
2. Broadcast address
3. Numero di host utilizzabili

---

### 🧩 Soluzione passo-passo

#### 🔹 1. Interpretazione del prefisso

```
/26 → 26 bit di rete
32 − 26 = 6 bit di host
```

#### 🔹 2. Calcolo degli host

```
2⁶ = 64 indirizzi totali
64 − 2 = 62 host utilizzabili
```

#### 🔹 3. Dimensione del blocco

Subnet mask /26 → ultimo ottetto:

```
256 − 192 = 64
```

➡️ Le sottoreti avanzano di **64**:

```
0, 64, 128, 192
```

#### 🔹 4. Individuazione della subnet

L’IP **192.168.10.77** cade nel range:

```
64 – 127
```

#### 🔹 5. Risultati

✅ Network address: **192.168.10.64**
📣 Broadcast address: **192.168.10.127**
💻 Host utilizzabili: **62**

---

## 🧠 Esercizio 6 – Verifica stessa rete con CIDR

### 🧾 Traccia

Due host:

* A: **10.0.5.14/20**
* B: **10.0.12.3/20**

Stabilisci se appartengono alla **stessa rete**.

---

### 🧩 Soluzione passo-passo

#### 🔹 1. Subnet mask da /20

```
/20 → 255.255.240.0
```

Ultimo ottetto rilevante: **240** → blocchi da:

```
256 − 240 = 16
```

#### 🔹 2. Individuazione subnet

Terzo ottetto:

* Host A: **5** → subnet **0–15**
* Host B: **12** → subnet **0–15**

#### 🔹 3. Network address

Entrambi:

```
10.0.0.0/20
```

✅ **Stessa rete**

---

## 🔢 Esercizio 7 – Subnetting: quante sottoreti?

### 🧾 Traccia

Una rete **192.168.1.0/24** viene suddivisa in subnet **/27**.

Calcolare:

1. Numero di subnet
2. Host per subnet

---

### 🧩 Soluzione passo-passo

#### 🔹 1. Bit presi agli host

```
/27 − /24 = 3 bit
```

#### 🔹 2. Numero di subnet

```
2³ = 8 subnet
```

#### 🔹 3. Host per subnet

```
32 − 27 = 5 bit host
2⁵ = 32
32 − 2 = 30 host
```

✅ **8 subnet da 30 host ciascuna**

---

## 🌐 Esercizio 8 – Calcolo subnet con AND logico

### 🧾 Traccia

Dato:

* IP: **172.20.35.200**
* Subnet mask: **255.255.255.192**

Calcolare:

1. Network address
2. Broadcast address

---

### 🧩 Soluzione passo-passo (AND bit a bit)

---

### 🔹 1. Conversione in binario

**Indirizzo IP**

```
172 = 10101100
20  = 00010100
35  = 00100011
200 = 11001000
```

**Subnet mask**

```
255 = 11111111
255 = 11111111
255 = 11111111
192 = 11000000
```

---

### 🔹 2. AND logico bit a bit (IP AND subnet mask)

```
10101100 AND 11111111 = 10101100
00010100 AND 11111111 = 00010100
00100011 AND 11111111 = 00100011
11001000 AND 11000000 = 11000000
```

---

### 🔹 3. Riconversione in decimale

```
10101100 = 172
00010100 = 20
00100011 = 35
11000000 = 192
```

✅ **Network address: 172.20.35.192**

---

### 🔹 4. Calcolo del Broadcast address

Il broadcast si ottiene ponendo **tutti i bit host a 1**.

Subnet mask: **/26**
Bit host: **6**

Parte host (ultimo ottetto):

```
00111111 = 63
```

Sommiamo alla parte di rete:

```
192 + 63 = 255
```

📣 **Broadcast address: 172.20.35.255**


---

## 🧩 Esercizio 9 – Aggregazione CIDR (supernetting)

### 🧾 Traccia

Le seguenti reti:

```
192.168.4.0/24
192.168.5.0/24
192.168.6.0/24
192.168.7.0/24
```

Possono essere aggregate?
Se sì, trovare il **prefisso CIDR risultante**.

---

### 🧩 Soluzione passo-passo

#### 🔹 1. Numero di reti

```
4 reti → 2²
```

➡️ Possibile aggregazione

#### 🔹 2. Calcolo nuovo prefisso

```
/24 − 2 = /22
```

#### 🔹 3. Verifica contiguità

Le reti sono consecutive ✔

#### 🔹 4. Risultato

✅ Supernet:

```
192.168.4.0/22
```

---

## 🚦 Esercizio 10 – Routing decisionale

### 🧾 Traccia

Un router ha la seguente tabella:

```
10.0.0.0/8
10.1.0.0/16
10.1.5.0/24
```

Destinazione pacchetto: **10.1.5.77**

Quale rotta viene scelta?

---

### 🧩 Soluzione passo-passo

#### 🔹 Regola fondamentale

👉 **Longest Prefix Match**

#### 🔹 Verifica corrispondenze

| Rete        | Match |
| ----------- | ----- |
| 10.0.0.0/8  | ✔     |
| 10.1.0.0/16 | ✔     |
| 10.1.5.0/24 | ✔     |

#### 🔹 Prefisso più lungo

```
/24 → più specifico
```

✅ Rotta scelta:

```
10.1.5.0/24
```

