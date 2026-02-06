# 📂 Raccolta esercizi avanzati – IP, Subnet e CIDR

### 🔌 Con collegamento esplicito alla logica AND bit a bit

---

## 🧮 Esercizio 5 – Network e broadcast con CIDR

*(metodo dei blocchi = AND “mascherato”)*

### 🧾 Traccia

* IP: **192.168.10.77/26**

Calcolare:

1. Network address
2. Broadcast address
3. Numero di host utilizzabili

---

## 🧠 Idea chiave (prima di iniziare)

📌 **Ogni network address nasce da:**

```
IP AND Subnet Mask
```

Il **metodo dei blocchi** è solo un modo **più veloce** per ottenere **lo stesso risultato dell’AND bit a bit**, quando la maschera “cade” su un ottetto.

---

### 🔹 1. Prefisso → subnet mask

```
/26 → 255.255.255.192
```

Ultimo ottetto:

```
192 = 11000000
```

👉 significa:

* **2 bit di rete**
* **6 bit di host**

---

### 🔹 2. Numero di host (bit host)

```
6 bit → 2⁶ = 64 indirizzi
64 − 2 = 62 host utilizzabili
```

---

### 🔹 3. Metodo dei blocchi (equivalente all’AND)

Calcolo ampiezza blocco:

```
256 − 192 = 64
```

Sottoreti nell’ultimo ottetto:

```
0 | 64 | 128 | 192
```

---

### 🔹 4. Individuazione subnet

```
77 ∈ [64 – 127]
```

---

### 🔹 5. Risultati

✅ Network address: **192.168.10.64**
📣 Broadcast address: **192.168.10.127**
💻 Host utilizzabili: **62**

🧠 *Nota didattica*:
se facessimo l’**AND bit a bit**, otterremmo **lo stesso 64**.

---

## 🧠 Esercizio 6 – Verifica stessa rete

*(AND logico concettuale)*

### 🧾 Traccia

* A: **10.0.5.14/20**
* B: **10.0.12.3/20**

---

### 🔹 1. Subnet mask

```
/20 → 255.255.240.0
240 = 11110000
```

---

### 🔹 2. Concetto chiave (importantissimo)

👉 Due host sono **nella stessa rete** se:

```
(IP A AND MASK) = (IP B AND MASK)
```

---

### 🔹 3. Metodo dei blocchi (AND semplificato)

Terzo ottetto:

```
256 − 240 = 16
```

Blocchi:

```
0–15 | 16–31 | ...
```

* Host A → 5 ∈ 0–15
* Host B → 12 ∈ 0–15

---

### 🔹 4. Network address comune

```
10.0.0.0/20
```

✅ **Stessa rete**

🧠 *L’AND “nasconde” i bit host e lascia solo quelli di rete.*

---

## 🔢 Esercizio 7 – Subnetting

*(uso esplicito dei bit)*

### 🧾 Traccia

Rete iniziale: **192.168.1.0/24**
Nuovo prefisso: **/27**

---

### 🔹 1. Bit presi agli host

```
27 − 24 = 3 bit
```

👉 3 bit diventano **bit di subnet**

---

### 🔹 2. Numero di subnet

```
2³ = 8 subnet
```

---

### 🔹 3. Bit host rimasti

```
32 − 27 = 5 bit
```

Host per subnet:

```
2⁵ − 2 = 30
```

✅ **8 subnet da 30 host**

🧠 *Subnetting = spostare il confine dell’AND più a destra.*

---

## 🌐 Esercizio 8 – AND logico bit a bit (esplicito)

### 🧾 Traccia

* IP: **172.20.35.200**
* Mask: **255.255.255.192**

---

### 🔹 1. Binario

**IP**

```
200 = 11001000
```

**Mask**

```
192 = 11000000
```

---

### 🔹 2. AND bit a bit (CUORE DELLA RETE)

```
11001000
AND 11000000
-----------
11000000
```

---

### 🔹 3. Riconversione

```
11000000 = 192
```

✅ Network address: **172.20.35.192**

---

### 🔹 4. Broadcast

Bit host = 6 → tutti a 1:

```
00111111 = 63
192 + 63 = 255
```

📣 Broadcast: **172.20.35.255**

🧠 *Il broadcast è la “negazione” della mask sulla parte host.*

---

## 🧩 Esercizio 9 – Aggregazione CIDR

*(operazione inversa dell’AND)*

### 🧾 Traccia

```
192.168.4.0/24
192.168.5.0/24
192.168.6.0/24
192.168.7.0/24
```

---

### 🔹 1. Numero reti

```
4 = 2²
```

---

### 🔹 2. Nuovo prefisso

```
/24 − 2 = /22
```

---

### 🔹 3. Significato logico

👉 Stiamo **ignorando 2 bit** di rete
👉 come se la mask facesse AND su meno bit

---

### 🔹 4. Risultato

✅ **192.168.4.0/22**

---

## 🚦 Esercizio 10 – Routing

*(AND + confronto prefissi)*

### 🧾 Traccia

Rotte:

```
10.0.0.0/8
10.1.0.0/16
10.1.5.0/24
```

Destinazione: **10.1.5.77**

---

### 🔹 Regola chiave

👉 **Longest Prefix Match**

---

### 🔹 Concetto logico

Ogni rotta fa:

```
DESTINATION AND MASK
```

👉 vince quella con **più bit di rete**

---

### 🔹 Verifica

| Rotta | Bit rete |
| ----- | -------- |
| /8    | 8        |
| /16   | 16       |
| /24   | 24 ✅     |

---

### ✅ Risultato finale

```
10.1.5.0/24
```

🧠 *Più bit = AND più preciso = rotta più specifica.*

---

## 🧠 IDEA FINALE DA FAR PASSARE AGLI STUDENTI

> 🔑 **Tutto il networking IPv4 si basa su una sola operazione logica:**
>
> ## 👉 AND bit a bit

* Network address → **IP AND mask**
* Stessa rete → **AND uguale**
* Subnetting → **sposto l’AND**
* Routing → **AND + confronto prefissi**

