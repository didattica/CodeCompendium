# Crittografia — Parte 1: Fondamenti e Crittografia Simmetrica
> **Livello:** 5° anno Liceo Scientifico / Informatico  
> **Durata:** 2 ore (120 minuti)  
> **Prerequisiti:** Aritmetica modulare di base, concetto di algoritmo, nozioni di teoria degli insiemi

---

## Indice

1. [Perché studiare la crittografia?](#1-perché-studiare-la-crittografia)
2. [Definizioni fondamentali](#2-definizioni-fondamentali)
3. [Aritmetica modulare — Ripasso essenziale](#3-aritmetica-modulare--ripasso-essenziale)
4. [Crittografia simmetrica classica](#4-crittografia-simmetrica-classica)
5. [Crittografia simmetrica moderna — cenni](#5-crittografia-simmetrica-moderna--cenni)
6. [Il problema dello scambio delle chiavi](#6-il-problema-dello-scambio-delle-chiavi)
7. [Esercizi](#7-esercizi)

---

## 1. Perché studiare la crittografia?

La crittografia è la scienza che studia le tecniche per rendere un messaggio incomprensibile a chi non è autorizzato a leggerlo.

Oggi è ovunque:
- HTTPS e TLS proteggono le connessioni web
- SSH protegge l'accesso remoto ai server
- Le firme digitali garantiscono l'autenticità dei documenti
- Le criptovalute usano crittografia per garantire le transazioni

> **Obiettivo delle 6 ore:** comprendere i principi matematici che rendono sicure queste tecnologie, dalla crittografia simmetrica fino alla crittografia asimmetrica e alle curve ellittiche.

---


## 2. Definizioni fondamentali

| Termine | Definizione |
|---|---|
| **Plaintext** $m \in \mathcal{M}$ | Messaggio originale in chiaro |
| **Ciphertext** $c \in \mathcal{C}$ | Messaggio cifrato |
| **Chiave** $k \in \mathcal{K}$ | Parametro segreto dell'algoritmo |
| **Cifratura** $E_k$ | Funzione che trasforma $m$ in $c$: $c = E_k(m)$ |
| **Decifratura** $D_k$ | Funzione che ricostruisce $m$: $m = D_k(c)$ |
| **Crittanalisi** | Studio delle tecniche per violare un sistema crittografico |

---

### Spazi fondamentali

- $\mathcal{M}$: insieme di tutti i possibili messaggi (plaintext)  
- $\mathcal{C}$: insieme di tutti i possibili messaggi cifrati  
- $\mathcal{K}$: insieme di tutte le possibili chiavi  

---

### Definizione di sistema crittografico

Un sistema crittografico è una quintupla:

$$
(\mathcal{M}, \mathcal{C}, \mathcal{K}, E, D)
$$

dove:

- $E$ è l’insieme delle funzioni di cifratura $E_k: \mathcal{M} \to \mathcal{C}$
- $D$ è l’insieme delle funzioni di decifratura $D_k: \mathcal{C} \to \mathcal{M}$

---

### Proprietà fondamentale (correttezza)

$$
D_k(E_k(m)) = m \quad \forall m \in \mathcal{M},\ k \in \mathcal{K}
$$

👉 In parole semplici:  
se cifri un messaggio e poi lo decifri con la stessa chiave, ottieni esattamente il messaggio originale.

---

### Nota intuitiva

Si può vedere così:

```

messaggio (m) --[cifratura con k]--> (c) --[decifratura con k]--> (m)

```

La crittografia funziona correttamente solo se questo “andata e ritorno” restituisce sempre il messaggio iniziale.

### Principio di Kerckhoffs (1883)

> *"La sicurezza di un sistema crittografico non deve dipendere dalla segretezza dell'algoritmo, ma solo dalla segretezza della chiave."*

Questo principio è ancora fondamentale oggi: tutti gli algoritmi moderni (AES, RSA, …) sono pubblici. La sicurezza risiede **solo nella chiave**.

---

## 3. Aritmetica Modulare — Ripasso Essenziale

### 3.1 Definizione di congruenza

Dati $a, b \in \mathbb{Z}$ e $n \in \mathbb{N}^+$, si dice che $a$ è **congruente** a $b$ modulo $n$ se $n \mid (a - b)$:

$$a \equiv b \pmod{n} \iff n \mid (a - b)$$

**Esempio:**
$$17 \equiv 5 \pmod{6} \quad \text{perché } 6 \mid (17 - 5) = 12$$

### 3.2 Operazioni in $\mathbb{Z}_n$

L'insieme $\mathbb{Z}_n = \{0, 1, 2, \dots, n-1\}$ con le operazioni di addizione e moltiplicazione modulo $n$ forma un **anello**.

$$\mathbb{Z}_{26} = \{0, 1, 2, \dots, 25\}$$

Questo è lo spazio naturale per la crittografia classica (26 lettere dell'alfabeto).

### 3.3 Inverso moltiplicativo

$a$ ammette inverso moltiplicativo in $\mathbb{Z}_n$ **se e solo se** $\gcd(a, n) = 1$:

$$a \cdot a^{-1} \equiv 1 \pmod{n}$$

**Esempio:** In $\mathbb{Z}_{26}$, $a = 3$:

$$3 \cdot 9 = 27 \equiv 1 \pmod{26} \implies 3^{-1} \equiv 9 \pmod{26}$$

**Esercizio rapido:** trovare $7^{-1} \pmod{26}$.

### 3.4 Algoritmo di Euclide Esteso

Per calcolare l'inverso, si usa l'algoritmo di Euclide esteso che trova $x, y$ tali che:

$$ax + ny = \gcd(a, n)$$

Se $\gcd(a,n) = 1$, allora $ax \equiv 1 \pmod{n}$, quindi $x = a^{-1} \pmod{n}$.

### 3.5 Il Piccolo Teorema di Fermat

Se $p$ è primo e $\gcd(a, p) = 1$, allora:

$$a^{p-1} \equiv 1 \pmod{p}$$

Corollario utile:

$$a^{p} \equiv a \pmod{p}$$

> Questo teorema è alla base di RSA. Lo rivedremo nella Parte 2.

---

## 4. Crittografia Simmetrica Classica

### 4.1 Cifrario di Cesare

Il cifrario più semplice: ogni lettera viene traslata di $k$ posizioni nell'alfabeto.

$$E(k, m) = (m + k) \pmod{26}$$
$$D(k, c) = (c - k) \pmod{26}$$

**Esempio con $k = 3$:**

| Plaintext | A | T | T | A | C | C | O |
|---|---|---|---|---|---|---|---|
| Numerico | 0 | 19 | 19 | 0 | 2 | 2 | 14 |
| $+3 \bmod 26$ | 3 | 22 | 22 | 3 | 5 | 5 | 17 |
| Ciphertext | D | W | W | D | F | F | R |

**Spazio delle chiavi:** $|\mathcal{K}| = 26$ → attacco a forza bruta banale.

### 4.2 Cifrario Affine

Generalizzazione del Cesare:

$$E(k, m) = (a \cdot m + b) \pmod{26}, \quad k = (a, b)$$
$$D(k, c) = a^{-1}(c - b) \pmod{26}$$

**Condizione:** $\gcd(a, 26) = 1$ (altrimenti $a^{-1}$ non esiste e la decifratura è impossibile).

**Spazio delle chiavi:** $|\mathcal{K}| = \phi(26) \times 26 = 12 \times 26 = 312$. Ancora troppo piccolo.

### 4.3 Cifrario di Vigenère

Usa una chiave di lunghezza $L$ (una parola), applicando un Cesare diverso per ogni posizione:

$$c_i = (m_i + k_{i \bmod L}) \pmod{26}$$

**Esempio:** chiave = `CHIAVE` $(= 2, 7, 8, 0, 21, 4)$, testo = `ATTACCO`

$$c_0 = (A + C) = (0+2) \bmod 26 = 2 = C$$
$$c_1 = (T + H) = (19+7) \bmod 26 = 0 = A$$
$$\vdots$$

**Attacco di Kasiski:** se la chiave è corta, si possono trovare pattern ripetuti nel ciphertext e dedurre la lunghezza $L$, poi ridurre al problema del Cesare $L$ volte.

### 4.4 One-Time Pad (Cifrario di Vernam)

Chiave casuale lunga quanto il messaggio, usata una sola volta:

$$c_i = m_i \oplus k_i$$
$$m_i = c_i \oplus k_i$$

dove $\oplus$ è lo XOR bit a bit.

**Teorema (Shannon, 1949):** Il One-Time Pad è **perfettamente sicuro**: il ciphertext non fornisce alcuna informazione sul plaintext.

**Dimostrazione (sketch):**

$$P(m \mid c) = P(m) \quad \forall m, c$$

Questo perché per ogni coppia $(m, c)$ esiste esattamente una chiave $k = m \oplus c$ che mappa $m$ in $c$, e tutte le chiavi sono equiprobabili.

**Problema pratico:** la chiave deve essere:
- lunga quanto il messaggio
- completamente casuale
- usata **una sola volta**
- scambiata in modo sicuro

Il problema dello scambio della chiave rimane irrisolto. Il One-Time Pad è perfetto in teoria, inutilizzabile in pratica su larga scala.

---

## 5. Crittografia Simmetrica Moderna — Cenni

### 5.1 AES (Advanced Encryption Standard)

AES è il cifrario simmetrico a blocchi più usato oggi. Opera su blocchi di **128 bit** con chiavi di 128, 192 o 256 bit.

La sicurezza di AES **non** si basa su un problema matematico dimostrabile, ma su anni di crittanalisi senza attacchi pratici noti.

Schema semplificato di un round AES:

```
Stato (4×4 byte)
    │
    ▼
SubBytes   ← sostituzione non-lineare (S-box)
    │
    ▼
ShiftRows  ← permutazione delle righe
    │
    ▼
MixColumns ← combinazione lineare delle colonne
    │
    ▼
AddRoundKey ← XOR con la sottochiave del round
```

AES esegue 10/12/14 round a seconda della lunghezza della chiave.

### 5.2 Modalità operative

Un cifrario a blocchi cifra blocchi di dimensione fissa. Per messaggi lunghi si usano **modalità operative**:

- **ECB** (Electronic Codebook): ogni blocco cifrato indipendentemente → **insicuro** (blocchi uguali → ciphertext uguale)
- **CBC** (Cipher Block Chaining): ogni blocco viene XORato con il ciphertext precedente prima della cifratura
- **CTR** (Counter Mode): trasforma AES in cifrario a flusso

$$c_i = E(k,\ \text{nonce} \| i) \oplus m_i$$

---

## 6. Il Problema dello Scambio delle Chiavi

Tutti i sistemi simmetrici soffrono dello stesso problema fondamentale:

> **Alice e Bob devono condividere la stessa chiave segreta prima di comunicare, ma come si scambiano questa chiave su un canale insicuro?**

Se usassimo un canale sicuro per scambiare la chiave, potremmo usare quel canale direttamente per comunicare!

### 6.1 Scala del problema

In una rete di $n$ utenti, ogni coppia ha bisogno di una chiave condivisa:

$$\text{Numero di chiavi} = \binom{n}{2} = \frac{n(n-1)}{2}$$

Per $n = 1000$ utenti servono **499.500 chiavi**. Per internet con miliardi di utenti, è impraticabile.

### 6.2 La svolta concettuale

Nel 1976, Diffie e Hellman pongono la domanda rivoluzionaria:

> *"È possibile concordare una chiave segreta comunicando su un canale completamente pubblico, dove un avversario ascolta tutto?"*

La risposta, sorprendentemente, è **sì**.  
Il meccanismo si chiama **scambio di chiavi Diffie-Hellman** e sarà il punto di partenza della Parte 2.

L'intuizione chiave è il concetto di **funzione a senso unico con trapdoor**, che introduciamo nella prossima parte.

---

## 7. Esercizi

### Esercizio 1 — Cifrario Affine
Cifra il messaggio `CIAO` con $a = 5$, $b = 8$ in $\mathbb{Z}_{26}$.  
Poi decifra il risultato per verificare.

### Esercizio 2 — Aritmetica Modulare
Calcola:
- $7^{-1} \pmod{26}$
- $11^{-1} \pmod{26}$
- $2^{10} \pmod{13}$ (usando il Piccolo Teorema di Fermat)

### Esercizio 3 — One-Time Pad
Alice vuole inviare il bit string $m = 10110$ a Bob. La chiave è $k = 01101$.
- Calcola il ciphertext $c = m \oplus k$
- Verifica che $c \oplus k = m$

### Esercizio 4 — Riflessione
Perché il Cifrario di Vigenère con chiave di lunghezza uguale al messaggio è equivalente al One-Time Pad? Quali sono le differenze pratiche?

### Esercizio 5 — Conteggio delle chiavi
In una rete di 50 utenti che usano crittografia simmetrica, quante chiavi diverse sono necessarie affinché ogni coppia possa comunicare privatamente?

---

*→ Continua con [Parte 2: Crittografia Asimmetrica e RSA](crittografia_parte2.md)*
