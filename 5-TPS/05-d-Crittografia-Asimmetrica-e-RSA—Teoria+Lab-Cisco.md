# 🔐 Crittografia Asimmetrica e RSA — Teoria e Lab Cisco

> **Livello:** 5° anno Liceo Scientifico / Informatico
> **Durata:** 2 ore (120 minuti)
> **Prerequisiti:** Aritmetica modulare, Piccolo Teorema di Fermat

---

## Connessione tra Teoria e Pratica

Il comando `crypto key generate rsa` che eseguirai in laboratorio non è magia: è esattamente l'algoritmo RSA che studierai in questo documento.

```
TEORIA                          PRATICA CISCO
──────                          ─────────────
Scegli p, q primi     ───►      Il router genera p, q internamente (CSPRNG)
Calcola n = p·q       ───►      La "modulus size" che inserisci (es. 2048 bit) è |n|
Calcola (e, d)        ───►      Il router ricava la coppia di chiavi
Pubblica (e, n)       ───►      Il client SSH riceve la chiave pubblica
Cifra con e           ───►      Handshake SSH: sessione cifrata
Decifra con d         ───►      Solo il router (con d segreto) può decifrare
```

> [!NOTE]
> SSH usa RSA **solo per la fase di autenticazione e scambio chiavi**. I dati della sessione vengono poi cifrati con algoritmi simmetrici (es. AES), molto più veloci. Questo schema si chiama **crittografia ibrida**.

---

## Parte 1 — Fondamenti Teorici

### 1.1 Storia e Origine di RSA

L'algoritmo **RSA** prende il nome da **Ron Rivest**, **Adi Shamir** e **Leonard Adleman**, i tre crittografi del MIT che lo pubblicarono per la prima volta nel **1977**.

Prima di RSA, la crittografia era esclusivamente **simmetrica**: per comunicare in segreto, due parti dovevano scambiarsi fisicamente una chiave condivisa prima di separarsi. Il problema centrale era quindi: *come scambiarsi una chiave segreta su una rete pubblica senza che qualcuno la intercetti?*

Nel 1976 Whitfield Diffie e Martin Hellman ipotizzarono l'esistenza della crittografia asimmetrica, ma furono Rivest, Shamir e Adleman a trovare la soluzione pratica, basata sulla **difficoltà di fattorizzare grandi numeri**.

> [!NOTE]
> **Curiosità storica:** Solo nel 1997 fu reso pubblico che il matematico britannico **Clifford Cocks**, del GCHQ (i servizi segreti del Regno Unito), aveva sviluppato un sistema equivalente già nel **1973**. La sua scoperta rimase classificata e non fu mai applicata su larga scala. Nel 2002 Rivest, Shamir e Adleman ricevettero il **Premio Turing** per il loro contributo.

---

### 1.2 Funzioni a Senso Unico e Trapdoor

Una funzione **one-way** è facile da calcolare in una direzione ma computazionalmente impossibile da invertire senza un'informazione segreta detta **trapdoor**.

| Operazione | Direzione | Difficoltà |
|:---|:---|:---|
| $f(p, q) = p \cdot q = n$ | Moltiplicazione | Facile — $O(\log^2 n)$ |
| $f^{-1}(n) = (p, q)$ | Fattorizzazione | **Difficile** — nessun algoritmo polinomiale noto |

> [!IMPORTANT]
> **Idea chiave:** rendi pubblica la funzione $f$ (chiunque può cifrare), tieni segreta la trapdoor (solo tu puoi decifrare). Per questo puoi distribuire liberamente la tua chiave pubblica senza rischi.

**L'analogia dei colori:** mescolare Giallo e Blu per ottenere Verde è facile. Partire dal Verde e ricavare esattamente le due tinte originali è praticamente impossibile. Allo stesso modo, moltiplicare $p \times q$ per ottenere $n$ è istantaneo; fattorizzare $n$ per ricavare $p$ e $q$ richiede, con le chiavi odierne, migliaia di anni di calcolo.

---

### 1.3 Base Matematica: il Teorema di Eulero

La **funzione di Eulero** $\phi(n)$ conta gli interi in $\{1, \dots, n\}$ coprimi con $n$. Per due primi distinti $p$ e $q$:

$$\phi(p \cdot q) = (p-1)(q-1)$$

Il **Teorema di Eulero** afferma che se $\gcd(a, n) = 1$:

$$a^{\phi(n)} \equiv 1 \pmod{n}$$

Da cui segue il corollario fondamentale su cui si basa la correttezza di RSA:

$$a^{k \cdot \phi(n) + 1} \equiv a \pmod{n} \quad \forall k \in \mathbb{Z}$$

---

### 1.4 Generazione delle Chiavi RSA

```
Step 1:  Scegli due primi grandi p e q
Step 2:  Calcola  n = p·q  e  φ(n) = (p-1)(q-1)
Step 3:  Scegli e  tale che  gcd(e, φ(n)) = 1
Step 4:  Calcola  d = e⁻¹ mod φ(n)  (con l'algoritmo di Euclide esteso)

Chiave pubblica  →  (e, n)   ← condividi liberamente
Chiave privata   →  (d, n)   ← tieni segreta
```

> [!WARNING]
> Dopo la generazione, **elimina** $p$, $q$ e $\phi(n)$. Se un avversario li conosce, può ricalcolare $d$ in pochi millisecondi. I router Cisco non li espongono mai all'esterno per questo motivo.

---

### 1.5 Cifratura, Decifratura e Correttezza

$$\text{Cifratura (chiave pubblica):} \quad c = m^e \pmod{n}$$
$$\text{Decifratura (chiave privata):} \quad m = c^d \pmod{n}$$

**Dimostrazione di correttezza.** Per costruzione $e \cdot d = k \cdot \phi(n) + 1$, quindi:

$$c^d = (m^e)^d = m^{ed} = m^{k\phi(n)+1} = \underbrace{(m^{\phi(n)})^k}_{\equiv\, 1} \cdot m \equiv m \pmod{n} \quad \blacksquare$$

---

### 1.6 Esempio Numerico Completo

| Parametro | Valore |
|:---|:---|
| $p = 61,\; q = 53$ | Due primi scelti |
| $n = 3233$ | Modulo pubblico |
| $\phi(n) = 3120$ | $(60 \times 52)$ — segreto |
| $e = 17$ | Esponente pubblico |
| $d = 2753$ | Esponente privato ($17 \times 2753 = 46801 = 15 \times 3120 + 1$) |

Cifra $m = 65$:
$$c = 65^{17} \bmod 3233 = 2790$$

Decifra:
$$m = 2790^{2753} \bmod 3233 = 65 \checkmark$$

Verifica in Python: `pow(2790, 2753, 3233)`

---

### 1.7 Firma Digitale

RSA permette anche di **firmare** messaggi: il mittente usa la propria **chiave privata** per produrre la firma, chiunque usa la **chiave pubblica** per verificarla.

$$\sigma = m^{d_A} \pmod{n_A} \quad \text{(firma)} \qquad m' = \sigma^{e_A} \pmod{n_A} \stackrel{?}{=} m \quad \text{(verifica)}$$

| Proprietà | Significato |
|:---|:---|
| **Autenticità** | Solo chi possiede $d_A$ può produrre $\sigma$ |
| **Integrità** | Se $m$ viene modificato, $\sigma$ non è più valido |
| **Non ripudio** | Il firmatario non può negare di aver firmato |

> [!NOTE]
> In pratica si firma l'**hash** del messaggio, non il messaggio diretto: $\sigma = H(m)^d \pmod{n}$, dove $H$ è SHA-256 o SHA-3. RSA è lento e questa ottimizzazione è fondamentale. È esattamente ciò che avviene nel certificato del router durante un handshake SSH.

---

### 1.8 Sicurezza e Dimensione delle Chiavi

La sicurezza di RSA dipende dalla difficoltà di fattorizzare $n$. Il miglior algoritmo noto (General Number Field Sieve) ha complessità sub-esponenziale: aggiungere pochi bit alla chiave aumenta enormemente il tempo necessario per violarla.

| Bit del modulo ($n$) | Livello di sicurezza | Note |
|:---|:---|:---|
| **512 bit** | **Insicuro** | Violabile in pochi minuti/ore |
| **1024 bit** | **Legacy** | Standard minimo su vecchi router |
| **2048 bit** | **Sicuro** | Raccomandato fino al 2030 |
| **4096 bit** | **Alta sicurezza** | Lento da generare, per dati molto sensibili |

> [!CAUTION]
> **La minaccia quantistica:** l'**Algoritmo di Shor**, eseguito su un computer quantistico sufficientemente potente, potrebbe fattorizzare $n$ in pochi minuti. Quando ciò diventerà realtà, RSA dovrà essere sostituito da algoritmi **post-quantistici** (come CRYSTALS-Kyber), basati su problemi matematici diversi dalla fattorizzazione.

---

## Parte 2 — Lab Cisco: Telnet (Insicuro)

### Obiettivo

Dimostrare perché Telnet non è accettabile come protocollo di accesso remoto.

---

### Configurazione e Connessione

```bash
RTR-A(config)# line vty 0 4
RTR-A(config-line)# password cisco
RTR-A(config-line)# login
RTR-A(config-line)# transport input telnet
RTR-A(config)# enable secret classe5A
```

Dal PC:

```bash
PC> telnet 192.168.1.1
Password: cisco
```

---

### Il Problema di Telnet

| Protocollo | Trasmissione |
|:---|:---|
| Telnet | ❌ In chiaro — ogni carattere in ASCII |
| SSH | ✅ Cifrato con AES |

> [!CAUTION]
> **Il paradosso di Telnet:** anche se si configura `enable secret` (memorizzato come hash), Telnet trasmette la password **in chiaro durante il login**. L'attaccante non deve craccare nulla: legge direttamente il traffico con uno sniffer (es. Wireshark, filtrando `tcp.port == 23`).
>
> La sicurezza locale è inutile senza un canale cifrato. SSH risolve questo perché cifra la comunicazione **prima** che qualsiasi credenziale venga trasmessa.

---

## Parte 3 — Lab Cisco: SSH (Soluzione Sicura)

### Dalla Teoria alla Pratica

| Concetto RSA | Comando Cisco | Cosa succede |
|:---|:---|:---|
| Scelta del modulo $n$ | `crypto key generate rsa` + dimensione | Il router genera $p, q$ e calcola $n$ |
| Chiave pubblica $(e, n)$ | Scambiata nell'handshake | Il client SSH la riceve e la memorizza |
| Chiave privata $(d, n)$ | Rimane nel router | Usata per decifrare e firmare la sessione |
| Autenticazione utente | `username ... secret` | Credenziali verificate dopo che il canale è cifrato |

---

### A — Rafforzare la Sicurezza delle Password

Prima di creare gli utenti, imponi una lunghezza minima globale per tutte le password:

```bash
RTR-A(config)# security passwords min-length 10
```

> [!IMPORTANT]
> Questo comando si applica a tutte le password configurate da quel momento in poi (`enable secret`, `username secret`, password di linea). Una password di 10 caratteri con lettere, numeri e simboli ha circa $72^{10} \approx 3{,}7 \times 10^{18}$ combinazioni: oltre 100 anni di brute force a 1 miliardo di tentativi al secondo. La protezione anti-brute force configurata più avanti riduce ulteriormente questa velocità.

---

### B — Configurazione SSH

#### Step 1 — Identità del Router (Hostname e Dominio)

```bash
RTR-A(config)# hostname RTR-A
RTR-A(config)# ip domain-name lab.sicuro.it
```

> [!CAUTION]
> Senza un `hostname` non predefinito e un `ip domain-name`, il comando di generazione delle chiavi **fallirà**. IOS combina i due valori (es. `RTR-A.lab.sicuro.it`) per costruire i metadati della chiave RSA.

---

#### Step 2 — Creazione delle Credenziali Utente

```bash
RTR-A(config)# username SSHadmin secret @AdminPass123!
```

> [!NOTE]
> Questo comando **non abilita SSH**: popola soltanto il database locale degli utenti autorizzati. Il "chi" è definito; il "come" (SSH) viene configurato nei passi successivi.

---

#### Step 3 — Generazione delle Chiavi RSA

```bash
RTR-A(config)# crypto key generate rsa
```

*Quando richiesto, inserisci la dimensione del modulo: `2048`*

> [!IMPORTANT]
> Questo comando **avvia il demone SSH** (verificabile con `show ip ssh`). Tuttavia, nessun client può ancora connettersi: le linee VTY non sono ancora istruite a usare queste chiavi. Scegliere 2048 bit significa rendere $n = p \cdot q$ abbastanza grande da rendere la fattorizzazione computazionalmente impossibile con i computer attuali.

---

#### Step 4 — Configurazione delle Linee VTY

```bash
RTR-A(config)# line vty 0 4
RTR-A(config-line)# transport input ssh
RTR-A(config-line)# login local
```

> [!WARNING]
> Questi due comandi completano la configurazione:
> - **`transport input ssh`** — rifiuta qualsiasi connessione non cifrata (Telnet incluso).
> - **`login local`** — impone l'autenticazione con il database utenti locale invece di una semplice password di linea.

---

### Riepilogo: Ruolo di Ogni Comando

| Comando | Funzione | Senza di esso… |
|:---|:---|:---|
| `ip domain-name` | Identità FQDN del router | Impossibile generare le chiavi RSA |
| `username ... secret` | Database utenti locale | SSH non sa a chi concedere l'accesso |
| `crypto key generate rsa` | Abilita il protocollo SSH | Il router non può cifrare; SSH resta "Disabled" |
| `transport input ssh` | Protegge la linea VTY | Il router continua ad accettare Telnet |
| `login local` | Richiede username + password | L'autenticazione non usa il database locale |

> [!TIP]
> Sintesi: `crypto key generate rsa` crea la **serratura crittografica**; `line vty` con `login local` decide **chi ha la chiave** e su quale porta può usarla.

---

### C — Protezione Anti-Brute Force

```bash
RTR-A(config)# login block-for 120 attempts 3 within 60
```

> *"Se si verificano 3 tentativi falliti in 60 secondi, blocca tutti gli accessi per 120 secondi."*

> [!CAUTION]
> **Importante in lab:** sbagliare la password 3 volte ti bloccherà fuori per 2 minuti. Assicurati di avere accesso fisico alla porta console prima di attivare questa funzione. L'accesso via `line con 0` non è soggetto al blocco.

> [!WARNING]
> Senza questa protezione, un attaccante può tentare migliaia di password al secondo contro SSH. RSA protegge il canale, ma le credenziali di autenticazione rimangono vulnerabili agli attacchi a dizionario senza un limite sui tentativi.

---

### D — Test e Verifica

#### Connessione SSH dal PC

```
PC> ssh -l SSHadmin 192.168.1.1
Password: @AdminPass123!
RTR-A>
```

Per forzare SSH versione 2 (preferibile in ambienti reali):

```
PC> ssh -v 2 -l SSHadmin 192.168.1.1
```

#### Verifica lato Router

```bash
RTR-A# show ip ssh        # Stato SSH, versione, parametri
RTR-A# show ssh           # Sessioni attive con IP sorgente e utente
RTR-A# show login         # Stato del blocco anti-brute force
RTR-A# show crypto key mypubkey rsa  # Conferma esistenza delle chiavi
```

> [!NOTE]
> Se `show ip ssh` riporta `SSH disabled`, le cause più comuni sono: chiavi non generate, nome di dominio assente, o versione di IOS che non supporta SSH.

#### Verifica che Telnet sia Disabilitato

```
PC> telnet 192.168.1.1
```

Il router deve rifiutare la connessione, confermando che `transport input ssh` ha escluso correttamente Telnet.

#### Test del Blocco Brute Force

Inserisci intenzionalmente la password sbagliata 3 volte, poi verifica con `show login` dal router (via console) che il blocco sia attivo.

---

### Cosa Succede Realmente Durante una Sessione SSH

```
Client (PC)                         Router Cisco (RTR-A)
───────────                         ────────────────────
1. Connessione TCP porta 22    ──►  Accetta connessione

2. Riceve chiave pubblica      ◄──  Invia (e, n) generata con crypto key generate rsa

3. Verifica fingerprint RSA    ──►  [prima connessione: l'utente deve fidarsi]

4. Genera chiave AES casuale,  ──►  Decifra con chiave privata (d, n):  m = c^d mod n
   la cifra con (e, n):              → ottiene la chiave di sessione AES
   c = m^e mod n

5. Da qui: tutto cifrato       ◄──► Comunicazione AES — dati illeggibili da rete

6. Invia username + password   ──►  Verifica con database locale (login local)
   (dentro il tunnel AES)            → accesso concesso o negato
```

> [!NOTE]
> Il passo 4 è esattamente la cifratura RSA: $c = m^e \pmod{n}$ eseguita dal client, $m = c^d \pmod{n}$ eseguita dal router. Il messaggio $m$ è la chiave AES generata casualmente per quella sessione — non viene mai trasmessa in chiaro.

---

## Esercizi

### Esercizio 1 — Generazione Chiavi RSA
Con $p = 11$, $q = 13$: calcola $n$ e $\phi(n)$, scegli un $e$ valido, ricava $d$, cifra $m = 7$ e verifica la decifratura.

### Esercizio 2 — Teorema di Eulero
Verifica che $3^{\phi(10)} \equiv 1 \pmod{10}$.

### Esercizio 3 — Firma Digitale
Con la chiave dell'Esercizio 1, firma $m = 5$: calcola $\sigma = m^d \pmod n$ e verifica che $\sigma^e \equiv m \pmod n$.

### Esercizio 4 — Analisi della Sicurezza
Un avversario conosce $n = 3233$ e lo fattorizza come $61 \times 53$. Sapendo che la chiave pubblica è $(e = 17, n = 3233)$, come calcolerebbe $d$? Perché eliminare $p$ e $q$ dopo la generazione non protegge la chiave se $n$ è già stato fattorizzato?

### Esercizio 5 — Lab Cisco Esteso
Dopo aver configurato SSH:
1. Verifica con `show ip ssh` che SSH sia attivo in versione 2
2. Testa il blocco brute force sbagliando intenzionalmente la password 3 volte
3. Controlla lo stato del blocco con `show login`

### Esercizio 6 — Implementazione Python

```python
# Verifica RSA con Python
p, q = 61, 53
n = p * q
phi_n = (p - 1) * (q - 1)
e = 17
d = pow(e, -1, phi_n)   # inverso modulare — Python 3.8+
m = 42
c = pow(m, e, n)
m_dec = pow(c, d, n)
print(f"Originale: {m}, Cifrato: {c}, Decifrato: {m_dec}")
assert m == m_dec, "Errore!"
```

> [!TIP]
> `pow(base, exp, mod)` usa internamente l'**esponenziazione rapida** (square-and-multiply), lo stesso algoritmo che il router Cisco impiega per RSA. Senza questo metodo, calcolare $2790^{2753}$ produrrebbe un numero con migliaia di cifre prima di applicare il modulo.

---

*← Parte 1: Fondamenti (aritmetica modulare, Fermat) | → Parte 3: Curve Ellittiche e Applicazioni Reali*
