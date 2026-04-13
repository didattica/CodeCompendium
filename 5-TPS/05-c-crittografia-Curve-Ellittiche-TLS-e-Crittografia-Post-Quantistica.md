# Crittografia — Parte 3: Curve Ellittiche, TLS e Crittografia Post-Quantistica
> **Livello:** 5° anno Liceo Scientifico / Informatico  
> **Durata:** 2 ore (120 minuti)  
> **Prerequisiti:** [Parte 1](crittografia_parte1.md), [Parte 2](crittografia-asimmetrica-e-RSA.md)

---

## Indice

1. [Perché le curve ellittiche?](#1-perché-le-curve-ellittiche)
2. [Curve ellittiche su ℝ](#2-curve-ellittiche-su-ℝ)
3. [Curve ellittiche su campi finiti](#3-curve-ellittiche-su-campi-finiti)
4. [ECDH — Diffie-Hellman su curve ellittiche](#4-ecdh--diffie-hellman-su-curve-ellittiche)
5. [ECDSA — Firma digitale su curve ellittiche](#5-ecdsa--firma-digitale-su-curve-ellittiche)
6. [TLS e HTTPS — Come tutto funziona insieme](#6-tls-e-https--come-tutto-funziona-insieme)
7. [Funzioni di Hash Crittografiche](#7-funzioni-di-hash-crittografiche)
8. [La minaccia quantistica e la crittografia post-quantistica](#8-la-minaccia-quantistica-e-la-crittografia-post-quantistica)
9. [Panoramica dei sistemi crittografici](#9-panoramica-dei-sistemi-crittografici)
10. [Esercizi finali e progetto](#10-esercizi-finali-e-progetto)

---

## 1. Perché le curve ellittiche?

RSA e Diffie-Hellman classico sono sicuri ma **costosi**: richiedono chiavi molto grandi.

**Confronto della lunghezza di chiave per sicurezza equivalente:**

| Sicurezza (bit) | RSA / DH | ECC (Curve Ellittiche) |
|---|---|---|
| 80 bit | 1024 bit | 160 bit |
| 112 bit | 2048 bit | 224 bit |
| 128 bit | 3072 bit | 256 bit |
| 256 bit | 15360 bit | 512 bit |

ECC con chiave di **256 bit** è equivalente a RSA con chiave di **3072 bit**.

**Vantaggi pratici:**
- Chiavi più piccole → meno memoria, meno banda, operazioni più veloci
- Fondamentale per dispositivi IoT, smartcard, telefoni
- Usata in TLS 1.3, Bitcoin, Signal, WhatsApp

---

## 2. Curve Ellittiche su ℝ

### 2.1 Equazione di Weierstrass

Una curva ellittica $E$ su $\mathbb{R}$ è l'insieme dei punti $(x, y) \in \mathbb{R}^2$ che soddisfano:

$$y^2 = x^3 + ax + b$$

con la condizione che il **discriminante** $\Delta = -16(4a^3 + 27b^2) \neq 0$ (per evitare singolarità — nodi e cuspidi).

Si aggiunge un **punto all'infinito** $\mathcal{O}$ che funge da elemento neutro del gruppo.

**Esempi di curve:**

| $a$ | $b$ | Curva |
|---|---|---|
| $-1$ | $0$ | $y^2 = x^3 - x$ |
| $0$ | $-1$ | $y^2 = x^3 - 1$ |
| $-3$ | $b$ | Forma usata da NIST (P-256) |

### 2.2 La legge di gruppo — addizione di punti

L'insieme dei punti di una curva ellittica forma un **gruppo abeliano** con la seguente operazione geometrica:

**Addizione $P + Q$** (per $P \neq Q$):
1. Traccia la retta passante per $P$ e $Q$
2. Trova il terzo punto di intersezione $R'$ con la curva
3. Rifletti $R'$ rispetto all'asse $x$: il risultato è $P + Q = R$

**Raddoppio $P + P = 2P$** (tangente):
1. Traccia la tangente alla curva in $P$
2. Trova il secondo punto di intersezione $R'$
3. Rifletti: $2P = R$

**Elemento neutro:** $\mathcal{O}$ (punto all'infinito). Per ogni punto $P$: $P + \mathcal{O} = P$.

**Inverso:** il simmetrico di $P = (x, y)$ è $-P = (x, -y)$. Si ha $P + (-P) = \mathcal{O}$.

### 2.3 Formule analitiche per l'addizione

Per $P = (x_1, y_1)$ e $Q = (x_2, y_2)$ con $P \neq \pm Q$:

$$\lambda = \frac{y_2 - y_1}{x_2 - x_1}$$

$$x_3 = \lambda^2 - x_1 - x_2$$

$$y_3 = \lambda(x_1 - x_3) - y_1$$

Per il raddoppio $P + P$ (con $y_1 \neq 0$):

$$\lambda = \frac{3x_1^2 + a}{2y_1}$$

poi stessa formula per $x_3, y_3$.

### 2.4 Moltiplicazione scalare

Definiamo la **moltiplicazione scalare** come addizione ripetuta:

$$nP = \underbrace{P + P + \cdots + P}_{n \text{ volte}}$$

Questo si calcola efficientemente con l'algoritmo **double-and-add** (analogo dello square-and-multiply):

```
Algoritmo double-and-add per nP:
Input: P, n (in binario: b_k b_{k-1} ... b_1 b_0)
Q ← O
for i from k downto 0:
    Q ← 2Q
    if b_i = 1:
        Q ← Q + P
return Q
```

Costo: $O(\log n)$ operazioni sul gruppo.

---

## 3. Curve Ellittiche su Campi Finiti

In crittografia non si usano le curve su $\mathbb{R}$ (i valori reali non sono rappresentabili esattamente), ma su **campi finiti** $\mathbb{F}_p$ con $p$ primo.

### 3.1 Definizione

La curva $E(\mathbb{F}_p)$ è l'insieme dei punti $(x, y) \in \mathbb{F}_p \times \mathbb{F}_p$ tali che:

$$y^2 \equiv x^3 + ax + b \pmod{p}$$

più il punto all'infinito $\mathcal{O}$.

Le formule per l'addizione rimangono **identiche**, ma tutte le operazioni sono in aritmetica modulare $\pmod{p}$.

### 3.2 Ordine del gruppo

Il **Teorema di Hasse** garantisce che:

$$|E(\mathbb{F}_p)| = p + 1 - t, \quad |t| \leq 2\sqrt{p}$$

Il numero di punti è circa $p$, e per $p$ di 256 bit si ottengono circa $2^{256}$ punti.

### 3.3 Il Problema del Logaritmo Discreto su Curve Ellittiche (ECDLP)

Dati un punto generatore $G$ e un punto $Q = kG$, trovare $k$ è il **Problema ECDLP**:

$$\text{ECDLP:} \quad \text{dato } Q = kG,\ \text{trovare } k$$

Il miglior algoritmo noto (Baby-step Giant-step, $\rho$ di Pollard) ha complessità:

$$O(\sqrt{|E(\mathbb{F}_p)|}) \approx O(2^{128}) \quad \text{per curve a 256 bit}$$

Questo è **esponenziale puro**, a differenza di RSA dove esiste l'algoritmo sub-esponenziale GNFS. Ecco perché le chiavi ECC possono essere molto più corte!

### 3.4 Curve standard

Le curve più usate:

| Nome | Campo | Ordine | Usata in |
|---|---|---|---|
| **P-256** (secp256r1) | $\mathbb{F}_p$, $p \approx 2^{256}$ | $\approx 2^{256}$ | TLS, HTTPS |
| **Curve25519** | $\mathbb{F}_p$, $p = 2^{255}-19$ | $\approx 2^{252}$ | Signal, WhatsApp, SSH |
| **secp256k1** | $\mathbb{F}_p$, $p \approx 2^{256}$ | $\approx 2^{256}$ | Bitcoin |

---

## 4. ECDH — Diffie-Hellman su Curve Ellittiche

### 4.1 Protocollo

Parametri pubblici: curva $E(\mathbb{F}_p)$, punto generatore $G$ di ordine $n$.

```
Alice                                    Bob
─────                                    ────
Sceglie a ∈ {1,...,n-1}                 Sceglie b ∈ {1,...,n-1}
  (segreto)                               (segreto)

Calcola A = aG         ──────────────►   Calcola B = bG
  (pubblico)           ◄──────────────     (pubblico)

Calcola K = aB = a(bG)                  Calcola K = bA = b(aG)
```

**Chiave condivisa:**

$$K = aB = a(bG) = abG = b(aG) = bA$$

La sicurezza si riduce all'ECDLP: trovare $a$ da $A = aG$ è computazionalmente difficile.

### 4.2 Forward Secrecy

In ECDH **effimero** (ECDHE), Alice e Bob generano una nuova coppia $(a, A)$ per ogni sessione e la scartano al termine.

**Proprietà:** anche se in futuro un avversario compromette la chiave privata a lungo termine, **non** può decifrare le sessioni passate registrate.

> TLS 1.3 usa esclusivamente ECDHE — la forward secrecy è **obbligatoria**.

---

## 5. ECDSA — Firma Digitale su Curve Ellittiche

ECDSA è la versione su curve ellittiche della firma DSA. È usata in Bitcoin, TLS, e molti altri sistemi.

### 5.1 Setup

Parametri: curva $E(\mathbb{F}_p)$, generatore $G$ di ordine $n$, funzione di hash $H$.

Chiave privata: $d \in \{1, \dots, n-1\}$ (segreto)  
Chiave pubblica: $Q = dG$ (pubblica)

### 5.2 Firma del messaggio $m$

1. Calcola $e = H(m)$ (hash del messaggio)
2. Scegli $k \in \{1, \dots, n-1\}$ **casuale e segreto** (il nonce)
3. Calcola $R = kG$, sia $r = x_R \pmod{n}$ (coordinata $x$ di $R$)
4. Calcola $s = k^{-1}(e + rd) \pmod{n}$
5. La firma è la coppia $(r, s)$

### 5.3 Verifica della firma $(r, s)$ su $m$

1. Calcola $e = H(m)$
2. Calcola $u_1 = s^{-1}e \pmod{n}$, $\quad u_2 = s^{-1}r \pmod{n}$
3. Calcola $X = u_1 G + u_2 Q$
4. La firma è valida se $x_X \equiv r \pmod{n}$

### 5.4 Avvertenza critica: il nonce deve essere casuale!

Se il nonce $k$ è riusato anche una sola volta per due messaggi diversi $(m_1, m_2)$, la chiave privata $d$ è **completamente recuperabile**:

$$s_1 - s_2 = k^{-1}(e_1 - e_2) \pmod{n}$$

$$k = \frac{e_1 - e_2}{s_1 - s_2} \pmod{n}$$

$$d = \frac{s_1 k - e_1}{r} \pmod{n}$$

> **Caso reale:** Sony PlayStation 3 (2010) usava un nonce costante in ECDSA. L'intera chiave privata fu recuperata, permettendo la firma non autorizzata di software.

---

## 6. TLS e HTTPS — Come tutto funziona insieme

TLS (Transport Layer Security) è il protocollo che protegge HTTPS, email, VPN e molto altro.

### 6.1 TLS 1.3 Handshake semplificato

```
Client                                        Server
──────                                        ──────
ClientHello                    ──────────►
  - versioni TLS supportate
  - curve ECC supportate
  - chiave pubblica ECDHE temporanea (A = aG)

                               ◄──────────    ServerHello
                                              - curva scelta
                                              - chiave pubblica ECDHE temporanea (B = bG)
                                              - certificato X.509 (firma ECDSA/RSA)
                                              - verifica firma (prova possesso chiave privata)

[Client verifica certificato]
[Entrambi calcolano K = abG]
[Da K derivano le chiavi simmetriche AES + HMAC]

Dati cifrati con AES-GCM  ◄──────────────►  Dati cifrati con AES-GCM
```

### 6.2 I componenti crittografici di TLS 1.3

| Componente | Algoritmo | Scopo |
|---|---|---|
| Scambio chiavi | ECDHE (P-256, X25519) | Stabilire chiave condivisa |
| Autenticazione server | ECDSA o RSA (firma) | Verificare identità server |
| Cifratura dati | AES-128-GCM o ChaCha20-Poly1305 | Riservatezza + integrità |
| MAC / Integrità | HMAC-SHA256 | Integrità aggiuntiva |
| Derivazione chiavi | HKDF (SHA-256) | Generare sottochiavi |

### 6.3 Il certificato X.509

Quando visiti `https://example.com`, il browser riceve un **certificato** contenente:
- Il nome del dominio
- La chiave pubblica del server
- La firma digitale di una **Certification Authority (CA)** fidata

La catena di fiducia:
```
Root CA (pre-installata nel tuo browser/OS)
    └── Intermediate CA (firmata dalla Root)
            └── Certificato del sito (firmato dall'Intermediate)
```

Il browser verifica ricorsivamente le firme fino alla Root CA.

---

## 7. Funzioni di Hash Crittografiche

Le funzioni di hash sono usate ovunque in crittografia: firma digitale, integrità dei dati, password, blockchain.

### 7.1 Definizione e proprietà

Una funzione di hash $H: \{0,1\}^* \to \{0,1\}^n$ è **crittograficamente sicura** se soddisfa:

| Proprietà | Definizione | Costo attacco |
|---|---|---|
| **Resistenza alla preimage** | Dato $h$, difficile trovare $m$ con $H(m) = h$ | $O(2^n)$ |
| **Resistenza alla seconda preimage** | Dato $m$, difficile trovare $m' \neq m$ con $H(m') = H(m)$ | $O(2^n)$ |
| **Resistenza alle collisioni** | Difficile trovare $m \neq m'$ con $H(m) = H(m')$ | $O(2^{n/2})$ (birthday attack) |

### 7.2 Il paradosso del compleanno

La probabilità di trovare una collisione in un insieme di output da $2^n$ valori dopo $k$ tentativi è:

$$P(\text{collisione}) \approx 1 - e^{-k^2 / 2^{n+1}}$$

Per avere $P \approx 50\%$, bastano circa $k \approx 2^{n/2}$ tentativi.

**Implicazione:** SHA-256 (output 256 bit) ha resistenza alle collisioni di $2^{128}$ operazioni — sicuro.

SHA-1 (output 160 bit) ha resistenza $2^{80}$ — **deprecato** dal 2017.

### 7.3 SHA-256 — cenni strutturali

SHA-256 usa la costruzione **Merkle-Damgård** con funzione di compressione basata su operazioni bit a bit:

- Il messaggio è diviso in blocchi da 512 bit
- Ogni blocco aggiorna uno stato interno di 256 bit con 64 round di operazioni
- L'hash finale è lo stato dopo l'ultimo blocco

Output di SHA-256 per alcune stringhe:
```
SHA256("hello")  = 2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824
SHA256("Hello")  = 185f8db32921bd46d35cc2e82d8ae361...  (completamente diverso!)
SHA256("")       = e3b0c44298fc1c149afbf4c8996fb924...  (hash della stringa vuota)
```

---

## 8. La Minaccia Quantistica e la Crittografia Post-Quantistica

### 8.1 Computers quantistici e crittografia

Un computer quantistico sfrutta **sovrapposizione** e **entanglement** per eseguire certi algoritmi esponenzialmente più veloci.

**Algoritmo di Shor (1994):** fattorizza $n$ e risolve il DLP in tempo **polinomiale**:

$$O\left((\log n)^3\right)$$

**Impatto:**

| Algoritmo | Sicurezza classica | Sicurezza con Shor |
|---|---|---|
| RSA-2048 | $\sim 2^{112}$ operazioni | **Rotto** |
| DH-2048 | $\sim 2^{112}$ operazioni | **Rotto** |
| ECDH-256 | $\sim 2^{128}$ operazioni | **Rotto** |
| AES-256 | $\sim 2^{256}$ operazioni | $\sim 2^{128}$ (Grover) — ancora sicuro |
| SHA-256 | $\sim 2^{128}$ collisioni | $\sim 2^{85}$ (Grover) — margine ridotto |

**Algoritmo di Grover:** offre un vantaggio quadratico nella ricerca, dimezzando i bit di sicurezza. Non rompe AES-256, ma riduce la sicurezza effettiva.

### 8.2 Lo stato attuale dei computer quantistici

I computer quantistici attuali (2024) hanno decine-centinaia di qubit **rumorosi** (NISQ — Noisy Intermediate-Scale Quantum).

Per rompere RSA-2048 servirebbero milioni di qubit **logici** (corretti dagli errori). Siamo ancora lontani, ma il rischio è reale nel lungo periodo.

> **Harvest now, decrypt later:** avversari potrebbero registrare oggi comunicazioni cifrate con RSA, per decifrarle quando avranno computer quantistici abbastanza potenti. Per questo la migrazione deve iniziare **ora**.

### 8.3 Crittografia Post-Quantistica (PQC)

Il NIST (National Institute of Standards and Technology) ha standardizzato nel 2024 i primi algoritmi PQC:

**Per scambio chiavi (KEM):**

**CRYSTALS-Kyber (ML-KEM)** — basato su **Learning With Errors (LWE)**:
- Si basa sulla difficoltà di risolvere sistemi lineari con rumore in reticoli
- Il problema LWE è difficile anche per computer quantistici
- Chiavi e ciphertext di circa 1-2 KB (più grandi di ECC ma gestibili)

**Per firma digitale:**

**CRYSTALS-Dilithium (ML-DSA)** e **FALCON** — basati su reticoli

**SPHINCS+** — basato su **funzioni di hash** (non su algebra, massima semplicità)

### 8.4 Il problema dei reticoli (intuizione)

Un **reticolo** $\Lambda$ in $\mathbb{R}^n$ è l'insieme di tutte le combinazioni intere di vettori base $\mathbf{b}_1, \dots, \mathbf{b}_n$:

$$\Lambda = \left\{ \sum_{i=1}^n a_i \mathbf{b}_i : a_i \in \mathbb{Z} \right\}$$

Il **Shortest Vector Problem (SVP):** trovare il vettore non nullo più corto in $\Lambda$.

Questo problema è difficile sia per computer classici che quantistici in dimensioni elevate ($n \geq 500$).

---

## 9. Panoramica dei Sistemi Crittografici

### 9.1 Mappa completa della crittografia moderna

```
CRITTOGRAFIA
├── SIMMETRICA (stessa chiave)
│   ├── Blocchi: AES, ChaCha20
│   └── Flusso: ChaCha20-Poly1305
│
├── ASIMMETRICA (chiave pubblica/privata)
│   ├── Basata su fattorizzazione
│   │   └── RSA (cifratura + firma)
│   ├── Basata su logaritmo discreto
│   │   ├── Diffie-Hellman (scambio chiavi)
│   │   └── ElGamal (cifratura)
│   └── Basata su curve ellittiche
│       ├── ECDH / ECDHE (scambio chiavi)
│       └── ECDSA, EdDSA (firma)
│
├── FUNZIONI DI HASH
│   └── SHA-2, SHA-3, BLAKE3
│
└── POST-QUANTISTICA
    ├── Reticoli: Kyber, Dilithium, FALCON
    └── Hash-based: SPHINCS+
```

### 9.2 Dove vivono nella vita reale

| Protocollo | Algoritmi usati |
|---|---|
| **HTTPS / TLS 1.3** | ECDHE + AES-GCM + ECDSA + SHA-256 |
| **SSH** | ECDH + AES + Ed25519 |
| **Signal / WhatsApp** | X25519 + AES + HMAC-SHA256 (Double Ratchet) |
| **Bitcoin** | secp256k1 + ECDSA + SHA-256 + RIPEMD-160 |
| **PGP / GPG** | RSA o ECC + AES + SHA-256 |
| **Passaporto elettronico** | RSA/ECDSA + AES |

---

## 10. Esercizi Finali e Progetto

### Esercizio 1 — Addizione su curve ellittiche
Sulla curva $y^2 = x^3 - x + 1 \pmod{7}$, verifica che $P = (0, 1)$ e $Q = (2, 1)$ sono sulla curva, poi calcola $P + Q$ usando le formule analitiche in $\mathbb{F}_7$.

### Esercizio 2 — ECDH su esempio piccolo
Usa la curva $y^2 = x^3 + 2x + 2 \pmod{17}$ con generatore $G = (5, 1)$:
- Alice sceglie $a = 3$, calcola $A = 3G$
- Bob sceglie $b = 7$, calcola $B = 7G$
- Verifica che $aB = bA$

### Esercizio 3 — Analisi di una connessione reale
Apri il browser, vai su `https://google.com`, clicca sul lucchetto → "La connessione è sicura" → "Certificato":
- Qual è l'algoritmo della chiave pubblica del certificato?
- Qual è la dimensione della chiave?
- Chi ha firmato il certificato (Certification Authority)?
- Qual è la data di scadenza?

### Esercizio 4 — Birthday Attack
Quanti hash SHA-256 devo calcolare mediamente per trovare una collisione? E per SHA-1? Esprimi la risposta come potenza di 2.

### Esercizio 5 — Riflessione finale
In 10 righe: spiega perché TLS 1.3 usa ECDHE invece di RSA per lo scambio delle chiavi, anche se il server ha già un certificato RSA. (Suggerimento: forward secrecy)

---

### Progetto facoltativo — Implementazione RSA in Python

```python
import random
from math import gcd

def is_prime(n, k=10):
    """Miller-Rabin primality test"""
    if n < 2: return False
    if n == 2: return True
    if n % 2 == 0: return False
    r, d = 0, n - 1
    while d % 2 == 0:
        r += 1
        d //= 2
    for _ in range(k):
        a = random.randrange(2, n - 1)
        x = pow(a, d, n)
        if x == 1 or x == n - 1:
            continue
        for _ in range(r - 1):
            x = pow(x, 2, n)
            if x == n - 1:
                break
        else:
            return False
    return True

def generate_prime(bits):
    """Genera un primo casuale di `bits` bit"""
    while True:
        p = random.getrandbits(bits) | (1 << bits - 1) | 1
        if is_prime(p):
            return p

def generate_rsa_keys(bits=512):
    p = generate_prime(bits // 2)
    q = generate_prime(bits // 2)
    n = p * q
    phi = (p - 1) * (q - 1)
    e = 65537
    d = pow(e, -1, phi)
    return (e, n), (d, n)  # pubblica, privata

def rsa_encrypt(m, public_key):
    e, n = public_key
    return pow(m, e, n)

def rsa_decrypt(c, private_key):
    d, n = private_key
    return pow(c, d, n)

# Test
pub, priv = generate_rsa_keys(512)
m = 42
c = rsa_encrypt(m, pub)
m2 = rsa_decrypt(c, priv)
print(f"Messaggio: {m}")
print(f"Cifrato:   {c}")
print(f"Decifrato: {m2}")
assert m == m2
```

**Estensioni possibili:**
1. Aggiungere la firma digitale
2. Implementare OAEP padding
3. Misurare i tempi di generazione delle chiavi al variare di `bits`

---

## Riepilogo del Percorso

| Parte | Argomenti | Ore |
|---|---|---|
| **Parte 1** | Fondamenti, aritmetica modulare, cifrari classici, OTP, problema scambio chiavi | 2h |
| **Parte 2** | One-way functions, Diffie-Hellman, RSA (generazione, cifratura, firma), sicurezza | 2h |
| **Parte 3** | Curve ellittiche, ECDH, ECDSA, TLS, hash, crittografia post-quantistica | 2h |

---

*← [Parte 2: RSA e Crittografia Asimmetrica](crittografia_parte2.md)*
