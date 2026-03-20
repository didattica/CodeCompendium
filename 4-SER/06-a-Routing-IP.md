
# 📡 Routing IP – Guida Introduttiva (con schemi Mermaid)

---

## 🔹 Cos'è il Routing IP

Il **routing IP** è il processo con cui un pacchetto dati viene instradato da una rete di origine a una rete di destinazione attraverso uno o più router.

### 🧠 Schema concettuale

```mermaid
flowchart LR
    A[Rete di origine] --> B[Router]
    B --> C[Router intermedio]
    C --> D[Rete di destinazione]
````

---

## 🔹 Indirizzo IP e struttura binaria

Un indirizzo IPv4 è composto da **32 bit**:

```mermaid
flowchart LR
    A[32 bit] --> B[Network bits]
    A --> C[Host bits]
```

Esempio:

```mermaid
flowchart LR
    A[192.168.1.10] --> B[11000000]
    A --> C[10101000]
    A --> D[00000001]
    A --> E[00001010]
```

---

## 🔹 Subnet Mask e logica AND

La subnet mask separa rete e host.

### 🧠 AND logico

```mermaid
flowchart TD
    A[IP Address] --> C[AND]
    B[Subnet Mask] --> C
    C --> D[Network Address]
```

Esempio pratico:

```mermaid
flowchart LR
    A[192.168.1.10] --> C[AND]
    B[255.255.255.0] --> C
    C --> D[192.168.1.0]
```

---

## 🔹 Network, Host e Broadcast

```mermaid
flowchart LR
    A[Rete] --> B[Host validi]
    B --> C[Broadcast]
```

Oppure più dettagliato:

```mermaid
flowchart LR
    N[Network\nhost bits=0] --> H[Host validi]
    H --> B[Broadcast\nhost bits=1]
```

---

## 🔹 Calcolo Broadcast con OR

```mermaid
flowchart TD
    A[Network Address] --> C[OR]
    B[NOT Subnet Mask] --> C
    C --> D[Broadcast Address]
```

---

## 🔹 Come funziona il Routing

```mermaid
flowchart TD
    A[Host invia pacchetto] --> B{Stessa rete?}
    B -- SI --> C[Invio diretto]
    B -- NO --> D[Invio al Gateway]
    D --> E[Router]
    E --> F[Tabella di routing]
    F --> G[Scelta percorso]
```

---

## 🔹 Tabella di Routing

```mermaid
flowchart TD
    A[Pacchetto in arrivo] --> B[Leggi IP destinazione]
    B --> C[Confronto con rotte]
    C --> D[Seleziona miglior match]
    D --> E[Invia su interfaccia]
```

---

## 🔹 Longest Prefix Match

```mermaid
flowchart TD
    A[Destinazione IP] --> B[Match con rete 1 /24]
    A --> C[Match con rete 2 /16]
    B --> D[Scelta migliore]
    C --> D
    D --> E[Prefisso più lungo vince]
```

---

## 🔹 Supernetting

```mermaid
flowchart LR
    A[192.168.0.0/24] --> C[Aggregazione]
    B[192.168.1.0/24] --> C
    C --> D[192.168.0.0/23]
```

---

## 🔹 Tipi di Routing

```mermaid
flowchart LR
    A[Routing] --> B[Statico]
    A --> C[Dinamico]
    C --> D[RIP]
    C --> E[OSPF]
    C --> F[BGP]
```

---

## 🔹 Riassunto logico (bit + operazioni)

```mermaid
flowchart TD
    A[IP Address] --> B[AND con Mask]
    B --> C[Network]
    C --> D[OR con NOT Mask]
    D --> E[Broadcast]
```

---

## 📌 Conclusione

```mermaid
flowchart LR
    A[Bit e binario] --> B[Subnetting]
    B --> C[Routing]
    C --> D[Internet reale]
```

Il routing IP unisce:

* logica binaria (AND/OR)
* indirizzamento
* decisioni dinamiche

<!--

---

Se vuoi fare un salto di qualità 🔥  
posso trasformarti questo in:

- mappa mentale completa stile “schema da interrogazione”
- oppure aggiungere **esercizi con diagrammi già pronti in Mermaid** (molto utili per verifiche)
-->
