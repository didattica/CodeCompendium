# Modulo 17 — Creazione di una Piccola Rete

## 17.1 Creazione di una Piccola Rete

---

### 17.1.1 Topologie di Reti di Piccole Dimensioni

La maggior parte delle imprese sono piccole; pertanto, anche la maggior parte delle reti aziendali sono piccole.
Un progetto di rete di piccole dimensioni è solitamente semplice. Il numero e il tipo di dispositivi inclusi sono notevolmente ridotti rispetto a quelli di una rete più ampia.

**Esempio — Componenti tipici di una piccola rete aziendale:**

Una piccola rete richiede generalmente i seguenti elementi per connettere utenti cablati e wireless:

- **1 Router** — per la connessione verso Internet (WAN)
- **1 Switch** — per la connessione dei dispositivi cablati
- **1 Punto di accesso wireless (AP)** — per i dispositivi wireless
- **Telefono IP**
- **Stampante**
- **Server**

> [!CAUTION] L'Access Point agisce come uno switch poiché utilizza i MAC address per indirizzare i dati in modo specifico ai dispositivi connessi, evitando di trasmettere a vuoto come un hub.
> Tuttavia, poiché l'aria è un mezzo condiviso, i dispositivi devono comunque fare a turno per comunicare, rendendo le prestazioni fisiche simili a quelle di un hub in termini di collisioni e gestione del traffico.

Le reti di piccole dimensioni hanno in genere una **singola connessione WAN** fornita da:

- DSL
- Cavo
- Connessione Ethernet

> [!NOTE]
> Le reti di grandi dimensioni richiedono un reparto IT dedicato per gestire, proteggere e risolvere i problemi dei dispositivi e dei dati. Le piccole reti sono invece gestite da un **tecnico IT locale** o da un **professionista appaltato**. Nonostante le dimensioni ridotte, le competenze necessarie sono molte delle stesse richieste per reti di maggiori dimensioni.

---

> [!WARNING]
> **Nota di aggiornamento — Il contenuto sopra riflette il curriculum Cisco CCNA nella versione originale (circa 2019-2020).**
>
> I corsi Cisco vengono revisionati con cadenza pluriennale, e alcuni riferimenti tecnologici possono risultare datati rispetto allo stato attuale del mercato. In particolare, la lista delle connessioni WAN necessita di un aggiornamento significativo.

#### Aggiornamento 2026: connettività WAN per piccole reti

**DSL: tecnologia in dismissione**

Il DSL (e in particolare l'ADSL) era la tecnologia WAN dominante per le piccole aziende fino a metà anni 2010. Ad oggi è considerata una tecnologia **legacy in fase di dismissione progressiva**: in Italia, le linee ADSL rappresentano meno del 12% degli accessi fissi totali, e la maggior parte degli operatori non la propone più per nuove attivazioni.

**Il panorama WAN nel 2026**

Una rete aziendale di piccole dimensioni progettata oggi dovrebbe considerare le seguenti opzioni di connettività WAN, in ordine di preferenza:

| Tecnologia | Descrizione | Quando sceglierla |
|---|---|---|
| **FTTH** (Fiber To The Home/Building) | Fibra ottica fino all'edificio. Velocità simmetriche fino a 10 Gbps. Standard de facto nelle aree coperte. | Prima scelta ovunque disponibile |
| **FWA** (Fixed Wireless Access) | Connessione wireless fissa via 4G/5G con antenna dedicata. Alternativa concreta alla fibra. | Zone non raggiunte da FTTH |
| **5G business** | Connessione 5G come accesso primario o di failover. Sempre più usata anche come unica WAN in sedi temporanee o filiali. Circa 331 Mbps, con upload a circa 58 Mbps e latenza media di circa 28 ms | Mobilità, filiali, backup |
| **Cavo / Ethernet broadband** | Ancora presente in alcuni mercati, in particolare negli Stati Uniti. | Dove disponibile e competitivo |
| **Satellite (es. Starlink Business)** | Connettività satellitare a bassa latenza. Opzione concreta per sedi rurali o remote. | Zone rurali, sedi isolate |
| **DSL / ADSL** | Tecnologia su rame. Ancora attiva in alcune zone non coperte da alternative, ma in dismissione. | Solo dove non esistono alternative migliori |

**Evoluzione dei dispositivi di rete**

Oltre alla connettività, anche i **componenti della rete locale** si sono evoluti rispetto al modello classico del curriculum:

- Il **router tradizionale** è spesso sostituito o affiancato da dispositivi **SD-WAN** (Software-Defined WAN), che permettono di gestire più connessioni WAN simultaneamente, scegliendo automaticamente il percorso migliore per ogni tipo di traffico.
- Il **punto di accesso wireless separato** è oggi frequentemente integrato in dispositivi **all-in-one** (router/switch/AP) o in sistemi **Wi-Fi mesh**, che semplificano la gestione nelle piccole sedi.
- Il **server fisico locale** è in molti casi sostituito da **servizi cloud** (Microsoft 365, Google Workspace, ecc.), riducendo o eliminando la necessità di infrastruttura server on-premises.
- Il **Telefono IP** fisico è in declino: molte piccole aziende adottano soluzioni **VoIP software** (softphone) o servizi di comunicazione unificata (UCaaS) accessibili da qualsiasi dispositivo.

> [!TIP]
> Per chi studia per la certificazione Cisco CCNA, è utile **conoscere entrambi i livelli**: il modello classico descritto nel curriculum (fondamentale per comprendere i concetti base) e il panorama tecnologico attuale, che riflette ciò che si trova nei contesti lavorativi reali. Le basi concettuali — routing, switching, indirizzamento IP, protocolli — rimangono valide indipendentemente dalla tecnologia WAN utilizzata.
---

### 17.1.2 Scelta dei Dispositivi per una Piccola Rete

Come le reti di grandi dimensioni, le reti di piccole dimensioni richiedono **pianificazione e progettazione** per soddisfare le esigenze degli utenti. La pianificazione assicura che tutti i requisiti, gli aspetti correlati al costo e le opzioni di implementazione ricevano l'attenzione dovuta.

Una delle prime considerazioni in fase di progettazione è il **tipo di dispositivi intermedi** da utilizzare per supportare la rete.

I principali fattori da considerare nella selezione dei dispositivi di rete sono i seguenti:

---

#### Costo

Il costo di uno switch o di un router è determinato dalla capacità e dalle funzionalità, tra cui:

- Numero e tipo di porte disponibili
- Velocità del backplane
- Funzionalità di gestione della rete
- Tecnologie di sicurezza integrate
- Tecnologie avanzate di switching opzionali

> [!NOTE]
> **Da considerare:** Il costo include anche i **cavi** necessari per connettere tutti i dispositivi e la quantità di **ridondanza** da incorporare nella rete.

---

#### Velocità e Tipi di Porte e Interfacce

La scelta del numero e del tipo di porte su router e switch è una decisione importante:

- I computer più recenti sono dotati di **NIC integrate da 1 Gbps**
- Alcuni server possono avere porte **10 Gbps**
- Scegliere dispositivi di Layer 2 con velocità superiori consente alla rete di **evolversi senza dover sostituire i dispositivi centrali** (sebbene più costosi)

---

#### Espandibilità

I dispositivi di rete sono disponibili in due tipologie:

| Tipologia | Descrizione |
|---|---|
| **Configurazione fissa** | Numero e tipo di porte predefiniti, non espandibili |
| **Configurazione modulare** | Slot di espansione per aggiungere nuovi moduli all'evolvere dei requisiti |

- Gli **switch** sono disponibili con porte aggiuntive per uplink ad alta velocità
- I **router** possono essere configurati per connettersi a diversi tipi di reti

> **Suggerimento:** Selezionare con attenzione i moduli e le interfacce appropriati per i supporti specifici.

> [!IMPORTANT]
> ### Scalabilità: Configurazione Fissa vs. Modulare
> 
> La scelta dell'hardware è un compromesso tra costo iniziale e flessibilità futura:
> 
> * **Dispositivi a Configurazione Fissa:** Hanno un numero di porte predefinito (es. 24 o 48 porte) e non possono essere espansi fisicamente. Sono più economici, ma richiedono la sostituzione o l'aggiunta di nuovi apparati in caso di crescita della rete.
> * **Dispositivi Modulari:** Sono composti da uno chassis con slot liberi. Permettono di installare moduli aggiuntivi (interfacce in fibra, schede di rete extra, alimentatori ridondanti) man mano che le esigenze aumentano, proteggendo l'investimento iniziale nel lungo termine.
>
> **In sintesi:** I dispositivi fissi sono ideali per reti stabili e budget ridotti; quelli modulari sono fondamentali per reti che prevedono una crescita significativa o necessità di diverse tecnologie di connessione.

---

#### Funzioni e Servizi del Sistema Operativo

I dispositivi di rete devono disporre di sistemi operativi in grado di supportare i requisiti organizzativi, tra cui:

- **Switch di Layer 3**
- **NAT** (Network Address Translation)
- **DHCP** (Dynamic Host Configuration Protocol)
- **Security** (sicurezza)
- **QoS** (Quality of Service — Qualità del Servizio)
- **VoIP** (Voice over IP)

---

### 17.1.3 Indirizzamento IP per una Piccola Rete

Quando si implementa una rete, è necessario **creare uno schema di indirizzamento IP** e utilizzarlo in modo coerente. Tutti gli host e i dispositivi in un'internetwork devono avere un **indirizzo univoco**.

**I dispositivi che rientrano nello schema di indirizzamento IP includono:**

- **Dispositivi utente finale** — numero e tipo di connessione (cablato, wireless, accesso remoto)
- **Server e periferiche** — stampanti, telecamere di sicurezza, ecc.
- **Dispositivi intermedi** — switch e punti di accesso

> **Best practice:** Si consiglia di **pianificare, documentare e gestire** lo schema di indirizzamento IP in base al tipo di dispositivo. Ciò semplifica l'identificazione dei dispositivi e la risoluzione dei problemi (ad esempio durante l'analisi del traffico con un analizzatore di protocollo).

---

#### Esempio — Schema di Indirizzamento IP per una PMI

Un'organizzazione di piccole e medie dimensioni con tre LAN utente:

- `192.168.1.0/24`
- `192.168.2.0/24`
- `192.168.3.0/24`

Ha adottato il seguente schema di indirizzamento coerente per ogni rete `192.168.x.0/24`:

| Tipo di Dispositivo | Intervallo di Indirizzi IP Assegnabile | Riepilogato come… |
|---|---|---|
| Gateway predefinito (Router) | `192.168.x.1` — `192.168.x.2` | `192.168.x.0/30` |
| Switch (max 2) | `192.168.x.5` — `192.168.x.6` | `192.168.x.4/30` |
| Punti di accesso (max 6) | `192.168.x.9` — `192.168.x.14` | `192.168.x.8/29` |
| Server (max 6) | `192.168.x.17` — `192.168.x.22` | `192.168.x.16/29` |
| Stampanti (max 6) | `192.168.x.25` — `192.168.x.30` | `192.168.x.24/29` |
| Telefoni IP (max 6) | `192.168.x.33` — `192.168.x.38` | `192.168.x.32/29` |
| Dispositivi cablati (max 62) | `192.168.x.65` — `192.168.x.126` | `192.168.x.64/26` |
| Dispositivi wireless (max 62) | `192.168.x.193` — `192.168.x.254` | `192.168.x.192/26` |

**Esempio applicato alla LAN `192.168.2.0/24`:**

| Dispositivo | Indirizzo IP |
|---|---|
| Gateway predefinito (Router) | `192.168.2.1/24` |
| Switch | `192.168.2.5/24` |
| Server | `192.168.2.17/24` |

> **Nota:** Gli intervalli di indirizzi IP assegnabili sono stati deliberatamente allocati sui **limiti della rete di subnet** per semplificare il riepilogo per gruppo di dispositivi. Ad esempio, se alla rete viene aggiunto un secondo switch con indirizzo `192.168.2.6`, per identificare tutti gli switch in un criterio di rete è sufficiente specificare il blocco riepilogato `192.168.x.4/30`.

> [!TIP]
> ### Pianificazione dell'Indirizzamento IP
> La progettazione di una sottorete non deve basarsi solo sul numero attuale di host, ma deve prevedere la crescita futura e la segmentazione logica.
>
> * **Relazione Bit-Host:** Maggiore è il numero di bit presi in prestito dalla parte host (aumentando il prefisso CIDR, es. da /24 a /26), minore sarà il numero di dispositivi ospitabili, ma maggiore sarà il numero di sottoreti create.
> * **Criteri di Segmentazione:** Non limitarti a creare una sola LAN. Dividi la rete in base a:
>   1. **Funzione:** Amministrazione, Vendite, Ospiti.
>   2. **Sicurezza:** Isolare dispositivi critici (Server) da quelli meno sicuri (IoT/Wi-Fi).
>   3. **Performance:** Contenere i domini di broadcast per evitare rallentamenti.
>
> **Nota Bene:** Ricorda di includere nel conteggio degli IP anche gli indirizzi per le interfacce dei router, gli switch gestiti e le stampanti di rete.

---

### 17.1.4 Ridondanza in una Piccola Rete

Un aspetto fondamentale della progettazione di rete è l'**affidabilità**. Anche le piccole imprese fanno spesso grande affidamento sulla rete per le attività aziendali, e un errore di rete può rivelarsi molto costoso.

Per mantenere un alto grado di affidabilità, è richiesta la **ridondanza** nella progettazione della rete. La ridondanza consente di **eliminare i singoli punti di errore** (_single point of failure_).

**Modalità di realizzazione della ridondanza:**

| Componente | Descrizione |
|---|---|
| **Server ridondanti** | Disponibili in caso di errore del server principale |
| **Collegamenti ridondanti** | Forniscono percorsi alternativi in caso di errore di collegamento |
| **Switch ridondanti** | Disponibili in caso di errore dello switch |
| **Router ridondanti** | Disponibili in caso di errore del router o del percorso |

> **Considerazione pratica:** Le reti di piccole dimensioni forniscono in genere un **unico punto di uscita verso Internet** tramite uno o più gateway predefiniti. Se il router si guasta, l'intera rete perde la connettività. Per questo motivo, per una piccola impresa può essere consigliabile valutare la sottoscrizione di un **secondo provider di servizi come backup**.

> [!CAUTION]
> ### Ridondanza e Continuità Operativa
> La ridondanza mira a eliminare i **Single Points of Failure (SPOF)** per garantire che la rete resti operativa anche in caso di guasti.
>
> 1. **Dispositivi Ridondanti:** Duplicare apparati critici come Router e Server. In ambito Cisco, protocolli come **HSRP** permettono a due router di apparire come un unico "gateway virtuale".
> 2. **Collegamenti Ridondanti:** Prevedere percorsi fisici alternativi tra gli switch (gestiti dal protocollo **STP**) per evitare che il guasto di un singolo cavo isoli un intero reparto.
> 3. **Protezione Energetica:** L'uso di **UPS** (Uninterruptible Power Supplies) e generatori è essenziale per proteggere l'hardware e garantire il servizio durante interruzioni elettriche.
>
> **Attenzione:** Non confondere la ridondanza con il *Load Balancing*. Mentre la prima garantisce la disponibilità del servizio, il secondo ottimizza l'uso delle risorse distribuendo il traffico su più link o dispositivi attivi.

---

### 17.1.5 Gestione del Traffico

L'obiettivo di una buona progettazione di rete, anche per una rete di piccole dimensioni, è:

- **Aumentare la produttività** dei dipendenti
- **Ridurre al minimo** le interruzioni dell'operatività della rete

I router e gli switch in una piccola rete devono essere configurati per supportare il **traffico in tempo reale** (voce e video) in modo appropriato rispetto ad altro traffico di dati.

Un buon progetto di rete implementa la **Qualità del Servizio (QoS)** per classificare il traffico in base alla priorità.

> [!note]
> Il QoS agisce come un vigile urbano per il traffico dati.
> Senza QoS, i dati vengono gestiti secondo il principio "Best Effort" (chi arriva prima passa, senza distinzioni). Con il QoS, il sistema analizza i pacchetti e decide chi ha la precedenza.

**Esempio di classificazione del traffico con QoS:**

| Tipo di Traffico | Priorità | Note |
|---|---|---|
| **Voce** | 🔴 Elevata | Inviato alla rete backbone con priorità massima |
| **SMTP** (e-mail) | 🟡 Media | Inviato al router senza priorità specifica |
| **Messaggistica istantanea** | 🟢 Normale | Trattato come traffico standard |
| **FTP** | ⚪ Bassa | Priorità minima, non sensibile alla latenza |

> [!note] **Principio chiave:** Il traffico voce e video è **sensibile alla latenza** e deve essere servito prima del traffico dati tradizionale. La QoS garantisce che le applicazioni critiche in tempo reale funzionino correttamente anche in condizioni di congestione della rete.
```
graph LR
    subgraph Ingresso
        IN[Traffico senza priorità]
    end

    subgraph Router_QoS [Processo di Accodamento nel Router]
        direction TB
        P1[Voce - Priorità Elevata]
        P2[SMTP - Priorità Media]
        P3[Messaggistica - Priorità Normale]
        P4[FTP - Priorità Bassa]
    end

    subgraph Uscita [Uscita<br> Il traffico viene inviato 
    alla rete backbone in ordien di priorita']
        BACKBONE((Rete Backbone))
    end

    IN --> Router_QoS
    P1 -->|1°| BACKBONE
    P2 -->|2°| BACKBONE
    P3 -->|3°| BACKBONE
    P4 -->|4°| BACKBONE

    style P1 fill:#6a1b9a,color:#fff
    style P2 fill:#00695c,color:#fff
    style P3 fill:#9e9d24,color:#fff
    style P4 fill:#2e7d32,color:#fff
```


> [!TIP]
> ### QoS: Dare Ordine al Caos
> Il **Quality of Service (QoS)** è l'insieme di tecnologie che gestiscono le congestioni di rete assicurando che il traffico prioritario non venga penalizzato.
>
> * **Classificazione e Marcatura:** I pacchetti vengono analizzati e "etichettati" in base alla loro importanza (es. traffico Voip vs traffico Email).
> * **Gestione delle Code:** Quando un router riceve più dati di quanti possa inviarne, utilizza algoritmi di accodamento per trasmettere prima i pacchetti sensibili al tempo.
> * **Obiettivo:** Ridurre la **Latenza** (ritardo totale) e il **Jitter** (instabilità del ritardo) per servizi critici come le videoconferenze o la telefonia IP.
>
> **Esempio:** Senza QoS, un pesante download di un aggiornamento Windows potrebbe interrompere o disturbare una chiamata su Google Meet. Con il QoS, il router rallenta leggermente il download per garantire fluidità alla chiamata.


---

# Modulo 17 — Creazione di una Piccola Rete

## 17.1 Creazione di una Piccola Rete

---

### 17.1.1 Topologie di Reti di Piccole Dimensioni

La maggior parte delle imprese sono piccole; pertanto, anche la maggior parte delle reti aziendali sono piccole.

Un progetto di rete di piccole dimensioni è solitamente semplice. Il numero e il tipo di dispositivi inclusi sono notevolmente ridotti rispetto a quelli di una rete più ampia.

**Esempio — Componenti tipici di una piccola rete aziendale:**

Una piccola rete richiede generalmente i seguenti elementi per connettere utenti cablati e wireless:

- **1 Router** — per la connessione verso Internet (WAN)
- **1 Switch** — per la connessione dei dispositivi cablati
- **1 Punto di accesso wireless (AP)** — per i dispositivi wireless
- **Telefono IP**
- **Stampante**
- **Server**

Le reti di piccole dimensioni hanno in genere una **singola connessione WAN** fornita da:

- DSL
- Cavo
- Connessione Ethernet

> **Nota:** Le reti di grandi dimensioni richiedono un reparto IT dedicato per gestire, proteggere e risolvere i problemi dei dispositivi e dei dati. Le piccole reti sono invece gestite da un **tecnico IT locale** o da un **professionista appaltato**. Nonostante le dimensioni ridotte, le competenze necessarie sono molte delle stesse richieste per reti di maggiori dimensioni.

---

### 17.1.2 Scelta dei Dispositivi per una Piccola Rete

Come le reti di grandi dimensioni, le reti di piccole dimensioni richiedono **pianificazione e progettazione** per soddisfare le esigenze degli utenti. La pianificazione assicura che tutti i requisiti, gli aspetti correlati al costo e le opzioni di implementazione ricevano l'attenzione dovuta.

Una delle prime considerazioni in fase di progettazione è il **tipo di dispositivi intermedi** da utilizzare per supportare la rete.

I principali fattori da considerare nella selezione dei dispositivi di rete sono i seguenti:

---

#### Costo

Il costo di uno switch o di un router è determinato dalla capacità e dalle funzionalità, tra cui:

- Numero e tipo di porte disponibili
- Velocità del backplane
- Funzionalità di gestione della rete
- Tecnologie di sicurezza integrate
- Tecnologie avanzate di switching opzionali

> **Da considerare:** Il costo include anche i **cavi** necessari per connettere tutti i dispositivi e la quantità di **ridondanza** da incorporare nella rete.

---

#### Velocità e Tipi di Porte e Interfacce

La scelta del numero e del tipo di porte su router e switch è una decisione importante:

- I computer più recenti sono dotati di **NIC integrate da 1 Gbps**
- Alcuni server possono avere porte **10 Gbps**
- Scegliere dispositivi di Layer 2 con velocità superiori consente alla rete di **evolversi senza dover sostituire i dispositivi centrali** (sebbene più costosi)

---

#### Espandibilità

I dispositivi di rete sono disponibili in due tipologie:

| Tipologia | Descrizione |
|---|---|
| **Configurazione fissa** | Numero e tipo di porte predefiniti, non espandibili |
| **Configurazione modulare** | Slot di espansione per aggiungere nuovi moduli all'evolvere dei requisiti |

- Gli **switch** sono disponibili con porte aggiuntive per uplink ad alta velocità
- I **router** possono essere configurati per connettersi a diversi tipi di reti

> **Suggerimento:** Selezionare con attenzione i moduli e le interfacce appropriati per i supporti specifici.

---

#### Funzioni e Servizi del Sistema Operativo

I dispositivi di rete devono disporre di sistemi operativi in grado di supportare i requisiti organizzativi, tra cui:

- **Switch di Layer 3**
- **NAT** (Network Address Translation)
- **DHCP** (Dynamic Host Configuration Protocol)
- **Security** (sicurezza)
- **QoS** (Quality of Service — Qualità del Servizio)
- **VoIP** (Voice over IP)

---

### 17.1.3 Indirizzamento IP per una Piccola Rete

Quando si implementa una rete, è necessario **creare uno schema di indirizzamento IP** e utilizzarlo in modo coerente. Tutti gli host e i dispositivi in un'internetwork devono avere un **indirizzo univoco**.

**I dispositivi che rientrano nello schema di indirizzamento IP includono:**

- **Dispositivi utente finale** — numero e tipo di connessione (cablato, wireless, accesso remoto)
- **Server e periferiche** — stampanti, telecamere di sicurezza, ecc.
- **Dispositivi intermedi** — switch e punti di accesso

> **Best practice:** Si consiglia di **pianificare, documentare e gestire** lo schema di indirizzamento IP in base al tipo di dispositivo. Ciò semplifica l'identificazione dei dispositivi e la risoluzione dei problemi (ad esempio durante l'analisi del traffico con un analizzatore di protocollo).

---

#### Esempio — Schema di Indirizzamento IP per una PMI

Un'organizzazione di piccole e medie dimensioni con tre LAN utente:

- `192.168.1.0/24`
- `192.168.2.0/24`
- `192.168.3.0/24`

Ha adottato il seguente schema di indirizzamento coerente per ogni rete `192.168.x.0/24`:

| Tipo di Dispositivo | Intervallo di Indirizzi IP Assegnabile | Riepilogato come… |
|---|---|---|
| Gateway predefinito (Router) | `192.168.x.1` — `192.168.x.2` | `192.168.x.0/30` |
| Switch (max 2) | `192.168.x.5` — `192.168.x.6` | `192.168.x.4/30` |
| Punti di accesso (max 6) | `192.168.x.9` — `192.168.x.14` | `192.168.x.8/29` |
| Server (max 6) | `192.168.x.17` — `192.168.x.22` | `192.168.x.16/29` |
| Stampanti (max 6) | `192.168.x.25` — `192.168.x.30` | `192.168.x.24/29` |
| Telefoni IP (max 6) | `192.168.x.33` — `192.168.x.38` | `192.168.x.32/29` |
| Dispositivi cablati (max 62) | `192.168.x.65` — `192.168.x.126` | `192.168.x.64/26` |
| Dispositivi wireless (max 62) | `192.168.x.193` — `192.168.x.254` | `192.168.x.192/26` |

**Esempio applicato alla LAN `192.168.2.0/24`:**

| Dispositivo | Indirizzo IP |
|---|---|
| Gateway predefinito (Router) | `192.168.2.1/24` |
| Switch | `192.168.2.5/24` |
| Server | `192.168.2.17/24` |

> **Nota:** Gli intervalli di indirizzi IP assegnabili sono stati deliberatamente allocati sui **limiti della rete di subnet** per semplificare il riepilogo per gruppo di dispositivi. Ad esempio, se alla rete viene aggiunto un secondo switch con indirizzo `192.168.2.6`, per identificare tutti gli switch in un criterio di rete è sufficiente specificare il blocco riepilogato `192.168.x.4/30`.

---

### 17.1.4 Ridondanza in una Piccola Rete

Un aspetto fondamentale della progettazione di rete è l'**affidabilità**. Anche le piccole imprese fanno spesso grande affidamento sulla rete per le attività aziendali, e un errore di rete può rivelarsi molto costoso.

Per mantenere un alto grado di affidabilità, è richiesta la **ridondanza** nella progettazione della rete. La ridondanza consente di **eliminare i singoli punti di errore** (_single point of failure_).

**Modalità di realizzazione della ridondanza:**

| Componente | Descrizione |
|---|---|
| **Server ridondanti** | Disponibili in caso di errore del server principale |
| **Collegamenti ridondanti** | Forniscono percorsi alternativi in caso di errore di collegamento |
| **Switch ridondanti** | Disponibili in caso di errore dello switch |
| **Router ridondanti** | Disponibili in caso di errore del router o del percorso |

> **Considerazione pratica:** Le reti di piccole dimensioni forniscono in genere un **unico punto di uscita verso Internet** tramite uno o più gateway predefiniti. Se il router si guasta, l'intera rete perde la connettività. Per questo motivo, per una piccola impresa può essere consigliabile valutare la sottoscrizione di un **secondo provider di servizi come backup**.

---

### 17.1.5 Gestione del Traffico

L'obiettivo di una buona progettazione di rete, anche per una rete di piccole dimensioni, è:

- **Aumentare la produttività** dei dipendenti
- **Ridurre al minimo** le interruzioni dell'operatività della rete

I router e gli switch in una piccola rete devono essere configurati per supportare il **traffico in tempo reale** (voce e video) in modo appropriato rispetto ad altro traffico di dati.

Un buon progetto di rete implementa la **Qualità del Servizio (QoS)** per classificare il traffico in base alla priorità.

**Esempio di classificazione del traffico con QoS:**

| Tipo di Traffico | Priorità | Note |
|---|---|---|
| **Voce** | 🔴 Elevata | Inviato alla rete backbone con priorità massima |
| **SMTP** (e-mail) | 🟡 Media | Inviato al router senza priorità specifica |
| **Messaggistica istantanea** | 🟢 Normale | Trattato come traffico standard |
| **FTP** | ⚪ Bassa | Priorità minima, non sensibile alla latenza |

> **Principio chiave:** Il traffico voce e video è **sensibile alla latenza** e deve essere servito prima del traffico dati tradizionale. La QoS garantisce che le applicazioni critiche in tempo reale funzionino correttamente anche in condizioni di congestione della rete.

---

## ✅ Domande di Verifica — Modulo 17.1

Questa sezione raccoglie le domande di verifica del modulo con la risposta corretta evidenziata e una breve spiegazione del perché quella risposta è esatta.

---

### Domanda 1
**Quale affermazione si riferisce correttamente a una piccola rete?**

| | Opzione |
|---|---|
| ❌ | Le piccole reti sono complesse. |
| ✅ | **Nella maggior parte dei casi le aziende hanno dimensioni ridotte.** |
| ❌ | Le reti di piccole dimensioni richiedono la manutenzione di un reparto IT. |

> **Spiegazione:** Come illustrato nella sezione 17.1.1, la maggior parte delle imprese sono piccole e di conseguenza anche la maggior parte delle reti aziendali lo sono. Un progetto di rete di piccole dimensioni è solitamente **semplice**, non complesso. Inoltre, le piccole reti non richiedono un reparto IT dedicato: vengono gestite da un tecnico IT locale o da un professionista appaltato.

---

### Domanda 2
**Quale fattore deve essere considerato quando si selezionano i dispositivi di rete?**

| | Opzione |
|---|---|
| ❌ | Elasticità |
| ✅ | **Costi** |
| ❌ | Connessioni della console |
| ❌ | Colore |

> **Spiegazione:** Come descritto nella sezione 17.1.2, i fattori rilevanti nella scelta dei dispositivi di rete sono **costo**, velocità e tipo di porte, espandibilità, e funzioni del sistema operativo. Il colore e le connessioni della console non rientrano tra i criteri di selezione tecnica. L'"elasticità" non è una terminologia Cisco standard in questo contesto.

---

### Domanda 3
**Cosa è necessario pianificare e utilizzare quando si implementa una rete?**

| | Opzione |
|---|---|
| ❌ | Posizione della stampante |
| ✅ | **Schema di indirizzamento IP** |
| ❌ | Nomi dei dispositivi |
| ❌ | Schema di indirizzamento MAC |

> **Spiegazione:** Come indicato nella sezione 17.1.3, quando si implementa una rete è fondamentale creare e utilizzare uno **schema di indirizzamento IP** coerente, in modo che ogni host e dispositivo abbia un indirizzo univoco. Gli indirizzi MAC sono assegnati dal produttore e non sono pianificabili dall'amministratore; i nomi dei dispositivi e la posizione della stampante non sono elementi strutturali della progettazione di rete.

---

### Domanda 4
**Cosa è necessario per mantenere un alto grado di affidabilità ed eliminare singoli punti di guasto?**

| | Opzione |
|---|---|
| ❌ | Espandibilità |
| ✅ | **Ridondanza** |
| ❌ | Accessibilità |
| ❌ | Integrità |

> **Spiegazione:** Come spiegato nella sezione 17.1.4, la **ridondanza** è il meccanismo che consente di eliminare i _single point of failure_ (singoli punti di guasto), garantendo la continuità del servizio tramite componenti duplicati: server, switch, router e collegamenti ridondanti. L'espandibilità riguarda la crescita della rete, non la sua affidabilità.

---

### Domanda 5
**Cosa è necessario per classificare il traffico in base alla priorità?**

| | Opzione |
|---|---|
| ❌ | Schema di indirizzamento IP |
| ✅ | **Qualità del servizio (QoS)** |
| ❌ | Routing |
| ❌ | Switching |

> **Spiegazione:** Come illustrato nella sezione 17.1.5, la **QoS (Quality of Service)** è lo strumento che consente di classificare il traffico di rete in base alla priorità, assegnando precedenza al traffico sensibile alla latenza (come voce e video) rispetto al traffico dati tradizionale (come FTP o e-mail). Il routing e lo switching gestiscono l'instradamento dei pacchetti, ma non la loro classificazione per priorità.

---

*Materiale didattico basato sul curriculum Cisco Networking Academy — Modulo 17.1*
