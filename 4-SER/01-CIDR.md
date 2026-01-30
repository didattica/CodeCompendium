# 🌐 Indirizzi IP, Subnet Mask e CIDR

Documento di studio per studenti 📘
(Modello **storico classful** → limiti → **CIDR**)

---

## 🧱 Classi di indirizzi IP (modello storico)

In origine, gli indirizzi **IPv4** erano divisi in **classi**.
La classe determina **quanta parte dell’indirizzo identifica la rete** e **quanta l’host**.

Questo modello è chiamato **classful**.

---

### 🔴 Classe A

* Primo ottetto: **1 – 126**
* Molte reti, **tantissimi host**
* Subnet mask: **255.0.0.0** → **/8**
* Host per rete: ~16 milioni 😵‍💫

---

### 🟠 Classe B

* Primo ottetto: **128 – 191**
* Compromesso tra reti e host
* Subnet mask: **255.255.0.0** → **/16**
* Host per rete: ~65.000

---

### 🟢 Classe C

* Primo ottetto: **192 – 223**
* Molte reti, **pochi host**
* Subnet mask: **255.255.255.0** → **/24**
* Host per rete: **254**

---

## ⚠️ Limiti del modello classful

❌ Poco flessibile
❌ Spreco di indirizzi IP
❌ Superato dal **CIDR**

Il problema chiave: **dimensione della rete fissa**.

---

## 🧠 Cos’è la Subnet Mask

La **subnet mask** indica:

* quale parte dell’IP è **rete** 🏠
* quale parte è **host** 💻

È un valore di **32 bit**, come l’indirizzo IP.

👉 Serve per **interpretare correttamente** un indirizzo IP.

---

## ❓ Perché è stata introdotta

Un indirizzo IP **da solo non basta**.

La subnet mask permette di:

* identificare la rete di appartenenza
* capire se due host sono nella **stessa rete**

È **fondamentale per il routing** 🚦.

---

## 🚦 Subnet mask e routing

I router **non instradano verso singoli host**, ma verso **reti**.

La subnet mask permette di:

* estrarre la parte di rete di un IP
* confrontarla con le **tabelle di routing**

📌 Senza subnet mask:

* il router non saprebbe a quale rete appartiene un IP
* non potrebbe decidere dove inoltrare il pacchetto

👉 **IP + subnet mask → network address**

---

## 💥 Perché il modello classful spreca IP

### Classe A

* ~16 milioni di host per rete
* Spesso usata per reti molto più piccole
* ➜ **milioni di IP inutilizzati**

### Classe B

* ~65.000 host per rete
* Troppo grande per molte organizzazioni

### Classe C

* 254 host per rete
* Spesso insufficiente
* Costringe a usare **più reti separate**

---

# ✏️ ESERCIZI CON SOLUZIONE GUIDATA

---

## 🧮 Esercizio 1 – AND bit a bit (routing)

### Traccia

Dato:

* IP: **192.168.1.34**
* Subnet mask **classful**

Calcola il **network address** usando l’operazione **AND bit a bit**.

---

### Soluzione guidata

Classe C → subnet mask: **255.255.255.0**

**Conversione in binario**

IP:

```
192 = 11000000
168 = 10101000
1   = 00000001
34  = 00100010
```

Subnet mask:

```
255 = 11111111
255 = 11111111
255 = 11111111
0   = 00000000
```

**AND bit a bit**

```
11000000 AND 11111111 = 11000000
10101000 AND 11111111 = 10101000
00000001 AND 11111111 = 00000001
00100010 AND 00000000 = 00000000
```

✅ **Network address: 192.168.1.0**

---

## 🔍 Esercizio 2 – Verifica stessa rete

### Traccia

Due host:

* A: **172.16.5.10**
* B: **172.16.200.3**

Modello **classful**.
Usa l’AND per verificare se sono nella **stessa rete**.

---

### Soluzione guidata

Classe B → subnet mask: **255.255.0.0**

AND:

```
172.16.5.10   AND 255.255.0.0 = 172.16.0.0
172.16.200.3  AND 255.255.0.0 = 172.16.0.0
```

✅ Network address uguale → **stessa rete**

---

## 🔢 Esercizio 3 – Conteggio host

### Traccia

Quanti host può avere una rete **classe C**?

---

### Soluzione guidata

Bit host: **8**

Totale combinazioni:

```
2⁸ = 256
```

Indirizzi non utilizzabili:

* Network address
* Broadcast

✅ Host utilizzabili:

```
256 − 2 = 254
```

---

## 🧠 Esercizio 4 – Interpretazione subnet mask

### Traccia

Subnet mask: **255.255.0.0**

* Quanti bit di rete?
* Quanti bit di host?

---

### Soluzione guidata

```
255 = 11111111
255 = 11111111
0   = 00000000
0   = 00000000
```

* Bit di rete: **16**
* Bit di host: **16**

---

# 🚀 CIDR (Classless Inter-Domain Routing)

Il passo naturale dopo il modello classful è il **CIDR**.

Nel modello classful:

* subnet mask fisse (/8, /16, /24)
* poca flessibilità
* spreco di IPv4

---

## 🎯 Obiettivi del CIDR

✔ Adattare la rete ai bisogni reali
✔ Ridurre lo spreco di indirizzi IP
✔ Routing più efficiente

Il CIDR **elimina le classi** e usa la notazione **/n**.

---

## 🧭 Routing flessibile

Con CIDR:

* la rete può avere **qualsiasi dimensione /n**
* meno voci nelle tabelle di routing
* routing più veloce

📌 I router instradano **per reti**, non per host.

---

## 🧩 Aggregazione di prefissi (supernetting)

CIDR permette di **raggruppare reti contigue**.

### Esempio

```
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
```

➡️ Aggregabili in:

```
192.168.0.0/22
```

---

## ⚡ Vantaggi dell’aggregazione

Senza aggregazione:

```
4 voci di routing
```

Con aggregazione:

```
1 sola voce
```

✔ Meno memoria
✔ Routing più veloce

---

## 💡 Regola pratica

👉 L’aggregazione di prefissi è utile:

* nei **router intermedi**
* nel **backbone**

🚫 L’ultimo router prima degli host **non ne trae grande beneficio**.


