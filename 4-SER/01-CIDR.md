---

# 🌐 Indirizzi IP, Subnet Mask e CIDR

### 📘 Guida ragionata con enfasi su **bit di rete** e **bit di host**

Documento di studio per studenti
(Modello **classful storico** → limiti → **CIDR**)

---

## 🧠 IDEA FONDAMENTALE (DA CAPIRE SUBITO)

Un indirizzo IPv4 è lungo **32 bit** ed è sempre diviso in due parti:

```
[ BIT DI RETE | BIT DI HOST ]
```

👉 **La subnet mask serve esattamente a dire dove sta il confine.**

TUTTI gli esercizi di:

* network address
* broadcast
* stessa rete
* routing
* subnetting

dipendono da una sola cosa:

> 📌 **sapere quali bit identificano la rete e quali l’host**

---

## 🧱 Classi di indirizzi IP (modello storico – classful)

Nel modello **classful**, il confine tra:

* bit di rete 🌐
* bit di host 💻

era **fisso** e deciso dalla **classe** dell’indirizzo.

---

### 🔴 Classe A

* Primo ottetto: **1 – 126**
* Subnet mask: **255.0.0.0 → /8**

```
[ 8 bit rete | 24 bit host ]
```

📌 Pochissime reti, **tantissimi host**

---

### 🟠 Classe B

* Primo ottetto: **128 – 191**
* Subnet mask: **255.255.0.0 → /16**

```
[ 16 bit rete | 16 bit host ]
```

📌 Compromesso tra reti e host

---

### 🟢 Classe C

* Primo ottetto: **192 – 223**
* Subnet mask: **255.255.255.0 → /24**

```
[ 24 bit rete | 8 bit host ]
```

📌 Molte reti, **pochi host**

---

## ⚠️ Limiti del modello classful

❌ Confine rete/host **rigido**
❌ Spreco di indirizzi IP
❌ Poco adattabile alle reti reali

👉 **Il problema NON è l’IP, ma la posizione del confine tra i bit.**

---

## 🧠 Cos’è davvero la Subnet Mask

La **subnet mask** è una sequenza di **32 bit** che indica:

```
1 → bit di RETE
0 → bit di HOST
```

📌 Esempio:

```
255.255.255.0
=
11111111.11111111.11111111.00000000
```

👉 Qui:

* **24 bit di rete**
* **8 bit di host**

---

## 🔑 Subnet mask = chiave di lettura dell’IP

Un indirizzo IP **senza subnet mask non ha senso completo**.

Solo con la subnet mask possiamo:

* sapere qual è la rete
* capire se due host comunicano direttamente
* decidere come instradare un pacchetto

👉 **IP AND subnet mask = network address**

---

## 🔌 AND bit a bit: il cuore di tutto

Quando facciamo:

```
IP AND SUBNET MASK
```

succede questo:

* i bit di rete (**1 AND x**) restano
* i bit di host (**0 AND x**) diventano 0

📌 È come dire:

> “tieni la rete, azzera l’host”

---

## 🚦 Subnet mask e routing

I router **non instradano verso host**, ma verso **reti**.

Per questo:

1. prendono l’IP di destinazione
2. applicano l’AND con la mask
3. confrontano il risultato con la tabella di routing

👉 Senza subnet mask, **il routing è impossibile**.

---

# ✏️ ESERCIZI (con richiamo ai bit di rete / host)

---

## 🧮 Esercizio 1 – Network address (AND bit a bit)

### Traccia

* IP: **192.168.1.34**
* Modello **classful**

---

### 🧠 Prima di calcolare: ragioniamo sui bit

Classe C → **/24**

```
[ 24 bit rete | 8 bit host ]
```

---

### Soluzione guidata

Subnet mask:

```
255.255.255.0
```

AND:

```
192.168.1.34
AND
255.255.255.0
=
192.168.1.0
```

✅ Network address: **192.168.1.0**

🧠 *I bit host vengono azzerati.*

---

## 🔍 Esercizio 2 – Stessa rete?

### Traccia

* A: **172.16.5.10**
* B: **172.16.200.3**

---

### 🧠 Analisi dei bit

Classe B → **/16**

```
[ 16 bit rete | 16 bit host ]
```

---

### Soluzione

```
A AND mask = 172.16.0.0
B AND mask = 172.16.0.0
```

✅ **Stessa rete**

---

## 🔢 Esercizio 3 – Numero di host

### Traccia

Rete **classe C**

---

### 🧠 Ragionamento sui bit

```
/24 → 8 bit host
```

Combinazioni:

```
2⁸ = 256
```

Host utilizzabili:

```
256 − 2 = 254
```

---

## 🧠 Esercizio 4 – Leggere una subnet mask

### Traccia

Subnet mask: **255.255.0.0**

---

### 🧠 Traduzione in binario

```
11111111.11111111.00000000.00000000
```

👉

* Bit rete: **16**
* Bit host: **16**

---

# 🚀 CIDR – Spostare il confine dei bit

Il CIDR nasce per **muovere liberamente il confine** tra:

```
[ bit di rete | bit di host ]
```

Non più solo:

* /8
* /16
* /24

Ma **qualsiasi /n**.

---

## 🎯 Perché il CIDR è fondamentale

✔ reti della dimensione giusta
✔ meno spreco di IP
✔ routing più efficiente

👉 Tutto grazie al controllo **preciso dei bit di rete**.

---

## 🧩 Aggregazione CIDR (supernetting)

Aggregare significa:

> **usare meno bit di rete** per rappresentare più reti insieme

---

### Esempio

```
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
```

Condividono i **primi 22 bit**:

```
→ 192.168.0.0/22
```

---

## ⚡ Perché conviene

✔ meno voci di routing
✔ tabelle più piccole
✔ router più veloci

---

## 🧠 REGOLA D’ORO FINALE

> 🔑 Se capisci **quali bit sono di rete e quali di host**,
> **sai già risolvere l’esercizio**.

Il resto (blocchi, formule, scorciatoie)
è solo un modo diverso di applicare:

## 👉 AND bit a bit

