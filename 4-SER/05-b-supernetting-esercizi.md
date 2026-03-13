
# Esercizi di Supernetting

## Introduzione

Questi esercizi ti guideranno nella pratica del **supernetting**, partendo da scenari semplici fino a scenari più complessi.  
L’obiettivo è esercitarsi nel calcolo del **nuovo prefisso**, **subnet mask**, **range host** e **broadcast** per reti contigue.

---

## Esercizio 1 – Base

Reti contigue:

```

192.168.10.0/24
192.168.11.0/24

```

**Obiettivo:**

1. Creare un supernet unico.
2. Calcolare:
   - Nuovo prefisso CIDR
   - Subnet mask
   - Range host
   - Broadcast
3. Verificare l’allineamento degli indirizzi.

---

## Esercizio 2 – Facile

Reti contigue:

```

10.0.0.0/25
10.0.0.128/25
10.0.1.0/25
10.0.1.128/25

```

**Obiettivo:**

1. Aggregare le reti in un unico blocco.
2. Determinare:
   - Nuovo prefisso CIDR
   - Subnet mask
   - Range host
   - Broadcast
3. Mostrare il calcolo dei bit di rete ridotti.

---

## Esercizio 3 – Intermedio

Reti contigue:

```

172.16.4.0/24
172.16.5.0/24
172.16.6.0/24
172.16.7.0/24

```

**Obiettivo:**

1. Creare un supernet da queste quattro reti.
2. Calcolare:
   - Nuovo prefisso CIDR
   - Subnet mask
   - Range host
   - Broadcast
3. Verificare il corretto allineamento dei blocchi a livello di bit.

---

## Esercizio 4 – Avanzato

Reti contigue:

```

192.168.0.0/26
192.168.0.64/26
192.168.0.128/26
192.168.0.192/26
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26

```

**Obiettivo:**

1. Aggregare tutte le 8 reti in un unico supernet.
2. Calcolare:
   - Nuovo prefisso CIDR
   - Subnet mask
   - Range host
   - Broadcast
3. Evidenziare come cambiano i bit di rete e di host.

---

## Esercizio 5 – Esperto

Reti contigue:

```

10.10.0.0/24
10.10.1.0/24
10.10.2.0/24
10.10.3.0/24
10.10.4.0/24
10.10.5.0/24
10.10.6.0/24
10.10.7.0/24

```

**Obiettivo:**

1. Creare un supernet unico da 8 reti contigue.
2. Calcolare:
   - Nuovo prefisso CIDR
   - Subnet mask
   - Range host
   - Broadcast
3. Mostrare la verifica dell’allineamento degli indirizzi e spiegare il ragionamento dei bit di rete e host.

---

> 🔹 Suggerimento: Per tutti gli esercizi, verifica sempre che il **primo indirizzo della rete aggregata sia un multiplo del blocco** determinato dal nuovo prefisso, così da garantire l’allineamento corretto.
```
