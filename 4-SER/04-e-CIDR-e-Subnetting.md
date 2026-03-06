# Lezione Sintetica: CIDR e Subnetting

---

## 1️⃣ Modello CIDR (Classless Inter-Domain Routing)

### Cos’è CIDR

| Concetto  | Descrizione                                                                                        |
| --------- | -------------------------------------------------------------------------------------------------- |
| CIDR      | Metodo per rappresentare indirizzi IP e subnet usando un **prefisso /n**                           |
| Scopo     | Superare i limiti delle classi A/B/C, migliorare la **gestione e aggregazione** degli indirizzi IP |
| Notazione | `192.168.1.0/24` → primi 24 bit sono **rete**, ultimi 8 bit sono **host**                          |

### Vantaggi del CIDR

| Vantaggio    | Spiegazione                                                  |
| ------------ | ------------------------------------------------------------ |
| Flessibilità | Subnet di qualsiasi dimensione, non vincolate alle classi    |
| Efficienza   | Riduzione spreco indirizzi IP                                |
| Scalabilità  | Permette aggregazione blocchi per ridurre tabelle di routing |
| Routing      | Supporta **Longest Prefix Match** nei router                 |

---

## 2️⃣ Determinare Network Address e Broadcast

### Dati di partenza

| Campo        | Esempio         |
| ------------ | --------------- |
| Indirizzo IP | 192.168.10.130  |
| CIDR         | /26             |
| Subnet mask  | 255.255.255.192 |

---

### Passaggi

1. Convertire l’IP e la subnet mask in **binario**
2. Applicare **AND bit a bit** tra IP e subnet mask → **Network Address**
3. Determinare **Broadcast Address**: mettere tutti i bit host a 1

---

### Tabella di Esempio

| IP             | Subnet Mask           | Network Address | Broadcast Address | Host Range                      |
| -------------- | --------------------- | --------------- | ----------------- | ------------------------------- |
| 192.168.10.130 | 255.255.255.192 (/26) | 192.168.10.128  | 192.168.10.191    | 192.168.10.129 – 192.168.10.190 |

---

## 3️⃣ Ruolo del Subnetting

### Concetto base

| Concetto    | Descrizione                                                      |
| ----------- | ---------------------------------------------------------------- |
| Subnetting  | Suddivisione di una rete più grande in **sottoreti più piccole** |
| Bit di rete | Si prendono bit dalla parte host per creare subnet               |
| Bit host    | Ridotti in base al numero di bit usati per la subnet             |

---

### Formula chiave

| Valore           | Formula                                |
| ---------------- | -------------------------------------- |
| Numero sottoreti | `2^n` (n = bit presi dalla parte host) |
| Host per subnet  | `2^(host_originali - n) - 2`           |
| Nuovo CIDR       | `/m + n` (m = prefisso originale)      |

---

### Esempio pratico

Rete iniziale: `192.168.1.0/24`
Obiettivo: dividere in 4 subnet

| Subnet | Network Address | Broadcast Address | Host Range                    |
| ------ | --------------- | ----------------- | ----------------------------- |
| 1      | 192.168.1.0     | 192.168.1.63      | 192.168.1.1 – 192.168.1.62    |
| 2      | 192.168.1.64    | 192.168.1.127     | 192.168.1.65 – 192.168.1.126  |
| 3      | 192.168.1.128   | 192.168.1.191     | 192.168.1.129 – 192.168.1.190 |
| 4      | 192.168.1.192   | 192.168.1.255     | 192.168.1.193 – 192.168.1.254 |

---

## 4️⃣ Benefici del Subnetting

| Aspetto            | Vantaggio                                                     |
| ------------------ | ------------------------------------------------------------- |
| Gestione           | Reti più piccole e isolate → meno conflitti e più sicurezza   |
| Scalabilità        | Possibilità di aggiungere subnet senza cambiare tutta la rete |
| Efficienza         | Minor spreco di indirizzi IP                                  |
| Controllo traffico | Riduzione broadcast domain, miglioramento performance         |

---

## 5️⃣ Schema Riassuntivo

```
Indirizzo IP + CIDR
│
├─> Network Address (AND tra IP e mask)
├─> Broadcast Address (bit host a 1)
├─> Host disponibili (host range)
│
└─> Subnetting:
     - Bit presi dalla parte host
     - Creazione di 2^n subnet
     - Nuovo CIDR = m + n
     - Host per subnet = 2^(host_originali - n) - 2
```

---

## 6️⃣ Esempio rapido di calcolo incrementale

Subnet mask /26 → ultimo ottetto = 192

```
Incremento = 256 - 192 = 64
```

Subnet partono ogni 64 indirizzi:

| Subnet | Network       | Broadcast     | Host Range  |
| ------ | ------------- | ------------- | ----------- |
| 1      | 192.168.1.0   | 192.168.1.63  | .1 – .62    |
| 2      | 192.168.1.64  | 192.168.1.127 | .65 – .126  |
| 3      | 192.168.1.128 | 192.168.1.191 | .129 – .190 |
| 4      | 192.168.1.192 | 192.168.1.255 | .193 – .254 |

---

Questa struttura è **schematica**, sintetica e pronta per essere usata come base per un elaborato rispondente alla traccia:

* CIDR e motivazioni
* Determinazione network e broadcast
* Ruolo del subnetting in gestione, scalabilità ed efficienza


