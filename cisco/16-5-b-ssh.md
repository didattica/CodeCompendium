# 🔐 Guida Completa: Configurazione SSH su Router Cisco

## 📋 Prerequisiti

> [!NOTE]
> Questa guida utilizza il file Packet Tracer: **16.5.1-packet-tracer---secure-network-devices.pka**
>
> **Cosa ti serve:**
> - Un PC connesso al router tramite cavo console (azzurro)
> - Il PC deve essere nella stessa rete di una delle interfacce del router
> - Accesso fisico al router tramite console per la configurazione iniziale

---

## 🧠 Sezione 0 — Perché SSH? Teoria e Confronto con Telnet

### SSH vs Telnet: confronto diretto

SSH (Secure Shell) è il protocollo standard per l'accesso remoto sicuro ai dispositivi di rete. A differenza di Telnet, SSH cifra l'intero canale di comunicazione, rendendo impossibile intercettare credenziali e comandi.

| Caratteristica | Telnet | SSH |
|----------------|--------|-----|
| Cifratura | ❌ Nessuna (testo in chiaro) | ✅ AES, 3DES, ecc. |
| Autenticazione | Password semplice | Password + chiavi RSA |
| Porta standard | 23 | 22 |
| Intercettabile? | ✅ Sì – con Wireshark | ❌ No – traffico cifrato |
| Versione sicura | Non esiste | SSH v2 (raccomandata) |
| Uso consigliato | Solo laboratorio isolato | Ambienti di produzione |

> [!CAUTION]
> **TELNET IN PRODUZIONE È UN RISCHIO CRITICO!**
>
> Con Wireshark, chiunque sulla stessa rete può catturare le tue credenziali in pochi secondi.
> SSH è lo standard industriale: usalo **SEMPRE** in ambienti reali.

---

### Come funziona SSH: la crittografia asimmetrica

SSH utilizza un sistema a chiave pubblica/privata (RSA) per autenticare il router e negoziare una chiave di sessione simmetrica:

1. Il router genera una coppia di chiavi RSA (pubblica + privata)
2. Il client si connette e il router invia la chiave pubblica
3. Il client cifra un messaggio di sfida con la chiave pubblica
4. Solo il router (con la chiave privata) può decifrarlo → autenticazione
5. Viene negoziata una chiave di sessione per cifrare tutto il traffico

> [!NOTE]
> **RSA Key Size — Linee guida:**
> - **512 bit** → Insicuro, rifiutato da SSH v2
> - **768-1024 bit** → Minimo accettabile, non raccomandato
> - **2048 bit** → ✅ RACCOMANDATO per produzione
> - **4096 bit** → Massima sicurezza, generazione più lenta
>
> Usa sempre **2048 bit** come best practice!

---

### La sintassi del comando `ssh -l`

Prima di iniziare la configurazione, è importante capire il comando con cui ci si connette via SSH dal PC:

```bash
PC> ssh -l SSHadmin 192.168.1.1
```

| Parte del comando | Significato |
|-------------------|-------------|
| `ssh` | Comando SSH disponibile dal terminale PC in Packet Tracer |
| `-l` | Flag *login*: specifica il nome utente (NON la password) |
| `SSHadmin` | Username configurato sul router (**case sensitive!**) |
| `192.168.1.1` | Indirizzo IP dell'interfaccia raggiungibile del router |

> [!TIP]
> **Differenza `-l` vs `-p`**
>
> ```
> ssh -l SSHadmin 192.168.1.1   → specifica lo username
> ssh -p 2222 192.168.1.1       → specifica una porta non standard
> ```
> In Packet Tracer si usa sempre la sintassi con `-l` seguita dallo username.

---

## 🔌 Fase 1 — Connessione Iniziale e Preparazione

### Step 1.1: Verifica degli indirizzi IP

Connettiti al router via cavo console e verifica le interfacce:

```bash
Router> enable
Router# show ip interface brief
```

**Output atteso:**

```
Interface              IP-Address      OK? Method Status    Protocol
GigabitEthernet0/0/0   192.168.1.1     YES manual up        up
GigabitEthernet0/0/1   192.168.2.1     YES manual up        up
```

> [!IMPORTANT]
> Annota l'indirizzo IP dell'interfaccia raggiungibile dal tuo PC.
> Questo IP sarà usato nel comando `ssh -l SSHadmin <IP>`.
>
> Il **cavo console azzurro** è la tua ancora di salvezza: non disconnetterlo mai prima di aver verificato che SSH funzioni!

---

### Step 1.2: Test di connettività

Prima di configurare SSH, verifica che il PC possa raggiungere il router:

```bash
PC> ping 192.168.1.1
```

> [!WARNING]
> Se il ping funziona ma SSH non risponde, è **normale**! Il servizio SSH non è ancora configurato.
> Il router non accetterà connessioni sulla porta 22 finché non viene abilitato.

---

### Step 1.3: Disabilita la ricerca DNS

> [!CAUTION]
> **Scenario tipico:** Digiti un comando sbagliato (es. `conft` invece di `conf t`) e il router sembra congelarsi per diversi secondi.
>
> **Cosa succede:** Il router pensa che tu stia cercando di connetterti a un server chiamato `conft` e avvia una ricerca DNS.
>
> **Sblocco immediato:** `CTRL + SHIFT + 6`

**Prevenzione definitiva:**

```bash
Router> enable
Router# configure terminal
Router(config)# no ip domain-lookup
Router(config)# exit
Router# write memory
```

---

## ⚙️ Fase 2 — Configurazione SSH (Step by Step con Errori)

> [!NOTE]
> **L'approccio graduale di questa guida**
>
> Invece di darti subito la configurazione perfetta, ti mostriamo gli errori tipici che si incontrano.
> Ogni step "rotto" ha una spiegazione e una soluzione. Questo ti aiuta a capire davvero SSH, non solo a copiare comandi.

---

### Step 2.1: Tentativo SSH senza configurazione — Primo errore

Proviamo a connetterci **prima** di configurare qualsiasi cosa:

```bash
PC> ssh -l SSHadmin 192.168.1.1
```

**Output che vedrai:**

```
% Connection refused by remote host
```

> [!CAUTION]
> **Analisi errore — Connection refused**
>
> Il router non ha SSH abilitato, quindi rifiuta qualsiasi connessione sulla porta 22.
> Le linee VTY usano ancora Telnet (o nessun protocollo).
>
> **Soluzione:** dobbiamo configurare SSH passo dopo passo.

---

### Step 2.2: Configura il domain name (obbligatorio!)

SSH richiede un domain name per generare le chiavi RSA. Senza di esso, la generazione fallirà:

```bash
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# ip domain-name cisco.local
```

> [!WARNING]
> **Cosa succede senza domain name:**
>
> Se tenti `crypto key generate rsa` senza `ip domain-name`:
> ```
> % Please define a domain-name first.
> ```
> Il router rifiuta di generare le chiavi! Il domain name è **obbligatorio**.

---

### Step 2.3: Generazione delle chiavi crittografiche RSA

Le chiavi RSA sono il cuore di SSH: senza di esse il protocollo non può funzionare.

```bash
Router(config)# crypto key generate rsa
```

**Interazione con il router:**

```
The name for the keys will be: Router.cisco.local
Choose the size of the key modulus in the range of 360 to 4096:
> 2048

% Generating 2048 bit RSA keys, keys will be non-exportable...
[OK] (elapsed time was 3 seconds)
```

> [!IMPORTANT]
> Inserisci sempre **2048** quando il router chiede la dimensione del modulo.
>
> Con chiavi inferiori a 768 bit, SSH v2 rifiuterà di avviarsi con l'errore:
> ```
> % SSH v2 requires RSA key pair of at least 768 bits.
> ```

---

### Step 2.4: Secondo tentativo SSH — Secondo errore atteso

Dopo aver generato le chiavi, riproviamo:

```bash
PC> ssh -l SSHadmin 192.168.1.1
```

**Output:**

```
Password:
Password:
Password:
% Authentication failed
```

> [!CAUTION]
> **Analisi errore — Authentication failed**
>
> Il router risponde (SSH è attivo!), ma l'autenticazione fallisce perché:
> 1. Non esiste ancora l'utente `SSHadmin` nel database locale
> 2. Le linee VTY non sono configurate per accettare SSH
> 3. Il metodo di login non è specificato
>
> **Soluzione:** creare l'utente e configurare le VTY nei prossimi step.

---

## 🔐 Fase 3 — Aggiungere Autenticazione Utente

### Step 3.1: Crea l'utente locale

SSH con autenticazione locale richiede che il router abbia un database utenti:

```bash
Router(config)# username SSHadmin privilege 15 secret Cisco@2026!
```

**Spiegazione parametri:**

| Parametro | Significato |
|-----------|-------------|
| `username SSHadmin` | Nome utente (deve corrispondere al parametro `-l`) |
| `privilege 15` | Livello massimo di privilegi (accesso diretto a `Router#`) |
| `secret Cisco@2026!` | Password cifrata con MD5 (usa `secret`, mai `password`!) |

> [!TIP]
> **`privilege 15` vs `privilege 1`**
>
> - `privilege 15` → l'utente entra direttamente in modo privilegiato (`Router#`)
> - `privilege 1` → l'utente entra in modo utente (`Router>`) e deve digitare `enable`
>
> Per un admin SSH, `privilege 15` è più comodo ma richiede una password forte!

---

### Step 3.2: Configura le linee VTY per SSH

```bash
Router(config)# line vty 0 4
Router(config-line)# transport input ssh
Router(config-line)# login local
Router(config-line)# exit
```

**Spiegazione comandi:**

- `transport input ssh` → accetta **SOLO** SSH, rifiuta Telnet
- `login local` → usa il database utenti locale per l'autenticazione

> [!WARNING]
> **Differenza critica: `login` vs `login local`**
>
> | Comando | Comportamento |
> |---------|--------------|
> | `login` | Usa la password configurata con `password <pwd>` sulla linea VTY |
> | `login local` | Usa il database `username`/`password` configurato con `username` |
>
> Per SSH con username, devi usare **`login local`**.
> Con solo `login` riceverai `Authentication failed` anche con la password giusta!

---

### Step 3.3: Terzo test SSH — Finalmente funziona (quasi)

```bash
PC> ssh -l SSHadmin 192.168.1.1
```

**Output:**

```
[Connecting to 192.168.1.1]... open

Password: [digita Cisco@2026!]

Router>
```

> [!CAUTION]
> **Attenzione: siamo entrati come `Router>` e non `Router#`!**
>
> Questo succede se l'utente è stato creato con `privilege 1` invece di `privilege 15`.
>
> **Soluzione:**
> ```bash
> Router(config)# no username SSHadmin
> Router(config)# username SSHadmin privilege 15 secret Cisco@2026!
> ```

---

## 🛡️ Fase 4 — SSH Versione 2 e Configurazione Sicura Completa

### Step 4.1: Forza SSH versione 2

SSH v2 è molto più sicuro di v1: corregge vulnerabilità crittografiche e aggiunge protezioni contro attacchi man-in-the-middle.

```bash
Router(config)# ip ssh version 2
```

> [!CAUTION]
> **SSH v1 è obsoleto e vulnerabile!**
>
> SSH v1 ha vulnerabilità crittografiche note dal 2001. Non usare **mai** `ip ssh version 1` in produzione.
>
> Se ricevi questo errore:
> ```
> % SSH v2 requires RSA key pair of at least 768 bits.
> ```
> Rigenera le chiavi con 2048 bit:
> ```bash
> Router(config)# crypto key zeroize rsa
> Router(config)# crypto key generate rsa   ← inserisci 2048
> ```

---

### Step 4.2: Configura timeout e retry SSH

Per migliorare la sicurezza, limitiamo il tempo di autenticazione e i tentativi falliti:

```bash
Router(config)# ip ssh time-out 60
Router(config)# ip ssh authentication-retries 3
```

| Comando | Effetto |
|---------|---------|
| `ip ssh time-out 60` | Disconnette se l'utente non si autentica entro 60 secondi |
| `ip ssh authentication-retries 3` | Massimo 3 tentativi di password, poi disconnette |

> [!TIP]
> **Protezione contro brute-force**
>
> Limitare i retry a 3 riduce drasticamente il rischio di attacchi a forza bruta.
> In produzione, abbina questa configurazione ad ACL per limitare gli IP che possono fare SSH.

---

### Step 4.3: Proteggi la modalità enable

```bash
Router(config)# enable secret @Sicurezza_Enable2026!
```

> [!IMPORTANT]
> **`enable secret` vs `enable password`**
>
> | Comando | Cifratura | Sicurezza |
> |---------|-----------|-----------|
> | `enable password` | Type 7 (decifrabile online in secondi) | ⚠️ Bassa |
> | `enable secret` | MD5 | ✅ Alta |
>
> Usa **sempre** `enable secret`. Non usare mai `enable password` da solo!

---

### Step 4.4: Verifica versione e stato SSH

```bash
Router# show ip ssh
```

**Output atteso:**

```
SSH Enabled - version 2.0
Authentication timeout: 60 secs; Authentication retries: 3
Minimum expected Diffie Hellman key size : 1024 bits
IOS Keys in SECSH format(ssh-rsa, base64 encoded): Router.cisco.local
```

---

## 🚫 Fase 5 — Disabilitare Telnet Definitivamente

> [!CAUTION]
> **ATTENZIONE: Telnet potrebbe essere ancora attivo!**
>
> Anche con SSH configurato, se non hai esplicitamente vietato Telnet, il router potrebbe ancora accettarlo. Verifica subito:
>
> ```bash
> PC> telnet 192.168.1.1
> ```
>
> Se risponde con `User Access Verification`, Telnet è **ancora attivo** — questo vanifica completamente la sicurezza di SSH!

### Step 5.1: Disabilita Telnet su tutte le linee VTY

```bash
Router(config)# line vty 0 4
Router(config-line)# transport input ssh
Router(config-line)# exit
```

> [!NOTE]
> **Quante linee VTY ha il tuo router?**
>
> ```bash
> Router(config)# line vty 0 ?
> ```
> Il router mostrerà il numero massimo disponibile (solitamente 4 o 15).
> Configura **TUTTE** le linee, non solo `0 4`!
>
> ```bash
> ! Se il router ha più di 5 linee VTY:
> Router(config)# line vty 5 15
> Router(config-line)# transport input ssh
> Router(config-line)# exit
> ```

---

### Step 5.2: Verifica che Telnet sia bloccato

```bash
PC> telnet 192.168.1.1
```

**Output atteso (Telnet bloccato correttamente):**

```
Trying 192.168.1.1...
% Connection refused by remote host
```

---

### Step 5.3: Opzioni `transport input` disponibili

```bash
Router(config-line)# transport input ?
```

| Opzione | Effetto |
|---------|---------|
| `transport input none` | Blocca **tutto** l'accesso remoto |
| `transport input ssh` | Solo SSH ✅ (raccomandato) |
| `transport input telnet` | Solo Telnet ⚠️ (insicuro!) |
| `transport input all` | SSH e Telnet ⚠️ (non raccomandato) |

---

## ✅ Fase 6 — Configurazione Completa: Script e Verifica

### Script di configurazione completo

```bash
! ══════════════════════════════════════════════════════
! CONFIGURAZIONE SSH COMPLETA – Router Cisco
! ══════════════════════════════════════════════════════

Router> enable
Router# configure terminal

! 1. Disabilita ricerca DNS
Router(config)# no ip domain-lookup

! 2. Configura hostname (necessario per RSA)
Router(config)# hostname R1

! 3. Configura domain name (obbligatorio per RSA)
R1(config)# ip domain-name cisco.local

! 4. Crea utente amministratore SSH
A1(config)# username SSHadmin privilege 15 secret Cisco@2026!

! 5. Genera chiavi RSA 2048 bit
R1(config)# crypto key generate rsa
! → Inserisci: 2048

! 6. Forza SSH versione 2
R1(config)# ip ssh version 2

! 7. Configura parametri SSH
R1(config)# ip ssh time-out 60
R1(config)# ip ssh authentication-retries 3

! 8. Configura linee VTY – solo SSH, login locale
R1(config)# line vty 0 4
R1(config-line)# transport input ssh
R1(config-line)# login local
R1(config-line)# exit

! 9. Proteggi enable con secret
R1(config)# enable secret @Sicurezza_Enable2026!

! 10. Salva configurazione
R1(config)# exit
R1# write memory
```

---

### Comandi di verifica

```bash
! Verifica SSH abilitato e versione
R1# show ip ssh

! Verifica sessioni SSH attive e cifratura usata
R1# show ssh

! Verifica chiavi RSA generate
R1# show crypto key mypubkey rsa

! Verifica configurazione VTY
R1# show running-config | section line vty

! Verifica utenti locali
R1# show running-config | section username

! Verifica running-config completa
R1# show running-config
```

> [!TIP]
> **Verifica sessioni attive con `show ssh`**
>
> ```
> R1# show ssh
> Connection  Version  Mode  Encryption   Hmac       State            Username
> 0           2.0      IN    aes256-cbc   hmac-sha1  Session started  SSHadmin
> ```
> Questo conferma che la sessione SSH è cifrata con **AES-256**!

---

## 🔍 Fase 7 — Troubleshooting: Problemi Comuni e Soluzioni

### Errore: `% Please define a domain-name first`

```
R1(config)# crypto key generate rsa
% Please define a domain-name first.
```

> [!CAUTION]
> **Causa:** Non hai configurato `ip domain-name` prima di generare le chiavi.
>
> **Soluzione:**
> ```bash
> R1(config)# ip domain-name cisco.local
> R1(config)# crypto key generate rsa
> ```

---

### Errore: `% SSH v2 requires RSA key pair of at least 768 bits`

```
R1(config)# ip ssh version 2
% SSH v2 requires RSA key pair of at least 768 bits.
```

> [!CAUTION]
> **Causa:** Le chiavi RSA sono state generate con meno di 768 bit (es. 512).
>
> **Soluzione:**
> ```bash
> R1(config)# crypto key zeroize rsa
> R1(config)# crypto key generate rsa   ← inserisci 2048
> ```

---

### Errore: `% Authentication failed` (password corretta)

```
PC> ssh -l SSHadmin 192.168.1.1
Password:
% Authentication failed
```

> [!CAUTION]
> **Causa 1:** Le VTY usano `login` invece di `login local`
> ```bash
> R1(config-line)# login local
> ```
>
> **Causa 2:** L'utente non esiste nel database locale
> ```bash
> R1(config)# username SSHadmin privilege 15 secret Cisco@2026!
> ```
>
> **Causa 3:** Errore di digitazione nello username (case sensitive!)
> Verifica: `ssh -l SSHadmin` (S maiuscola, H maiuscola)

---

### Errore: `% Connection refused by remote host`

```
PC> ssh -l SSHadmin 192.168.1.1
% Connection refused by remote host
```

> [!CAUTION]
> **Causa 1:** SSH non è abilitato (chiavi RSA non generate)
> ```bash
> R1# show ip ssh   ← verifica se SSH è enabled
> ```
>
> **Causa 2:** Le VTY usano `transport input none` o `transport input telnet`
> ```bash
> R1(config-line)# transport input ssh
> ```
>
> **Causa 3:** L'IP di destinazione non è raggiungibile
> ```bash
> PC> ping 192.168.1.1
> ```

---

### Problema: Entro come `Router>` invece di `Router#`

```
PC> ssh -l SSHadmin 192.168.1.1
Password:
Router>    ← modalità utente, non privilegiata!
```

> [!CAUTION]
> **Causa:** L'utente è stato creato con `privilege 1` invece di `privilege 15`.
>
> **Soluzione:**
> ```bash
> R1(config)# no username SSHadmin
> R1(config)# username SSHadmin privilege 15 secret Cisco@2026!
> ```

---

## 📊 Tabelle Riepilogative

### Livelli di sicurezza SSH

| Fase | Configurazione | Sicurezza | Uso consigliato |
|------|----------------|-----------|-----------------|
| **Fase 1** | SSH senza utente DB | ⚠️ Bassa | Solo test iniziali |
| **Fase 2** | SSH + username locale | ⚠️⚠️ Media | Lab controllato |
| **Fase 3** | SSH v2 + RSA 2048 bit | ✅ Alta | Ambienti di produzione |
| **Fase 4** | SSH v2 + disable Telnet | ✅✅ Molto alta | Standard aziendale |

---

### Confronto metodi di autenticazione

| Metodo | Comando | Sicurezza | Note |
|--------|---------|-----------|------|
| Nessuna password | *(nessun login)* | ❌ Nulla | Solo lab isolato |
| Password VTY in chiaro | `password cisco` + `login` | ⚠️ Bassa | Evitare |
| Password VTY cifrata | `password cisco` + `service password-encryption` | ⚠️⚠️ Media | Type 7, decifrabile |
| Username + secret | `username` + `login local` | ✅ Alta | **Raccomandato** |

---

## 📚 Quick Reference — Comandi SSH

```bash
! ── PREREQUISITI ────────────────────────────────────────
Router(config)# no ip domain-lookup          # Disabilita DNS
Router(config)# hostname R1                  # Imposta hostname
R1(config)#     ip domain-name cisco.local   # Domain name (obbligatorio!)

! ── UTENTE E CHIAVI ─────────────────────────────────────
R1(config)# username SSHadmin privilege 15 secret Cisco@2026!
R1(config)# crypto key generate rsa          # Scegli 2048 bit
R1(config)# crypto key zeroize rsa           # Elimina chiavi esistenti

! ── SSH ─────────────────────────────────────────────────
R1(config)# ip ssh version 2
R1(config)# ip ssh time-out 60
R1(config)# ip ssh authentication-retries 3

! ── VTY (disabilita Telnet, abilita SSH) ─────────────────
R1(config)# line vty 0 4
R1(config-line)# transport input ssh
R1(config-line)# login local
R1(config-line)# exit

! ── PROTEZIONE ENABLE ───────────────────────────────────
R1(config)# enable secret @Sicurezza_Enable2026!

! ── SALVATAGGIO ─────────────────────────────────────────
R1# write memory

! ── VERIFICA ────────────────────────────────────────────
R1# show ip ssh
R1# show ssh
R1# show crypto key mypubkey rsa
R1# show running-config | section line vty

! ── CONNESSIONE DA PC ───────────────────────────────────
PC> ssh -l SSHadmin 192.168.1.1
```

---

> [!TIP]
> ### 💡 Ricorda i 3 comandi chiave:
>
> 1. **`crypto key generate rsa`** → cuore di SSH, genera la coppia di chiavi (usa 2048 bit!)
> 2. **`transport input ssh`** → blocca Telnet, accetta solo SSH
> 3. **`login local`** → usa il database utenti, non la password VTY

---

> [!NOTE]
> ### 📘 Documento precedente: Configurazione Telnet
>
> Questa guida è il naturale seguito della **Guida Telnet** (Modulo 16).
> Ora che conosci SSH, sai perché Telnet non dovrebbe mai essere usato in produzione.
>
> **Differenza fondamentale:**
> - Telnet → tutto in chiaro, intercettabile con Wireshark
> - SSH → traffico cifrato end-to-end, standard industriale

---

**Documento creato per il Modulo 16 - Cisco CCNA**  
*Versione: 1.0 | Ultimo aggiornamento: 2026*
