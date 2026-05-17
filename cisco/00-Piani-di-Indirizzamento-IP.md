# 📡 Piani di Indirizzamento IP — Subnetting FLSM con Classe C Privata

> Guida di riferimento per la progettazione di sottoreti a partire da un indirizzo **192.168.x.0/24**,  
> con la tecnica **FLSM (Fixed Length Subnet Masking)**.

---

## 🧮 Concetti Base

Partendo da un indirizzo **/24** si hanno a disposizione **8 bit** per la parte host (256 indirizzi totali).  
Per ricavare più sottoreti si "prestano" bit dalla parte host verso la parte rete:

| Bit prestati | Sottoreti ottenute | Nuova prefix | Nuova subnet mask     | Host utilizzabili/sottorete |
|:---:|:---:|:---:|:---:|:---:|
| 1 | 2  | /25 | 255.255.255.128 | 126 |
| 2 | 4  | /26 | 255.255.255.192 | 62  |
| 3 | 8  | /27 | 255.255.255.224 | 30  |
| 4 | 16 | /28 | 255.255.255.240 | 14  |

> [!NOTE]
> La formula generale è: **sottoreti = 2ⁿ** e **host per sottorete = 2⁽⁸⁻ⁿ⁾ − 2**,  
> dove *n* è il numero di bit prestati. Si sottraggono sempre 2 indirizzi (network address e broadcast).

> [!TIP]
> Tutti gli esempi usano `192.168.10.0` come base. Sostituisci `10` con qualsiasi valore da `0` a `255`  
> per adattare il piano al tuo indirizzo scelto (es. `192.168.5.0`, `192.168.100.0`, ecc.).  
> L'indirizzo scelto deve sempre appartenere al range privato classe C: `192.168.0.0 – 192.168.255.255`.

---

## 🔵 Caso 1 — 2 Sottoreti

### Come si ottengono 2 sottoreti

Si presta **1 bit** dalla parte host:

```
Indirizzo base : 192.168.10.0  /24
Bit prestati   : 1
Nuova prefix   : /25
Subnet mask    : 255.255.255.128
Blocco         : 128 indirizzi per sottorete
Host per rete  : 2⁷ − 2 = 126
```

### Piano di indirizzamento — base `192.168.10.0/24` → `/25`

| # | Network Address      | Subnet Mask     | First Host    | Last Host      | Broadcast      |
|---|----------------------|-----------------|---------------|----------------|----------------|
| 1 | 192.168.10.0 /25     | 255.255.255.128 | 192.168.10.1  | 192.168.10.126 | 192.168.10.127 |
| 2 | 192.168.10.128 /25   | 255.255.255.128 | 192.168.10.129| 192.168.10.254 | 192.168.10.255 |

> [!TIP]
> Con `/25` ogni sottorete supporta fino a **126 host**. Ideale per reti di medie dimensioni  
> divise in due segmenti (es. piano terra e primo piano, uffici e laboratori).

### Come leggere il blocco

```
Rete 1 → da 192.168.10.0   a 192.168.10.127   (blocco di 128)
Rete 2 → da 192.168.10.128 a 192.168.10.255   (blocco di 128)
```

---

## 🟡 Caso 2 — 3 Sottoreti

### Come si ottengono (almeno) 3 sottoreti

Con 3 sottoreti non esiste una potenza di 2 esatta: occorre prestare **2 bit** (che danno **4 sottoreti**) e **utilizzarne solo 3**, lasciando la quarta inutilizzata oppure assegnandola a un uso futuro.

```
Indirizzo base : 192.168.10.0  /24
Bit prestati   : 2
Nuova prefix   : /26
Subnet mask    : 255.255.255.192
Blocco         : 64 indirizzi per sottorete
Host per rete  : 2⁶ − 2 = 62
Sottoreti disp.: 4  (si usano le prime 3)
```

### Piano di indirizzamento — base `192.168.10.0/24` → `/26`

| # | Network Address       | Subnet Mask     | First Host    | Last Host      | Broadcast      |
|---|-----------------------|-----------------|---------------|----------------|----------------|
| 1 | 192.168.10.0 /26      | 255.255.255.192 | 192.168.10.1  | 192.168.10.62  | 192.168.10.63  |
| 2 | 192.168.10.64 /26     | 255.255.255.192 | 192.168.10.65 | 192.168.10.126 | 192.168.10.127 |
| 3 | 192.168.10.128 /26    | 255.255.255.192 | 192.168.10.129| 192.168.10.190 | 192.168.10.191 |
| ~~4~~ | ~~192.168.10.192 /26~~ | ~~255.255.255.192~~ | — | — | ~~192.168.10.255~~ |

> [!NOTE]
> La riga 4 (barrata) è la sottorete matematicamente disponibile ma **non assegnata** in questo piano.  
> Può essere riservata per espansioni future o per un collegamento WAN/punto-punto.

> [!TIP]
> Con `/26` ogni sottorete supporta fino a **62 host**. Adatto per laboratori scolastici,  
> piccoli uffici o reti Packet Tracer con switch separati per reparto.

### Come leggere il blocco

```
Rete 1 → da 192.168.10.0   a 192.168.10.63    (blocco di 64)
Rete 2 → da 192.168.10.64  a 192.168.10.127   (blocco di 64)
Rete 3 → da 192.168.10.128 a 192.168.10.191   (blocco di 64)
```

---

## 🔴 Caso 3 — 4 Sottoreti

### Come si ottengono 4 sottoreti

Si prestano **2 bit** dalla parte host (stessa prefix del caso precedente, ma si usano **tutte e 4** le sottoreti):

```
Indirizzo base : 192.168.10.0  /24
Bit prestati   : 2
Nuova prefix   : /26
Subnet mask    : 255.255.255.192
Blocco         : 64 indirizzi per sottorete
Host per rete  : 2⁶ − 2 = 62
Sottoreti disp.: 4  (tutte utilizzate)
```

### Piano di indirizzamento — base `192.168.10.0/24` → `/26`

| # | Network Address       | Subnet Mask     | First Host    | Last Host      | Broadcast      |
|---|-----------------------|-----------------|---------------|----------------|----------------|
| 1 | 192.168.10.0 /26      | 255.255.255.192 | 192.168.10.1  | 192.168.10.62  | 192.168.10.63  |
| 2 | 192.168.10.64 /26     | 255.255.255.192 | 192.168.10.65 | 192.168.10.126 | 192.168.10.127 |
| 3 | 192.168.10.128 /26    | 255.255.255.192 | 192.168.10.129| 192.168.10.190 | 192.168.10.191 |
| 4 | 192.168.10.192 /26    | 255.255.255.192 | 192.168.10.193| 192.168.10.254 | 192.168.10.255 |

> [!TIP]
> Con 4 sottoreti e `/26` si ottimizza l'uso dell'intero spazio /24: nessun indirizzo viene sprecato.  
> Assegna ogni sottorete a un segmento fisico distinto (switch, reparto, piano dell'edificio).

> [!IMPORTANT]
> Il **default gateway** da configurare su ogni end device deve essere l'indirizzo IP  
> assegnato all'interfaccia del router nella **stessa sottorete** del dispositivo,  
> solitamente il **first host** di ogni rete (es. `192.168.10.1`, `192.168.10.65`, …).

### Come leggere il blocco

```
Rete 1 → da 192.168.10.0   a 192.168.10.63    (blocco di 64)
Rete 2 → da 192.168.10.64  a 192.168.10.127   (blocco di 64)
Rete 3 → da 192.168.10.128 a 192.168.10.191   (blocco di 64)
Rete 4 → da 192.168.10.192 a 192.168.10.255   (blocco di 64)
```

---

## 📊 Riepilogo Comparativo

| Sottoreti richieste | Bit prestati | Prefix | Subnet Mask     | Host/rete | Blocco |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 2 | 1 | /25 | 255.255.255.128 | 126 | 128 |
| 3 | 2 | /26 | 255.255.255.192 | 62  | 64  |
| 4 | 2 | /26 | 255.255.255.192 | 62  | 64  |

> [!NOTE]
> Per 3 e 4 sottoreti si usa la **stessa subnet mask `/26`**: la differenza sta nell'utilizzo  
> della quarta sottorete (ignorata per 3, assegnata per 4).

---

## 🔢 Come Calcolare Qualsiasi Piano — Regola Rapida

```
1. Scegli un indirizzo: 192.168.X.0
2. Determina quante sottoreti servono → trova il più piccolo 2ⁿ ≥ sottoreti
3. Calcola la nuova prefix: /24 + n
4. Calcola il blocco: 256 / 2ⁿ
5. Elenca le reti sommando il blocco all'ottetto finale:
   .0 → .blocco → .blocco×2 → .blocco×3 → …
6. Per ogni rete:
   - Network = primo indirizzo del blocco
   - First host = Network + 1
   - Broadcast = primo indirizzo del blocco successivo − 1
   - Last host = Broadcast − 1
```

> [!CAUTION]
> Non assegnare mai ai dispositivi l'indirizzo di **network** né quello di **broadcast**:  
> sono riservati e il loro uso causa malfunzionamenti nella comunicazione di rete.

---

*Riferimento per esercitazioni Cisco Packet Tracer — Subnetting FLSM Classe C Privata*
