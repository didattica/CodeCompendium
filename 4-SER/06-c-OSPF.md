
# 🌐 OSPF (Open Shortest Path First) – Introduzione Completa

---

# 1. Perché OSPF?

Nel capitolo precedente abbiamo studiato **RIP**, un protocollo di routing di tipo **Distance-Vector**.

RIP funziona bene in reti piccole, ma presenta diversi limiti:

| Limite RIP                       | Conseguenza            |
| -------------------------------- | ---------------------- |
| Max 15 hop                       | reti poco scalabili    |
| Convergenza lenta                | routing instabile      |
| Metrica solo hop count           | ignora banda e latenza |
| Aggiornamenti periodici completi | overhead inutile       |

OSPF nasce per risolvere questi problemi.

> [!NOTE]
> OSPF è oggi uno dei protocolli di routing interni (IGP) più usati nelle reti enterprise.

---

# 2. Cos'è OSPF?

**OSPF (Open Shortest Path First)** è un protocollo di routing dinamico di tipo:

* **Link-State**
* standard aperto (RFC 2328)
* progettato per reti medio-grandi

A differenza di RIP:

| RIP                     | OSPF                |
| ----------------------- | ------------------- |
| Distance-Vector         | Link-State          |
| Hop count               | Cost                |
| Aggiornamenti periodici | Event-driven        |
| Convergenza lenta       | Convergenza rapida  |
| Max 15 hop              | altamente scalabile |

---

# 3. Distance-Vector vs Link-State

## RIP (Distance-Vector)

Ogni router:

* conosce solo i vicini
* apprende rotte tramite aggiornamenti periodici
* non conosce tutta la topologia

```mermaid
flowchart LR
    R1 -->|tabella routing| R2
    R2 -->|tabella routing| R3
```

---

## OSPF (Link-State)

Ogni router:

* scopre tutta la topologia
* costruisce una mappa completa della rete
* calcola autonomamente il percorso migliore

```mermaid
graph TD
    R1((R1))
    R2((R2))
    R3((R3))
    R4((R4))

    R1 --- R2
    R2 --- R3
    R2 --- R4
```

> [!IMPORTANT]
> In OSPF ogni router possiede una copia della topologia dell'area.

---

# 4. Architettura OSPF

OSPF lavora in 3 fasi principali:

```mermaid
flowchart LR
    A[Neighbor Discovery] --> B[LSDB Synchronization]
    B --> C[SPF Calculation]
```

| Fase                 | Descrizione                         |
| -------------------- | ----------------------------------- |
| Neighbor Discovery   | scoperta dei router vicini          |
| LSDB Synchronization | sincronizzazione database topologia |
| SPF Calculation      | calcolo shortest path con Dijkstra  |

---

# 5. Neighbor Discovery – Hello Packets

I router OSPF inviano periodicamente pacchetti **Hello**.

Servono per:

* scoprire vicini
* verificare che siano attivi
* formare adiacenze

---

## Multicast OSPF

| Tipo             | Indirizzo   |
| ---------------- | ----------- |
| All OSPF Routers | `224.0.0.5` |
| DR/BDR           | `224.0.0.6` |

---

## Hello Packet

Contiene:

* Router ID
* Area ID
* Hello Timer
* Dead Timer
* Authentication
* lista neighbor

```mermaid
packet-beta
    title OSPF Hello Packet
    0-31: "Router ID"
    32-63: "Area ID"
    64-95: "Hello Timer"
    96-127: "Dead Timer"
```

> [!CAUTION]
> Due router OSPF diventano neighbor solo se alcuni parametri coincidono:
>
> * Area ID
> * subnet mask
> * authentication
> * hello/dead timers

---

# 6. Router ID

Ogni router OSPF possiede un identificatore univoco:

```text
1.1.1.1
2.2.2.2
10.255.255.1
```

---

## Priorità di selezione

OSPF sceglie il Router ID così:

| Priorità | Sorgente                          |
| -------- | --------------------------------- |
| 1        | router-id configurato manualmente |
| 2        | loopback più alta                 |
| 3        | IP fisico più alto                |

---

# 7. Link-State Advertisements (LSA)

I router OSPF non inviano l'intera routing table.

Inviano invece informazioni sullo stato dei link:

* reti connesse
* costo link
* neighbor

Queste informazioni si chiamano:

# 👉 LSA (Link-State Advertisement)

---

## Flooding delle LSA

```mermaid
graph LR
    R1((R1))
    R2((R2))
    R3((R3))
    R4((R4))

    R1 -->|LSA| R2
    R2 -->|LSA| R3
    R2 -->|LSA| R4
```

Ogni router inoltra le LSA ricevute.

---

# 8. Link-State Database (LSDB)

Tutte le LSA formano il database topologico:

# 👉 LSDB (Link-State Database)

Ogni router dell'area possiede una LSDB identica.

```mermaid
flowchart TD
    A[LSA da R1]
    B[LSA da R2]
    C[LSA da R3]

    A --> D[LSDB]
    B --> D
    C --> D
```

---

# 9. Algoritmo SPF (Dijkstra)

Una volta costruita la LSDB:

* ogni router esegue l'algoritmo SPF
* calcola lo shortest path tree
* costruisce la routing table

---

## Esempio

```mermaid
graph LR
    A((R1))
    B((R2))
    C((R3))
    D((R4))

    A -- 10 --> B
    A -- 5 --> C
    C -- 2 --> D
    B -- 1 --> D
```

---

## Calcolo del percorso

Da R1 a R4:

| Percorso     | Costo |
| ------------ | ----- |
| R1 → R2 → R4 | 11    |
| R1 → R3 → R4 | 7     |

OSPF sceglie:

# ✅ R1 → R3 → R4

---

# 10. Metrica OSPF – Cost

OSPF usa una metrica chiamata:

# 👉 Cost

Basata sulla banda del link.

Formula classica Cisco:

```text
Cost = Reference Bandwidth / Interface Bandwidth
```

---

## Esempio

| Banda    | Cost                       |
| -------- | -------------------------- |
| 10 Mbps  | 10                         |
| 100 Mbps | 1                          |
| 1 Gbps   | 1 (default Cisco classico) |

---

> [!NOTE]
> RIP ignora completamente la velocità dei link.
>
> OSPF invece preferisce link più veloci.

---

# 11. Aree OSPF

OSPF divide la rete in:

# 👉 Aree

per migliorare:

* scalabilità
* convergenza
* dimensione LSDB

---

## Backbone Area

L'area principale è:

# 👉 Area 0

```mermaid
graph TD
    A0[Area 0 Backbone]

    A1[Area 1]
    A2[Area 2]
    A3[Area 3]

    A1 --- A0
    A2 --- A0
    A3 --- A0
```

---

## Tipi di router OSPF

| Tipo            | Funzione                           |
| --------------- | ---------------------------------- |
| Internal Router | tutte interfacce nella stessa area |
| ABR             | collega aree                       |
| ASBR            | connette altri protocolli          |
| Backbone Router | connesso ad Area 0                 |

---

# 12. DR e BDR

Su reti multi-accesso (Ethernet), OSPF elegge:

* **DR** → Designated Router
* **BDR** → Backup Designated Router

per ridurre il flooding.

---

## Senza DR

Numero adiacenze:

```text
n(n-1)/2
```

Con 5 router:

```text
5×4/2 = 10 adiacenze
```

---

## Con DR/BDR

```mermaid
graph TD
    DR((DR))

    R1((R1))
    R2((R2))
    R3((R3))
    R4((R4))

    R1 --- DR
    R2 --- DR
    R3 --- DR
    R4 --- DR
```

Molto più efficiente.

---

# 13. Stati Neighbor OSPF

| Stato    | Significato                 |
| -------- | --------------------------- |
| Down     | nessun hello ricevuto       |
| Init     | hello ricevuto              |
| 2-Way    | comunicazione bidirezionale |
| ExStart  | negoziazione database       |
| Exchange | scambio database            |
| Loading  | richiesta LSA mancanti      |
| Full     | sincronizzazione completa   |

---

> [!IMPORTANT]
> Lo stato finale desiderato è:
>
> # FULL

---

# 14. Pacchetti OSPF

OSPF usa direttamente il protocollo IP:

| Campo           | Valore    |
| --------------- | --------- |
| Protocol Number | 89        |
| TCP/UDP         | non usati |

---

## Tipi di pacchetti

| Tipo  | Funzione             |
| ----- | -------------------- |
| Hello | neighbor discovery   |
| DBD   | database description |
| LSR   | link-state request   |
| LSU   | link-state update    |
| LSAck | acknowledgment       |

---

# 15. Configurazione Cisco IOS

## Base

```bash
router ospf 1
 router-id 1.1.1.1
 network 10.0.12.0 0.0.0.3 area 0
 network 192.168.1.0 0.0.0.255 area 0
```

---

## Wildcard Mask

OSPF usa wildcard mask:

| Subnet Mask     | Wildcard  |
| --------------- | --------- |
| 255.255.255.0   | 0.0.0.255 |
| 255.255.255.252 | 0.0.0.3   |

---

> [!TIP]
> Wildcard = inversione della subnet mask.

---

# 16. Verifica OSPF

## Neighbor

```bash
show ip ospf neighbor
```

---

## Routing table

```bash
show ip route ospf
```

---

## Database LSDB

```bash
show ip ospf database
```

---

# 17. OSPF vs RIP

| Caratteristica | RIP             | OSPF           |
| -------------- | --------------- | -------------- |
| Tipo           | Distance-Vector | Link-State     |
| Metrica        | Hop count       | Cost           |
| Max hop        | 15              | molto elevato  |
| Convergenza    | lenta           | rapida         |
| Aggiornamenti  | periodici       | triggered      |
| Scalabilità    | bassa           | alta           |
| Algoritmo      | Bellman-Ford    | Dijkstra       |
| Trasporto      | UDP 520         | IP Protocol 89 |

---

# 18. Esempio Completo

## Topologia

```mermaid
graph LR
    R1((R1))
    R2((R2))
    R3((R3))
    LAN1[192.168.1.0/24]
    LAN2[192.168.2.0/24]

    LAN1 --- R1
    R1 --- R2
    R2 --- R3
    R3 --- LAN2
```

---

## Processo

### Step 1 – Hello

I router scoprono i neighbor.

### Step 2 – LSA Flooding

Ogni router pubblica i propri link.

### Step 3 – LSDB

Tutti costruiscono la stessa topologia.

### Step 4 – SPF

Ogni router calcola shortest paths.

### Step 5 – Routing Table

Le rotte vengono installate.

---

# 19. Problemi comuni

| Problema          | Possibile causa     |
| ----------------- | ------------------- |
| Neighbor non FULL | mismatch timer      |
| Nessuna adiacenza | area mismatch       |
| Route mancanti    | wildcard errata     |
| Instabilità       | duplicate router-id |

---

> [!CAUTION]
> Router ID duplicati causano problemi gravi di convergenza.

---

# 20. Riepilogo Finale

| Concetto    | OSPF                  |
| ----------- | --------------------- |
| Tipo        | Link-State            |
| Algoritmo   | Dijkstra SPF          |
| Metrica     | Cost                  |
| Trasporto   | IP Protocol 89        |
| Multicast   | 224.0.0.5 / 224.0.0.6 |
| Database    | LSDB                  |
| Scalabilità | elevata               |
| Backbone    | Area 0                |

---

# 21. Prossimi Argomenti Consigliati

Dopo OSPF:

1. Dijkstra Algorithm approfondito
2. OSPF Areas avanzate
3. Route Summarization
4. EIGRP
5. BGP
6. MPLS
7. IPv6 + OSPFv3

---

# 📚 Concetti chiave da ricordare

> [!SUMMARY]
>
> * OSPF è un protocollo Link-State
> * Ogni router conosce la topologia dell'area
> * Usa Dijkstra per calcolare shortest path
> * La metrica è il Cost basato sulla banda
> * Area 0 è il backbone
> * Convergenza molto più rapida rispetto a RIP
