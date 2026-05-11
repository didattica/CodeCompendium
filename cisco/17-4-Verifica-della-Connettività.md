# Modulo 17 – Costruire una Piccola Rete

## 17.4 Verifica della Connettività di Rete

---

### 17.4.1 Verifica della Connettività con Ping

Il comando `ping` è il modo più efficace per testare rapidamente la connettività **Layer 3** tra un indirizzo IP di origine e di destinazione. Visualizza inoltre varie statistiche relative al **tempo di andata e ritorno** (round-trip time).

#### Protocollo utilizzato

Il comando `ping` si basa sul protocollo **ICMP (Internet Control Message Protocol)**:

| Tipo ICMP | Descrizione |
|---|---|
| **Type 8** | Echo Request (messaggio inviato dalla sorgente) |
| **Type 0** | Echo Reply (risposta dalla destinazione) |

> [!NOTE]
> Il comando `ping` è disponibile nella maggior parte dei sistemi operativi: **Windows**, **Linux**, **macOS** e **Cisco IOS**.

#### Comportamento su Windows 10

Un host Windows 10 invia **quattro messaggi echo ICMP** consecutivi e si aspetta quattro risposte echo ICMP dalla destinazione.

**Esempio:** PC A esegue il ping verso PC B (10.1.1.10)

```
C:\Users\PC-A> ping 10.1.1.10

Pinging 10.1.1.10 with 32 bytes of data:
Reply from 10.1.1.10: bytes=32 time=47ms TTL=51
Reply from 10.1.1.10: bytes=32 time=60ms TTL=51
Reply from 10.1.1.10: bytes=32 time=53ms TTL=51
Reply from 10.1.1.10: bytes=32 time=50ms TTL=51

Ping statistics for 10.1.1.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 47ms, Maximum = 60ms, Average = 52ms

C:\Users\PC-A>
```

L'output convalida la **connettività Layer 3** tra PC A e PC B.

#### Comportamento su Cisco IOS

Il ping IOS invia **cinque messaggi echo ICMP** (anziché quattro) e usa un formato di output differente:

```
R1# ping 10.1.1.10

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.1.10, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/2 ms
R1#
```

Ogni carattere nell'output rappresenta lo stato di una singola risposta echo ICMP. La tabella seguente elenca i caratteri più comuni:

#### Indicatori del Ping IOS

| Carattere | Significato |
|---|---|
| `!` | Ricezione corretta di un messaggio di risposta echo. Convalida la connettività Layer 3 tra origine e destinazione. |
| `.` | Timeout: il tempo è scaduto in attesa di una risposta echo. Indica un problema di connettività lungo il percorso. |
| `U` | Un router lungo il percorso ha risposto con un messaggio ICMP **Destination Unreachable (Type 3)**. Le cause possibili includono: route verso la rete di destinazione sconosciuta, oppure host di destinazione non trovato. |

> [!NOTE]
> Altre possibili risposte ping includono `Q`, `M`, `?`, `0` e `&`. Il loro significato non è trattato in questo modulo.

---

### 17.4.2 Ping Esteso

Un ping standard utilizza come indirizzo sorgente **l'IP dell'interfaccia più vicina alla rete di destinazione**. Ad esempio, eseguendo `ping 10.1.1.10` su R1, l'indirizzo sorgente sarebbe quello dell'interfaccia `G0/0/0` (es. `209.165.200.225`).

Cisco IOS offre una modalità **ping esteso** che permette di personalizzare i parametri del comando, incluso l'indirizzo IP sorgente.

#### Come avviare un ping esteso

Il ping esteso si avvia in modalità **Privileged EXEC** digitando `ping` senza specificare un indirizzo IP di destinazione. IOS guiderà l'utente attraverso una serie di prompt interattivi.

**Esempio:** testare la connettività dalla LAN di R1 (`192.168.10.0/24`) verso la rete `10.1.1.0/24`, specificando come sorgente l'interfaccia `G0/0/1` (`192.168.10.1`):

```
R1# ping
Protocol [ip]:
Target IP address: 10.1.1.10
Repeat count [5]:
Datagram size [100]:
Timeout in seconds [2]:
Extended commands [n]: y
Ingress ping [n]:
Source address or interface: 192.168.10.1
DSCP Value [0]:
Type of service [0]:
Set DF bit in IP header? [no]:
Validate reply data? [no]:
Data pattern [0x0000ABCD]:
Loose, Strict, Record, Timestamp, Verbose [none]:
Sweep range of sizes [n]:
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.1.10, timeout is 2 seconds:
Packet sent with a source address of 192.168.10.1
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
R1#
```

> [!TIP]
> Il ping esteso è particolarmente utile per simulare il traffico proveniente da una subnet specifica, senza dover accedere fisicamente a un host in quella rete.

> [!NOTE]
> Per i ping estesi in ambiente **IPv6**, utilizzare il comando `ping ipv6`.

---

### 17.4.3 Verifica della Connettività con il Comando Traceroute

Il comando `ping` è utile per rilevare rapidamente un problema di connettività Layer 3, ma **non identifica dove si trova il problema** lungo il percorso. Il comando `traceroute` (o `tracert` su Windows) restituisce invece un elenco degli **hop** attraversati da un pacchetto lungo il percorso verso la destinazione.

#### Sintassi del comando

| Sistema | Comando |
|---|---|
| **Windows** | `tracert 10.1.1.10` |
| **Cisco IOS** | `traceroute 10.1.1.10` |

#### Esempio – Output tracert su Windows 10

```
C:\Users\PC-A> tracert 10.1.1.10

Tracing route to 10.1.1.10 over a maximum of 30 hops:

  1     2 ms     2 ms     2 ms   192.168.10.1
  2     *        *        *      Request timed out.
  3     *        *        *      Request timed out.
  4     *        *        *      Request timed out.
^C
C:\Users\PC-A>
```

L'unica risposta ricevuta proviene dal gateway R1 (`192.168.10.1`). Gli hop successivi hanno restituito timeout (`*`), indicando un problema di connettività **tra R1 e R2**.

> [!NOTE]
> Utilizzare `Ctrl+C` per interrompere un `tracert` in Windows.

#### Esempio – Output traceroute su Cisco IOS

Topologia di riferimento: `R1 → R2 → R3 → PC B (10.1.1.10)`

**Trace riuscita:**

```
R1# traceroute 10.1.1.10

Type escape sequence to abort.
Tracing the route to 10.1.1.10
VRF info: (vrf in name/id, vrf out name/id)
  1  209.165.200.226  1 msec  0 msec  1 msec
  2  209.165.200.230  1 msec  0 msec  1 msec
  3  10.1.1.10        1 msec  0 msec  1 msec
R1#
```

Tutti e tre gli hop hanno risposto: la connettività verso PC B è confermata.

**Trace con destinazione non raggiungibile:**

```
R1# traceroute 10.1.1.10

Type escape sequence to abort.
Tracing the route to 10.1.1.10
VRF info: (vrf in name/id, vrf out name/id)
  1  209.165.200.226  1 msec  0 msec  1 msec
  2  209.165.200.230  1 msec  0 msec  1 msec
  3  *  *  *
  4  *  *  *
  5  *  *  *
```

I timeout a partire dall'hop 3 indicano che PC B non è raggiungibile.

> [!NOTE]
> Utilizzare `Ctrl+Shift+6` per interrompere un `traceroute` in Cisco IOS.

> [!IMPORTANT]
> L'implementazione Windows di `tracert` invia **Echo Request ICMP**. Cisco IOS e Linux utilizzano invece **UDP con numero di porta non valido**: la destinazione finale risponderà con un messaggio ICMP **Port Unreachable**.

---

### 17.4.4 Traceroute Esteso

Analogamente al ping esteso, Cisco IOS dispone di un comando **traceroute esteso** che permette di personalizzare i parametri dell'operazione. È particolarmente utile per:

- Individuare problemi durante la risoluzione di **loop di routing**.
- Determinare l'**esatto router dell'hop successivo**.
- Identificare dove i pacchetti vengono **ignorati o negati** da un router o firewall.

#### Opzioni di tracert su Windows

Su Windows, i parametri si specificano direttamente nella riga di comando:

```
C:\Users\PC-A> tracert /?

Usage: tracert [-d] [-h maximum_hops] [-j host-list] [-w timeout]
               [-R] [-S srcaddr] [-4] [-6] target_name

Options:
    -d                 Do not resolve addresses to hostnames.
    -h maximum_hops    Maximum number of hops to search for target.
    -j host-list       Loose source route along host-list (IPv4-only).
    -w timeout         Wait timeout milliseconds for each reply.
    -R                 Trace round-trip path (IPv6-only).
    -S srcaddr         Source address to use (IPv6-only).
    -4                 Force using IPv4.
    -6                 Force using IPv6.
```

#### Traceroute esteso su Cisco IOS

Il traceroute esteso si avvia in modalità **Privileged EXEC** digitando `traceroute` senza indirizzo IP. IOS guiderà l'utente tramite prompt interattivi.

**Esempio:** testare la connettività verso PC B specificando come sorgente l'interfaccia LAN di R1 (`192.168.10.1`):

```
R1# traceroute
Protocol [ip]:
Target IP address: 10.1.1.10
Ingress traceroute [n]:
Source address: 192.168.10.1
DSCP Value [0]:
Numeric display [n]:
Timeout in seconds [3]:
Probe count [3]:
Minimum Time to Live [1]:
Maximum Time to Live [30]:
Port Number [33434]:
Loose, Strict, Record, Timestamp, Verbose [none]:
Type escape sequence to abort.
Tracing the route to 10.1.1.10
VRF info: (vrf in name/id, vrf out name/id)
  1  209.165.200.226  1 msec  1 msec  1 msec
  2  209.165.200.230  0 msec  1 msec  0 msec
  3  10.1.1.10        2 msec  2 msec  *
R1#
```

> [!TIP]
> Premere **Invio** ai prompt interattivi per accettare i valori di default indicati tra parentesi quadre.

---

### 17.4.5 Baseline di Rete

Uno degli strumenti più efficaci per il monitoraggio e la risoluzione dei problemi di prestazione è stabilire una **baseline di rete** (o riferimento). La baseline rappresenta una fotografia delle prestazioni della rete in condizioni normali, e serve come punto di confronto per rilevare anomalie future.

> [!IMPORTANT]
> Una baseline efficace si costruisce **nel tempo**, misurando le prestazioni in momenti e condizioni di carico variabili. Non è sufficiente una singola rilevazione.

#### Come costruire una baseline

Un metodo semplice consiste nel:

1. Eseguire comandi di rete (`ping`, `traceroute`, ecc.) su host e router chiave.
2. Copiare e incollare l'output in un **file di testo**.
3. **Etichettare il file con la data** e salvarlo in un archivio.
4. Ripetere periodicamente e confrontare i risultati nel tempo.

Tra gli elementi da monitorare:

- **Messaggi di errore** nei risultati dei comandi.
- **Tempi di risposta** da host a host (round-trip time).

> [!WARNING]
> Un aumento considerevole dei tempi di risposta rispetto alla baseline è un indicatore di un potenziale **problema di latenza** che richiede indagine.

#### Esempio pratico – Confronto nel tempo

**Rilevazione di agosto (baseline):**

```
August 19, 2019 at 08:14:43

C:\Users\PC-A> ping 10.1.1.10

Pinging 10.1.1.10 with 32 bytes of data:
Reply from 10.1.1.10: bytes=32 time<1ms TTL=64
Reply from 10.1.1.10: bytes=32 time<1ms TTL=64
Reply from 10.1.1.10: bytes=32 time<1ms TTL=64
Reply from 10.1.1.10: bytes=32 time<1ms TTL=64

Ping statistics for 10.1.1.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

Round-trip time: **< 1 ms** → prestazioni ottimali.

**Rilevazione di settembre (un mese dopo):**

```
September 19, 2019 at 10:18:21

C:\Users\PC-A> ping 10.1.1.10

Pinging 10.1.1.10 with 32 bytes of data:
Reply from 10.1.1.10: bytes=32 time=50ms TTL=64
Reply from 10.1.1.10: bytes=32 time=49ms TTL=64
Reply from 10.1.1.10: bytes=32 time=46ms TTL=64
Reply from 10.1.1.10: bytes=32 time=47ms TTL=64

Ping statistics for 10.1.1.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 46ms, Maximum = 50ms, Average = 48ms
```

Round-trip time: **~48 ms** → aumento significativo rispetto alla baseline, possibile problema di latenza.

> [!TIP]
> Per le reti aziendali sono disponibili **strumenti software professionali** per l'archiviazione e l'aggiornamento automatico delle informazioni di baseline. Per approfondire le best practice Cisco, cercare su Internet: *"Baseline Process Best Practices"*.

---

### 17.4.6 

# Verifica della latenza di rete con ping e traceroute

> **Modulo:** 17.4 – Verifica della connettività  
> **Corso:** CCNA Introduzione alle reti 2026  
> **Categoria:** Laboratorio pratico  

---

## Indice

- [Obiettivi](#obiettivi)
- [Introduzione e scenario](#introduzione-e-scenario)
- [Risorse necessarie](#risorse-necessarie)
- [Parte 1 – Utilizzo del comando `ping`](#parte-1--utilizzo-del-comando-ping)
  - [Fase 1 – Verifica della connettività](#fase-1--verifica-della-connettività)
  - [Fase 2 – Raccolta dei dati di rete](#fase-2--raccolta-dei-dati-di-rete)
  - [Fase 3 – Verifica della raccolta dati](#fase-3--verifica-della-raccolta-dati)
  - [Tabella dei risultati – Parte 1](#tabella-dei-risultati--parte-1)
- [Parte 2 – Utilizzo del comando `tracert`](#parte-2--utilizzo-del-comando-tracert)
  - [Fase 1 – Esecuzione di tracert e salvataggio dell'output](#fase-1--esecuzione-di-tracert-e-salvataggio-delloutput)
  - [Fase 2 – Analisi del percorso tracciato](#fase-2--analisi-del-percorso-tracciato)
- [Parte 3 – Traceroute esteso (opzione `-d`)](#parte-3--traceroute-esteso-opzione--d)
- [Domande di approfondimento](#domande-di-approfondimento)
- [Riepilogo dei comandi](#riepilogo-dei-comandi)

---

## Obiettivi

- Utilizzare il comando **`ping`** per misurare e documentare la latenza di rete verso host remoti.
- Utilizzare il comando **`tracert`** (Windows) / **`traceroute`** (Linux/macOS) per tracciare il percorso dei pacchetti e analizzare la latenza hop per hop.
- Costruire una **baseline delle prestazioni di rete** raccogliendo dati statistici (minimo, massimo, media).

---

## Introduzione e scenario

La **latenza di rete** è il tempo che un pacchetto impiega per viaggiare da un host sorgente a un host destinazione e tornare indietro. Viene misurata in **millisecondi (ms)** e rappresenta uno degli indicatori fondamentali per valutare le prestazioni di una rete.

In questo laboratorio si analizza la latenza verso tre siti appartenenti ai **RIR (Regional Internet Registry)**, registri regionali per la gestione degli indirizzi IP a livello mondiale:

| Sito | Organizzazione | Regione |
|------|---------------|---------|
| `www.lacnic.net` | LACNIC | America Latina e Caraibi |
| `www.afrinic.net` | AFRINIC | Africa |
| `www.apnic.net` | APNIC | Asia-Pacifico |

> [!NOTE]
> I siti `www.ripe.net` (Europa) e `www.arin.net` (Nord America) **non rispondono alle richieste ICMP** e non possono essere utilizzati in questo laboratorio.

L'obiettivo è raccogliere dati in momenti diversi della giornata per ottenere un **campione rappresentativo** dell'attività di rete tipica.

---

## Risorse necessarie

- 1 PC con accesso a Internet
- Sistema operativo Windows (per i comandi `ping` e `tracert`)
- Accesso al **prompt dei comandi** (`cmd`) — potrebbe richiedere privilegi amministrativi

> [!TIP]
> Per aprire il prompt dei comandi con privilegi amministrativi su Windows, cerca `cmd` nel menu Start, fai clic destro e seleziona **"Esegui come amministratore"**.

---

## Parte 1 – Utilizzo del comando `ping`

### Cos'è il comando `ping`?

Il comando `ping` invia pacchetti **ICMP Echo Request** a un host remoto e attende le corrispondenti **ICMP Echo Reply**. Viene utilizzato per:

- Verificare se un host è **raggiungibile** in rete.
- Misurare il **Round-Trip Time (RTT)**, ovvero il tempo di andata e ritorno di un pacchetto.
- Diagnosticare problemi di **connettività** e **latenza**.

---

### Fase 1 – Verifica della connettività

Prima di raccogliere dati statistici, è necessario verificare che i siti di destinazione siano raggiungibili.

**Comandi da eseguire:**

```cmd
C:\Users\User1> ping www.lacnic.net
C:\Users\User1> ping www.afrinic.net
C:\Users\User1> ping www.apnic.net
```

**Output simulato – `ping www.lacnic.net`:**

```
Esecuzione di Ping www.lacnic.net [200.3.14.147] con 32 byte di dati:
Risposta da 200.3.14.147: byte=32 durata=218ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=221ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=219ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=220ms TTL=49

Statistiche Ping per 200.3.14.147:
    Pacchetti: Trasmessi = 4, Ricevuti = 4, Persi = 0 (0% persi),
Tempo approssimativo percorso andata/ritorno in millisecondi:
    Minimo = 218ms, Massimo = 221ms, Medio = 219ms
```

> **Analisi tecnica:**  
> Il TTL (Time To Live) ricevuto è **49**, indicando che il pacchetto ha attraversato circa **15 router** (64 − 49 = 15 hop, assumendo un TTL iniziale di 64). Il tempo medio di ~219 ms è atteso per un host in America Latina. La perdita di pacchetti è **0%**, confermando buona connettività.

---

**Output simulato – `ping www.afrinic.net`:**

```
Esecuzione di Ping www.afrinic.net [196.216.2.136] con 32 byte di dati:
Risposta da 196.216.2.136: byte=32 durata=187ms TTL=47
Risposta da 196.216.2.136: byte=32 durata=185ms TTL=47
Risposta da 196.216.2.136: byte=32 durata=189ms TTL=47
Risposta da 196.216.2.136: byte=32 durata=186ms TTL=47

Statistiche Ping per 196.216.2.136:
    Pacchetti: Trasmessi = 4, Ricevuti = 4, Persi = 0 (0% persi),
Tempo approssimativo percorso andata/ritorno in millisecondi:
    Minimo = 185ms, Massimo = 189ms, Medio = 187ms
```

> **Analisi tecnica:**  
> Il server AFRINIC si trova in **Sudafrica**. La latenza di ~187 ms riflette la distanza geografica e il numero di hop intercontinentali attraversati.

---

**Output simulato – `ping www.apnic.net`:**

```
Esecuzione di Ping www.apnic.net [202.12.29.205] con 32 byte di dati:
Risposta da 202.12.29.205: byte=32 durata=302ms TTL=43
Risposta da 202.12.29.205: byte=32 durata=298ms TTL=43
Risposta da 202.12.29.205: byte=32 durata=305ms TTL=43
Risposta da 202.12.29.205: byte=32 durata=301ms TTL=43

Statistiche Ping per 202.12.29.205:
    Pacchetti: Trasmessi = 4, Ricevuti = 4, Persi = 0 (0% persi),
Tempo approssimativo percorso andata/ritorno in millisecondi:
    Minimo = 298ms, Massimo = 305ms, Medio = 302ms
```

> **Analisi tecnica:**  
> APNIC ha sede in **Australia**. La latenza elevata (~302 ms) è conseguenza della grande distanza geografica e del numero maggiore di hop necessari per raggiungere la regione Asia-Pacifico.

> [!NOTE]
> Se i siti web vengono risolti in **indirizzi IPv6**, è possibile forzare la risoluzione IPv4 usando l'opzione `-4`:
> ```cmd
> ping -4 www.apnic.net
> ```

---

### Fase 2 – Raccolta dei dati di rete

Per ottenere statistiche affidabili, si inviano **25 richieste echo** a ciascun host. L'output viene reindirizzato in file di testo per una successiva analisi.

**Visualizzare le opzioni disponibili del comando `ping`:**

```cmd
C:\Users\User1> ping
```

```
Utilizzo: ping [-t] [-a] [-n conteggio] [-l dim] [-f] [-i TTL] [-v TOS]
              [-r conteggio] [-s conteggio] [[-j elenco-host] | [-k elenco-host]]
              [-w timeout] [-R] [-S indirizzo-origine] [-c compartimento] [-p]
              [-4] [-6] destinazione

Opzioni:
    -t             Esegue il ping dell'host specificato finché non viene interrotto.
    -n conteggio   Numero di richieste echo da inviare.
    -l dim         Dimensione del buffer di invio.
    -4             Forza l'uso di IPv4.
    -6             Forza l'uso di IPv6.
    -w timeout     Timeout in millisecondi per ogni risposta.
```

> [!TIP]
> L'opzione **`-n`** specifica il numero di pacchetti da inviare. Il valore predefinito di `ping` su Windows è **4 pacchetti**. Per una baseline affidabile, si usano **25 pacchetti**.

**Comandi con reindirizzamento dell'output su file:**

```cmd
C:\Users\User1> ping -n 25 www.lacnic.net > lacnic.txt
C:\Users\User1> ping -n 25 www.afrinic.net > afrinic.txt
C:\Users\User1> ping -n 25 www.apnic.net > apnic.txt
```

> [!IMPORTANT]
> Durante l'esecuzione dei comandi, **il terminale rimarrà vuoto**: l'output viene reindirizzato al file di testo e non mostrato a schermo. Questo è il comportamento atteso.

> [!WARNING]
> Il simbolo `>` **sovrascrive** il file di destinazione se già esistente. Per **aggiungere** dati a un file esistente senza sovrascriverlo, usa `>>`:
> ```cmd
> ping -n 25 www.lacnic.net >> lacnic.txt
> ```

---

### Fase 3 – Verifica della raccolta dati

Dopo l'esecuzione, verificare che i file siano stati creati correttamente.

**Elencare i file `.txt` nella directory:**

```cmd
C:\Users\User1> dir *.txt
```

```
Volume in drive C is OS
Volume Serial Number is 0A97-D265

 Directory of C:\Users\User1

07/02/2025  12:58  PM             1.589 lacnic.txt
07/02/2025  12:59  PM             1.642 afrinic.txt
07/02/2025  01:00  PM             1.615 apnic.txt
               3 File(s)          4.846 byte
               0 Dir(s)   45.231.616.000 byte disponibili
```

**Visualizzare il contenuto di un file:**

```cmd
C:\Users\User1> more lacnic.txt
```

> [!NOTE]
> Il comando `more` visualizza il contenuto del file una schermata alla volta.  
> - Premi **`Barra spaziatrice`** per avanzare alla schermata successiva.  
> - Premi **`q`** per uscire.

**Output simulato del file `lacnic.txt` (25 pacchetti):**

```
Esecuzione di Ping www.lacnic.net [200.3.14.147] con 32 byte di dati:
Risposta da 200.3.14.147: byte=32 durata=218ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=222ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=215ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=219ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=224ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=217ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=220ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=221ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=216ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=218ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=225ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=213ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=219ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=223ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=218ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=221ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=214ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=220ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=217ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=222ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=219ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=218ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=221ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=220ms TTL=49
Risposta da 200.3.14.147: byte=32 durata=217ms TTL=49

Statistiche Ping per 200.3.14.147:
    Pacchetti: Trasmessi = 25, Ricevuti = 25, Persi = 0 (0% persi),
Tempo approssimativo percorso andata/ritorno in millisecondi:
    Minimo = 213ms, Massimo = 225ms, Medio = 219ms
```

> **Analisi tecnica:**  
> Con 25 campioni si ottiene una distribuzione statistica più affidabile rispetto al test predefinito di 4 pacchetti. La variazione tra minimo (213 ms) e massimo (225 ms) è contenuta (~12 ms), indicando una connessione **stabile** verso LACNIC. Se la variazione fosse elevata (es. 50–100 ms), indicherebbe **jitter** o congestione di rete.

---

### Tabella dei risultati – Parte 1

Compilare la tabella con i dati raccolti dai tre file di testo:

| Destinazione | Minimo (ms) | Massimo (ms) | Media (ms) |
|---|---|---|---|
| `www.afrinic.net` | 185 | 195 | 187 |
| `www.apnic.net` | 298 | 310 | 302 |
| `www.lacnic.net` | 213 | 225 | 219 |

> [!NOTE]
> I valori nella tabella sono **simulati a scopo didattico**. I risultati reali varieranno in base alla posizione geografica dell'utente, all'ISP utilizzato e al carico della rete al momento del test.

**Domanda: In che modo il ritardo viene influenzato dalla posizione geografica?**

> La latenza è direttamente correlata alla **distanza geografica** tra l'host sorgente e la destinazione. Un host in America Latina (LACNIC) o Africa (AFRINIC) produce latenze moderate, mentre un host nell'area Asia-Pacifico (APNIC) produce latenze significativamente più alte. Questo è dovuto alla maggiore distanza fisica che i pacchetti devono percorrere attraverso cavi sottomarini e infrastrutture intercontinentali, e al numero maggiore di **hop** (router intermedi) attraversati lungo il percorso.

---

## Parte 2 – Utilizzo del comando `tracert`

### Cos'è il comando `tracert`?

`tracert` (Windows) / `traceroute` (Linux e macOS) è uno strumento diagnostico che **mappa il percorso** che i pacchetti seguono per raggiungere un host remoto. A differenza di `ping`, che misura solo il RTT totale verso la destinazione, `tracert` mostra la latenza **hop per hop**, identificando ogni router intermedio attraversato.

**Come funziona tecnicamente:**

`tracert` invia pacchetti ICMP con un campo **TTL (Time To Live)** incrementale, partendo da 1. Ogni router che riceve un pacchetto con TTL = 0 invia un messaggio di errore **"ICMP TTL Exceeded"** al mittente, rivelando così la propria posizione nel percorso. Il processo si ripete finché si raggiunge l'host di destinazione, che risponde con un **ICMP Echo Reply**.

---

### Fase 1 – Esecuzione di tracert e salvataggio dell'output

```cmd
C:\Users\User1> tracert www.lacnic.net > traceroute_lacnic.txt
C:\Users\User1> tracert www.afrinic.net > traceroute_afrinic.txt
C:\Users\User1> tracert www.apnic.net > traceroute_apnic.txt
```

> [!NOTE]
> Come per il comando `ping`, se i siti vengono risolti in IPv6, aggiungere l'opzione `-4` per forzare IPv4:
> ```cmd
> tracert -4 www.lacnic.net > traceroute_lacnic.txt
> ```

> [!WARNING]
> Il comando `tracert` può richiedere **diversi minuti** per completarsi, specialmente verso host geograficamente distanti. Il terminale rimarrà vuoto fino al completamento poiché l'output viene reindirizzato al file.

---

### Fase 2 – Analisi del percorso tracciato

**Visualizzare il contenuto del file:**

```cmd
C:\Users\User1> more traceroute_lacnic.txt
```

**Output simulato – `traceroute_lacnic.txt`:**

```
Traccia instradamento verso www.lacnic.net [200.3.14.147]
su un massimo di 30 hop:

  1    <1 ms    <1 ms    <1 ms  192.168.1.1
  2     8 ms     7 ms     8 ms  10.0.0.1
  3    12 ms    11 ms    13 ms  87.5.0.1
  4    15 ms    14 ms    16 ms  ae-3.r01.mlnoit01.it.bb.gin.ntt.net [129.250.9.17]
  5    18 ms    17 ms    19 ms  ae-4.r21.parsfr04.fr.bb.gin.ntt.net [129.250.6.66]
  6    37 ms    36 ms    38 ms  4.28.58.177
  7    78 ms    77 ms    80 ms  xe-0-0-1.cr01.mia01.us [64.125.31.246]
  8   298 ms   295 ms   301 ms  et-0-0-5.cr01.bog01.co [64.125.25.196]
  9   302 ms   299 ms   305 ms  xe-1-2-0.pr01.gru01.br [64.125.14.77]
 10   315 ms   312 ms   318 ms  200.3.14.1
 11   219 ms   217 ms   221 ms  www.lacnic.net [200.3.14.147]

Traccia completata.
```

> **Analisi tecnica hop per hop:**
>
> | Hop | RTT medio | Interpretazione |
> |-----|-----------|-----------------|
> | 1 | < 1 ms | **Gateway predefinito** (router locale). Latenza trascurabile sulla LAN. |
> | 2–3 | 7–13 ms | Rete dell'ISP locale (accesso e aggregazione). |
> | 4–5 | 14–19 ms | Backbone NTT, transit provider intercontinentale. Hop in Italia e Francia. |
> | 6 | ~37 ms | Transito verso infrastruttura transatlantica. |
> | 7 | ~78 ms | Arrivo in **Nord America** (Miami, USA). |
> | **8** | **~298 ms** | **Salto significativo** (+220 ms): attraversamento del cavo sottomarino verso il Sud America (Colombia). |
> | 9–10 | ~302–315 ms | Percorso in **Sud America** (Brasile). |
> | 11 | ~219 ms | Destinazione finale: `www.lacnic.net` (Uruguay). |

> [!IMPORTANT]
> Il **grande aumento di latenza tra l'hop 7 e l'hop 8** (da ~78 ms a ~298 ms) indica il punto in cui il pacchetto attraversa un **cavo sottomarino transatlantico** o transpacifico. Questi salti di latenza intercontinentali sono normali e attesi. Non indicano necessariamente un problema di rete.

> [!TIP]
> Per analizzare i risultati degli altri file, ripeti il comando `more` con i nomi file corrispondenti:
> ```cmd
> C:\Users\User1> more traceroute_afrinic.txt
> C:\Users\User1> more traceroute_apnic.txt
> ```

---

**Domanda: Che cosa è possibile concludere in merito alla relazione tra il tempo di round trip e la posizione geografica?**

> Il **RTT aumenta progressivamente** man mano che i pacchetti si allontanano dall'host sorgente. I salti più significativi di latenza coincidono con i **collegamenti intercontinentali** (cavi sottomarini o link satellitari). Più la destinazione è geograficamente distante, maggiore sarà il numero di hop attraversati e il RTT totale. Questo dimostra che la **posizione geografica è il principale fattore determinante della latenza** in una rete globale.

---

## Parte 3 – Traceroute esteso (opzione `-d`)

### Cos'è la risoluzione inversa dei nomi?

Per impostazione predefinita, `tracert` tenta di risolvere l'indirizzo IP di ogni hop nel corrispondente **nome di dominio** tramite una query **DNS inversa (PTR record)**. Questo processo, chiamato **reverse DNS lookup**, può:

- Aggiungere ritardo all'esecuzione del comando.
- Produrre risultati inesatti o timeout se il DNS non risponde.

### Utilizzo dell'opzione `-d`

L'opzione **`-d`** disabilita la risoluzione inversa dei nomi, mostrando solo gli indirizzi IP degli hop.

```cmd
C:\Users\User1> tracert -d www.lacnic.net > traceroute_d_lacnic.txt
C:\Users\User1> tracert -d www.afrinic.net > traceroute_d_afrinic.txt
C:\Users\User1> tracert -d www.apnic.net > traceroute_d_apnic.txt
```

**Visualizzare il file risultante:**

```cmd
C:\Users\User1> more traceroute_d_lacnic.txt
```

**Confronto output – con e senza opzione `-d`:**

*Senza `-d` (risoluzione nomi attiva):*
```
  7    78 ms    77 ms    80 ms  xe-0-0-1.cr01.mia01.us [64.125.31.246]
  8   298 ms   295 ms   301 ms  et-0-0-5.cr01.bog01.co [64.125.25.196]
```

*Con `-d` (risoluzione nomi disabilitata):*
```
  7    78 ms    77 ms    80 ms  64.125.31.246
  8   298 ms   295 ms   301 ms  64.125.25.196
```

> **Analisi tecnica:**  
> Con l'opzione `-d`, `tracert` mostra solo gli **indirizzi IP** degli hop, senza tentare di risolverli in nomi host. L'output è più essenziale ma si ottiene **più rapidamente**, poiché si eliminano i tempi di attesa per le query DNS inverse. Questa modalità è particolarmente utile in ambienti dove il DNS non è disponibile o è lento.

**Domanda: Che cosa è cambiato nell'output di `tracert` dopo l'aggiunta dell'opzione `-d`?**

> Con l'opzione `-d`, gli hop vengono mostrati con i soli **indirizzi IP numerici**, senza la corrispondente risoluzione del nome host. Il comando viene eseguito più velocemente perché non effettua query DNS inverse per ogni router intermedio. Questo è utile per diagnosi rapide o in reti dove la risoluzione DNS potrebbe essere lenta o non disponibile.

> [!NOTE]
> Su **Cisco IOS**, il comando equivalente è `traceroute` in modalità estesa. A differenza di Windows, Cisco IOS non usa opzioni da riga di comando, ma presenta una **serie interattiva di domande** che permettono all'amministratore di personalizzare parametri come protocollo, TTL minimo/massimo, timeout e dimensione dei pacchetti.

---

## Domande di approfondimento

### 1. Come ottenere una baseline accurata della latenza di rete?

Per costruire una **baseline delle prestazioni** affidabile è necessario:

- Eseguire i test **in momenti diversi della giornata** (mattina, pomeriggio, sera, notte) per catturare variazioni legate al traffico.
- Ripetere le misurazioni in **giorni diversi** (feriali e festivi) per identificare pattern ricorrenti.
- Usare un **numero elevato di campioni** (almeno 25–50 pacchetti per sessione) per calcolare statistiche significative.
- Documentare le misurazioni in una **tabella o database** con timestamp, per analisi temporali.
- Misurare verso **destinazioni multiple** a distanze geografiche diverse.
- Registrare anche **eventi anomali** (latenze elevate, perdita di pacchetti) come riferimento per il confronto futuro.

### 2. Come utilizzare le informazioni di baseline?

La baseline di rete serve come **riferimento di confronto** per:

- **Rilevare anomalie**: se la latenza attuale supera significativamente la baseline, è probabile che ci sia un problema (congestione, guasto hardware, attacco DDoS).
- **Pianificare la capacità**: identificare ore di punta e dimensionare l'infrastruttura di conseguenza.
- **Validare modifiche**: dopo aggiornamenti o riconfigurazioni, confrontare le nuove misurazioni con la baseline per verificare che le prestazioni non siano degradate.
- **Supportare gli SLA** (Service Level Agreement): dimostrare con dati oggettivi che la rete rispetta i livelli di servizio concordati.
- **Troubleshooting proattivo**: individuare trend di peggioramento progressivo prima che si trasformino in interruzioni di servizio.

---

## Riepilogo dei comandi

| Comando | Descrizione | Esempio |
|---|---|---|
| `ping <host>` | Verifica connettività e misura RTT (4 pacchetti) | `ping www.lacnic.net` |
| `ping -n 25 <host>` | Invia 25 pacchetti echo | `ping -n 25 www.lacnic.net` |
| `ping -4 <host>` | Forza risoluzione IPv4 | `ping -4 www.apnic.net` |
| `ping -n 25 <host> > file.txt` | Salva output su file | `ping -n 25 www.lacnic.net > lacnic.txt` |
| `tracert <host>` | Traccia percorso con risoluzione DNS | `tracert www.lacnic.net` |
| `tracert -d <host>` | Traccia percorso senza risoluzione DNS | `tracert -d www.lacnic.net` |
| `tracert -4 <host>` | Traccia percorso forzando IPv4 | `tracert -4 www.apnic.net` |
| `dir *.txt` | Elenca i file di testo nella directory | `dir *.txt` |
| `more <file>` | Visualizza contenuto del file pagina per pagina | `more lacnic.txt` |

---

> [!CAUTION]
> Prima di eseguire comandi `ping` e `tracert` su una rete aziendale o scolastica, verificare sempre con l'amministratore di rete o l'istruttore eventuali **restrizioni di sicurezza** o **policy locali**. Alcuni ambienti bloccano il traffico ICMP per motivi di sicurezza.

---

*Documento generato per uso didattico nell'ambito del corso CCNA Introduzione alle reti 2026 — Modulo 17.4*  
*© 2013–2020 Cisco e/o relative affiliate. Tutti i diritti riservati.*

*Modulo basato sul materiale Cisco Networking Academy – Cisco Packet Tracer*
