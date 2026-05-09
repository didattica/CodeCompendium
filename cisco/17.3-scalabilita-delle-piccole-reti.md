# Modulo 17 – Costruire una Piccola Rete

## 17.3 Scalabilità delle Piccole Reti

---

### 17.3.1 Crescita delle Piccole Reti

La crescita è un processo naturale per molte piccole imprese: la rete aziendale deve essere in grado di crescere di conseguenza. Se una rete è progettata per una piccola impresa, si presuppone che tale azienda possa espandersi, e la rete deve **scalare** insieme ad essa.

Idealmente, l'amministratore di rete dispone di tempo sufficiente per prendere decisioni ponderate sulla crescita della rete, in linea con la crescita dell'azienda.

#### Elementi necessari per implementare la scalabilità

Per scalare correttamente una rete sono necessari i seguenti elementi:

| Elemento | Descrizione |
|---|---|
| **Documentazione di rete** | Topologia fisica e logica della rete |
| **Inventario dei dispositivi** | Elenco dei dispositivi che utilizzano o costituiscono la rete |
| **Budget** | Budget IT dettagliato, incluso il costo previsto per l'acquisto di apparecchiature nell'anno fiscale |
| **Analisi del traffico** | Documentazione di protocolli, applicazioni, servizi e relativi requisiti di traffico |

> [!NOTE]
> Questi elementi forniscono informazioni essenziali per supportare il processo decisionale che accompagna la scalabilità di una piccola rete.

---

### 17.3.2 Analisi dei Protocolli

Man mano che la rete cresce, diventa fondamentale determinare come gestire il traffico di rete. È importante:

- Comprendere il **tipo di traffico** che attraversa la rete.
- Analizzare il **flusso di traffico corrente**.

#### Strumenti di analisi

Esistono diversi strumenti di gestione della rete per questo scopo. Uno dei più utilizzati in ambito didattico e operativo è **Wireshark**, un analizzatore di protocollo open source.

Eseguire Wireshark su diversi host chiave della rete consente di:

- Identificare i **tipi di traffico** che scorrono attraverso la rete.
- Visualizzare le **statistiche della gerarchia dei protocolli** (ad esempio per un host Windows in una rete di piccole dimensioni).

#### Best practice per la cattura del traffico

Per determinare correttamente i modelli di flusso del traffico, è importante seguire queste indicazioni:

- **Acquisire il traffico durante le ore di picco** di utilizzo, per ottenere una rappresentazione realistica dei diversi tipi di traffico.
- **Eseguire l'acquisizione su diversi segmenti di rete e dispositivi**, poiché una parte del traffico è locale per un particolare segmento e potrebbe non essere visibile altrove.

#### Utilizzo dell'analisi

Le informazioni raccolte dall'analizzatore di protocollo vengono valutate in base a:

- **Origine e destinazione** del traffico.
- **Tipo di traffico** inviato.

Questa analisi consente di prendere decisioni su come gestire il traffico in modo più efficiente, ad esempio:

- Ridurre i **flussi di traffico superflui**.
- Modificare interi **modelli di flusso**, come spostare un server in un segmento di rete diverso.

> [!TIP]
> In alcuni casi, riassegnare semplicemente un server o un servizio a un altro segmento di rete è sufficiente per migliorare le prestazioni. In altri casi, può rendersi necessaria una **riprogettazione completa** della rete.

---

### 17.3.3 Utilizzo della Rete da Parte dei Dipendenti

Oltre a comprendere le tendenze del traffico, un amministratore di rete deve monitorare come **cambia l'utilizzo della rete** nel tempo da parte degli utenti.

#### Strumenti integrati in Windows

I sistemi operativi Windows forniscono diversi strumenti integrati per raccogliere queste informazioni:

- **Task Manager** – Monitoraggio in tempo reale di CPU, RAM, rete e processi.
- **Visualizzatore eventi** – Registro degli eventi di sistema, applicazione e sicurezza.
- **Utilizzo dati (Data Usage)** – Statistiche sul consumo di rete per applicazione.

#### Informazioni raccoglibili ("istantanea")

Questi strumenti consentono di acquisire una **fotografia** dello stato del sistema in un dato momento, includendo:

- Sistema operativo e relativa versione
- Utilizzo CPU
- Utilizzo della RAM
- Utilizzo del disco
- Applicazioni **non di rete** in esecuzione
- Applicazioni **di rete** in esecuzione

> [!IMPORTANT]
> Documentare istantanee periodiche per i dipendenti in una piccola rete è utile per identificare l'**evoluzione dei requisiti dei protocolli** e dei flussi di traffico associati. Un cambiamento nell'utilizzo delle risorse può richiedere che l'amministratore adegui di conseguenza l'allocazione delle risorse di rete.

#### Strumento Utilizzo Dati – Windows 10

Lo strumento **Utilizzo dati** di Windows 10 è particolarmente indicato per determinare quali applicazioni utilizzano i servizi di rete su un host.

**Percorso di accesso:**

```
Settings > Network & Internet > Data usage > [interfaccia di rete]
```

Questo strumento mostra il consumo di rete per singola applicazione negli **ultimi 30 giorni**, ed è molto utile per analizzare l'utilizzo su host remoti connessi tramite Wi-Fi o altre interfacce.

---

## ✅ Domande di Verifica

### Domanda 1

**Quali elementi sono necessari per scalare su una rete più grande?** *(Scegliere due risposte.)*

- [x] **Budget** ✔️
- [ ] Configurazioni del dispositivo
- [ ] Host di Windows
- [x] **Documentazione della rete** ✔️
- [ ] Maggiore larghezza di banda

> [!NOTE]
> **Risposte corrette: `Budget` e `Documentazione della rete`**
>
> | Opzione | Esito | Motivazione |
> |---|---|---|
> | **Budget** | ✅ Corretto | Il budget IT è uno degli elementi esplicitamente elencati nella sezione 17.3.1. Permette di pianificare l'acquisto di nuove apparecchiature necessarie alla crescita della rete. |
> | **Documentazione della rete** | ✅ Corretto | La documentazione di topologia fisica e logica è fondamentale per comprendere lo stato attuale della rete e pianificare l'espansione in modo informato. |
> | Configurazioni del dispositivo | ❌ Errato | Le configurazioni dei singoli dispositivi sono un dettaglio operativo, non un elemento strategico per la pianificazione della scalabilità. Non rientrano tra i quattro elementi chiave indicati nel modulo. |
> | Host di Windows | ❌ Errato | Il tipo di sistema operativo degli host non è un requisito per scalare una rete. La scalabilità è indipendente dalla piattaforma client utilizzata. |
> | Maggiore larghezza di banda | ❌ Errato | Aumentare la larghezza di banda può essere una *conseguenza* di una decisione di scalabilità, ma non è un elemento di pianificazione preventiva. Prima si analizza il traffico, poi si decide se e dove aumentare la banda. |

---

### Domanda 2

**Quale software installato su host chiave può rivelare i tipi di traffico di rete che scorre attraverso la rete?**

- [ ] Windows
- [ ] MacOS
- [ ] Linux
- [x] **Wireshark** ✔️
- [ ] SSH

> [!NOTE]
> **Risposta corretta: `Wireshark`**
>
> | Opzione | Esito | Motivazione |
> |---|---|---|
> | **Wireshark** | ✅ Corretto | Wireshark è un analizzatore di protocollo che, installato su host chiave, cattura e analizza il traffico di rete in tempo reale. Permette di visualizzare la gerarchia dei protocolli e i flussi di dati, come descritto nella sezione 17.3.2. |
> | Windows | ❌ Errato | Windows è un sistema operativo, non un software di analisi del traffico. Fornisce strumenti di monitoraggio (Task Manager, Data Usage), ma non è un analizzatore di protocollo. |
> | MacOS | ❌ Errato | MacOS è anch'esso un sistema operativo. Come Windows, non è uno strumento di analisi del traffico di rete. |
> | Linux | ❌ Errato | Linux è un sistema operativo. Sebbene esistano strumenti di analisi del traffico disponibili su Linux (come `tcpdump`), Linux in sé non è un analizzatore di protocollo. |
> | SSH | ❌ Errato | SSH (Secure Shell) è un protocollo per l'accesso remoto sicuro ai dispositivi. Non ha funzionalità di cattura o analisi del traffico di rete. |

---

### Domanda 3

**Quale strumento di Windows 10 è utile per determinare quali applicazioni utilizzano i servizi di rete su un host?**

- [ ] Windows Explorer
- [ ] Windows Defender Firewall
- [ ] File Manager
- [ ] Pannello di controllo
- [x] **Consumo dati** ✔️

> [!NOTE]
> **Risposta corretta: `Consumo dati (Data Usage)`**
>
> | Opzione | Esito | Motivazione |
> |---|---|---|
> | **Consumo dati** | ✅ Corretto | Lo strumento *Data Usage* (Utilizzo dati), accessibile da `Settings > Network & Internet > Data usage`, mostra il consumo di rete suddiviso per applicazione negli ultimi 30 giorni. È lo strumento indicato esplicitamente nella sezione 17.3.3 per questo scopo. |
> | Windows Explorer | ❌ Errato | Windows Explorer (o Esplora file) è il gestore dei file del sistema operativo. Serve per navigare tra cartelle e file, non per monitorare il traffico di rete delle applicazioni. |
> | Windows Defender Firewall | ❌ Errato | Il firewall di Windows gestisce le regole di accesso alla rete per le applicazioni (blocca o consente il traffico), ma non fornisce statistiche sul consumo di banda per applicazione. |
> | File Manager | ❌ Errato | File Manager è sostanzialmente un sinonimo di Windows Explorer. Gestisce i file locali e non ha alcuna funzione di monitoraggio della rete. |
> | Pannello di controllo | ❌ Errato | Il Pannello di controllo è un hub di configurazione generale del sistema. Pur contenendo alcune impostazioni di rete, non offre una vista dettagliata del consumo di banda per singola applicazione. |

---

*Modulo basato sul materiale Cisco Networking Academy – Cisco Packet Tracer*
