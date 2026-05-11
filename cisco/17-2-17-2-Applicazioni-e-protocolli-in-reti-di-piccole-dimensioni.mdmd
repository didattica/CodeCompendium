# Modulo 17 — Applicazioni e Protocolli in Reti di Piccole Dimensioni

## 17.2 Applicazioni e Protocolli in Reti di Piccole Dimensioni

---

### 17.2.1 Applicazioni Comuni

Dopo aver configurato una rete, questa ha bisogno di determinati tipi di **applicazioni e protocolli** per funzionare correttamente.

> **Principio chiave:** La rete è utile solo quanto lo sono le applicazioni in essa utilizzate.

Esistono due forme di processi o programmi software che forniscono accesso alla rete:

---

#### Applicazioni di Rete

Le **applicazioni di rete** sono i programmi software utilizzati per comunicare attraverso la rete.

Alcune applicazioni per gli utenti finali sono **network-aware** (consapevoli della rete), ovvero:

- Implementano protocolli del layer applicativo
- Sono in grado di comunicare direttamente con i layer inferiori dello stack di protocolli

**Esempi:**
- Client e-mail
- Browser web

---

#### Servizi del Layer Applicativo

Altri programmi richiedono l'assistenza dei **servizi del layer applicativo** per utilizzare risorse di rete come:

- Trasferimento di file
- Spooling di stampa di rete

Benché trasparenti all'utente finale, questi servizi rappresentano i programmi che si interfacciano con la rete e preparano i dati per il trasferimento. Diversi tipi di dati (testo, grafica, video) richiedono servizi di rete diversi per garantire una preparazione adeguata per l'elaborazione nei layer inferiori del modello OSI.

> **Nota:** Ogni applicazione o servizio di rete utilizza **protocolli**, che definiscono gli standard e i formati di dati da utilizzare. Senza protocolli, la rete dati non potrebbe disporre di un modo condiviso per la formattazione e l'indirizzamento dei dati.

> **Strumento utile:** Su un sistema Windows è possibile utilizzare **Gestione Attività** per visualizzare le applicazioni, i processi e i servizi in esecuzione sul computer.

---

### 17.2.2 Protocolli Comuni

La maggior parte del lavoro di un tecnico di rete, in reti di piccole o grandi dimensioni, riguarda in una certa misura i **protocolli di rete**, che supportano le applicazioni e i servizi utilizzati dai dipendenti.

---

#### Accesso Remoto: Telnet e SSH

Gli amministratori di rete richiedono l'accesso remoto ai dispositivi e ai server di rete. Le due soluzioni più comuni sono:

| Protocollo | Descrizione |
|---|---|
| **Telnet** | Accesso remoto tradizionale, non cifrato |
| **SSH (Secure Shell)** | Alternativa sicura a Telnet, con cifratura della comunicazione |

**SSH** viene utilizzato per stabilire una connessione di accesso remoto protetta tra un client SSH e altri dispositivi abilitati SSH:

- **Dispositivo di rete** (router, switch, access point, ecc.) — deve supportare SSH per fornire servizi di accesso remoto ai client
- **Server** (web, e-mail, ecc.) — deve supportare i servizi SSH per l'accesso remoto ai client

> Una volta connessi tramite SSH, gli amministratori possono accedere al dispositivo come se fossero connessi **localmente**.

---

#### Server di Rete Comuni e Protocolli Associati

| Server | Protocolli | Funzione |
|---|---|---|
| **Server Web** | HTTP, HTTPS | Scambio di contenuti web; HTTPS per comunicazioni sicure |
| **Server E-mail** | SMTP, POP3, IMAP | Invio e ricezione di messaggi di posta elettronica |
| **Server FTP** | FTP, FTPS, SFTP | Download e upload di file tra client e server |
| **Server DHCP** | DHCP | Assegnazione automatica di configurazioni IP ai client |
| **Server DNS** | DNS | Risoluzione di nomi di dominio in indirizzi IP |

---

##### Server Web

- I client e i server web scambiano traffico utilizzando **HTTP** (Hypertext Transfer Protocol)
- **HTTPS** (Hypertext Transfer Protocol Secure) viene utilizzato per la comunicazione web sicura

---

##### Server E-mail

- I server e i client utilizzano **SMTP** (Simple Mail Transfer Protocol) per **inviare** messaggi di posta elettronica
- I client utilizzano **POP3** (Post Office Protocol) o **IMAP** (Internet Message Access Protocol) per **recuperare** la posta elettronica
- I destinatari vengono specificati nel formato `user@xyz.xxx`

---

##### Server FTP

- **FTP** (File Transfer Protocol) consente di scaricare e caricare file tra un client e un server
- **FTPS** (FTP Secure) e **SFTP** (Secure FTP) vengono utilizzati per proteggere lo scambio di file

---

##### Server DHCP

- **DHCP** (Dynamic Host Configuration Protocol) viene utilizzato dai client per acquisire automaticamente una configurazione IP, che include:
  - Indirizzo IP
  - Subnet mask
  - Gateway predefinito
  - Ulteriori parametri di configurazione

---

##### Server DNS

- **DNS** (Domain Name System) risolve un nome di dominio in un indirizzo IP
  - Esempio: `cisco.com` → `72.163.4.185`
- Fornisce l'indirizzo IP di un sito web (nome di dominio) a un host richiedente

---

> **Nota:** Un singolo server può fornire **più servizi di rete contemporaneamente**. Ad esempio, un server può fungere da server e-mail, FTP e SSH allo stesso tempo.

---

#### Struttura di un Protocollo di Rete

I protocolli di rete costituiscono gli strumenti fondamentali di un professionista della rete. Ciascun protocollo definisce:

- I **processi** in una delle due estremità di una sessione di comunicazione
- I **tipi di messaggi**
- La **sintassi** dei messaggi
- Il **significato dei campi informativi**
- Il **modo in cui i messaggi vengono inviati** e la risposta prevista
- L'**interazione con il layer inferiore** successivo

> **Best practice:** Molte aziende hanno stabilito una politica per l'utilizzo di **versioni sicure** dei protocolli (es. SSH, SFTP, HTTPS) ove possibile.

---

### 17.2.3 Applicazioni Voce e Video

Le aziende utilizzano sempre più la **telefonia IP** e lo **streaming multimediale** per comunicare con clienti e partner commerciali. Molti utenti richiedono accesso a software e file aziendali, nonché supporto per applicazioni vocali e video, anche da remoto.

L'amministratore di rete deve garantire che:
- Nella rete siano installate le **apparecchiature adeguate**
- I dispositivi siano configurati per garantire la **consegna in base alle priorità**

---

#### Infrastruttura

- L'infrastruttura di rete deve supportare le **applicazioni in tempo reale**
- I dispositivi e i cavi esistenti devono essere **testati e convalidati**
- Potrebbero essere necessari **prodotti di rete più recenti**

---

#### VoIP (Voice over IP)

- I dispositivi VoIP convertono i **segnali telefonici analogici** in **pacchetti IP digitali**
- In genere è **meno costoso** di una soluzione di telefonia IP dedicata, ma la qualità delle comunicazioni può essere inferiore
- Per reti vocali e video di piccole dimensioni è possibile utilizzare soluzioni come **Skype** o versioni non aziendali di **Cisco WebEx**

---

#### Telefonia IP

- Un **telefono IP** esegue la conversione da voce a IP utilizzando un **server dedicato** per il controllo delle chiamate e la segnalazione
- Molti fornitori offrono soluzioni di telefonia IP per piccole imprese, come i prodotti **Cisco Business Edition 4000 Series**

---

#### Applicazioni in Tempo Reale

- La rete deve supportare meccanismi di **QoS (Quality of Service)** per ridurre al minimo i problemi di latenza per le applicazioni di streaming in tempo reale
- I protocolli che supportano questo requisito sono:

| Protocollo | Nome completo | Funzione |
|---|---|---|
| **RTP** | Real-Time Transport Protocol | Trasporto dei dati multimediali in tempo reale |
| **RTCP** | Real-Time Transport Control Protocol | Monitoraggio e controllo della qualità della sessione RTP |

---

## ✅ Domande di Verifica — Modulo 17.2

---

### Domanda 1
**Quali sono due forme di programmi software o processi che forniscono l'accesso alla rete? (Scegliere due risposte.)**

| | Opzione |
|---|---|
| ❌ | Software di gioco |
| ❌ | Software antivirus |
| ❌ | Software di produttività |
| ❌ | Software di macchine virtuali |
| ✅ | **Applicazioni di rete** |
| ✅ | **Servizi del layer applicativo** |

> **Spiegazione:** Come descritto nella sezione 17.2.1, le due forme di programmi che forniscono accesso alla rete sono le **applicazioni di rete** (come browser e client e-mail, che implementano direttamente i protocolli del layer applicativo) e i **servizi del layer applicativo** (che operano in modo trasparente per preparare i dati al trasferimento). Software di gioco, antivirus e produttività sono categorie generiche di applicazioni, ma non identificano le due forme specifiche di accesso alla rete descritte nel modulo.

---

### Domanda 2
**Quali due protocolli di rete vengono utilizzati per stabilire una connessione di rete di accesso remoto a un dispositivo? (Scegliere due risposte.)**

| | Opzione |
|---|---|
| ❌ | Remote Connect (RC) |
| ❌ | Hypertext Transfer Protocol (HTTP) |
| ✅ | **Secure Shell (SSH)** |
| ❌ | FTP (File Transfer Protocol) |
| ✅ | **Telnet** |
| ❌ | Simple Mail Transfer Protocol (SMTP) |

> **Spiegazione:** Come illustrato nella sezione 17.2.2, le due soluzioni standard per l'accesso remoto ai dispositivi di rete sono **Telnet** e **SSH**. Telnet è il protocollo tradizionale, mentre SSH rappresenta l'alternativa sicura con cifratura della comunicazione. HTTP è un protocollo per il web, FTP per il trasferimento di file, SMTP per la posta elettronica, e "Remote Connect (RC)" non è un protocollo Cisco standard.

---

*Materiale didattico basato sul curriculum Cisco Networking Academy — Modulo 17.2*
