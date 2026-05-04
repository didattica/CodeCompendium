# 🔐 Crittografia Asimmetrica e RSA — Teoria + Lab Cisco
> **Livello:** 5° anno Liceo Scientifico / Informatico  
> **Durata:** 2 ore (120 minuti)  
> **Prerequisiti:** Aritmetica modulare, Piccolo Teorema di Fermat

---

## Connessione tra Teoria e Pratica

Questo documento unifica la teoria della crittografia asimmetrica con la sua applicazione concreta su router Cisco. Il comando `crypto key generate rsa` che eseguirai in laboratorio **non è magia**: è esattamente l'algoritmo RSA che studierai qui sotto.

```
TEORIA                          PRATICA CISCO
──────                          ─────────────
Scegli p, q primi     ───►      Il router genera p, q internamente (CSPRNG)
Calcola n = p·q       ───►      La "modulus size" che inserisci (es. 1024 bit) è |n|
Calcola (e, d)        ───►      Il router ricava la coppia di chiavi
Pubblica (e, n)       ───►      Il client SSH riceve la chiave pubblica
Cifra con e           ───►      Handshake SSH: sessione cifrata
Decifra con d         ───►      Solo il router (con d segreto) può decifrare
```

> [!NOTE]
> SSH usa RSA **solo per la fase di autenticazione e scambio chiavi**. I dati della sessione vengono poi cifrati con algoritmi simmetrici (es. AES), molto più veloci. Questo schema si chiama **crittografia ibrida**.

---

## Parte 1 — Teoria (sintesi)

### 1.1 Funzioni a senso unico e Trapdoor

Una funzione **one-way** è facile da calcolare in una direzione, computazionalmente impossibile da invertire senza un'informazione segreta detta **trapdoor**.

| Operazione | Direzione | Difficoltà |
|:---|:---|:---|
| $f(p, q) = p \cdot q = n$ | Moltiplicazione | Facile — $O(\log^2 n)$ |
| $f^{-1}(n) = (p, q)$ | Fattorizzazione | **Difficile** — nessun algoritmo polinomiale noto |

> [!IMPORTANT]
> **Idea chiave della crittografia asimmetrica:** rendi pubblica la funzione $f$ (chiunque può cifrare), tieni segreta la trapdoor $t$ (solo tu puoi decifrare). Questo è il motivo per cui puoi pubblicare la tua chiave pubblica senza rischi.

---

### 1.2 Il Teorema di Eulero (base matematica di RSA)

La **funzione di Eulero** $\phi(n)$ conta gli interi in $\{1, \dots, n\}$ coprimi con $n$.

Per $p, q$ primi distinti:
$$\phi(p \cdot q) = (p-1)(q-1)$$

Il **Teorema di Eulero** afferma che se $\gcd(a, n) = 1$:
$$a^{\phi(n)} \equiv 1 \pmod{n}$$

**Corollario fondamentale** (è esattamente ciò che rende RSA corretto):
$$a^{k \cdot \phi(n) + 1} \equiv a \pmod{n} \quad \forall k \in \mathbb{Z}$$

---

### 1.3 Algoritmo RSA — Generazione delle Chiavi

```
Step 1:  Scegli due primi grandi p e q
Step 2:  Calcola  n = p·q  e  φ(n) = (p-1)(q-1)
Step 3:  Scegli e  tale che  gcd(e, φ(n)) = 1
Step 4:  Calcola  d = e⁻¹ mod φ(n)  (con Euclide esteso)

Chiave pubblica  →  (e, n)   ← condividi liberamente
Chiave privata   →  (d, n)   ← tieni segreta
```

> [!WARNING]
> Dopo la generazione, **elimina** $p$, $q$ e $\phi(n)$. Se un avversario li conosce, può ricalcolare $d$ in pochi millisecondi. Il router Cisco non li espone mai all'esterno per questo motivo.

---

### 1.4 Cifratura e Decifratura

$$\text{Cifratura (chiave pubblica):} \quad c = m^e \pmod{n}$$
$$\text{Decifratura (chiave privata):} \quad m = c^d \pmod{n}$$

**Perché funziona?** Per costruzione $e \cdot d = k \cdot \phi(n) + 1$, quindi:
$$c^d = (m^e)^d = m^{ed} = m^{k\phi(n)+1} = \underbrace{(m^{\phi(n)})^k}_{\equiv\, 1^k \,=\, 1} \cdot m \equiv m \pmod{n} \quad \blacksquare$$

---

### 1.5 Esempio numerico completo (piccoli numeri)

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

### 1.6 Firma Digitale

RSA permette anche di **firmare** messaggi: Alice usa la sua **chiave privata** per firmare, chiunque usa la sua **chiave pubblica** per verificare.

$$\sigma = m^{d_A} \pmod{n_A} \quad \text{(firma)}$$
$$m' = \sigma^{e_A} \pmod{n_A} \stackrel{?}{=} m \quad \text{(verifica)}$$

| Proprietà | Significato |
|:---|:---|
| **Autenticità** | Solo chi possiede $d_A$ ha potuto produrre $\sigma$ |
| **Integrità** | Se $m$ è modificato, $\sigma$ non è più valido |
| **Non ripudio** | Alice non può negare di aver firmato |

> [!NOTE]
> In pratica non si firma $m$ direttamente (RSA è lento), ma il suo **hash** crittografico: $\sigma = H(m)^d \pmod{n}$, dove $H$ è SHA-256 o SHA-3. Questo è esattamente ciò che accade nel certificato del router durante un handshake SSH.

---


### 1.7 Perché RSA è sicuro? (Il cuore del problema)

La sicurezza di RSA si basa su un concetto matematico chiamato **funzione a senso unico con trappola** (*trapdoor one-way function*). 

#### L'Analogia dei Colori e dei Numeri Primi

Per capire cosa succede nel router quando digiti `crypto key generate rsa`, immagina questa situazione:

> [!TIP]
> **1. L'operazione facile (Cifratura/Generazione):**
> È come mescolare due colori, ad esempio **Giallo** e **Blu**, per ottenere il **Verde**. 
> In matematica, il router sceglie due numeri primi giganti ($p$ e $q$) e li moltiplica tra loro per ottenere il modulo $n$.
> *   Fare $p \times q = n$ è velocissimo.
> *   Il risultato $n$ (il "Verde") fa parte della **Chiave Pubblica** che il router distribuisce a tutti.

> [!IMPORTANT]
> **2. L'operazione difficile (Attacco/Decifratura):**
> Se ti do un secchio di vernice **Verde**, puoi dirmi esattamente quali tonalità di giallo e blu ho usato? No, dovresti andare per tentativi infiniti.
> In matematica, partendo dal numero enorme $n$, è difficilissimo risalire ai due numeri primi originali $p$ e $q$. Questa operazione si chiama **Fattorizzazione**.
> *   Senza conoscere $p$ e $q$, un hacker non può calcolare la **Chiave Privata** ($d$).
> *   La sicurezza sta tutta qui: rompere il modulo $n$ per trovare i fattori primi è un'impresa che richiederebbe migliaia di anni ai computer attuali.

#### Difficoltà Computazionale

Il miglior algoritmo di fattorizzazione noto (General Number Field Sieve) ha una complessità sub-esponenziale. Questo significa che aggiungere pochi bit alla chiave aumenta enormemente il tempo necessario per violarla.

**Dimensioni delle chiavi raccomandate:**

| Bit del Modulo ($n$) | Grado di Sicurezza | Note per il Lab Cisco |
|:---|:---|:---|
| **512 bit** | **Insicuro** | Violabile in pochi minuti/ore. |
| **1024 bit** | **Minimo** | Standard legacy, ancora comune nei vecchi router. |
| **2048 bit** | **Sicuro** | Lo standard attuale (raccomandato fino al 2030). |
| **4096 bit** | **Militare** | Molto lento da generare, usato per dati sensibilissimi. |

> [!CAUTION]
> **La fine di RSA? (Minaccia Quantistica)**
> Esiste un algoritmo teorico, l'**Algoritmo di Shor**, che se eseguito su un computer quantistico sufficientemente potente, potrebbe separare i "colori" (fattorizzare $n$) in pochi minuti. 
> In quel giorno, il calcolo $O((\log n)^2 \cdot \log \log n)$ diventerà realtà e dovremo sostituire RSA con nuovi algoritmi "Post-Quantistici" (come CRYSTALS-Kyber) che si basano su problemi matematici diversi dalla fattorizzazione.



### Cosa abbiamo imparato?
Quando esegui il laboratorio, ricorda: il comando `crypto key generate rsa 2048` sta creando un "colore verde" così complesso che nessun computer attuale può separare nel "giallo" e "blu" originali. È questa impossibilità matematica che protegge la tua password amministrativa su SSH!

---

## Parte 2 — Lab Cisco: Configurazione SSH

### Connessione teoria → pratica

| Concetto RSA | Comando Cisco | Cosa succede |
|:---|:---|:---|
| Scelta di $n$ (modulus) | `crypto key generate rsa` + dimensione | Il router genera $p, q$ e calcola $n$ |
| Chiave pubblica $(e, n)$ | Scambiata automaticamente nell'handshake | Il client SSH la riceve e la memorizza |
| Chiave privata $(d, n)$ | Rimane nel router, non esce mai | Usata per decifrare e firmare la sessione |
| Autenticazione utente | `username ... secret` | Credenziali locali per `login local` |

---

### A — Prima di tutto: dimostrare perché Telnet non è sicuro

Prima di configurare SSH, collegati al router tramite **Telnet** — il protocollo che SSH è nato per sostituire. L'obiettivo è vedere con i tuoi occhi perché non è accettabile usarlo.

#### Connessione Telnet dal PC

```
PC> telnet 192.168.1.1
```

Di default, Telnet è abilitato sulle linee VTY. Dovresti riuscire a entrare (se è configurata una password di linea) oppure ricevere un prompt di accesso. La connessione **funziona** — questo è il problema.

> [!WARNING]
> Telnet funziona, ma trasmette **tutto in chiaro**: username, password, e ogni singolo comando che digiti. Chiunque sulla stessa rete con uno sniffer può leggere la tua sessione come se fosse testo normale.

#### Cosa vede un attaccante (simulazione con Wireshark)

Se in lab avete Wireshark disponibile su un PC nella stessa rete, avviatelo e filtrate per `telnet` oppure `tcp.port == 23`. Durante una sessione Telnet vedrete i dati **in chiaro**, inclusa la password digitata carattere per carattere.

Confrontatelo con una sessione SSH: i pacchetti saranno illeggibili — solo dati cifrati con AES.

> [!NOTE]
> Questo esperimento rende visibile in pochi secondi il motivo per cui Telnet è stato abbandonato. RSA non serve solo a "fare crittografia in astratto": serve a rendere impossibile esattamente questo tipo di intercettazione.

---

### B — Rafforzare la sicurezza delle password

Prima di creare gli utenti, imponiamo una **lunghezza minima** per tutte le password configurate sul dispositivo:

```bash
RTR-A(config)# security passwords min-length 10
```

> [!IMPORTANT]
> Questo comando si applica **globalmente** a tutte le password configurate da quel momento in poi (`enable secret`, `username secret`, password di linea). Se provi a impostare una password più corta di 10 caratteri, IOS la rifiuterà con un errore. È la prima linea di difesa contro password banali come `cisco` o `1234`.

> [!NOTE]
> Una password di 10 caratteri con lettere, numeri e simboli ha circa $72^{10} \approx 3.7 \times 10^{18}$ combinazioni possibili. Anche con un attacco brute force da 1 miliardo di tentativi al secondo ci vorrebbero oltre 100 anni — e il `login block-for` che configureremo dopo riduce ulteriormente la velocità degli attacchi.

---

### C — Configurazione SSH (Accesso Remoto Sicuro)

#### Step 1 — Preparare l'identità (Hostname e Dominio)

Prima di generare le chiavi, il router deve avere un'identità univoca.

```bash
RTR-A(config)# hostname RTR-A
RTR-A(config)# ip domain-name lab.sicuro.it
```

> [!CAUTION]
> **Il vincolo dell'identità:** Senza un `hostname` (diverso da quello di default "Router") e un `ip domain-name`, il comando di generazione chiavi **fallirà**. Il sistema IOS combina questi due parametri per creare il nome dell'identità (es: `RTR-A.lab.sicuro.it`) che verrà inserito nei metadati della chiave RSA.

---

#### Step 2 — Creare le credenziali dell'utente

```bash
RTR-A(config)# username SSHadmin secret @AdminPass123!
```

> [!NOTE]
> **Il comando `username` abilita SSH?**
> **No.** Questo comando si limita a popolare il database locale del router.
> - **Cosa fa:** Crea un account con privilegi di accesso.
> - **Cosa NON fa:** Non attiva protocolli, non apre porte e non abilita la crittografia. È semplicemente la definizione di "chi" è autorizzato a entrare, ma il "come" (SSH) non è ancora configurato.

---

#### Step 3 — Generare il "motore" crittografico (RSA)

```bash
RTR-A(config)# crypto key generate rsa
```
*Quando richiesto, inserisci la dimensione del modulo: `1024`*

> [!IMPORTANT]
> **Questo comando abilita SSH?**
> **Sì e No.** Dal punto di vista software, questo è il comando che "sblocca" il servizio SSH. Appena le chiavi vengono generate, il router avvia il demone SSH (puoi verificarlo con `show ip ssh`). Tuttavia, **nessun utente può ancora collegarsi** perché le linee di accesso (VTY) non sanno ancora di dover usare queste chiavi.

> [!TIP]
> **Relazione con la teoria:** Scegliere 1024 o 2048 bit significa decidere quanto grande sarà il numero $n = p \cdot q$. Più è grande, più l'operazione di fattorizzazione (invertire la funzione a senso unico) diventa impossibile per un attaccante.

---

#### Step 4 — Aprire la porta e forzare la sicurezza (Line VTY)

Questo è il passaggio finale dove tutto si unisce: l'utente creato allo Step 2 e le chiavi generate allo Step 3.

```bash
RTR-A(config)# line vty 0 4
RTR-A(config-line)# transport input ssh
RTR-A(config-line)# login local
```

> [!WARNING]
> **Perché SSH non funziona senza questi comandi?**
> Anche se le chiavi RSA sono attive, le linee VTY di default potrebbero accettare Telnet o non richiedere un utente specifico.
> 1. **`transport input ssh`**: È il comando "escludente". Dice al router: "Smetti di accettare connessioni in chiaro (Telnet). Se la comunicazione non è cifrata con le chiavi RSA, rifiutala."
> 2. **`login local`**: Dice al router: "Non chiedere solo una password generica. Chiedi il binomio Username/Password che abbiamo definito nel database locale."

---

### Riepilogo Funzionale dei Comandi

Per capire meglio la differenza tra "preparare" e "abilitare", ecco una tabella comparativa:

| Comando | Cosa "accende"? | Senza di esso... |
| :--- | :--- | :--- |
| `ip domain-name` | L'identità FQDN | Non puoi generare le chiavi RSA. |
| `username ... secret` | Il database utenti | SSH non saprebbe chi far entrare (accesso negato). |
| `crypto key generate rsa` | Il protocollo SSH | Il router non può cifrare i dati. SSH resta "Disabled". |
| `transport input ssh` | La protezione della linea | Il router continua ad accettare Telnet (insicuro). |

> [!TIP]
> In sintesi: `crypto key` crea la **serratura elettronica** (la crittografia), mentre `line vty` con `login local` decide **chi ha la chiave** e su quale porta può inserirla.

---

### D — Blocco Attacchi Brute Force

```bash
RTR-A(config)# login block-for 120 attempts 3 within 60
```

**Lettura del comando:**

> *"Se si verificano 3 tentativi di login falliti nell'arco di 60 secondi, blocca tutti gli accessi per 120 secondi."*

> [!CAUTION]
> **Attenzione in lab:** se sbagli la password 3 volte, verrai bloccato fuori dal router per 2 minuti. Questo è intenzionale — è esattamente la difesa contro attacchi brute force che volete testare. Assicurati di avere accesso alla console fisica prima di attivare questa funzione.

> [!WARNING]
> Senza questa protezione, un attaccante può tentare migliaia di password al secondo contro SSH. Il comando `login block-for` è la contromisura diretta: anche se RSA rende il canale cifrato, le credenziali di autenticazione rimangono vulnerabili agli attacchi a dizionario se non si limita il numero di tentativi.

---

### E — Test della Connessione SSH

Una volta completata la configurazione, è il momento di verificare che tutto funzioni. Il test si esegue **dal PC** verso il router.

#### Test base — Connessione SSH dal PC

In Cisco Packet Tracer, apri il **Command Prompt** del PC e digita:

```
PC> ssh -l SSHadmin 192.168.1.1
```

> Il flag `-l` specifica il **username** (la `l` sta per *login*). L'IP è quello dell'interfaccia del router raggiungibile dal PC.

Quando richiesto, inserisci la password:
```
Password: @AdminPass123!
```

Se la configurazione è corretta, vedrai il prompt del router:
```
RTR-A>
```

> [!TIP]
> Puoi specificare anche la versione SSH da usare. Per forzare SSH versione 2 (più sicuro):
> ```
> PC> ssh -v 2 -l SSHadmin 192.168.1.1
> ```
> SSH v2 corregge diverse vulnerabilità di v1 ed è sempre preferibile in ambienti reali.

---

#### Verifica lato router — Comandi di debug

Dal router, puoi confermare che SSH sia attivo e ispezionare le sessioni:

```bash
RTR-A# show ip ssh
```
Dovresti vedere `SSH Enabled - version 2.0` e i parametri di timeout/autenticazione.

```bash
RTR-A# show ssh
```
Mostra le **sessioni SSH attive** in questo momento, con IP sorgente e utente connesso.

```bash
RTR-A# show login
```
Mostra lo stato del sistema anti-brute force: quanti tentativi falliti, se il blocco è attivo e quanto manca al termine.

> [!NOTE]
> Se `show ip ssh` riporta `SSH disabled`, le cause più comuni sono: chiavi RSA non generate, nome di dominio non configurato, o versione di IOS che non supporta SSH. Verifica con `show crypto key mypubkey rsa` che le chiavi esistano.

---

#### Test del blocco brute force

Per verificare che la protezione anti-brute force funzioni, prova intenzionalmente a inserire la password **sbagliata** 3 volte di fila:

```
PC> ssh -l SSHadmin 192.168.1.1
Password: wrongpass
Password: wrongpass
Password: wrongpass
```

Dopo il terzo tentativo, il router bloccherà tutti gli accessi per 120 secondi. Dal router (via console), verifica con:

```bash
RTR-A# show login
```

> [!CAUTION]
> Esegui questo test **solo se hai accesso fisico alla console del router**. Durante il blocco, SSH sarà completamente inaccessibile da rete. L'accesso via cavo console (porta `line con 0`) rimane sempre disponibile e non è soggetto al blocco.

---

#### Verifica che Telnet sia disabilitato

Un controllo importante: assicurati che il vecchio protocollo Telnet (non cifrato) non sia più accettato:

```
PC> telnet 192.168.1.1
```

Il router dovrebbe rifiutare la connessione o non rispondere. Questo conferma che `transport input ssh` ha sostituito correttamente `transport input all` (o `telnet`).

> [!WARNING]
> Telnet trasmette username, password e tutti i dati **in chiaro**. Chiunque sulla stessa rete con uno sniffer (es. Wireshark) può leggere tutto. RSA e SSH esistono esattamente per eliminare questo rischio — un test con Wireshark in lab può rendere visivamente evidente la differenza tra i due protocolli.

---

## Collegamento Finale: Cosa Succede Davvero durante SSH

```
Client (PC)                        Router Cisco (RTR-A)
──────────                         ──────────────────────
1. Connessione TCP porta 22   ──►  Accetta connessione

2. Riceve chiave pubblica     ◄──  Invia (e, n) — generata con crypto key generate rsa
   del router

3. Verifica impronta          ──►  [prima connessione: l'utente deve fidarsi]
   (fingerprint RSA)

4. Genera chiave di sessione  ──►  Decifra con chiave privata (d, n)
   cifrata con (e, n)               → ottiene la chiave di sessione AES

5. Da qui in poi: tutto       ◄──► Comunicazione cifrata con AES
   cifrato con AES

6. Invia username + password  ──►  Verifica con database locale (login local)
   (cifrati nel tunnel AES)         → accesso concesso o negato
```

> [!NOTE]
> Il passo 4 è esattamente la cifratura RSA: $c = m^e \pmod{n}$ eseguita dal client, $m = c^d \pmod{n}$ eseguita dal router. Il messaggio $m$ è la chiave AES generata casualmente per quella sessione.

---

## Esercizi

### Esercizio 1 — Generazione chiavi RSA (piccola)
Con $p = 11$, $q = 13$:
- Calcola $n$ e $\phi(n)$
- Scegli un $e$ valido
- Calcola $d$
- Cifra $m = 7$ e verifica la decifratura

### Esercizio 2 — Verifica del Teorema di Eulero
Verifica che $3^{\phi(10)} \equiv 1 \pmod{10}$.

### Esercizio 3 — Firma digitale
Con la chiave dell'Esercizio 1, firma $m = 5$:
- Calcola $\sigma = m^d \pmod n$
- Verifica che $\sigma^e \equiv m \pmod n$

### Esercizio 4 — Ragionamento sulla sicurezza
Un avversario conosce $n = 3233$ e lo fattorizza come $61 \times 53$. Sapendo che la chiave pubblica è $(e = 17, n = 3233)$, come calcolerebbe $d$? Perché eliminare $p$ e $q$ dopo la generazione non salva la chiave se $n$ è già stato fattorizzato?

### Esercizio 5 — Lab Cisco esteso
Dopo aver configurato SSH con i passaggi descritti:
1. Verifica con `show ip ssh` che SSH sia attivo
2. Testa il blocco brute force sbagliando intenzionalmente la password 3 volte
3. Con `show login` verifica lo stato del blocco

### Esercizio 6 — Python
```python
# Verifica RSA con Python
p, q = 61, 53
n = p * q
phi_n = (p-1) * (q-1)
e = 17
d = pow(e, -1, phi_n)   # inverso modulare — Python 3.8+
m = 42
c = pow(m, e, n)
m_dec = pow(c, d, n)
print(f"Originale: {m}, Cifrato: {c}, Decifrato: {m_dec}")
assert m == m_dec, "Errore!"
```

> [!TIP]
> `pow(base, exp, mod)` in Python usa internamente l'**esponenziazione rapida** (square-and-multiply), lo stesso algoritmo che il router Cisco usa per RSA. Senza questo trucco, calcolare $2790^{2753}$ prima di prendere il modulo richiederebbe numeri con migliaia di cifre.

---

*← Parte 1: Fondamenti (aritmetica modulare, Fermat) | → Parte 3: Curve Ellittiche e Applicazioni Reali*
