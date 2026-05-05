# 🌐 Guida Completa: Configurazione Telnet su Router Cisco

## 📋 Prerequisiti

> [!NOTE]
> Questa guida utilizza il file Packet Tracer: **16.5.1-packet-tracer---secure-network-devices.pka**
>
> **Cosa ti serve:**
> - Un PC connesso al router tramite cavo console (azzurro)
> - Accesso fisico al router
> - Conoscenza degli indirizzi IP del router

---

## 🔌 Fase 1: Connessione Iniziale via Cavo Console

### Step 1.1: Collegamento Fisico

> [!TIP]
> Il **cavo console azzurro** è la tua "chiave di emergenza" per accedere al router quando nessun altro metodo funziona.

1. Collega il cavo console azzurro tra il PC e la porta Console del router
2. Apri il terminale del PC
3. Accedi alla CLI del router

### Step 1.2: Verifica degli Indirizzi IP

Una volta connesso, verifica gli indirizzi IP configurati sul router:

```bash
Router> enable
Router# show ip interface brief
```

**Output atteso:**

```
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0/0   192.168.1.1     YES manual up                    up 
GigabitEthernet0/0/1   192.168.2.1     YES manual up                    up
```

> [!IMPORTANT]
> Annota questi indirizzi IP! Ti serviranno per connetterti via Telnet dal PC.

### Step 1.3: Test di Connettività

Prima di configurare Telnet, verifica che il PC possa raggiungere il router:

```bash
# Dal PC, esegui ping verso l'interfaccia del router
ping 192.168.1.1
```

> [!WARNING]
> Se il ping funziona ma Telnet non risponde, è normale! Il servizio Telnet **non è ancora configurato**.

---

## ⚙️ Configurazione Preventiva: Disabilitare la Ricerca DNS

### Problema Comune: Il Router "Si Blocca"

> [!CAUTION]
> **Scenario tipico:**
> Digiti un comando sbagliato (es. `conft` invece di `conf t`) e il router sembra congelarsi per diversi secondi.
>
> **Cosa succede:** Il router pensa che tu stia cercando di connetterti a un server chiamato "conft" e inizia una ricerca DNS che rallenta tutto.

### La Soluzione

**Sblocco immediato (quando sei già bloccato):**
```
CTRL + SHIFT + 6
```

**Prevenzione definitiva:**

```bash
Router> enable
Router# configure terminal
Router(config)# no ip domain-lookup
Router(config)# exit
Router# write memory
```

> [!TIP]
> Il comando `no ip domain-lookup` disabilita la ricerca DNS automatica. Eseguilo sempre all'inizio della configurazione!

---

## 📡 Fase 2: Configurazione Telnet (Livello 1 - NESSUNA PASSWORD)

> [!DANGER]
> **Questa configurazione è ESTREMAMENTE INSICURA!** 
> Chiunque conosca l'IP del router può accedere senza alcuna autenticazione. Da usare solo per test in laboratorio.

### Step 2.1: Accesso alla Configurazione

```bash
Router> enable
Router# configure terminal
```

### Step 2.2: Configurare le Linee VTY

Le **linee VTY (Virtual TeletYpe)** sono "slot virtuali" che permettono connessioni remote simultanee.

```bash
Router(config)# line vty 0 4
Router(config-line)# transport input telnet
Router(config-line)# exit
Router(config)# exit
Router# write memory
```

**Spiegazione comandi:**
- `line vty 0 4` → Configura 5 slot virtuali (da 0 a 4) per connessioni contemporanee
- `transport input telnet` → Abilita solo il protocollo Telnet su queste linee

### Step 2.3: Verifica Configurazione

```bash
Router# show line
```

**Output atteso:**
Vedrai le linee VTY 0-4 elencate con stato "ready"

### Step 2.4: Test di Connessione

Dal PC, prova a connetterti:

```bash
telnet 192.168.1.1
```

> [!NOTE]
> Se tutto funziona, entrerai direttamente nella modalità utente (`Router>`) senza password!

---

## 🔐 Fase 3: Configurazione Telnet (Livello 2 - PASSWORD IN CHIARO)

> [!WARNING]
> Questa configurazione è più sicura della precedente, ma la password viaggia **in chiaro** sulla rete. Chiunque intercetti il traffico può leggerla!

### Step 3.1: Impostare Password VTY

```bash
Router> enable
Router# configure terminal
Router(config)# line vty 0 4
Router(config-line)# password cisco123
Router(config-line)# login
Router(config-line)# exit
Router(config)# exit
Router# write memory
```

**Spiegazione comandi:**
- `password cisco123` → Imposta la password per l'accesso Telnet
- `login` → Attiva la richiesta di password al login

### Step 3.2: Verifica Configurazione

```bash
Router# show running-config
```

Cerca la sezione:
```
line vty 0 4
 password cisco123
 login
 transport input telnet
```

> [!CAUTION]
> Guarda attentamente: la password appare **in chiaro** nella configurazione! Chiunque acceda al router può leggerla.

### Step 3.3: Test di Connessione

Dal PC:

```bash
telnet 192.168.1.1
```

**Output atteso:**
```
Trying 192.168.1.1...
Connected to 192.168.1.1.

User Access Verification

Password: [digita cisco123]
Router>
```

---

## 🛡️ Fase 4: Configurazione Telnet (Livello 3 - PASSWORD CIFRATA)

> [!TIP]
> Questa è la configurazione più sicura possibile per Telnet. La password viene cifrata nella configurazione del router.

### Step 4.1: Abilitare la Cifratura delle Password

```bash
Router> enable
Router# configure terminal
Router(config)# service password-encryption
Router(config)# exit
Router# write memory
```

### Step 4.2: Verifica Cifratura

```bash
Router# show running-config
```

**Prima della cifratura:**
```
line vty 0 4
 password cisco123
```

**Dopo la cifratura:**
```
line vty 0 4
 password 7 0822455D0A16
```

> [!NOTE]
> Il numero `7` indica il tipo di cifratura Cisco Type 7. La stringa esadecimale è la password cifrata.

### Step 4.3: Protezione Aggiuntiva - Enable Secret

Per proteggere l'accesso alla modalità privilegiata:

```bash
Router> enable
Router# configure terminal
Router(config)# enable secret @Sicurezza123!
Router(config)# exit
Router# write memory
```

**Differenza tra enable password e enable secret:**
- `enable password` → Password in chiaro o cifrata Type 7 (debole)
- `enable secret` → Password cifrata con MD5 (molto più sicuro)

> [!IMPORTANT]
> Usa sempre `enable secret`, mai `enable password`!

---

## 📊 Comandi di Diagnostica Utili

### Visualizzare le Linee VTY Attive

```bash
Router# show line
```

**Da dove si esegue:** Modalità privilegiata (`Router#`)

**Cosa mostra:** Tutte le linee disponibili (console, aux, vty) con:
- Numero linea
- Tipo di connessione
- Stato (in uso / libera)
- Timeout configurato

### Disabilitare la Ricerca DNS

```bash
Router(config)# no ip domain-lookup
```

**Da dove si esegue:** Modalità configurazione globale (`Router(config)#`)

**Cosa fa:** Impedisce al router di interpretare comandi errati come nomi di host da risolvere via DNS

### Configurare Range di Linee VTY

```bash
Router(config)# line vty 0 ?
```

**Da dove si esegue:** Modalità configurazione globale

**Cosa mostra:** Il numero massimo di linee VTY disponibili (solitamente 15)

**Esempio:**
- `line vty 0 4` → Prime 5 linee (connessioni simultane da 0 a 4)
- `line vty 0 15` → Tutte le 16 linee disponibili

### Specificare Protocolli di Input

```bash
Router(config-line)# transport input telnet
```

**Da dove si esegue:** Modalità configurazione linea (`Router(config-line)#`)

**Opzioni disponibili:**
- `transport input telnet` → Solo Telnet
- `transport input ssh` → Solo SSH
- `transport input all` → Telnet e SSH
- `transport input none` → Nessun accesso remoto

---

## 🔍 Tabella Riepilogativa Livelli di Sicurezza

| Livello | Configurazione | Sicurezza | Uso Consigliato |
|---------|---------------|-----------|------------------|
| **Livello 1** | Nessuna password | ⚠️ Molto bassa | Solo test in laboratorio isolato |
| **Livello 2** | Password in chiaro | ⚠️⚠️ Bassa | Test in rete locale protetta |
| **Livello 3** | Password cifrata Type 7 | ⚠️⚠️⚠️ Media | Ambienti didattici controllati |
| **Raccomandato** | SSH con chiavi RSA | ✅ Alta | Ambienti di produzione |

---

## ⚠️ Limitazioni di Sicurezza di Telnet

> [!DANGER]
> **TELNET È INTRINSECAMENTE INSICURO!**
>
> ### Problemi principali:
>
> 1. **Tutto in chiaro:** Password, comandi e dati viaggiano non cifrati sulla rete
> 2. **Intercettabile:** Chiunque con accesso alla rete può "ascoltare" la sessione con tool come Wireshark
> 3. **Vulnerabile:** Nessuna protezione contro attacchi man-in-the-middle
> 4. **Type 7 debole:** La cifratura Cisco Type 7 può essere decifrata in secondi con tool online
>
> ### Regola d'oro:
> **Usa Telnet SOLO per:**
> - Laboratori didattici isolati
> - Test in ambiente protetto
> - Dispositivi legacy che non supportano SSH

---

## 🚀 Prossimi Passi

> [!NOTE]
> ### 📘 Prossimo Documento: Configurazione SSH
>
> Nel prossimo tutorial vedremo come configurare **SSH (Secure Shell)**, il protocollo che ha sostituito Telnet negli ambienti di produzione.
>
> **Cosa imparerai:**
> - Generazione di chiavi RSA
> - Configurazione SSH versione 2
> - Autenticazione con username/password
> - Best practices di sicurezza
> - Confronto diretto SSH vs Telnet
>
> **Perché SSH è meglio:**
> - Cifratura end-to-end
> - Autenticazione con chiavi pubbliche/private
> - Protezione contro attacchi di rete
> - Standard industriale per accesso remoto sicuro

---

## 📚 Comandi Quick Reference

```bash
# Disabilita DNS lookup (da fare sempre!)
Router(config)# no ip domain-lookup

# Verifica IP delle interfacce
Router# show ip interface brief

# Configura Telnet base (NO PASSWORD)
Router(config)# line vty 0 4
Router(config-line)# transport input telnet

# Configura Telnet con password in chiaro
Router(config)# line vty 0 4
Router(config-line)# password cisco123
Router(config-line)# login

# Abilita cifratura password
Router(config)# service password-encryption

# Proteggi modalità privilegiata
Router(config)# enable secret @Sicurezza123!

# Verifica configurazione
Router# show running-config
Router# show line

# Salva configurazione
Router# write memory
```

---

> [!TIP]
> ### 💡 Ricorda:
> - **CTRL + SHIFT + 6** per sbloccare ricerche DNS bloccate
> - Salva sempre con `write memory` dopo ogni modifica
> - Testa la connessione da un altro dispositivo prima di disconnettere il cavo console!

---

**Documento creato per il Modulo 16 - Cisco CCNA**  
*Versione: 1.0 | Ultimo aggiornamento: 2026*
