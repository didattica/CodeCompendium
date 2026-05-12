# Modulo 17.7 — Scenari di risoluzione dei problemi

---

## 17.7.1 Problemi di funzionamento duplex e mancata corrispondenza

### Definizione di duplex

Nelle comunicazioni dati, il termine **duplex** fa riferimento alla **direzione di trasmissione dei dati** tra due dispositivi.

Esistono due modalità di comunicazione duplex:

- **Half-duplex** — Le comunicazioni sono limitate allo scambio di dati in **una direzione alla volta**.
- **Full-duplex** — Le comunicazioni possono essere **inviate e ricevute simultaneamente**.

---

### Autonegoziazione Ethernet

Le interfacce Ethernet di interconnessione devono funzionare nella **stessa modalità duplex** per:

- ottenere le migliori prestazioni di comunicazione,
- evitare inefficienze e latenza sul collegamento.

La funzione di **autonegoziazione Ethernet** facilita la configurazione e massimizza le prestazioni tra due dispositivi Ethernet interconnessi. Il processo si svolge in due fasi:

1. I dispositivi connessi **annunciano le funzionalità supportate**.
2. Viene **selezionata la modalità con le prestazioni più elevate** supportata da entrambe le estremità (ad esempio, full-duplex).

---

### Duplex Mismatch

Se uno dei due dispositivi connessi funziona in **full-duplex** e l'altro in **half-duplex**, si verifica un **duplex mismatch**.

> [!WARNING]
> ### ⚠️ Attenzione: Duplex Mismatch
> Sebbene la trasmissione dati attraverso un collegamento con duplex mismatch avvenga comunque, le **prestazioni di collegamento saranno molto scadenti**.

**Cause comuni del duplex mismatch:**

- Interfaccia configurata in modo errato.
- Autonegoziazione non riuscita (caso raro).

> [!CAUTION]
> ### 🔍 Difficoltà diagnostica
> I duplex mismatch possono essere **difficili da risolvere** perché la comunicazione tra i dispositivi continua a funzionare, rendendo il problema non immediatamente evidente.

---

## 17.7.2 Problemi di indirizzamento IP sui dispositivi IOS

### Descrizione del problema

I problemi relativi agli **indirizzi IP** impediscono ai dispositivi nella rete remota di comunicare correttamente.

Poiché gli indirizzi IP sono **gerarchici**, qualsiasi indirizzo IP assegnato a un dispositivo di rete deve essere conforme all'intervallo di indirizzi della propria rete.

Gli indirizzi IP erroneamente assegnati causano:

- **Conflitti di indirizzi IP**
- **Problemi di routing**

---

### Cause comuni

Due cause principali dell'assegnazione IPv4 errata:

1. **Errori manuali di assegnazione** — Gli amministratori di rete assegnano manualmente gli indirizzi a dispositivi quali server e router. Un errore di digitazione o di pianificazione causa problemi di comunicazione.
2. **Problemi correlati a DHCP** — Se il server DHCP non è raggiungibile o è mal configurato, i dispositivi ricevono indirizzi errati o non ricevono alcun indirizzo.

---

### Verifica con comandi IOS

Su un dispositivo IOS, utilizzare i seguenti comandi per verificare gli indirizzi IPv4 assegnati alle interfacce:

```
show ip interface
show ip interface brief
```

**Esempio di output — `show ip interface brief` su R1:**

```
R1# show ip interface brief
Interface              IP-Address       OK? Method Status   Protocol
GigabitEthernet0/0/0  209.165.200.225  YES manual up       up
GigabitEthernet0/0/1  192.168.10.1     YES manual up       up
Serial0/1/0            unassigned       NO  unset  down     down
Serial0/1/1            unassigned       NO  unset  down     down
GigabitEthernet0      unassigned       YES unset  administratively down  down
```

> [!TIP]
> ### 💡 Consiglio operativo
> Il comando `show ip interface brief` è il modo più rapido per ottenere una panoramica dello stato di tutte le interfacce di un router Cisco IOS.

---

## 17.7.3 Problemi di indirizzamento IP sui dispositivi terminali

### APIPA — Automatic Private IP Addressing

Nei computer basati su **Windows**, quando il dispositivo non riesce a contattare un server DHCP, Windows assegna automaticamente un indirizzo nell'intervallo:

```
169.254.0.0/16
```

Questa funzione è denominata **APIPA (Automatic Private IP Addressing)** ed è progettata per facilitare la comunicazione all'interno della rete locale.

> [!IMPORTANT]
> ### 💡 Concetto chiave — APIPA
> Un computer con un indirizzo APIPA **non sarà in grado di comunicare con altri dispositivi nella rete**, poiché molto probabilmente questi non appartengono alla rete `169.254.0.0/16`. La presenza di un indirizzo APIPA è un segnale chiaro di un problema con il server DHCP.

> [!NOTE]
> ### 📝 Nota — Altri sistemi operativi
> Altri sistemi operativi, quali **Linux** e **macOS (OS X)**, **non assegnano** un indirizzo IPv4 all'interfaccia di rete se la comunicazione con il server DHCP non riesce.

---

### Verifica dell'indirizzo IP su Windows

Per verificare gli indirizzi IP assegnati a un computer basato su Windows, utilizzare il comando:

```cmd
ipconfig
```

**Esempio di output:**

```
C:\Users\PC-A> ipconfig

Windows IP Configuration

Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  :
   Link-local IPv6 Address . . . . : fe80::a4aa:2dd1:ae2d:a75e%16
   IPv4 Address. . . . . . . . . . : 192.168.10.10
   Subnet Mask . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . : 192.168.10.1
```

---

## 17.7.4 Problemi del gateway predefinito

### Definizione

Il **gateway predefinito** per un dispositivo terminale è il **dispositivo di rete più vicino capace di inoltrare il traffico ad altre reti**.

> [!IMPORTANT]
> ### 💡 Concetto chiave — Gateway predefinito
> Se un dispositivo presenta un indirizzo del gateway predefinito **errato o inesistente**, non potrà comunicare con i dispositivi nelle **reti remote**. L'indirizzo del gateway predefinito deve appartenere alla **stessa rete** del dispositivo terminale.

---

### Cause comuni

L'indirizzo del gateway predefinito può essere impostato:

- **Manualmente** — Errori di configurazione da parte dell'amministratore.
- **Automaticamente tramite DHCP** — Problemi con il server DHCP.

---

### Risoluzione

**Per gateway configurato manualmente:** verificare e correggere l'indirizzo con quello appropriato.

**Per gateway ottenuto via DHCP:**

1. Verificare che il dispositivo possa comunicare con il server DHCP.
2. Verificare che sull'interfaccia del router siano configurati correttamente l'indirizzo IPv4 e la subnet mask.
3. Verificare che l'interfaccia del router sia **attiva (up)**.

---

### Verifica su dispositivi terminali Windows

```cmd
C:\Users\PC-A> ipconfig

Windows IP Configuration

Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  :
   Link-local IPv6 Address . . . . : fe80::a4aa:2dd1:ae2d:a75e%16
   IPv4 Address. . . . . . . . . . : 192.168.10.10
   Subnet Mask . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . : 192.168.10.1
```

---

### Verifica su router IOS

Su un router, utilizzare il comando `show ip route` per elencare la tabella di routing e verificare il **gateway predefinito** (noto come *route predefinita*).

```
R1# show ip route | begin Gateway

Gateway of last resort is 209.165.200.226 to network 0.0.0.0

O*E2  0.0.0.0/0 [110/1] via 209.165.200.226, 02:19:50, GigabitEthernet0/0/0
      10.0.0.0/24 is subnetted, 1 subnets
O       10.1.1.0 [110/3] via 209.165.200.226, 02:05:42, GigabitEthernet0/0/0
      192.168.10.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.10.0/24 is directly connected, GigabitEthernet0/0/1
L       192.168.10.1/32 is directly connected, GigabitEthernet0/0/1
      209.165.200.0/24 is variably subnetted, 3 subnets, 2 masks
C       209.165.200.224/30 is directly connected, GigabitEthernet0/0/0
L       209.165.200.225/32 is directly connected, GigabitEthernet0/0/0
O       209.165.200.228/30 [110/2] via 209.165.200.226, 02:07:19, GigabitEthernet0/0/0
```

**Lettura dell'output:**

| Riga | Significato |
|------|-------------|
| `Gateway of last resort is 209.165.200.226` | Il gateway predefinito è configurato sull'indirizzo `209.165.200.226` |
| `O*E2 0.0.0.0/0 via 209.165.200.226` | R1 ha appreso il gateway predefinito tramite il protocollo **OSPF** |

> [!NOTE]
> ### 📝 Nota — Route predefinita
> La route `0.0.0.0/0` è la **route predefinita**: viene utilizzata quando l'indirizzo di destinazione del pacchetto non corrisponde ad alcuna altra route nella tabella di routing. Rappresenta il *"gateway di ultima istanza"*.

---

## 17.7.5 Risoluzione dei problemi di DNS

### Cos'è il DNS

Il **Domain Name System (DNS)** è un servizio automatizzato che fa corrispondere i nomi simbolici (come `www.cisco.com`) ai relativi indirizzi IP.

> [!IMPORTANT]
> ### 💡 Concetto chiave — DNS e percezione dell'utente
> Sebbene la risoluzione DNS **non sia fondamentale** per la comunicazione tra dispositivi a livello di rete, è **essenziale per l'esperienza dell'utente finale**. Un server DNS irraggiungibile porta spesso l'utente a credere erroneamente che "la rete sia inattiva" o che "internet non funzioni", anche quando il routing e gli altri servizi di rete sono pienamente operativi.

---

### Assegnazione degli indirizzi DNS

Gli indirizzi del server DNS possono essere assegnati:

- **Manualmente** — Tipicamente dagli amministratori di rete per server e dispositivi fissi.
- **Automaticamente tramite DHCP** — Per i client di rete.

---

### Server DNS pubblici di riferimento

| Provider | Indirizzo IPv4 | Indirizzo IPv6 |
|----------|----------------|----------------|
| **Google DNS** | `8.8.8.8` | `2001:4860:4860::8888` |
| **Cisco OpenDNS** (Preferred) | `208.67.222.222` | — |
| **Cisco OpenDNS** (Alternate) | `208.67.220.220` | — |

> [!TIP]
> ### 💡 Cisco OpenDNS
> Cisco offre **OpenDNS**, che fornisce un servizio DNS sicuro con filtraggio di phishing e siti malware. Funzionalità avanzate come il filtraggio dei contenuti Web e la sicurezza sono disponibili per famiglie e aziende.

---

### Verifica del server DNS su Windows

Utilizzare il comando `ipconfig /all` per visualizzare il server DNS in uso:

```cmd
C:\Users\PC-A> ipconfig /all

Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  :
   Description . . . . . . . . . . : Intel(R) Dual Band Wireless-AC 8265
   Physical Address. . . . . . . . : F8-94-C2-E4-C5-0A
   DHCP Enabled. . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . : Yes
   Link-local IPv6 Address . . . . : fe80::a4aa:2dd1:ae2d:a75e%16 (Preferred)
   IPv4 Address. . . . . . . . . . : 192.168.10.10 (Preferred)
   Subnet Mask . . . . . . . . . . : 255.255.255.0
   Lease Obtained. . . . . . . . . : August 17, 2019 1:20:17 PM
   Lease Expires . . . . . . . . . : August 18, 2019 1:20:18 PM
   Default Gateway . . . . . . . . : 192.168.10.1
   DHCP Server . . . . . . . . . . : 192.168.10.1
   DHCPv6 IAID . . . . . . . . . . : 100177090
   DHCPv6 Client DUID. . . . . . . : 00-01-00-01-21-F3-76-75-54-E1-AD-DE-DA-9A
   DNS Servers . . . . . . . . . . : 208.67.222.222
   NetBIOS over Tcpip. . . . . . . : Enabled
```

---

### Utilizzo di nslookup

Il comando `nslookup` è uno strumento per la risoluzione manuale di query DNS e l'analisi delle risposte.

```cmd
C:\Users\PC-A> nslookup
Default Server:  Home-Net
Address:  192.168.1.1

> cisco.com
Server:  Home-Net
Address:  192.168.1.1

Non-authoritative answer:
Name:    cisco.com
Addresses:  2001:420:1101:1::185
            72.163.4.185

> 8.8.8.8
Server:  Home-Net
Address:  192.168.1.1

Name:    dns.google
Address:  8.8.8.8

> 208.67.222.222
Server:  Home-Net
Address:  192.168.1.1

Name:    resolver1.opendns.com
Address:  208.67.222.222
```

> [!TIP]
> ### 💡 Utilizzo avanzato di nslookup
> Con `nslookup` è possibile inserire anche un **indirizzo IP** per ottenere la risoluzione inversa del nome (reverse DNS lookup). Ad esempio, inserendo `8.8.8.8` viene restituito il nome `dns.google`.

---

## Glossario / Ripasso rapido

| Termine | Descrizione |
|---------|-------------|
| **Duplex** | Direzione di trasmissione dei dati tra due dispositivi |
| **Half-duplex** | Comunicazione in una sola direzione alla volta |
| **Full-duplex** | Comunicazione bidirezionale simultanea |
| **Duplex Mismatch** | Condizione in cui due dispositivi connessi utilizzano modalità duplex diverse; causa degrado delle prestazioni |
| **Autonegoziazione** | Meccanismo Ethernet che seleziona automaticamente la modalità duplex ottimale tra due dispositivi |
| **DHCP** | Dynamic Host Configuration Protocol — protocollo per l'assegnazione automatica degli indirizzi IP |
| **APIPA** | Automatic Private IP Addressing — assegna un indirizzo nel range `169.254.0.0/16` quando il DHCP non è raggiungibile (solo Windows) |
| **Gateway predefinito** | Dispositivo di rete più vicino capace di inoltrare traffico verso altre reti |
| **Route predefinita** | Route `0.0.0.0/0` nella tabella di routing; usata quando nessuna altra route corrisponde alla destinazione |
| **Gateway di ultima istanza** | Termine Cisco per il gateway predefinito configurato su un router |
| **DNS** | Domain Name System — traduce i nomi di dominio in indirizzi IP |
| **OSPF** | Open Shortest Path First — protocollo di routing dinamico a stato dei link |
| **OpenDNS** | Servizio DNS sicuro offerto da Cisco, con filtraggio di phishing e malware |
| **Google DNS** | Server DNS pubblico di Google: `8.8.8.8` (IPv4) e `2001:4860:4860::8888` (IPv6) |
| **nslookup** | Comando per interrogare manualmente i server DNS e analizzare le risposte |
| **ipconfig** | Comando Windows per visualizzare la configurazione di rete (indirizzo IP, subnet mask, gateway) |
| **ipconfig /all** | Variante estesa di `ipconfig`; mostra anche server DHCP, DNS, indirizzi MAC e dettagli lease |
| **show ip interface brief** | Comando IOS per visualizzare lo stato e gli indirizzi IP di tutte le interfacce di un router |
| **show ip route** | Comando IOS per visualizzare la tabella di routing completa |
| **IOS** | Internetwork Operating System — sistema operativo dei dispositivi Cisco |
| **IPv4** | Protocollo Internet versione 4; indirizzi a 32 bit in notazione decimale puntata |
| **IPv6** | Protocollo Internet versione 6; indirizzi a 128 bit in notazione esadecimale |
| **SOHO** | Small Office Home Office — piccoli uffici o uffici domestici |
| **ISP** | Internet Service Provider — fornitore di accesso a Internet |
