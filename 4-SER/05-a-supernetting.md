# Supernetting (Aggregation di Reti IP)

## Introduzione

Il **Supernetting** è una tecnica di gestione degli indirizzi IP che permette di **unire più reti contigue in un blocco unico**, riducendo il numero di entry necessarie nelle tabelle di routing.

Se nel **subnetting** si divide una rete grande in subnet più piccole, nel **supernetting** facciamo l’opposto: aggregiamo reti più piccole per creare una rete più grande e più semplice da gestire.

### Perché il supernetting è utile

* Riduce le **dimensioni delle tabelle di routing** in router e ISP.
* Migliora la **scalabilità delle reti** grandi o dei backbone.
* Permette di trattare blocchi contigui come un’unica rete logica, semplificando la gestione.

> 🔹 Nota: il subnetting è il concetto opposto e si basa sulla divisione di bit di host in più subnet. Il supernetting invece **riduce i bit di rete**, aumentando i bit host disponibili.

---

## Concetti fondamentali

Ogni indirizzo IPv4 ha 32 bit:

* **Bit di rete**: identificano la rete
* **Bit host**: identificano il dispositivo nella rete

Nel supernetting, si **riduce il numero di bit di rete** per combinare reti contigue, aumentando il numero di bit host e quindi la dimensione del blocco aggregato.

### Regola pratica

Per aggregare `2^n` reti contigue:

1. Identificare il numero di reti da unire.
2. Calcolare `n = log2(numero_reti)`.
3. Ridurre il prefisso CIDR originale di `n` bit:

```
Nuovo CIDR = CIDR originale - n
```

---

## Esempio pratico

### Scenario

Abbiamo quattro reti contigue:

```
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
```

**Obiettivo:** creare un supernet unico.

---

### Passaggio 1: Numero reti da unire

```
Numero reti = 4
```

---

### Passaggio 2: Calcolo bit di rete da ridurre

```
2^n = 4 → n = 2
```

---

### Passaggio 3: Nuovo prefisso

```
Nuovo CIDR = /24 - 2 = /22
```

* Subnet mask: `255.255.252.0`
* Indirizzo di rete: `192.168.0.0/22`
* Range host: `192.168.0.1 – 192.168.3.254`
* Broadcast: `192.168.3.255`

> 🔹 Osservazione a livello di bit: le reti originali avevano 24 bit di rete e 8 bit host. Unendo le 4 reti contigue, riduciamo i bit di rete a 22, aumentando i bit host a 10, ottenendo un blocco unico più grande.

---

## Esempio avanzato: aggregazione di 8 reti /25

Reti contigue:

```
10.0.0.0/25
10.0.0.128/25
10.0.1.0/25
10.0.1.128/25
10.0.2.0/25
10.0.2.128/25
10.0.3.0/25
10.0.3.128/25
```

### Passaggio 1: Numero reti da aggregare

```
Numero reti = 8 → 2^3 = 8 → n = 3 bit da ridurre
```

### Passaggio 2: Nuovo prefisso

```
/25 - 3 = /22
```

* Subnet mask: `255.255.252.0`
* Indirizzo di rete: `10.0.0.0/22`
* Range host: `10.0.0.1 – 10.0.3.254`
* Broadcast: `10.0.3.255`

> 🔹 In termini di bit: prima ogni rete /25 aveva 25 bit di rete e 7 bit host. Dopo il supernetting, i bit di rete diventano 22 e i bit host 10, creando un blocco più grande e aggregato.

---

## Regole pratiche per il supernetting

1. Le reti devono essere **contigue**.
2. Il numero di reti deve essere **potenza di 2** (2, 4, 8, …).
3. Ridurre il prefisso di **log2(numero_reti)** bit.
4. Verificare che gli indirizzi siano **allineati** correttamente (multipli del nuovo incremento).

---

## Confronto Subnetting vs Supernetting

| Concetto     | Obiettivo                           | Bit di rete | Bit host | Uso principale                     |
| ------------ | ----------------------------------- | ----------- | -------- | ---------------------------------- |
| Subnetting   | Dividere rete in subnet più piccole | +           | -        | Gestione interna e isolamento      |
| Supernetting | Aggregare reti contigue             | -           | +        | Ridurre routing e semplificare ISP |

---

## Esercizio pratico consigliato

Reti contigue:

```
172.16.0.0/24
172.16.1.0/24
172.16.2.0/24
172.16.3.0/24
```

* Obiettivo: creare un supernet unico.
* Calcolare: nuovo prefisso, subnet mask, range host, broadcast.
* Verificare allineamento degli indirizzi a livello di bit.

---
<!--
Se vuoi, posso creare **una versione “supernetting con tabelle e bit” già risolta** con diversi esempi, pronta da usare come esercizi GitHub per studenti.

Vuoi che lo faccia?
-->
