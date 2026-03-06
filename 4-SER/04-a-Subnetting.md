
# Subnetting

---

# Introduzione: Perché usare il Subnetting

Il **subnetting** nasce dall’esigenza di gestire in modo efficiente lo spazio di indirizzi IP.

Motivazioni principali:

* **Ottimizzazione degli indirizzi**: evitare sprechi quando una rete contiene meno host di quelli disponibili.
* **Isolamento dei segmenti di rete**: ogni reparto, ufficio o servizio può avere una propria subnet separata, migliorando sicurezza e gestione.
* **Controllo del traffico e performance**: subnet più piccole riducono il traffico broadcast e semplificano il routing interno.
* **Scalabilità e pianificazione**: permette di organizzare reti grandi in blocchi logici gestibili, pronti per espansioni future.

> 🔹 In pratica, il subnetting è uno strumento matematico che consente di **partizionare lo spazio IP** senza sprechi, spostando alcuni bit dalla parte host a quella di rete.

---

# 1️⃣ Obiettivo del Subnetting

Il **subnetting** consiste nel:

> Suddividere una rete IP in più sottoreti più piccole.

Matematicamente significa:

* Prendere alcuni bit dalla parte **host**
* Trasformarli in bit di **rete**

---

# 2️⃣ Struttura di un Indirizzo IPv4

Un IPv4 ha:

```
32 bit totali
```

Divisi in:

```
[ bit rete | bit host ]
```

Se abbiamo:

```
/24
```

Significa:

```
24 bit rete
8 bit host
```

Totale combinazioni host:

```
2^8 = 256 indirizzi
Host utilizzabili = 256 - 2 = 254
```

---

# 3️⃣ Principio Matematico del Subnetting

Se "prendiamo in prestito" `n` bit dalla parte host:

* Nuovo CIDR = CIDR originale + n
* Numero di sottoreti = 2^n
* Nuovi host per sottorete = 2^(bit_host - n)

---

# 4️⃣ Esempio Base

## Rete iniziale:

```
192.168.1.0/24
```

### Analisi binaria

Ultimo ottetto:

```
00000000
```

Host bit:

```
8 bit
```

Totale indirizzi:

```
2^8 = 256
```

---

# 5️⃣ Caso 1 – Dividere in 4 Sottoreti

## Domanda

Quanti bit servono per ottenere almeno 4 sottoreti?

Cerchiamo `n` tale che:

```
2^n ≥ 4
```

Calcolo:

```
2^1 = 2  → insufficiente
2^2 = 4  → sufficiente
```

👉 Servono 2 bit.

---

## Nuovo CIDR

```
/24 + 2 = /26
```

---

## Nuova subnet mask

```
/26 = 255.255.255.192
```

Ultimo ottetto:

```
11000000
```

---

## Host rimasti

Bit host originali: 8
Bit presi: 2

Nuovi host bit:

```
8 - 2 = 6
```

Indirizzi per sottorete:

```
2^6 = 64
```

Host utilizzabili:

```
64 - 2 = 62
```

---

# 6️⃣ Calcolo Incremento (Metodo Numerico)

Incremento =

```
256 - valore mask ultimo ottetto
```

Nel nostro caso:

```
256 - 192 = 64
```

Quindi le subnet partono ogni 64.

---

# 7️⃣ Sottoreti Generate

| Subnet | Network       | Broadcast     | Range Host  |
| ------ | ------------- | ------------- | ----------- |
| 1      | 192.168.1.0   | 192.168.1.63  | .1 – .62    |
| 2      | 192.168.1.64  | 192.168.1.127 | .65 – .126  |
| 3      | 192.168.1.128 | 192.168.1.191 | .129 – .190 |
| 4      | 192.168.1.192 | 192.168.1.255 | .193 – .254 |

---

# 8️⃣ Dimostrazione Binaria (Prima Subnet)

Mask:

```
11111111.11111111.11111111.11000000
```

Incremento binario:

```
00000000
01000000
10000000
11000000
```

Ogni incremento è:

```
64 in decimale
```

Perché:

```
2^6 = 64
```

---

# 9️⃣ Caso 2 – Dividere in 8 Sottoreti

Troviamo n:

```
2^n ≥ 8
2^3 = 8
```

👉 Servono 3 bit.

---

## Nuovo CIDR

```
/24 + 3 = /27
```

Host bit rimasti:

```
8 - 3 = 5
```

Indirizzi per subnet:

```
2^5 = 32
```

Host utilizzabili:

```
32 - 2 = 30
```

---

## Incremento

Mask /27:

```
255.255.255.224
```

Ultimo ottetto:

```
11100000
```

Incremento:

```
256 - 224 = 32
```

Subnet ogni 32:

```
0, 32, 64, 96, 128, 160, 192, 224
```

Totale 8 sottoreti.

---

# 🔟 Formula Generale del Subnetting

Dato:

* CIDR iniziale = /m
* Si prendono n bit

Allora:

Nuovo CIDR:

```
/(m + n)
```

Numero sottoreti:

```
2^n
```

Host per subnet:

```
2^(32 - (m+n)) - 2
```

Incremento:

```
256 - valore_mask_ottetto_interessato
```

Oppure matematicamente:

```
Incremento = 2^(bit_host_rimasti)
```

---

# 1️⃣1️⃣ Interpretazione Puramente Binaria

Subnetting =

> Spostare il confine tra rete e host verso destra.

Esempio:

Prima:

```
RRRRRRRR.HHHHHHHH
```

Dopo subnetting:

```
RRRRRRRR.RRHHHHHH
```

I bit presi diventano identificatore di sottorete.

---

# 1️⃣2️⃣ Schema Concettuale

```
Rete originale
│
│  prendo n bit host
▼
Nuovo CIDR = m + n
│
├── Numero subnet = 2^n
│
├── Host per subnet = 2^(host_originali - n) - 2
│
▼
Sottoreti indipendenti
```

---

# 1️⃣3️⃣ Concetto Chiave

Subnetting è:

* Algebra delle potenze di 2
* Manipolazione binaria
* Spostamento del confine rete/host
* Partizionamento dello spazio degli indirizzi

È una suddivisione matematica dello spazio:

```
Spazio totale = 2^(bit_host_originali)
Suddivisione:
2^n blocchi da 2^(bit_host_originali - n)
```


