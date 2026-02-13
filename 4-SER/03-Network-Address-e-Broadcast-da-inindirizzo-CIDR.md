# Calcolo di Network Address e Broadcast da un indirizzo CIDR

## 1. Introduzione

Un indirizzo IP scritto nel formato:

```

xxx.xxx.xxx.xxx/nn

```

segue il modello **CIDR (Classless Inter-Domain Routing)**.

Esempio:

```

192.168.1.34/27

```

Questo formato contiene **tutte le informazioni necessarie** per individuare:

- la rete
- gli host
- il broadcast

---

## 2. Concetti fondamentali

### Indirizzo IP

Un indirizzo IPv4 è composto da **32 bit**, divisi in 4 ottetti:

```

# 192.168.1.34

11000000.10101000.00000001.00100010

```

---

### CIDR (/nn)

Il numero dopo lo slash indica:

```

numero di bit di rete

```

Quindi:

```

/nn = bit di NETWORK
32 - nn = bit di HOST

```

Esempio:

```

/27 → 27 bit rete + 5 bit host

```

---

## 3. Subnet Mask

Il CIDR corrisponde ad una maschera fatta così:

- bit rete → 1
- bit host → 0

Esempio:

```

/27

```

Mask binaria:

```

11111111.11111111.11111111.11100000

```

Mask decimale:

```

255.255.255.224

```

---

## 4. Network Address

Il **Network Address** identifica la rete.

👉 Serve ai router per instradare i pacchetti.

Un router non invia i pacchetti al singolo host, ma alla **rete di destinazione**.

Si ottiene facendo:

```

IP AND Subnet Mask

```

Operazione AND:

| Bit IP | Bit Mask | Risultato |
|--------|----------|-----------|
|   1    |    1     |     1     |
|   1    |    0     |     0     |
|   0    |    1     |     0     |
|   0    |    0     |     0     |

---

## 5. Broadcast Address

Il **Broadcast Address** serve per:

👉 inviare un pacchetto a **tutti gli host della rete**

Si ottiene:

- lasciando invariati i bit di rete
- mettendo a **1 tutti i bit host**

---

## 6. Procedura passo passo

Dato:

```

IP /nn

```

### Step 1
Trova:

```

bit rete = nn
bit host = 32 - nn

```

---

### Step 2
Scrivi la subnet mask in binario.

---

### Step 3
Converti l’IP in binario.

---

### Step 4
Esegui AND bit a bit:

```

IP AND MASK = NETWORK ADDRESS

```

---

### Step 5
Per il Broadcast:

metti tutti i bit host = 1

---

## 7. Esempi

---

### Esempio 1

```

IP: 192.168.1.34/27

```

Bit:

```

27 rete
5 host

```

Mask:

```

# 255.255.255.224

11100000 (ultimo ottetto)

```

IP:

```

34 = 00100010

```

AND:

```

00100010
11100000
========

00100000

```

Network:

```

192.168.1.32

```

Broadcast:

Host = 5 bit → tutti a 1

```

00100000 → 00111111

```
```

192.168.1.63

```

---

### Esempio 2

```

IP: 10.0.5.130/25

```

Mask:

```

# 255.255.255.128

10000000

```

IP:

```

130 = 10000010

```

AND:

```

10000010
10000000
========

10000000

```

Network:

```

10.0.5.128

```

Broadcast:

```

10.0.5.255

```

---

### Esempio 3

```

IP: 172.16.20.77/26

```

Mask:

```

# 255.255.255.192

11000000

```

IP:

```

77 = 01001101

```

AND:

```

01001101
11000000
========

01000000

```

Network:

```

172.16.20.64

```

Broadcast:

```

172.16.20.127

```

---

## 8. Conclusione

Da un indirizzo:

```

IP/nn

```

possiamo sempre determinare:

- Network Address → identifica la rete
- Broadcast → comunica con tutti gli host

Il metodo universale è:

```

NETWORK = IP AND MASK
BROADCAST = NETWORK + host tutti a 1

