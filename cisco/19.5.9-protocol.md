# Il concetto di "Protocollo" nel Networking

> [!NOTE]
> Questo documento ha lo scopo di chiarire un'ambiguità comune: la parola **"protocollo"** nel networking è un **termine ombrello** (iperonimo) che non si riferisce esclusivamente a protocolli applicativi come HTTP o a protocolli di trasporto come TCP. Il suo significato dipende fortemente dal **contesto** e dal **layer OSI** di riferimento.

---

## Indice

1. [Cosa significa davvero "protocollo"?](#1-cosa-significa-davvero-protocollo)
2. [Perché esistono protocolli a più layer?](#2-perché-esistono-protocolli-a-più-layer)
3. [La mappa dei protocolli nel modello OSI](#3-la-mappa-dei-protocolli-nel-modello-osi)
4. [Hardware vs Protocollo: una distinzione fondamentale](#4-hardware-vs-protocollo-una-distinzione-fondamentale)
5. [Il "line protocol" nei comandi Cisco](#5-il-line-protocol-nei-comandi-cisco)
6. [Esempi pratici con i comandi Cisco](#6-esempi-pratici-con-i-comandi-cisco)
7. [Riepilogo visivo](#7-riepilogo-visivo)

---

## 1. Cosa significa davvero "protocollo"?

Molti studenti, quando sentono la parola **"protocollo"**, pensano immediatamente a:

- `HTTP` / `HTTPS` (navigazione web)
- `FTP` (trasferimento file)
- `SMTP` (posta elettronica)
- `TCP/IP` (trasporto affidabile)

Questa associazione è comprensibile, perché sono i protocolli più visibili all'utente finale. Tuttavia, si tratta solo di una **piccola parte** del quadro complessivo.

### Definizione tecnica

Un **protocollo di rete** è un insieme formalizzato di regole che definisce:

| Aspetto | Descrizione |
|---|---|
| **Formato dei dati** | Come sono strutturati i pacchetti/frame/segmenti |
| **Semantica dei messaggi** | Cosa significa ogni campo e ogni valore |
| **Sincronizzazione** | Come si coordinano temporalmente mittente e destinatario |
| **Comportamento degli endpoint** | Cosa deve fare ciascuna entità in ogni situazione |
| **Gestione degli errori** | Come si rilevano e gestiscono i problemi |
| **Modalità di trasmissione** | Come avviene lo scambio (unicast, broadcast, ecc.) |

In sintesi:

> **Un protocollo stabilisce *come* due entità comunicano.**

> [!IMPORTANT]
> Un protocollo **non è hardware**. È una convenzione logica, implementata in software o firmware.
> I protocolli esistono a tutti i layer del modello OSI. Al Layer 1 si parla più propriamente di standard fisici o specifiche, ma anche questi rientrano nella categoria generale di "regole formalizzate per la comunicazione".
> Anche le specifiche fisiche sono "regole formalizzate", ma il termine protocollo viene usato con maggiore precisione quando c'è una logica di comunicazione — non solo una forma o una misura.

---

## 2. Perché esistono protocolli a più layer?

La comunicazione di rete è un problema complesso, suddiviso in **sotto-problemi distinti**, ciascuno risolto da un layer specifico del modello OSI.

Ogni layer si occupa di una domanda diversa:

| Layer OSI | Domanda che risolve |
|---|---|
| **7 – Applicazione** | Che messaggio voglio inviare? Qual è il formato dei dati applicativi? |
| **4 – Trasporto** | Come garantisco la consegna? Come gestisco l'ordine dei dati? |
| **3 – Rete** | Quale percorso seguo per raggiungere la destinazione? |
| **2 – Data Link** | Come comunico in modo affidabile con il nodo direttamente connesso? |
| **1 – Fisico** | Come trasmetto fisicamente i bit sul mezzo trasmissivo? |

Poiché ogni layer risolve un problema diverso, ogni layer ha **protocolli specializzati** e indipendenti.

### Analogia: la spedizione internazionale

Immagina una spedizione internazionale. Anche in quel caso esistono più livelli organizzativi:

- Il **mittente** scrive il messaggio (Layer 7)
- Il **corriere** garantisce la consegna e il tracciamento (Layer 4)
- Il **sistema doganale e postale** instrada il pacco tra Paesi (Layer 3)
- Il **camion locale** consegna al destinatario nel quartiere (Layer 2)
- Il **sistema stradale** è il mezzo fisico su cui tutto si muove (Layer 1)

Ogni livello usa le proprie regole, indipendentemente dagli altri.

---

## 3. La mappa dei protocolli nel modello OSI

Ecco una panoramica dei principali protocolli suddivisi per layer:

| Layer | Nome | Esempi di protocolli |
|---|---|---|
| **7** | Applicazione | HTTP, HTTPS, DNS, FTP, SMTP, DHCP |
| **4** | Trasporto | TCP, UDP |
| **3** | Rete | IP, ICMP, OSPF, BGP, EIGRP |
| **2** | Data Link | Ethernet, PPP, HDLC, ARP, 802.11 (Wi-Fi) |
| **1** | Fisico | Segnale elettrico, ottico, radio (pochi protocolli logici "puri") |

> [!CAUTION]
> **Errore comune:** associare "protocollo" solo ai layer alti (4–7). In realtà, quando si parla di **configurazione e diagnostica di rete** (specialmente su apparati Cisco), il termine "protocollo" si riferisce spessissimo ai layer **2 e 3**.

---

## 4. Hardware vs Protocollo: una distinzione fondamentale

Questo è uno dei concetti più importanti da interiorizzare.

### Layer 1 – Fisico (Hardware)

Il livello fisico riguarda:

- Voltaggio e corrente
- Clock e temporizzazione
- Tipo di segnale (elettrico, ottico, radio)
- Connettori e cavi (RJ45, fibra, coassiale)
- Pin e interfacce

### Layer 2+ – Protocollo (Logica)

I protocolli riguardano:

- Formato e struttura dei dati
- Regole di comunicazione e stati logici
- Sincronizzazione e controllo del flusso
- Indirizzamento (MAC, IP, ecc.)
- Rilevamento e correzione degli errori

> [!IMPORTANT]
> Un protocollo è una **costruzione logica astratta**, implementata in software o firmware. **Non coincide con l'hardware fisico**, anche quando è strettamente legato a esso.

### Esempio: Ethernet non è "un cavo"

Ethernet è un **protocollo Layer 2**. Definisce:

- Il formato del **frame** (preambolo, MAC sorgente/destinazione, tipo, payload, FCS)
- L'**indirizzamento MAC**
- Il **CRC** per il rilevamento degli errori
- La **MTU** (Maximum Transmission Unit)
- Il comportamento in caso di collisione (storicamente, con CSMA/CD)

Il cavo RJ45 (o la fibra) è solo il **mezzo fisico** su cui Ethernet opera. Senza il protocollo Ethernet, quel cavo trasporterebbe segnali privi di significato.

---

## 5. Il "line protocol" nei comandi Cisco

Arriviamo ora al punto cruciale per la diagnostica Cisco.

Quando si esegue `show interfaces` su un router o switch Cisco, si ottiene un output simile a questo:

```
GigabitEthernet0/0 is up, line protocol is up
```

Molti studenti si chiedono: *di quale "protocollo" si parla?*

> [!CAUTION]
> Nel comando `show interfaces`, il termine **"line protocol"** **non** si riferisce a protocolli applicativi come HTTP o HTTPS, né al protocollo di trasporto TCP. Si riferisce al **protocollo logico di Data Link (Layer 2)** associato all'interfaccia.

### Cosa indicano i due campi

Cisco separa deliberatamente due informazioni distinte:

| Campo | Layer | Cosa indica |
|---|---|---|
| `GigabitEthernet0/0 is up` | **Layer 1** | Il livello fisico è attivo: il segnale è rilevato, il cavo è connesso, c'è carrier detection |
| `line protocol is up` | **Layer 2** | Il protocollo logico di collegamento è operativo: i frame sono validi, i keepalive funzionano, l'encapsulation è corretta |

### Cosa verifica il "line protocol"

Il `line protocol` controlla elementi come:

- **Frame validi** ricevuti sull'interfaccia
- **Keepalive** correttamente scambiati con il peer
- **Encapsulation coerente** tra i due estremi del collegamento (es. entrambi usano HDLC, oppure entrambi usano PPP)
- **Negoziazione** del protocollo di Data Link completata con successo

> [!TIP]
> Puoi pensare al `line protocol` come all'**handshake logico** tra due dispositivi vicini. Anche se il cavo fisico è integro, il collegamento logico può non essere stabilito — e in quel caso il traffico non passerà.

---

## 6. Esempi pratici con i comandi Cisco

### `show interfaces` — I quattro scenari possibili

#### ✅ Scenario 1: tutto funziona

```
GigabitEthernet0/0 is up, line protocol is up
```

Sia il Layer 1 (fisico) che il Layer 2 (logico) sono operativi. L'interfaccia può instradare traffico.

---

#### ⚠️ Scenario 2: fisico OK, logico KO

```
GigabitEthernet0/0 is up, line protocol is down
```

> [!WARNING]
> Il cavo è collegato e il segnale fisico è presente, ma il **protocollo di Data Link non riesce a stabilirsi**. Possibili cause:
> - Mismatch di encapsulation (es. un lato usa PPP, l'altro usa HDLC)
> - Keepalive non ricevuti dal peer
> - Fallimento della negoziazione PPP (LCP, autenticazione)
> - Inconsistenza di VLAN su un trunk

---

#### ❌ Scenario 3: interfaccia amministrativamente disabilitata

```
GigabitEthernet0/0 is administratively down, line protocol is down
```

L'interfaccia è stata disattivata manualmente con il comando `shutdown`.

---

#### ❌ Scenario 4: nessun segnale fisico

```
GigabitEthernet0/0 is down, line protocol is down
```

Il Layer 1 non rileva segnale: cavo scollegato, porta danneggiata, o problema sul peer.

---

### `show protocols` — Il protocollo di Layer 3

> [!CAUTION]
> Nel comando `show protocols`, il termine "protocollo" si riferisce ai **protocolli di Layer 3** configurati sulle interfacce (tipicamente **IP**), **non** a protocolli applicativi.

Esempio di output:

```
Router# show protocols
Global values:
  Internet Protocol routing is enabled
GigabitEthernet0/0 is up, line protocol is up
  Internet address is 192.168.1.1/24
GigabitEthernet0/1 is up, line protocol is down
  Internet address is 10.0.0.1/30
```

Questo comando mostra se il protocollo IP è attivo e configurato su ciascuna interfaccia, ma **non dice nulla su HTTP, TCP, o altri protocolli superiori**.

---

### Schema riassuntivo dei comandi Cisco e dei layer coinvolti

| Comando Cisco | Layer principale coinvolto | Cosa verifica |
|---|---|---|
| `show interfaces` | Layer 1 + Layer 2 | Stato fisico e stato del line protocol |
| `show protocols` | Layer 3 | Protocollo di rete (IP) e indirizzi configurati |
| `show ip route` | Layer 3 | Tabella di routing IP |
| `show ip ospf neighbor` | Layer 3 | Stato dei vicini OSPF |
| `debug ppp negotiation` | Layer 2 | Negoziazione del protocollo PPP |

---

## 7. Riepilogo visivo

### Formula mentale

```
Hardware (Layer 1)  →  "Come si trasmettono i bit fisicamente"
Protocollo (L2+)    →  "Come si interpretano e organizzano quei bit"
```

### Mappa concettuale

```
                    ┌─────────────────────────────────────────┐
                    │           PROTOCOLLO (termine ombrello)  │
                    └──────────────────┬──────────────────────┘
                                       │
          ┌────────────────────────────┼───────────────────────────┐
          │                            │                           │
   ┌──────▼──────┐             ┌───────▼──────┐           ┌───────▼──────┐
   │  Layer 2    │             │   Layer 3    │           │   Layer 4–7  │
   │  Data Link  │             │    Rete      │           │  Trasporto + │
   │             │             │              │           │  Applicazione│
   │ Ethernet    │             │  IP, OSPF,   │           │              │
   │ PPP, HDLC   │             │  BGP, ICMP   │           │  TCP, UDP,   │
   │ 802.11      │             │              │           │  HTTP, DNS,  │
   │             │             │              │           │  SMTP, FTP   │
   └─────────────┘             └──────────────┘           └──────────────┘
         ▲
         │
  "line protocol"
  nei comandi Cisco
```

> [!NOTE]
> Quando un tecnico di rete o un comando Cisco usa la parola "protocollo", è **indispensabile capire il contesto** per sapere a quale layer si riferisce. Non assumere mai che si parli di HTTP o TCP: spesso ci si riferisce a protocolli di livello molto più basso, fondamentali per il funzionamento dell'infrastruttura.

---

## Conclusione

Il termine **"protocollo"** nel networking è un **iperonimo**: un termine generale che abbraccia una vasta famiglia di standard e convenzioni, distribuiti su tutti i layer del modello OSI.

- I protocolli applicativi (HTTP, SMTP, FTP) sono solo la **punta dell'iceberg**.
- I protocolli di trasporto (TCP, UDP), di rete (IP, OSPF) e di Data Link (Ethernet, PPP) sono **altrettanto fondamentali**.
- Nei comandi Cisco come `show interfaces` e `show protocols`, il termine "protocollo" si riferisce tipicamente a **Layer 2 o Layer 3**, non ai livelli superiori.

Comprendere a quale layer appartiene un protocollo è la chiave per interpretare correttamente i messaggi di diagnostica, configurare le interfacce e risolvere i problemi di rete in modo efficace.
