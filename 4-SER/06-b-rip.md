# 📡 RIP (Routing Information Protocol) – Lezione Completa

---

## 1. Collegamento con Longest Prefix Match

Prima di entrare in RIP, richiamiamo il concetto di **Longest Prefix Match (LPM)**, perché i due concetti lavorano insieme.

### Cosa fa LPM?

Quando un router riceve un pacchetto destinato a `192.168.1.50`, consulta la sua tabella di routing e trova più rotte candidate. LPM sceglie quella con il prefisso **più lungo** (più specifico).

**Esempio concreto:**

| Rete di destinazione | Next-hop       | Origine |
|----------------------|----------------|---------|
| `192.168.0.0/16`     | `10.0.0.1`     | RIP     |
| `192.168.1.0/24`     | `10.0.0.2`     | RIP     |
| `0.0.0.0/0`          | `10.0.0.254`   | statico |

Il pacchetto arriva con destinazione `192.168.1.50`:

- `/16` → match (192.168.x.x copre 192.168.1.50) ✅
- `/24` → match (192.168.1.x copre 192.168.1.50) ✅
- `/0`  → match (copre tutto) ✅

**LPM sceglie `/24`** → next-hop `10.0.0.2` → perché ha il prefisso più lungo.

### Quanti bit si confrontano?

```
Destinazione:  192.168.1.50  →  11000000.10101000.00000001.00110010
Rete /24:      192.168.1.0   →  11000000.10101000.00000001.00000000
                                 ^^^^^^^^ ^^^^^^^^ ^^^^^^^^           ← 24 bit uguali ✅

Rete /16:      192.168.0.0   →  11000000.10101000.00000000.00000000
                                 ^^^^^^^^ ^^^^^^^^                    ← solo 16 bit uguali
```

> **Punto chiave:** LPM non crea le rotte, le *sceglie*. È RIP (o altri protocolli) che le *crea*.

---

## 2. Cos'è RIP?

**RIP (Routing Information Protocol)** è un protocollo di routing dinamico di tipo **Distance-Vector**.

Serve a costruire automaticamente la tabella di routing senza che l'amministratore inserisca ogni rotta a mano.

### Versioni

| Versione | Anno | Novità principali |
|----------|------|-------------------|
| RIPv1    | 1988 | classful, no subnet mask negli aggiornamenti |
| RIPv2    | 1994 | classless, invia subnet mask, supporta VLSM |
| RIPng    | 1997 | versione per IPv6 |

> Oggi si usa quasi solo **RIPv2**. RIPv1 è obsoleto perché non trasmette la subnet mask e non supporta VLSM.

---

## 3. Il meccanismo Distance-Vector

Ogni router:
1. conosce solo le reti **direttamente connesse**
2. invia la propria tabella ai **soli router vicini** (neighbor)
3. riceve le tabelle dei vicini e **aggiorna la propria**
4. sceglie il percorso con **meno hop**

### Topologia di esempio

```
[R1] --- [R2] --- [R3] --- [R4]
 |
[R5]
```

Indirizzi delle interfacce:

| Link       | Rete           | R-left        | R-right       |
|------------|----------------|---------------|---------------|
| R1 ↔ R2   | `10.0.12.0/30` | `10.0.12.1`   | `10.0.12.2`   |
| R2 ↔ R3   | `10.0.23.0/30` | `10.0.23.1`   | `10.0.23.2`   |
| R3 ↔ R4   | `10.0.34.0/30` | `10.0.34.1`   | `10.0.34.2`   |
| R1 ↔ R5   | `10.0.15.0/30` | `10.0.15.1`   | `10.0.15.2`   |

Reti LAN collegate:

| Router | LAN            |
|--------|----------------|
| R1     | `192.168.1.0/24` |
| R4     | `192.168.4.0/24` |
| R5     | `172.16.5.0/24`  |

---

## 4. Evoluzione della tabella di routing – passo per passo

### Stato iniziale (solo reti direttamente connesse)

**Tabella R1:**

| Destinazione     | Metric (hop) | Next-hop  |
|------------------|:------------:|-----------|
| `192.168.1.0/24` | 0            | diretto   |
| `10.0.12.0/30`   | 0            | diretto   |
| `10.0.15.0/30`   | 0            | diretto   |

**Tabella R2:**

| Destinazione     | Metric (hop) | Next-hop  |
|------------------|:------------:|-----------|
| `10.0.12.0/30`   | 0            | diretto   |
| `10.0.23.0/30`   | 0            | diretto   |

### Dopo il primo ciclo di aggiornamenti (30 secondi)

R1 invia la sua tabella a R2 e R5. R2 apprende:

| Destinazione     | Metric (hop) | Next-hop    | Come l'ha imparata |
|------------------|:------------:|-------------|---------------------|
| `10.0.12.0/30`   | 0            | diretto     | —                   |
| `10.0.23.0/30`   | 0            | diretto     | —                   |
| `192.168.1.0/24` | **1**        | `10.0.12.1` | da R1               |
| `10.0.15.0/30`   | **1**        | `10.0.12.1` | da R1               |

### Dopo il secondo ciclo

R3 riceve da R2 le rotte con metrica 1 e le aggiunge con metrica 2:

| Destinazione     | Metric (hop) | Next-hop    |
|------------------|:------------:|-------------|
| `192.168.1.0/24` | **2**        | `10.0.23.1` |
| `192.168.4.0/24` | **1**        | `10.0.34.2` |

### Stato finale (convergenza completa)

**Tabella R1 a convergenza:**

| Destinazione     | Metric (hop) | Next-hop    |
|------------------|:------------:|-------------|
| `192.168.1.0/24` | 0            | diretto     |
| `10.0.12.0/30`   | 0            | diretto     |
| `10.0.15.0/30`   | 0            | diretto     |
| `10.0.23.0/30`   | 1            | `10.0.12.2` |
| `192.168.4.0/24` | 3            | `10.0.12.2` |
| `10.0.34.0/30`   | 2            | `10.0.12.2` |
| `172.16.5.0/24`  | 1            | `10.0.15.2` |

> R1 raggiunge `192.168.4.0/24` in 3 hop: R1 → R2 → R3 → R4.

---

## 5. La metrica: Hop Count

RIP misura la distanza solo in **numero di router attraversati**.

```
R1 --- R2 --- R3 --- R4
              |
              R5 --- R6
```

Per arrivare a R6:
- Via R3 → R5 → R6 = **2 hop** da R3, **4 hop** da R1
- RIP sceglie il percorso con meno hop, anche se il link R1→R3 è lentissimo (es. 56 Kbps) e R1→R2→R4→R6 è fibra ottica.

> **Limite critico:** RIP non conosce la banda, la latenza o l'affidabilità dei link. Sceglie solo per hop count.

### Hop count massimo: 15

| Hop count | Significato           |
|:---------:|-----------------------|
| 0         | rete direttamente connessa |
| 1–15      | rete raggiungibile    |
| **16**    | rete **irraggiungibile** (infinito) |

Una rete a 16 hop non viene inserita nella tabella di routing.

---

## 6. Formato del messaggio RIP

RIPv2 usa **UDP porta 520**. Ogni 30 secondi ogni router invia un messaggio di aggiornamento in **broadcast/multicast** (`224.0.0.9`) ai vicini.

Struttura semplificata di un pacchetto RIPv2:

```
0                   1                   2                   3
0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Command (1)  |  Version (2)  |         Must be Zero          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Address Family Identifier    |          Route Tag            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                         IP Address                            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                         Subnet Mask                           |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                         Next Hop                              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                         Metric                                |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

- **Command:** 1 = Request, 2 = Response
- **Version:** 2 (per RIPv2)
- **IP Address + Subnet Mask:** la rotta annunciata (es. `192.168.1.0` + `255.255.255.0`)
- **Metric:** hop count (1–16)

Ogni messaggio può contenere fino a **25 rotte** per pacchetto.

---

## 7. Timer RIP

| Timer            | Valore default | Descrizione |
|------------------|:--------------:|-------------|
| Update Timer     | 30 s           | ogni quanto vengono inviati gli aggiornamenti |
| Invalid Timer    | 180 s          | se non si sente la rotta per 180s, metrica → 16 |
| Holddown Timer   | 180 s          | dopo che una rotta è diventata irraggiungibile, si ignorano aggiornamenti per questo periodo |
| Flush Timer      | 240 s          | dopo 240s senza aggiornamenti, la rotta viene rimossa dalla tabella |

---

## 8. Il problema del Count-to-Infinity

Questo è il problema più noto di RIP.

### Scenario

```
R1 --- R2 --- R3
              |
          192.168.3.0/24
```

R3 conosce `192.168.3.0/24` con metrica 0. R2 la conosce con metrica 1. R1 con metrica 2.

**Se il link R3 ↔ 192.168.3.0/24 cade:**

1. R3 imposta la metrica a 16 (irraggiungibile)
2. Prima che R3 invii l'aggiornamento, R2 invia a R3: *"io raggiungo 192.168.3.0/24 con metrica 1"*
3. R3 pensa: *"ah, R2 la conosce con 1 hop, quindi io la raggiungo con 2 hop"* → aggiorna a 2
4. R2 riceve da R3 metrica 2 → aggiorna a 3
5. Si continua così fino a 16 → **count to infinity**

### Soluzioni implementate in RIP

**Split Horizon:** R2 non annuncia a R3 le rotte che ha imparato da R3.

```
R2 impara 192.168.3.0/24 da R3
→ R2 NON reinvia questa rotta verso R3
→ il loop non si forma
```

**Poison Reverse:** variante di Split Horizon. R2 annuncia a R3 la rotta con metrica 16 (invece di non annunciarla), confermando esplicitamente che non è utilizzabile da quella direzione.

**Triggered Updates:** quando una rotta cambia, l'aggiornamento viene inviato **immediatamente**, senza aspettare i 30 secondi. Riduce il tempo di convergenza.

---

## 9. Configurazione RIPv2 su router Cisco (IOS)

```
R1(config)# router rip
R1(config-router)# version 2
R1(config-router)# no auto-summary
R1(config-router)# network 192.168.1.0
R1(config-router)# network 10.0.12.0
R1(config-router)# network 10.0.15.0
```

> `no auto-summary` disabilita la summarizzazione classful automatica — fondamentale in RIPv2 con VLSM.

Verifica:

```
R1# show ip route rip
R1# show ip protocols
R1# debug ip rip
```

Output di `show ip route rip` su R1 (dopo convergenza):

```
R    10.0.23.0/30 [120/1] via 10.0.12.2, 00:00:17, FastEthernet0/0
R    10.0.34.0/30 [120/2] via 10.0.12.2, 00:00:17, FastEthernet0/0
R    192.168.4.0/24 [120/3] via 10.0.12.2, 00:00:17, FastEthernet0/0
R    172.16.5.0/24  [120/1] via 10.0.15.2, 00:00:22, FastEthernet0/1
```

`[120/1]` → **120** è la administrative distance di RIP, **1** è la metrica (hop count).

---

## 10. RIP vs LPM – come lavorano insieme

```
[RIP costruisce la tabella]           [LPM sceglie quale rotta usare]

  R1 impara da R2:                      Pacchetto verso 10.0.23.5:
  10.0.23.0/30 via 10.0.12.2           
  10.0.0.0/8   via 10.0.12.2           → match /30: 10.0.23.0  ✅ (24 bit uguali... /30 = 30 bit)
                                        → match /8:  10.0.0.0   ✅ (8 bit uguali)
                                        → LPM sceglie /30  🏆
```

| Concetto | Funzione                        | Protocollo/meccanismo |
|----------|---------------------------------|-----------------------|
| RIP      | costruisce la routing table     | protocollo di routing |
| LPM      | seleziona la rotta da usare     | regola di lookup      |

---

## 11. Confronto RIP vs OSPF (cenni)

| Caratteristica       | RIP                   | OSPF                      |
|----------------------|-----------------------|---------------------------|
| Tipo                 | Distance-Vector       | Link-State                |
| Metrica              | Hop count             | Costo (basato su banda)   |
| Max dimensione rete  | 15 hop                | illimitato (teoricamente) |
| Convergenza          | lenta (minuti)        | rapida (secondi)          |
| Scalabilità          | piccole reti          | grandi reti enterprise    |
| Protocollo trasporto | UDP 520               | direttamente su IP (89)   |
| Aggiornamenti        | periodici (30s)       | triggered + flooding      |

---

## 12. Esercizi pratici

### Esercizio 1 – Calcolo hop count

Data la topologia:

```
[A] --- [B] --- [C]
         |
        [D] --- [E] --- [F]
```

Quanti hop da A a F?
- Percorso A→B→D→E→F = **4 hop**

RIP sceglierebbe questo percorso. Se esistesse anche A→B→C→F (3 hop), RIP preferirebbe A→B→C→F anche se il link C→F fosse lentissimo.

---

### Esercizio 2 – LPM con indirizzi reali

Un router ha questa tabella:

| Rete               | Next-hop     |
|--------------------|--------------|
| `10.0.0.0/8`       | `172.16.0.1` |
| `10.10.0.0/16`     | `172.16.0.2` |
| `10.10.10.0/24`    | `172.16.0.3` |
| `0.0.0.0/0`        | `172.16.0.4` |

Arriva un pacchetto per `10.10.10.55`. Quale rotta viene scelta?

**Soluzione:**

```
10.10.10.55 in binario: 00001010.00001010.00001010.00110111

/8  → 00001010                           ← 8 bit match ✅
/16 → 00001010.00001010                  ← 16 bit match ✅
/24 → 00001010.00001010.00001010         ← 24 bit match ✅
/0  → (nessun bit richiesto)             ← match ✅

Scelta: /24 → next-hop 172.16.0.3
```

---

### Esercizio 3 – Count-to-Infinity

Nella rete seguente il link tra R3 e la LAN `10.3.0.0/24` cade improvvisamente. Descrivi cosa succede senza Split Horizon e come Split Horizon risolve il problema.

```
R1 --- R2 --- R3 --- [LAN 10.3.0.0/24]
```

**Stato prima del guasto:**

| Router | Rotta          | Metrica | Next-hop |
|--------|----------------|:-------:|----------|
| R3     | 10.3.0.0/24   | 0       | diretto  |
| R2     | 10.3.0.0/24   | 1       | R3       |
| R1     | 10.3.0.0/24   | 2       | R2       |

**Senza Split Horizon** → count-to-infinity fino a 16 (vedi sezione 8).

**Con Split Horizon:**
- R2 non annuncia `10.3.0.0/24` verso R3 (perché l'ha imparata da R3)
- R3 segnala metrica 16 → R2 aggiorna a 16 → R1 aggiorna a 16
- Convergenza rapida, nessun loop

---

### Esercizio 4 – Progettazione indirizzamento per RIP

Hai 4 router in fila. Devi assegnare gli indirizzi ai link punto-punto usando `/30` (4 IP per link, 2 utilizzabili).

```
R1 --- R2 --- R3 --- R4
```

Usa il blocco `10.0.0.0/24`:

| Link    | Rete           | R-left      | R-right     | Broadcast    |
|---------|----------------|-------------|-------------|--------------|
| R1↔R2  | `10.0.0.0/30`  | `10.0.0.1`  | `10.0.0.2`  | `10.0.0.3`   |
| R2↔R3  | `10.0.0.4/30`  | `10.0.0.5`  | `10.0.0.6`  | `10.0.0.7`   |
| R3↔R4  | `10.0.0.8/30`  | `10.0.0.9`  | `10.0.0.10` | `10.0.0.11`  |

Perché `/30`? Con 2 bit di host:
- `00` → network address
- `01` → primo host
- `10` → secondo host
- `11` → broadcast

```
/30 in binario: 11111111.11111111.11111111.11111100
                                              ^^
                                          2 bit host
```

---

## 13. Quando usare RIP oggi

RIP è oggi considerato un protocollo **didattico e legacy**. È ancora usato in:

- reti molto piccole (< 10 router)
- ambienti di laboratorio e certificazioni (CCNA)
- dispositivi embedded con risorse limitate

In produzione è stato sostituito da **OSPF** (reti medie/grandi) e **BGP** (routing inter-AS su Internet).

---

## Riepilogo finale

| Concetto          | Valore/caratteristica |
|-------------------|-----------------------|
| Tipo              | Distance-Vector       |
| Metrica           | Hop count             |
| Max hop           | 15 (16 = irraggiungibile) |
| Update interval   | 30 secondi            |
| Invalid timer     | 180 secondi           |
| Flush timer       | 240 secondi           |
| Trasporto         | UDP porta 520         |
| Multicast RIPv2   | `224.0.0.9`           |
| Admin distance    | 120                   |
| Problema noto     | Count-to-Infinity     |
| Soluzioni         | Split Horizon, Poison Reverse, Triggered Updates |

---

> **Prossimo step consigliato:** OSPF – routing link-state con algoritmo di Dijkstra, metrica basata sulla banda, convergenza rapida e supporto per reti di grandi dimensioni.
