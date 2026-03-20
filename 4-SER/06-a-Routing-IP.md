
# 📡 Routing IP – Guida Introduttiva

## 🔹 Cos'è il Routing IP
Il **routing IP** è il processo con cui un pacchetto dati viene instradato da una rete di origine a una rete di destinazione attraverso uno o più router.

Un router decide **dove inviare un pacchetto** basandosi sull'indirizzo IP di destinazione.

---

## 🔹 Indirizzo IP e struttura binaria

Un indirizzo IPv4 è composto da **32 bit**, divisi in 4 ottetti:

Esempio:
192.168.1.10  
→ in binario:  
11000000.10101000.00000001.00001010

### ✔ Divisione:
- **Parte di rete (network bits)**
- **Parte host (host bits)**

Questa divisione è definita dalla **subnet mask**.

---

## 🔹 Subnet Mask e logica AND

La subnet mask serve a separare la parte rete dalla parte host.

Esempio:
IP:        192.168.1.10  
Mask:      255.255.255.0  

Binario:
IP:        11000000.10101000.00000001.00001010  
Mask:      11111111.11111111.11111111.00000000  

### 👉 Operazione AND logico

IP AND Mask = Network Address

Risultato:
11000000.10101000.00000001.00000000  
= 192.168.1.0

✔ Questo è l'indirizzo di rete

---

## 🔹 Indirizzo di rete, host e broadcast

In ogni rete IP:

- **Network address** → tutti i bit host = 0  
- **Broadcast address** → tutti i bit host = 1  
- **Host validi** → valori tra questi due

Esempio: rete /24

| Tipo        | Indirizzo        |
|------------|------------------|
| Network     | 192.168.1.0      |
| Host        | 192.168.1.1 - 192.168.1.254 |
| Broadcast   | 192.168.1.255    |

---

## 🔹 Routing: come funziona

Quando un dispositivo invia un pacchetto:

1. Controlla se la destinazione è nella stessa rete
2. Se sì → invio diretto
3. Se no → invio al **default gateway**

Il router:
- legge l'IP di destinazione
- consulta la **tabella di routing**
- inoltra il pacchetto verso la rete corretta

---

## 🔹 Tabella di Routing

Contiene:

- Network di destinazione
- Subnet mask
- Gateway
- Interfaccia di uscita

Esempio:

| Destinazione | Mask        | Gateway     |
|-------------|------------|-------------|
| 192.168.1.0 | 255.255.255.0 | diretto |
| 0.0.0.0     | 0.0.0.0     | 192.168.1.1 |

👉 0.0.0.0 = default route

---

## 🔹 Matching: confronto binario

Il router usa una logica simile a:

(IP destinazione) AND (subnet mask)

per trovare la rete corretta.

Sceglie la route con il **match più lungo** (Longest Prefix Match).

---

## 🔹 OR logico e Broadcast

Per ottenere il broadcast:

Network OR (NOT subnet mask)

Esempio:

Network: 192.168.1.0  
Mask:    255.255.255.0  

NOT Mask:
00000000.00000000.00000000.11111111

OR:
192.168.1.255

---

## 🔹 Supernetting e Routing

Il supernetting (aggregazione) serve a:

- Ridurre il numero di rotte
- Migliorare l'efficienza

Esempio:
192.168.0.0/24  
192.168.1.0/24  

→ aggregato: 192.168.0.0/23

---

## 🔹 Tipi di Routing

### ✔ Routing statico
Configurato manualmente

### ✔ Routing dinamico
Router che si scambiano informazioni tramite protocolli:

- RIP
- OSPF
- BGP

---

## 🔹 Concetti chiave riassunti

- IP = 32 bit
- Subnet mask divide rete/host
- AND → trova rete
- OR → trova broadcast
- Router usa tabelle per decidere il percorso
- Longest prefix match = scelta migliore

---

## 📌 Conclusione

Il routing IP combina:

- **Logica binaria**
- **Struttura degli indirizzi**
- **Decisioni basate su tabelle**

Capire bit, AND/OR e subnet è fondamentale per capire davvero come funzionano le reti.
```

<!--
Se vuoi, posso anche prepararti:

* esercizi pratici (tipo “trova rete e broadcast”)
* oppure un secondo documento su **Routing dinamico (OSPF/BGP)** 👍
-->
