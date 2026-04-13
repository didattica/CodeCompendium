# Crittografia — Parte 2: Crittografia Asimmetrica e RSA
> **Livello:** 5° anno Liceo Scientifico / Informatico  
> **Durata:** 2 ore (120 minuti)  
> **Prerequisiti:** [Parte 1](crittografia_parte1.md) — aritmetica modulare, Piccolo Teorema di Fermat

---

## Indice

1. [Funzioni a senso unico e trapdoor](#1-funzioni-a-senso-unico-e-trapdoor)
2. [Il protocollo Diffie-Hellman](#2-il-protocollo-diffie-hellman)
3. [Il problema RSA](#3-il-problema-rsa)
4. [Algoritmo RSA — Generazione delle chiavi](#4-algoritmo-rsa--generazione-delle-chiavi)
5. [RSA — Cifratura e decifratura](#5-rsa--cifratura-e-decifratura)
6. [Dimostrazione della correttezza di RSA](#6-dimostrazione-della-correttezza-di-rsa)
7. [Esempio numerico completo](#7-esempio-numerico-completo)
8. [Firma digitale con RSA](#8-firma-digitale-con-rsa)
9. [Sicurezza e limiti di RSA](#9-sicurezza-e-limiti-di-rsa)
10. [Esercizi](#10-esercizi)

---

## 1. Funzioni a senso unico e Trapdoor

### 1.1 Funzioni a senso unico (One-Way Functions)

Una funzione $f: X \to Y$ è detta **one-way** se:

- $f(x)$ è **facile** da calcolare per ogni $x \in X$
- $f^{-1}(y)$ è **computazionalmente difficile** da calcolare per quasi ogni $y \in Y$

"Facile" e "difficile" si intendono nel senso della **complessità computazionale**:
- Facile = tempo polinomiale in $|x|$
- Difficile = nessun algoritmo polinomiale noto (o dimostrabilmente non esistente)

**Nota:** L'esistenza delle one-way functions non è ancora dimostrata formalmente — è uno dei grandi problemi aperti della matematica (legato a $P \neq NP$). In pratica usiamo funzioni che *si comportano* come one-way.

### 1.2 Esempi di funzioni one-way candidate

**Moltiplicazione vs. fattorizzazione:**

$$f(p, q) = p \cdot q = n \quad \text{(facile)}$$
$$f^{-1}(n) = (p, q) \text{ tali che } p \cdot q = n \quad \text{(difficile per } n \text{ grande)}$$

Moltiplicare due primi è $O(\log^2 n)$. Fattorizzare $n$ non ha algoritmi polinomiali noti.

**Esponenziale modulare vs. logaritmo discreto:**

$$f(a, x) = a^x \pmod{p} \quad \text{(facile — esponenziazione rapida)}$$
$$f^{-1}(y) = \log_a y \pmod{p} \quad \text{(difficile — nessun algoritmo efficiente noto)}$$

### 1.3 Trapdoor Functions

Una **trapdoor function** è una funzione one-way $f$ tale che esiste un'informazione segreta $t$ (la *trapdoor*) che rende $f^{-1}$ facile:

$$f^{-1}(y) \text{ è difficile senza } t, \quad \text{facile con } t$$

> **Idea chiave della crittografia asimmetrica:** pubblica $f$ (chiunque può cifrare), tieni segreta $t$ (solo tu puoi decifrare).

---

## 2. Il Protocollo Diffie-Hellman

### 2.1 Setup pubblico

Si fissano e si rendono **pubblici** un primo $p$ e un generatore $g$ di $\mathbb{Z}_p^*$:

$$\mathbb{Z}_p^* = \{1, 2, \dots, p-1\}$$

$g$ è un **generatore primitivo** se $\{g^0, g^1, g^2, \dots, g^{p-2}\} = \mathbb{Z}_p^*$.

### 2.2 Scambio di chiavi

```
Alice                           Bob
──────                          ────
Sceglie a ∈ {2,...,p-2}        Sceglie b ∈ {2,...,p-2}
  (segreto)                       (segreto)

Calcola A = g^a mod p   ──────►  Calcola B = g^b mod p
        (pubblico)      ◄──────          (pubblico)

Calcola K = B^a mod p           Calcola K = A^b mod p
```

**Verifica:** entrambi ottengono la stessa chiave:

$$K = B^a \equiv (g^b)^a \equiv g^{ab} \equiv (g^a)^b \equiv A^b \pmod{p}$$

### 2.3 Sicurezza — Il Problema del Logaritmo Discreto

Un avversario che intercetta $g, p, A = g^a, B = g^b$ deve trovare $K = g^{ab}$ senza conoscere $a$ né $b$.

Il problema è computazionalmente equivalente a trovare $a$ da $A = g^a \pmod p$: il **Problema del Logaritmo Discreto (DLP)**.

$$\text{DLP:} \quad \text{dato } A = g^a \pmod{p},\ \text{trovare } a$$

Non esiste nessun algoritmo polinomiale noto per il DLP su gruppi ciclici ben scelti.

### 2.4 Esempio numerico

Parametri pubblici: $p = 23$, $g = 5$

| | Alice | Bob |
|---|---|---|
| Segreto privato | $a = 6$ | $b = 15$ |
| Valore pubblico | $A = 5^6 \bmod 23 = 8$ | $B = 5^{15} \bmod 23 = 19$ |
| Chiave condivisa | $K = 19^6 \bmod 23 = 2$ | $K = 8^{15} \bmod 23 = 2$ ✓ |

> **Nota:** nella pratica $p$ ha almeno 2048 bit (~617 cifre decimali).

---

## 3. Il problema RSA

RSA (Rivest–Shamir–Adleman, 1977) si basa sulla difficoltà di **fattorizzare** numeri interi grandi.

### 3.1 La funzione di Eulero

La **funzione di Eulero** $\phi(n)$ conta gli interi in $\{1, \dots, n\}$ coprimi con $n$:

$$\phi(n) = |\{k \in \{1,\dots,n\} : \gcd(k, n) = 1\}|$$

**Proprietà fondamentali:**

Per $p$ primo:
$$\phi(p) = p - 1$$

Per $p, q$ primi distinti:
$$\phi(p \cdot q) = (p-1)(q-1)$$

**Esempio:** $\phi(15) = \phi(3 \cdot 5) = 2 \cdot 4 = 8$

### 3.2 Il Teorema di Eulero

Se $\gcd(a, n) = 1$, allora:

$$a^{\phi(n)} \equiv 1 \pmod{n}$$

Questo generalizza il Piccolo Teorema di Fermat (che vale solo per $n$ primo).

**Corollario:** per ogni intero $k$:

$$a^{k \cdot \phi(n) + 1} \equiv a \pmod{n}$$

> Questo corollario è esattamente ciò che rende RSA corretto.

---

## 4. Algoritmo RSA — Generazione delle Chiavi

### Step 1 — Scegliere i primi

Scegli due numeri primi grandi $p$ e $q$ (nella pratica: 1024–2048 bit ciascuno) in modo casuale e indipendente.

### Step 2 — Calcolare il modulo

$$n = p \cdot q$$

$$\phi(n) = (p-1)(q-1)$$

### Step 3 — Scegliere l'esponente pubblico

Scegli $e$ tale che:

$$1 < e < \phi(n) \quad \text{e} \quad \gcd(e, \phi(n)) = 1$$

Il valore $e = 65537 = 2^{16} + 1$ è lo standard de facto (primo, pochi bit a 1 → esponenziazione rapida).

### Step 4 — Calcolare l'esponente privato

Trova $d$ tale che:

$$e \cdot d \equiv 1 \pmod{\phi(n)}$$

ovvero $d = e^{-1} \pmod{\phi(n)}$, calcolabile con l'algoritmo di Euclide esteso.

### Riepilogo delle chiavi

$$\text{Chiave pubblica:} \quad (e,\ n)$$
$$\text{Chiave privata:} \quad (d,\ n)$$

> $p$, $q$ e $\phi(n)$ vanno **eliminati** dopo la generazione: se un avversario li conosce, può calcolare $d$ facilmente.

---

## 5. RSA — Cifratura e Decifratura

### Cifratura (usa la chiave pubblica del destinatario)

Il messaggio $m$ deve essere un intero con $0 \le m < n$:

$$c = m^e \pmod{n}$$

### Decifratura (usa la chiave privata del destinatario)

$$m = c^d \pmod{n}$$

### Schema visivo

```
Alice (mittente)                          Bob (destinatario)
────────────────                          ────────────────────
Bob pubblica (e, n)                       Genera (p, q, e, d, n)
                                          Pubblica (e, n)
                                          Tiene segreto d

m → [  c = m^e mod n  ] → c ─────────► c → [  m = c^d mod n  ] → m
         cifratura                              decifratura
      (chiave pubblica di Bob)              (chiave privata di Bob)
```

---

## 6. Dimostrazione della Correttezza di RSA

**Teorema:** Per ogni $m$ con $\gcd(m, n) = 1$:

$$D(d,\ E(e,\ m)) = (m^e)^d \equiv m \pmod{n}$$

**Dimostrazione:**

Per costruzione, $e \cdot d \equiv 1 \pmod{\phi(n)}$, quindi esiste $k \in \mathbb{Z}$ tale che:

$$e \cdot d = k \cdot \phi(n) + 1$$

Allora, applicando il Teorema di Eulero (valido perché $\gcd(m, n) = 1$):

$$m^{ed} = m^{k\phi(n)+1} = \left(m^{\phi(n)}\right)^k \cdot m \equiv 1^k \cdot m \equiv m \pmod{n}$$

$\blacksquare$

**Nota tecnica:** La dimostrazione richiede $\gcd(m, n) = 1$. Questo è quasi sempre verificato nella pratica (la probabilità che un messaggio casuale sia divisibile per $p$ o $q$ è circa $1/p + 1/q \approx 0$). Esiste una versione più generale che usa il Teorema Cinese del Resto per gestire i casi degeneri.

---

## 7. Esempio Numerico Completo

Usiamo numeri piccoli per seguire tutti i passaggi a mano.

### Generazione delle chiavi

Scegli $p = 61$, $q = 53$:

$$n = 61 \times 53 = 3233$$

$$\phi(n) = (61-1)(53-1) = 60 \times 52 = 3120$$

Scegli $e = 17$ (verifica: $\gcd(17, 3120) = 1$ ✓)

Calcola $d = 17^{-1} \pmod{3120}$:

Usando Euclide esteso si ottiene $d = 2753$

**Verifica:** $17 \times 2753 = 46801 = 15 \times 3120 + 1$ ✓

$$\text{Chiave pubblica:} \quad (17,\ 3233)$$
$$\text{Chiave privata:} \quad (2753,\ 3233)$$

### Cifratura

Messaggio: $m = 65$

$$c = 65^{17} \pmod{3233}$$

Usando l'esponenziazione rapida (square-and-multiply):

$$65^{17} \equiv 2790 \pmod{3233}$$

### Decifratura

$$m = 2790^{2753} \pmod{3233} = 65 \checkmark$$

> In classe si può verificare con Python in pochi secondi: `pow(2790, 2753, 3233)`

---

## 8. Firma Digitale con RSA

RSA permette anche di **firmare** messaggi: dimostrare che un messaggio è stato creato dal possessore della chiave privata.

### Creazione della firma

Alice firma il messaggio $m$ con la sua **chiave privata**:

$$\sigma = m^{d_A} \pmod{n_A}$$

### Verifica della firma

Chiunque, usando la **chiave pubblica** di Alice $(e_A, n_A)$, può verificare:

$$m' = \sigma^{e_A} \pmod{n_A} \stackrel{?}{=} m$$

### Proprietà garantite

| Proprietà | Significato |
|---|---|
| **Autenticità** | Solo chi possiede $d_A$ ha potuto produrre $\sigma$ |
| **Integrità** | Se $m$ è modificato, $\sigma$ non sarà più valido |
| **Non ripudio** | Alice non può negare di aver firmato |

### Firma con hash (uso reale)

In pratica non si firma $m$ direttamente (RSA è lento), ma il suo **hash**:

$$\sigma = H(m)^d \pmod{n}$$

dove $H$ è una funzione di hash crittografica (SHA-256, SHA-3).

---

## 9. Sicurezza e Limiti di RSA

### 9.1 Su cosa si basa la sicurezza?

**Problema RSA:** dato $c = m^e \pmod n$ e la chiave pubblica $(e, n)$, trovare $m$.

Il problema RSA è **computazionalmente equivalente** (o almeno non più difficile) della fattorizzazione di $n$.

$$\text{Se sai fattorizzare } n = pq \implies \text{puoi calcolare } \phi(n) \implies \text{puoi trovare } d$$

Il miglior algoritmo di fattorizzazione noto (General Number Field Sieve) ha complessità:

$$O\left(\exp\left(c \cdot (\log n)^{1/3} (\log \log n)^{2/3}\right)\right)$$

Questa è sub-esponenziale ma super-polinomiale: per $n$ di 2048 bit, impraticabile con hardware classico.

### 9.2 Dimensioni delle chiavi raccomandate

| Anno | Dimensione minima raccomandata |
|---|---|
| Fino al 2010 | 1024 bit |
| 2010–2030 | 2048 bit |
| Dopo il 2030 | 3072 bit o più |

### 9.3 Attacchi pratici da evitare

- **Mai riusare** $(p, q)$ o $\phi(n)$ tra chiavi diverse
- **Mai usare** $e$ piccolo senza padding (vulnerabilità di Coppersmith)
- **Sempre usare** OAEP (Optimal Asymmetric Encryption Padding) nella pratica
- **Generare** $p$ e $q$ con un generatore di numeri casuali crittograficamente sicuro (CSPRNG)

### 9.4 La minaccia quantistica

L'algoritmo di Shor (1994), se eseguito su un computer quantistico sufficientemente grande, fattorizza $n$ in tempo:

$$O\left((\log n)^2 \cdot \log \log n\right)$$

ovvero **polinomiale**! Questo renderebbe RSA e Diffie-Hellman completamente insicuri.

> La crittografia **post-quantistica** (NIST sta già standardizzando nuovi algoritmi come CRYSTALS-Kyber e CRYSTALS-Dilithium) è pensata per resistere anche ai computer quantistici. Vedremo cenni nella Parte 3.

---

## 10. Esercizi

### Esercizio 1 — Generazione chiavi RSA (piccola)
Con $p = 11$, $q = 13$:
- Calcola $n$ e $\phi(n)$
- Scegli un $e$ valido
- Calcola $d$
- Cifra $m = 7$ e verifica la decifratura

### Esercizio 2 — Verifica del Teorema di Eulero
Verifica che $3^{\phi(10)} \equiv 1 \pmod{10}$.  
Calcola $\phi(10)$, poi verifica con la formula.

### Esercizio 3 — Firma digitale
Con la chiave dell'Esercizio 1, simula la firma del messaggio $m = 5$:
- Calcola $\sigma = m^d \pmod n$
- Verifica che $\sigma^e \equiv m \pmod n$

### Esercizio 4 — Ragionamento sulla sicurezza
Supponi che un avversario conosca $n = 3233$ e riesca a fattorizzarlo come $61 \times 53$. Sapendo che la chiave pubblica è $(e = 17, n = 3233)$, come calcolerebbe $d$?

### Esercizio 5 — Python (per casa)
```python
# Verifica RSA con Python
p, q = 61, 53
n = p * q
phi_n = (p-1) * (q-1)
e = 17
d = pow(e, -1, phi_n)   # inverso modulare in Python 3.8+
m = 42
c = pow(m, e, n)
m_dec = pow(c, d, n)
print(f"Originale: {m}, Cifrato: {c}, Decifrato: {m_dec}")
assert m == m_dec, "Errore!"
```

---

*← [Parte 1: Fondamenti](crittografia_parte1.md) | → [Parte 3: Curve Ellittiche e Applicazioni Reali](crittografia_parte3.md)*
