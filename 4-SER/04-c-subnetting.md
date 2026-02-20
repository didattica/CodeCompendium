
# 🧠 ESERCIZIO 1

## Dato:

```
172.16.10.0/24
```

## Richiesta:

Dividere in **4 sottoreti** e indicare:

* Indirizzo di rete
* Broadcast
* Range host

---

## 🔹 1️⃣ Calcolo bit da prendere

Serve n tale che:

```
2^n ≥ 4
```

```
2^2 = 4
```

👉 n = 2 bit

---

## 🔹 2️⃣ Nuovo CIDR

```
/24 + 2 = /26
```

Subnet mask:

```
255.255.255.192
```

---

## 🔹 3️⃣ Calcolo incremento

```
256 - 192 = 64
```

👉 Le sottoreti partono ogni 64.

---

## 🔹 4️⃣ Sottoreti

| Subnet | Network          | Broadcast     | Host        |
| ------ | ---------------- | ------------- | ----------- |
| 1      | 172.16.10.0/26   | 172.16.10.63  | .1 – .62    |
| 2      | 172.16.10.64/26  | 172.16.10.127 | .65 – .126  |
| 3      | 172.16.10.128/26 | 172.16.10.191 | .129 – .190 |
| 4      | 172.16.10.192/26 | 172.16.10.255 | .193 – .254 |

---

# 🧠 ESERCIZIO 2

## Dato:

```
192.168.50.0/25
```

Questa rete ha:

* 7 bit host (perché 32 − 25 = 7)

## Richiesta:

Dividere in **4 sottoreti**

---

## 🔹 1️⃣ Calcolo bit

```
2^2 = 4
```

n = 2

---

## 🔹 2️⃣ Nuovo CIDR

```
/25 + 2 = /27
```

Subnet mask:

```
255.255.255.224
```

---

## 🔹 3️⃣ Incremento

```
256 - 224 = 32
```

---

## 🔹 4️⃣ Attenzione ⚠

La rete iniziale è:

```
192.168.50.0 – 192.168.50.127
```

Perché /25 divide già in due metà.

Quindi lavoriamo **solo nel primo blocco da 128 indirizzi**.

---

## 🔹 5️⃣ Sottoreti ottenute

| Subnet | Network          | Broadcast      | Host       |
| ------ | ---------------- | -------------- | ---------- |
| 1      | 192.168.50.0/27  | 192.168.50.31  | .1 – .30   |
| 2      | 192.168.50.32/27 | 192.168.50.63  | .33 – .62  |
| 3      | 192.168.50.64/27 | 192.168.50.95  | .65 – .94  |
| 4      | 192.168.50.96/27 | 192.168.50.127 | .97 – .126 |

---

# 🧠 ESERCIZIO 3 (livello esame)

## Dato:

```
10.0.0.0/23
```

## Richiesta:

Dividere in 4 sottoreti.

---

## 🔹 1️⃣ Analisi iniziale

/23 significa:

```
32 - 23 = 9 bit host
```

Totale indirizzi:

```
2^9 = 512
```

Range totale:

```
10.0.0.0 – 10.0.1.255
```

---

## 🔹 2️⃣ Bit necessari

```
2^2 = 4
```

n = 2

---

## 🔹 3️⃣ Nuovo CIDR

```
/23 + 2 = /25
```

---

## 🔹 4️⃣ Incremento

/25 → mask 255.255.255.128

```
256 - 128 = 128
```

---

## 🔹 5️⃣ Sottoreti

| Subnet | Network       | Broadcast  |
| ------ | ------------- | ---------- |
| 1      | 10.0.0.0/25   | 10.0.0.127 |
| 2      | 10.0.0.128/25 | 10.0.0.255 |
| 3      | 10.0.1.0/25   | 10.0.1.127 |
| 4      | 10.0.1.128/25 | 10.0.1.255 |

Ogni subnet ha:

```
128 indirizzi
126 host utilizzabili
```
