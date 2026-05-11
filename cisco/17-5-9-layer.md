# Cisco Networking Layers Explained - Cos'è un Layer?

Un **layer** (livello) è una parte specifica del processo di comunicazione di rete.

Ogni layer ha responsabilità precise.

Il modello più usato per studiare il networking è il modello OSI.

---

# Modello OSI

| Layer | Nome | Funzione |
|---|---|---|
| 7 | Application | Applicazioni utente |
| 6 | Presentation | Formato dati |
| 5 | Session | Gestione sessioni |
| 4 | Transport | TCP / UDP |
| 3 | Network | Routing IP |
| 2 | Data Link | MAC, Switch, VLAN |
| 1 | Physical | Cavi e segnali |

---

> [!IMPORTANT]
> Nel networking Cisco i layer più importanti sono:
>
> - Layer 1
> - Layer 2
> - Layer 3
>
> La maggior parte dei comandi Cisco lavora principalmente su questi livelli.

---

# Layer 1 — Physical

Il Layer 1 riguarda:

- cavi
- segnali elettrici
- fibra ottica
- stato fisico delle interfacce

Non esistono IP o MAC a questo livello.

## Esempio Cisco

```bash
show interfaces
````

Output tipico:

```text
GigabitEthernet0/0 is up
```

Significa:

* il cavo è collegato
* il segnale fisico funziona

---

> [!NOTE]
> Se un'interfaccia è:
>
> ```text
> administratively down
> ```
>
> significa che è stata disabilitata manualmente con:
>
> ```bash
> shutdown
> ```

---

# Layer 2 — Data Link

Il Layer 2 gestisce:

* MAC address
* Ethernet
* switching
* VLAN
* trunk
* frame

Qui lavorano gli switch.

---

# Concetti principali Layer 2

## MAC Address

Ogni dispositivo ha un indirizzo MAC unico.

Esempio:

```text
00:1A:2B:3C:4D:5E
```

---

## VLAN

Le VLAN dividono una rete fisica in reti logiche separate.

---

## Switch

Uno switch Layer 2 inoltra frame usando MAC address.

---

# Comandi Cisco Layer 2

## Visualizzare MAC table

```bash
show mac address-table
```

---

## Visualizzare VLAN

```bash
show vlan brief
```

---

## Visualizzare trunk

```bash
show interfaces trunk
```

---

> [!TIP]
> Se nei comandi vedi:
>
> * MAC
> * VLAN
> * trunk
> * spanning-tree
>
> stai lavorando a Layer 2.

---

# Layer 3 — Network

Il Layer 3 gestisce:

* indirizzi IP
* subnet
* routing
* comunicazione tra reti diverse

Qui lavorano principalmente i router.

---

# Concetti principali Layer 3

## IP Address

Esempio:

```text
192.168.1.1/24
```

---

## Routing

Il router decide dove inviare i pacchetti.

---

## Default Gateway

Permette ai dispositivi di comunicare fuori dalla propria rete.

---

# Comandi Cisco Layer 3

## Visualizzare IP

```bash
show ip interface brief
```

---

## Visualizzare routing table

```bash
show ip route
```

---

## Visualizzare protocolli

```bash
show protocols
```

---

# Esempio reale

```bash
show protocols
```

Output:

```text
Global values:
  Internet Protocol routing is enabled
```

Significa:

* il routing IPv4 è attivo
* il router può inoltrare pacchetti IP
* il dispositivo sta operando come Layer 3

---

> [!IMPORTANT]
> Questa riga NON significa automaticamente che Internet funziona.
>
> Significa solo che il routing IP è abilitato.

---

# Interfacce Cisco

## Stato interfaccia

### Up / Up

```text
is up, line protocol is up
```

Significa:

* Layer 1 OK
* Layer 2 OK

---

### Administratively Down

```text
administratively down
```

Significa:

* interfaccia spenta manualmente

Per riattivarla:

```bash
configure terminal
interface g0/0
no shutdown
```

---

# Layer 4 — Transport

Layer 4 gestisce:

* TCP
* UDP
* porte

Esempi:

| Protocollo | Porta |
| ---------- | ----- |
| HTTP       | 80    |
| HTTPS      | 443   |
| SSH        | 22    |

---

# Comandi utili Layer 4

## Visualizzare connessioni TCP

```bash
show tcp brief
```

---

# Come riconoscere rapidamente il layer

| Se vedi...             | Layer   |
| ---------------------- | ------- |
| cavi, segnale, up/down | Layer 1 |
| MAC, VLAN, switch      | Layer 2 |
| IP, routing, subnet    | Layer 3 |
| TCP, UDP, porte        | Layer 4 |

---

# Cisco Router vs Switch

| Dispositivo    | Layer principale  |
| -------------- | ----------------- |
| Hub            | Layer 1           |
| Switch normale | Layer 2           |
| Router         | Layer 3           |
| Layer 3 Switch | Layer 2 + Layer 3 |

---

# Layer 3 Switch

Uno switch Layer 3 può:

* fare switching
* fare routing

Esempio:

```bash
ip routing
```

abilita il routing sullo switch.

---

> [!WARNING]
> Non tutti gli switch supportano Layer 3.
>
> Gli switch base spesso supportano solo Layer 2.

---

# Comandi Cisco più importanti da conoscere

| Comando                 | Layer |
| ----------------------- | ----- |
| show interfaces         | 1     |
| show mac address-table  | 2     |
| show vlan brief         | 2     |
| show spanning-tree      | 2     |
| show ip interface brief | 3     |
| show ip route           | 3     |
| show protocols          | 2/3   |
| ping                    | 3     |
| traceroute              | 3     |

---

# Ping e Layer

## Ping funziona a Layer 3

```bash
ping 8.8.8.8
```

Serve a verificare:

* connettività IP
* routing
* raggiungibilità

---

# Regola mentale semplice

## Layer 1

"Il cavo funziona?"

---

## Layer 2

"Lo switch sa dove inviare il frame?"

---

## Layer 3

"Il router sa dove inviare il pacchetto IP?"

---

# Riassunto finale

| Layer | Focus Cisco         |
| ----- | ------------------- |
| 1     | Interfacce fisiche  |
| 2     | Switch, MAC, VLAN   |
| 3     | Router, IP, Routing |
| 4     | TCP/UDP             |

---

> [!SUCCESS]
> Per iniziare bene con Cisco:
>
> 1. Impara Layer 1
> 2. Poi Layer 2
> 3. Poi Layer 3
>
> Questi tre livelli coprono gran parte del networking pratico.

```
```
