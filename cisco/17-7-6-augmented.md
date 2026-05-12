<!--
QUESTO DOCUEMTNO E' STATO OTTENUTO UTILIZZANDO IL SEGUENTE PROMPT!


Sto per inviarti un file Markdown (.md) relativo alla sezione Cisco:

# 17.7.6 — Packet Tracer: Risoluzione dei problemi di connettività

L’obiettivo dell’attività è trasformare il contenuto originale in un documento Markdown professionale, ben organizzato e compatibile con GitHub.

## Obiettivo principale

NON devi risolvere gli esercizi o fornire direttamente le soluzioni ai problemi di troubleshooting.

Il tuo compito è invece:

* migliorare la leggibilità del materiale,

* aggiungere contesto tecnico utile,

* spiegare concetti chiave,

* inserire definizioni e chiarimenti,

* aiutare lo studente a comprendere il significato delle attività richieste.

Devi comportarti come un assistente didattico che arricchisce il materiale, NON come un motore che risolve il laboratorio Cisco.

---

# Cosa devi fare

## Conversione Markdown

* Mantieni il documento in formato Markdown compatibile con GitHub.

* Conserva la struttura originale della sezione Cisco.

* Usa correttamente le intestazioni Markdown:

  * #

  * ##

  * ###

  * ecc.

* Mantieni la terminologia tecnica Cisco coerente con il testo originale.

---

# Arricchimento del contenuto

Puoi aggiungere brevi sezioni di supporto per aiutare lo studente a capire meglio il contesto tecnico.

Ad esempio puoi aggiungere:

* definizioni di protocolli,

* spiegazioni sintetiche dei concetti di networking,

* descrizioni generali dei comandi Cisco,

* chiarimenti sul significato di errori comuni,

* note sul troubleshooting,

* osservazioni operative,

* best practice generali.

## Importante

NON fornire:

* la soluzione completa degli esercizi,

* configurazioni finali complete,

* diagnosi definitive,

* output inventati,

* risposte dirette alle domande del laboratorio.

Se il contesto non è sufficiente per determinare una soluzione, limita la risposta a spiegazioni teoriche o suggerimenti generali.

---

# Linee guida per il contenuto aggiuntivo

Le spiegazioni devono essere:

* brevi,

* chiare,

* tecnicamente corrette,

* utili allo studio,

* contestuali alla sezione.

Evita lunghe spiegazioni teoriche non necessarie.

L’obiettivo è supportare la comprensione del materiale originale, non sostituirlo.

---

# Admonition Block GitHub

Usa blocchi Admonition GitHub per evidenziare concetti importanti o suggerimenti utili.

Esempi:

md

> [!IMPORTANT]

> Verificare sempre la configurazione IP prima di analizzare il routing.


md

> [!NOTE]

> Il comando `ping` verifica solo la raggiungibilità Layer 3.


Puoi usare anche:

* [!TIP]

* [!WARNING]

* [!CAUTION]

---

# Glossario finale

Alla fine del documento crea una sezione:

# Glossario dei concetti chiave

Inserisci una tabella con:

* termini tecnici,

* protocolli,

* acronimi,

* comandi Cisco,

* concetti di networking,

* tecnologie citate nel documento.

Formato esempio:

md

| Termine | Definizione |

|----------|-------------|

| DHCP | Protocollo per l’assegnazione automatica degli indirizzi IP |

| VLAN | Segmentazione logica di una rete Layer 2 |


---

# Output richiesto

Il risultato finale deve essere:

* in formato .md,

* compatibile con GitHub,

* ben strutturato,

* leggibile,

* adatto a materiale didattico tecnico.

* tradotto in italiano

Di seguito ti fornirò il file Markdown da elaborare.

-->


# 17.7.6 — Packet Tracer: Risoluzione dei problemi di connettività

## Obiettivo dell’attività

In questa attività di Packet Tracer, lo scopo è identificare e risolvere eventuali problemi di connettività di rete. Quando un problema non può essere corretto direttamente, esso deve essere documentato chiaramente per consentire un’escalation tecnica.

> [!IMPORTANT]
> Nel troubleshooting di rete è fondamentale seguire un approccio metodico:
> verificare prima la configurazione IP locale, poi la connettività Layer 2/3 e infine i servizi applicativi come DNS e HTTP.

---

# Packet Tracer - Troubleshoot Connectivity Issues

## Tabella di indirizzamento

| Dispositivo | Interfaccia  | Indirizzo IP    | Subnet Mask     | Gateway predefinito |
| ----------- | ------------ | --------------- | --------------- | ------------------- |
| **R1**      | G0/0         | 172.16.1.1      | 255.255.255.0   | N/D                 |
|             | G0/1         | 172.16.2.1      | 255.255.255.0   | N/D                 |
|             | S0/0/0       | 209.165.200.226 | 255.255.255.252 | N/D                 |
| **R2**      | G0/0         | 209.165.201.1   | 255.255.255.224 | N/D                 |
|             | S0/0/0 (DCE) | 209.165.200.225 | 255.255.255.252 | N/D                 |
| **PC-01**   | NIC          | 172.16.1.3      | 255.255.255.0   | 172.16.1.1          |
| **PC-02**   | NIC          | 172.16.1.4      | 255.255.255.0   | 172.16.1.1          |
| **PC-A**    | NIC          | 172.16.2.3      | 255.255.255.0   | 172.16.2.1          |
| **PC-B**    | NIC          | 172.16.2.4      | 255.255.255.0   | 172.16.2.1          |
| **Web**     | NIC          | 209.165.201.2   | 255.255.255.224 | 209.165.201.1       |
| **DNS1**    | NIC          | 209.165.201.3   | 255.255.255.224 | 209.165.201.1       |
| **DNS2**    | NIC          | 209.165.201.4   | 255.255.255.224 | 209.165.201.1       |

---

## Obiettivi

In questa attività Packet Tracer dovrai:

* identificare problemi di connettività;
* verificare la configurazione IP dei dispositivi;
* testare la raggiungibilità della rete;
* controllare il funzionamento del DNS;
* documentare eventuali anomalie;
* applicare procedure base di troubleshooting.

---

## Scenario

Gli utenti segnalano di non riuscire ad accedere al server web **[www.cisco.pka](http://www.cisco.pka)** dopo un recente aggiornamento della rete che include l’aggiunta di un secondo server DNS.

Il compito consiste nel:

* individuare la causa del problema;
* tentare di risolverlo;
* documentare chiaramente eventuali problemi persistenti;
* eseguire un’escalation se necessario.

Non è disponibile l’accesso ai dispositivi presenti nel cloud né al server **[www.cisco.pka](http://www.cisco.pka)**.

> [!NOTE]
> Il router R1 è accessibile esclusivamente tramite SSH utilizzando:
>
> * Username: `Admin01`
> * Password: `cisco12345`

> [!TIP]
> Quando un host riesce a raggiungere un server tramite indirizzo IP ma non tramite nome DNS, il problema è spesso legato alla risoluzione DNS e non al routing IP.

---

# Istruzioni

## Parte 1 — Determinare i problemi di connettività da PC-01

### a. Verifica configurazione IP

Su **PC-01**, aprire il prompt dei comandi ed eseguire:

```bash
ipconfig
```

Verificare:

* indirizzo IP;
* subnet mask;
* gateway predefinito.

Correggere eventuali configurazioni errate confrontandole con la tabella di indirizzamento.

> [!NOTE]
> Il comando `ipconfig` consente di visualizzare la configurazione TCP/IP del dispositivo Windows.

---

### b. Verifica della connettività

Dopo aver verificato o corretto la configurazione IP, eseguire test di connettività tramite `ping`.

Verificare la raggiungibilità di:

* gateway predefinito (`172.16.1.1`);
* server web (`209.165.201.2`);
* PC-02;
* PC-A;
* PC-B.

Registrare i risultati ottenuti.

> [!IMPORTANT]
> Il comando `ping` verifica esclusivamente la raggiungibilità Layer 3 tramite protocollo ICMP.
> Un ping riuscito non garantisce il corretto funzionamento dei servizi applicativi.

> [!TIP]
> Se il ping verso il gateway fallisce, il problema è spesso locale:
>
> * configurazione IP errata;
> * subnet mask non corretta;
> * cavo scollegato;
> * interfaccia disabilitata.

---

### c. Verifica accesso web

Aprire il browser web su PC-01 e tentare di accedere al server:

```text
http://www.cisco.pka
```

Successivamente provare l’accesso tramite indirizzo IP:

```text
209.165.201.2
```

Registrare i risultati.

Domande guida:

* PC-01 riesce ad accedere a `www.cisco.pka`?
* L’accesso funziona utilizzando direttamente l’indirizzo IP?

> [!NOTE]
> Se l’accesso tramite IP funziona ma tramite nome no, è probabile un problema DNS.

---

### d. Documentazione

Documentare:

* problemi individuati;
* possibili cause;
* eventuali correzioni effettuate;
* test eseguiti.

---

# Parte 2 — Determinare i problemi di connettività da PC-02

## a. Verifica configurazione IP

Su **PC-02**, aprire il prompt dei comandi ed eseguire:

```bash
ipconfig
```

Verificare:

* indirizzo IP;
* subnet mask;
* gateway predefinito.

Correggere eventuali errori.

---

## b. Test di connettività

Eseguire ping verso:

* gateway predefinito (`172.16.1.1`);
* server web (`209.165.201.2`);
* PC-01;
* PC-A;
* PC-B.

Registrare i risultati.

> [!TIP]
> Durante il troubleshooting è utile verificare la connettività partendo dai dispositivi più vicini e procedendo gradualmente verso reti remote.

---

## c. Verifica accesso web

Tentare di raggiungere:

```text
www.cisco.pka
```

dal browser web di PC-02.

Annotare:

* funzionamento tramite nome DNS;
* funzionamento tramite indirizzo IP.

---

## d. Documentazione

Documentare problemi e possibili correzioni.

> [!CAUTION]
> Evitare di modificare configurazioni non necessarie:
> nel troubleshooting è importante isolare il problema senza introdurre nuovi errori.

---

# Parte 3 — Determinare i problemi di connettività da PC-A

## a. Verifica configurazione IP

Su **PC-A**, utilizzare:

```bash
ipconfig
```

per controllare:

* indirizzo IP;
* subnet mask;
* gateway predefinito.

Correggere eventuali configurazioni errate.

---

## b. Test di connettività

Eseguire ping verso:

* server web (`209.165.201.2`);
* gateway (`172.16.2.1`);
* PC-B;
* PC-01;
* PC-02.

Registrare i risultati.

> [!NOTE]
> La mancata comunicazione tra subnet differenti può indicare problemi di routing o gateway predefinito.

---

## c. Verifica accesso web

Aprire il browser e tentare di raggiungere:

```text
www.cisco.pka
```

Annotare i risultati ottenuti.

---

## d. Documentazione

Documentare:

* anomalie rilevate;
* verifiche effettuate;
* eventuali interventi correttivi.

---

# Parte 4 — Determinare i problemi di connettività da PC-B

## a. Verifica configurazione IP

Su **PC-B**, eseguire:

```bash
ipconfig
```

Verificare i parametri IP e correggere eventuali problemi.

---

## b. Test di connettività

Eseguire ping verso:

* server web (`209.165.201.2`);
* gateway (`172.16.2.1`);
* PC-A;
* PC-01;
* PC-02.

Registrare i risultati.

---

## c. Verifica accesso web

Utilizzare il browser per verificare l’accesso a:

```text
www.cisco.pka
```

e successivamente tramite indirizzo IP.

---

## d. Documentazione

Documentare:

* problemi individuati;
* eventuali limitazioni;
* modifiche applicate;
* comportamento osservato.

---

## e. Analisi DNS

Domanda operativa:

* Tutti i problemi possono essere risolti mantenendo l’utilizzo di DNS2?
* Se no, quali ulteriori azioni sarebbero necessarie?

> [!IMPORTANT]
> In presenza di più server DNS è essenziale verificare:
>
> * corretta configurazione degli indirizzi DNS;
> * raggiungibilità dei server;
> * presenza dei record DNS richiesti.

> [!TIP]
> Un server DNS può essere raggiungibile ma comunque non contenere i record necessari per la risoluzione dei nomi.

---

# Parte 5 — Verifica finale della connettività

Verificare che tutti i PC riescano ad accedere al server web:

```text
www.cisco.pka
```

Controllare che:

* la configurazione IP sia corretta;
* i gateway predefiniti siano configurati correttamente;
* il DNS funzioni;
* la connettività tra subnet sia operativa.

> [!NOTE]
> In Packet Tracer, una percentuale di completamento inferiore al 100% può indicare:
>
> * errori di configurazione;
> * problemi di connettività;
> * parametri non coerenti con la tabella di indirizzamento.

---

# Suggerimenti generali di troubleshooting

## Approccio consigliato

1. Verificare la configurazione IP locale.
2. Testare il gateway predefinito.
3. Verificare la connettività locale.
4. Testare la connettività remota.
5. Verificare DNS e servizi applicativi.
6. Documentare ogni modifica effettuata.

---

## Comandi Cisco utili

| Comando                   | Funzione                                  |
| ------------------------- | ----------------------------------------- |
| `ipconfig`                | Visualizza la configurazione IP del PC    |
| `ping`                    | Verifica la raggiungibilità Layer 3       |
| `tracert`                 | Mostra il percorso dei pacchetti          |
| `ssh`                     | Accesso remoto sicuro a dispositivi Cisco |
| `show ip interface brief` | Verifica stato e IP delle interfacce      |
| `show running-config`     | Visualizza la configurazione corrente     |
| `show ip route`           | Visualizza la tabella di routing          |

> [!WARNING]
> Modificare configurazioni di routing o DNS senza analisi preventiva può causare ulteriori interruzioni di rete.

---

# Glossario dei concetti chiave

| Termine             | Definizione                                                              |
| ------------------- | ------------------------------------------------------------------------ |
| DNS                 | Domain Name System, servizio che traduce nomi di dominio in indirizzi IP |
| Gateway predefinito | Router utilizzato per raggiungere reti esterne alla subnet locale        |
| ICMP                | Protocollo utilizzato dal comando `ping`                                 |
| IP Address          | Indirizzo logico utilizzato per identificare un host in rete             |
| Layer 2             | Livello collegamento dati del modello OSI                                |
| Layer 3             | Livello rete del modello OSI                                             |
| NIC                 | Network Interface Card, interfaccia di rete del dispositivo              |
| Packet Tracer       | Simulatore di rete Cisco                                                 |
| Ping                | Strumento di verifica della connettività IP                              |
| Routing             | Processo di instradamento dei pacchetti tra reti                         |
| SSH                 | Secure Shell, protocollo per accesso remoto sicuro                       |
| Subnet Mask         | Maschera utilizzata per identificare rete e host                         |
| TCP/IP              | Suite di protocolli utilizzata nelle reti IP                             |
| Troubleshooting     | Processo di identificazione e risoluzione dei problemi                   |
| URL                 | Uniform Resource Locator, indirizzo di una risorsa web                   |
| Web Server          | Server che fornisce contenuti tramite protocollo HTTP                    |
| DNS Record          | Associazione tra nome host e indirizzo IP                                |
| HTTP                | HyperText Transfer Protocol utilizzato per il traffico web               |
| Escalation          | Procedura di inoltro del problema a un livello tecnico superiore         |
