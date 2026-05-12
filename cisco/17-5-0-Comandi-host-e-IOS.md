# Modulo 17.5 — Verifica della connettività IP e comandi di diagnostica

> Corso: **Cisco Networking Academy — Introduction to Networks (ITN)**  
> Modulo: **17 — Build a Small Network**  
> Sezione: **17.5 — Verifica della connettività IP**

---

## Indice

- [17.5.1 Configurazione IP su un host Windows](#1751-configurazione-ip-su-un-host-windows)
- [17.5.2 Configurazione IP su un host Linux](#1752-configurazione-ip-su-un-host-linux)
- [17.5.3 Configurazione IP su un host macOS](#1753-configurazione-ip-su-un-host-macos)
- [17.5.4 Comando `arp`](#1754-comando-arp)
- [17.5.5 Rivisitazione dei comandi `show` comuni](#1755-rivisitazione-dei-comandi-show-comuni)
- [17.5.6 Comando `show cdp neighbors`](#1756-comando-show-cdp-neighbors)
- [17.5.7 Comando `show ip interface brief`](#1757-comando-show-ip-interface-brief)
- [17.5.8 Il comando `show version`](#1758-il-comando-show-version)
- [17.5.9 Lab — Interpretare l'output del comando `show`](#1759-lab--interpretare-loutput-del-comando-show)

---

## 17.5.1 Configurazione IP su un host Windows

> [!TIP]
> ### Strumenti di Verifica: Host vs Router
> Per un troubleshooting efficace, bisogna saper usare gli strumenti giusti su ogni dispositivo:
>
> * **Sul PC (End Device):** Usa `ipconfig /all` per verificare la tua "identità" in rete e `arp -a` per vedere chi altro è presente nel tuo segmento locale.
> * **Sul Router (Network Device):** Usa `show ip interface brief` per lo stato fisico e `show ip route` per capire il percorso dei pacchetti verso reti remote.
> * **Risoluzione conflitti:** Se due PC hanno lo stesso IP, il comando `release/renew` forza il protocollo DHCP a rinegoziare un indirizzo univoco, risolvendo l'errore senza riavviare la macchina.

### Descrizione

Quando si verificano problemi di connettività, il primo passo è controllare la **configurazione IP dei dispositivi host**. Su sistemi Windows è possibile farlo sia tramite interfaccia grafica (Network and Sharing Center) che da riga di comando.

Gli amministratori di rete preferiscono generalmente la **riga di comando**, più rapida e scriptabile.

---

### Comando: `ipconfig`

**Scopo:** Visualizza le informazioni di base sulla configurazione IP delle interfacce di rete attive.

**Quando si usa:** Come primo controllo rapido per verificare indirizzo IP, maschera di sottorete e gateway predefinito.

```cmd
C:\Users\PC-A> ipconfig
```

**Output simulato:**

```
Windows IP Configuration

Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::a4aa:2dd1:ae2d:a75e%16
   IPv4 Address. . . . . . . . . . . : 192.168.10.10
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.10.1
```

> [!NOTE]
> Le quattro informazioni fondamentali da verificare sono: **indirizzo IP**, **maschera di sottorete**, **gateway predefinito** e **server DNS**. Un errore in una di queste voci causa la perdita di connettività.

---

### Comando: `ipconfig /all`

**Scopo:** Visualizza informazioni dettagliate su tutte le interfacce, inclusi indirizzo MAC, stato DHCP, lease time e server DNS.

**Quando si usa:** Quando si ha bisogno di informazioni complete sul Layer 2 e Layer 3 del dispositivo, ad esempio per verificare se l'indirizzo è stato assegnato via DHCP o configurato manualmente.

```cmd
C:\Users\PC-A> ipconfig /all
```

**Output simulato:**

```
Windows IP Configuration

   Host Name . . . . . . . . . . . . : PC-A-00H20
   Primary Dns Suffix  . . . . . . . : cisco.com
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : cisco.com

Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Intel(R) Dual Band Wireless-AC 8265
   Physical Address. . . . . . . . . : F8-94-C2-E4-C5-0A
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::a4aa:2dd1:ae2d:a75e%16 (Preferred)
   IPv4 Address. . . . . . . . . . . : 192.168.10.10 (Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Lease Obtained. . . . . . . . . . : August 17, 2019 1:20:17 PM
   Lease Expires . . . . . . . . . . : August 18, 2019 1:20:18 PM
   Default Gateway . . . . . . . . . : 192.168.10.1
   DHCP Server . . . . . . . . . . . : 192.168.10.1
   DHCPv6 IAID . . . . . . . . . . . : 100177090
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-21-F3-76-75-54-E1-AD-DE-DA-9A
   DNS Servers . . . . . . . . . . . : 192.168.10.1
   NetBIOS over Tcpip. . . . . . . . : Enabled
```

> [!TIP]
> Il campo **Physical Address** corrisponde all'indirizzo MAC dell'interfaccia. Il campo **DHCP Enabled: Yes** indica che l'indirizzo è stato assegnato dinamicamente. Il **Lease Obtained/Expires** indica la durata del contratto DHCP.

---

### Comandi: `ipconfig /release` e `ipconfig /renew`

**Scopo:** Rilasciano e rinnovano l'indirizzo IP su un client DHCP.

**Quando si usa:** Quando si sospetta che l'indirizzo IP corrente sia errato, scaduto o in conflitto con un altro host. Utile durante il troubleshooting DHCP.

```cmd
C:\Users\PC-A> ipconfig /release
```

```
Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::a4aa:2dd1:ae2d:a75e%16
   Default Gateway . . . . . . . . . :
```

> [!NOTE]
> Dopo `/release`, l'indirizzo IPv4 viene rimosso e il campo Default Gateway risulta vuoto. Il dispositivo non ha più connettività di Layer 3.

```cmd
C:\Users\PC-A> ipconfig /renew
```

```
Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::a4aa:2dd1:ae2d:a75e%16
   IPv4 Address. . . . . . . . . . . : 192.168.1.124
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.1.1
```

> [!NOTE]
> Dopo `/renew`, il client contatta di nuovo il server DHCP e ottiene un nuovo indirizzo IP. L'indirizzo può essere lo stesso o diverso rispetto a quello precedente, a seconda della configurazione del server.

---

### Comando: `ipconfig /displaydns`

**Scopo:** Visualizza la cache DNS locale del sistema, cioè tutti i nomi di dominio precedentemente risolti e memorizzati in memoria.

**Quando si usa:** Per verificare se un nome di dominio è già stato risolto e per controllare il valore TTL (Time To Live) delle voci in cache. Utile per diagnosticare problemi di risoluzione DNS.

```cmd
C:\Users\PC-A> ipconfig /displaydns
```

**Output simulato:**

```
Windows IP Configuration

netacad.com
----------------------------------------
    Record Name . . . . . : netacad.com
    Record Type . . . . . : 1
    Time To Live  . . . . : 602
    Data Length . . . . . : 4
    Section . . . . . . . : Answer
    A (Host) Record . . . : 54.165.95.219
```

> [!TIP]
> Il **TTL (Time To Live)** indica i secondi rimanenti prima che la voce venga eliminata dalla cache. Il **Record Type 1** corrisponde a un record di tipo **A (Host Record)**, cioè un'associazione nome → indirizzo IPv4. Per svuotare la cache DNS su Windows si usa il comando `ipconfig /flushdns`.

---

## 17.5.2 Configurazione IP su un host Linux

### Descrizione

Su Linux la verifica della configurazione IP tramite GUI varia a seconda della distribuzione e dell'ambiente desktop (es. GNOME su Ubuntu). Da riga di comando, i comandi principali sono `ifconfig` e `ip address`.

---

### Comando: `ifconfig`

**Scopo:** Visualizza lo stato e la configurazione IP delle interfacce di rete attive.

**Quando si usa:** Per visualizzare indirizzi IP, MAC address, statistiche di traffico (pacchetti RX/TX) e stato delle interfacce su sistemi Linux.

```bash
[analyst@secOps ~]$ ifconfig
```

**Output simulato:**

```
enp0s3    Link encap:Ethernet  HWaddr 08:00:27:b5:d6:cb
          inet addr:10.0.2.15  Bcast:10.0.2.255  Mask:255.255.255.0
          inet6 addr: fe80::57c6:ed95:b3c9:2951/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1332239 errors:0 dropped:0 overruns:0 frame:0
          TX packets:105910 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:1855455014 (1.8 GB)  TX bytes:13140139 (13.1 MB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
```

> [!NOTE]
> L'interfaccia `lo` è il **loopback** (127.0.0.1), sempre presente e utilizzata per la comunicazione interna al sistema. L'interfaccia `enp0s3` è la scheda di rete Ethernet fisica. Il flag `UP BROADCAST RUNNING` indica che l'interfaccia è attiva e operativa.

---

### Comando: `ip address`

**Scopo:** Visualizza gli indirizzi IP e le loro proprietà. Può essere usato anche per aggiungere o rimuovere indirizzi IP.

**Quando si usa:** È il comando moderno e preferito rispetto a `ifconfig` sulle distribuzioni Linux più recenti. Fornisce informazioni più dettagliate e supporta pienamente IPv6.

```bash
[analyst@secOps ~]$ ip address show
```

> [!NOTE]
> L'output di `ip address` può variare a seconda della distribuzione Linux in uso. Su distribuzioni moderne (Ubuntu 20.04+, Fedora, ecc.), `ifconfig` potrebbe non essere installato di default e va sostituito con `ip address`.

---

## 17.5.3 Configurazione IP su un host macOS

### Descrizione

Su macOS è possibile verificare la configurazione IP tramite **Network Preferences → Advanced** nella GUI. Da riga di comando si utilizzano `ifconfig` e i comandi `networksetup`.

---

### Comando: `ifconfig`

**Scopo:** Visualizza la configurazione delle interfacce di rete, analogamente a Linux.

```bash
MacBook-Air:~ Admin$ ifconfig en0
```

**Output simulato:**

```
en0: flags=8863 mtu 1500
    ether c4:b3:01:a0:64:98
    inet6 fe80::c0f:1bf4:60b1:3adb%en0 prefixlen 64 secured scopeid 0x5
    inet 10.10.10.113 netmask 0xffffff00 broadcast 10.10.10.255
    nd6 options=201
    media: autoselect
    status: active
```

> [!NOTE]
> Su macOS la maschera di sottorete viene espressa in formato esadecimale: `0xffffff00` corrisponde a `255.255.255.0`. Il campo `ether` indica l'indirizzo MAC dell'interfaccia.

---

### Comando: `networksetup -listallnetworkservices`

**Scopo:** Elenca tutti i servizi di rete configurati sul sistema macOS.

```bash
MacBook-Air:~ Admin$ networksetup -listallnetworkservices
```

**Output simulato:**

```
An asterisk (*) denotes that a network service is disabled.
iPhone USB
Wi-Fi
Bluetooth PAN
Thunderbolt Bridge
```

---

### Comando: `networksetup -getinfo <network service>`

**Scopo:** Visualizza le impostazioni IP dettagliate per un servizio di rete specifico.

**Quando si usa:** Per verificare rapidamente la configurazione DHCP, IP, maschera, router e MAC address di un'interfaccia specifica su macOS.

```bash
MacBook-Air:~ Admin$ networksetup -getinfo Wi-Fi
```

**Output simulato:**

```
DHCP Configuration
IP address: 10.10.10.113
Subnet mask: 255.255.255.0
Router: 10.10.10.1
Client ID:
IPv6: Automatic
IPv6 IP address: none
IPv6 Router: none
Wi-Fi ID: c4:b3:01:a0:64:98
```

> [!TIP]
> A differenza di `ifconfig`, il comando `networksetup -getinfo` mostra la maschera di sottorete in formato decimale puntato (es. `255.255.255.0`), più leggibile. È particolarmente utile per script di amministrazione su macOS.

---

## 17.5.4 Comando `arp`

### Descrizione

Il comando `arp` è disponibile su Windows, Linux e macOS. Visualizza la **cache ARP** dell'host, cioè la tabella che associa gli indirizzi IPv4 agli indirizzi fisici (MAC) dei dispositivi con cui il sistema ha comunicato di recente.

Il protocollo ARP (Address Resolution Protocol) opera al **Layer 2** ed è fondamentale per la comunicazione sulla stessa rete LAN.

---

### Topologia di riferimento

```
                    10.0.0.254/24
                         |
    PC-A         [Switch/Hub]
  10.0.0.5/24        |
              -----+-----+-----+-----
              |         |     |     |
         10.0.0.1  10.0.0.2  10.0.0.3  10.0.0.4
```

---

### Comando: `arp -a`

**Scopo:** Visualizza tutte le voci presenti nella cache ARP locale: indirizzo IP, indirizzo MAC corrispondente e tipo (statico o dinamico).

**Quando si usa:** Per verificare quali dispositivi sono stati contattati di recente, per diagnosticare conflitti ARP o per identificare un dispositivo a partire dal suo indirizzo MAC.

```cmd
C:\Users\PC-A> arp -a
```

**Output simulato (su PC-A con IP 10.0.0.5):**

```
Interface: 192.168.93.175 --- 0xc
  Internet Address      Physical Address      Type
  10.0.0.2              d0-67-e5-b6-56-4b     dynamic
  10.0.0.3              78-48-59-e3-b4-01     dynamic
  10.0.0.4              00-21-b6-00-16-97     dynamic
  10.0.0.254            00-15-99-cd-38-d9     dynamic
```

> [!NOTE]
> L'indirizzo `10.0.0.5` **non compare** nella cache ARP perché si tratta dell'indirizzo dello stesso PC-A — un host non inserisce sé stesso nella propria tabella ARP. L'indirizzo `10.0.0.1` non è presente perché PC-A non ha comunicato con quel dispositivo di recente. La cache ARP elenca **solo** i dispositivi contattati di recente.

> [!TIP]
> Per aggiungere un dispositivo alla cache ARP è sufficiente eseguire un `ping` verso di esso. La tabella verrà aggiornata automaticamente con la nuova associazione IP ↔ MAC.

---

### Svuotare la cache ARP

Per forzare il ripopolamento della cache ARP con informazioni aggiornate, è possibile svuotarla con:

```cmd
C:\Users\PC-A> netsh interface ip delete arpcache
```

> [!WARNING]
> Per eseguire questo comando potrebbe essere necessario disporre dei **privilegi di amministratore** sull'host Windows. Se eseguito senza i permessi corretti, il comando restituisce un errore di accesso negato.

---

## 17.5.5 Rivisitazione dei comandi `show` comuni

### Descrizione

Cisco IOS mette a disposizione una serie di comandi `show` che consentono agli amministratori di rete di **verificare la configurazione**, **monitorare lo stato delle interfacce** e **diagnosticare problemi** su router e switch. Praticamente ogni processo o funzionalità del router può essere ispezionato tramite un comando `show`.

---

### Tabella riepilogativa dei comandi `show`

| Comando | Utilizzato per… |
|---|---|
| `show running-config` | Verificare la configurazione e le impostazioni correnti |
| `show interfaces` | Verificare lo stato dell'interfaccia e visualizzare messaggi di errore |
| `show ip interface` | Verificare le informazioni di Layer 3 relative a un'interfaccia |
| `show arp` | Verificare la lista degli host noti sulle LAN Ethernet locali |
| `show ip route` | Verificare le informazioni di routing Layer 3 |
| `show protocols` | Verificare quali protocolli sono operativi |
| `show version` | Verificare memoria, interfacce e licenze attive sul dispositivo |

---

### Comando: `show running-config`

**Scopo:** Visualizza la configurazione attualmente in esecuzione sul dispositivo (salvata in RAM). Include hostname, configurazione delle interfacce, routing, banner, password e molto altro.

**Quando si usa:** Come primo passo per verificare che la configurazione del dispositivo corrisponda a quanto atteso. Fondamentale durante il troubleshooting.

```
R1# show running-config
```

**Output simulato:**

```
!
version 15.5
service timestamps debug datetime msec
service timestamps log datetime msec
service password-encryption
!
hostname R1
!
interface GigabitEthernet0/0/0
 description Link to R2
 ip address 209.165.200.225 255.255.255.252
 negotiation auto
!
interface GigabitEthernet0/0/1
 description Link to LAN
 ip address 192.168.10.1 255.255.255.0
 negotiation auto
!
router ospf 10
 network 192.168.10.0 0.0.0.255 area 0
 network 209.165.200.224 0.0.0.3 area 0
!
banner motd C Authorized access only! ^C
!
line con 0
 password 7 14141B180F0B
 login
!
line vty 0 4
 password 7 00071A150754
 login
 transport input telnet ssh
!
end
```

> [!NOTE]
> La configurazione `running-config` risiede in **RAM** ed è quella attiva. Non viene salvata automaticamente: per renderla persistente è necessario usare il comando `copy running-config startup-config`. Le password mostrate come `password 7` sono offuscate con l'algoritmo Cisco Type 7 (non sicuro per ambienti di produzione).

---

### Comando: `show interfaces`

**Scopo:** Visualizza informazioni dettagliate sullo stato fisico e logico di tutte le interfacce, inclusi contatori di errori, statistiche di traffico, MTU, duplex e velocità.

**Quando si usa:** Per diagnosticare problemi di connettività fisica (es. interfaccia down), errori di CRC, collisioni o reset anomali dell'interfaccia.

```
R1# show interfaces
```

**Output simulato:**

```
GigabitEthernet0/0/0 is up, line protocol is up
  Hardware is ISR4321-2x1GE, address is ab:e0:af:0d:e1:40 (bia ab:e0:af:0d:e1:40)
  Description: Link to R2
  Internet address is 209.165.200.225/30
  MTU 1500 bytes, BW 100000 Kbit/sec, DLY 100 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Full Duplex, 100Mbps, link type is auto, media type is RJ45
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:01, output 00:00:21, output hang never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     5127 packets input, 590285 bytes, 0 no buffer
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     1150 packets output, 153999 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
```

> [!TIP]
> Presta attenzione ai campi **CRC**, **input errors** e **interface resets**: valori alti indicano problemi fisici come cavi difettosi, connettori allentati o incompatibilità duplex. Un contatore **interface resets** che cresce nel tempo può indicare instabilità del collegamento.

> [!CAUTION]
> La combinazione `GigabitEthernet0/0/0 is up, line protocol is down` indica che il livello fisico funziona (cavo collegato) ma c'è un problema di Layer 2 (es. mismatch di encapsulation o keepalive). Invece, `is administratively down` significa che l'interfaccia è stata disabilitata manualmente con il comando `shutdown`.

---

### Comando: `show ip interface`

**Scopo:** Visualizza informazioni di Layer 3 dettagliate per ogni interfaccia: indirizzo IP, access list applicate, stato Proxy ARP, CEF, multicast, ecc.

**Quando si usa:** Per verificare la corretta applicazione di ACL su un'interfaccia, lo stato del CEF (Cisco Express Forwarding), o per diagnosticare problemi di routing IP.

```
R1# show ip interface
```

**Output simulato (estratto per GigabitEthernet0/0/0):**

```
GigabitEthernet0/0/0 is up, line protocol is up
  Internet address is 209.165.200.225/30
  Broadcast address is 255.255.255.255
  MTU is 1500 bytes
  Helper address is not set
  Directed broadcast forwarding is disabled
  Outgoing Common access list is not set
  Outgoing access list is not set
  Inbound Common access list is not set
  Inbound access list is not set
  Proxy ARP is enabled
  IP fast switching is enabled
  IP CEF switching is enabled
```

> [!NOTE]
> I campi **Outgoing/Inbound access list** mostrano eventuali ACL applicate all'interfaccia. Se risultano `not set`, nessun filtro è attivo. Il **Proxy ARP enabled** significa che il router risponde alle richieste ARP per conto di host su altre reti (comportamento predefinito su Cisco IOS).

---

### Comando: `show arp`

**Scopo:** Visualizza la tabella ARP del router: associazioni tra indirizzi IP e indirizzi MAC degli host raggiungibili direttamente sulle interfacce del router.

**Quando si usa:** Per verificare quali host sono stati contattati di recente dal router e per diagnosticare problemi di comunicazione a Layer 2 tra router e host della LAN.

```
R1# show arp
```

**Output simulato:**

```
Protocol  Address          Age (min)  Hardware Addr       Type    Interface
Internet  192.168.10.1            -   a0e0.af0d.e141      ARPA    GigabitEthernet0/0/1
Internet  192.168.10.10          95   c07b.bcc4.a9c0      ARPA    GigabitEthernet0/0/1
Internet  209.165.200.225         -   ab e0.af0d.e140      ARPA    GigabitEthernet0/0/0
Internet  209.165.200.226       138   a03d.6fe1.9d90      ARPA    GigabitEthernet0/0/0
```

> [!NOTE]
> Le voci con **Age `-`** corrispondono agli indirizzi IP del router stesso (nessuna scadenza). Le voci con un valore numerico in minuti sono associate ad host remoti e scadono dopo un certo periodo (default 4 ore su Cisco IOS). Se un host non compare nella tabella ARP, il router non ha comunicato con esso di recente.

---

### Comando: `show ip route`

**Scopo:** Visualizza la tabella di routing IP del router, mostrando tutte le reti raggiungibili e il percorso per raggiungerle.

**Quando si usa:** Per verificare che le rotte siano presenti e corrette, per diagnosticare problemi di raggiungibilità di rete e per capire da dove provengono le informazioni di routing (statico, OSPF, EIGRP, ecc.).

```
R1# show ip route
```

**Output simulato:**

```
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       * - candidate default

Gateway of last resort is 209.165.200.226 to network 0.0.0.0

O*E2  0.0.0.0/0 [110/1] via 209.165.200.226, 02:19:50, GigabitEthernet0/0/0
      10.0.0.0/24 is subnetted, 1 subnets
O        10.1.1.0 [110/3] via 209.165.200.226, 02:05:42, GigabitEthernet0/0/0
      192.168.10.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.10.0/24 is directly connected, GigabitEthernet0/0/1
L        192.168.10.1/32 is directly connected, GigabitEthernet0/0/1
      209.165.200.0/24 is variably subnetted, 3 subnets, 2 masks
C        209.165.200.224/30 is directly connected, GigabitEthernet0/0/0
L        209.165.200.225/32 is directly connected, GigabitEthernet0/0/0
O        209.165.200.228/30 [110/2] via 209.165.200.226, 02:07:19, GigabitEthernet0/0/0
```

> [!NOTE]
> Le rotte con codice **C** (Connected) indicano reti direttamente connesse alle interfacce del router. Le rotte **L** (Local) indicano gli indirizzi IP specifici delle interfacce del router stesso. Le rotte **O** (OSPF) provengono dal protocollo di routing dinamico OSPF. La rotta `0.0.0.0/0` è il **gateway of last resort** (default route): viene usata quando nessuna altra rotta corrisponde alla destinazione.

---

### Comando: `show protocols`

**Scopo:** Fornisce un riepilogo rapido dello stato operativo di tutte le interfacce e dei protocolli di rete attivi.

**Quando si usa:** Per avere una visione immediata e compatta delle interfacce attive/inattive e degli indirizzi IP associati, senza i dettagli completi di `show interfaces`.

```
R1# show protocols
```

**Output simulato:**

```
Global values:
  Internet Protocol routing is enabled
GigabitEthernet0/0/0 is up, line protocol is up
  Internet address is 209.165.200.225/30
GigabitEthernet0/0/1 is up, line protocol is up
  Internet address is 192.168.10.1/24
Serial0/1/0 is down, line protocol is down
Serial0/1/1 is down, line protocol is down
GigabitEthernet0 is administratively down, line protocol is down
```

> [!NOTE]
> Questo output mostra chiaramente quali interfacce sono operative e quali no. Le interfacce `Serial0/1/0` e `Serial0/1/1` risultano **down/down** (nessun cavo collegato o problema fisico). `GigabitEthernet0` risulta **administratively down** perché è stata esplicitamente disabilitata con il comando `shutdown`.

---

### Comando: `show version`

**Scopo:** Visualizza informazioni sul sistema operativo IOS, sull'hardware del dispositivo (tipo di processore, quantità di RAM e Flash), sulle interfacce presenti e sulle licenze attive.

**Quando si usa:** Per verificare la versione di IOS installata, la quantità di memoria disponibile per un aggiornamento, il tempo di uptime del dispositivo e il tipo di hardware.

```
R1# show version
```

**Output simulato:**

```
Cisco IOS XE Software, Version 03.16.08.S - Extended Support Release
Cisco IOS Software, ISR Software (X86_64_LINUX_IOSD-UNIVERSALK9-M), Version 15.5(3)S8

ROM: IOS-XE ROMMON

R1 uptime is 2 hours, 25 minutes
System returned to ROM by reload
System image file is "bootflash:/isr4300-universalk9.03.16.08.S.155-3.S8-ext.SPA.bin"
Last reload reason: LocalSoft

Processor board ID FLM2044W0LT
2 Gigabit Ethernet interfaces
2 Serial interfaces
32768K bytes of non-volatile configuration memory.
4194304K bytes of physical memory.
3207167K bytes of flash memory at bootflash:.
978928K bytes of USB flash at usb0:.

Configuration register is 0x2102

Technology Package License Information:
Technology    Technology-package   Technology-package
              Current Type         Next reboot
appxk9        appxk9               RightToUse
securityk9    securityk9           Permanent
ipbase        ipbasek9             Permanent
```

> [!TIP]
> Il campo **Configuration register** (`0x2102`) indica la modalità di avvio del router. Il valore `0x2102` è quello standard (avvio da flash con configurazione salvata). Se il valore fosse `0x2142`, il router si avvierebbe ignorando la configurazione salvata (usato per il recupero della password).

---

## 17.5.6 Comando `show cdp neighbors`

### Descrizione

**CDP (Cisco Discovery Protocol)** è un protocollo proprietario Cisco che opera al **Layer 2 (Data Link Layer)**. Viene avviato automaticamente su tutti i dispositivi Cisco e consente di **scoprire automaticamente i dispositivi Cisco direttamente collegati**, indipendentemente dai protocolli di Layer 3 configurati.

CDP scambia periodicamente pacchetti di annuncio (advertisement) con i vicini diretti, condividendo informazioni hardware e software.

### Informazioni fornite da CDP per ogni vicino

| Informazione | Descrizione |
|---|---|
| **Device ID** | Hostname configurato sul dispositivo vicino |
| **Address List** | Indirizzo di Layer 3 del dispositivo vicino |
| **Port ID** | Nome della porta locale e remota |
| **Capabilities** | Tipo di dispositivo (router, switch L2/L3, ecc.) |
| **Platform** | Modello hardware del dispositivo (es. Cisco 2960+) |

---

### Topologia di riferimento

```
R3 (G0/0/1) ──────── (F0/5) S3 ──────── S4
```

---

### Comando: `show cdp neighbors`

**Scopo:** Elenca i dispositivi Cisco direttamente collegati che inviano annunci CDP.

**Quando si usa:** Per scoprire la topologia fisica di rete, identificare dispositivi vicini sconosciuti, o verificare le connessioni tra dispositivi.

```
R3# show cdp neighbors
```

**Output simulato:**

```
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater, P - Phone,
                  D - Remote, C - CVTA, M - Two-port Mac Relay

Device ID   Local Intrfce   Holdtme   Capability  Platform      Port ID
S3          Gig 0/0/1       122             S      WS-C2960+     Fas 0/5

Total cdp entries displayed: 1
```

> [!NOTE]
> CDP rileva **solo i dispositivi direttamente collegati**. Per questo motivo, R3 vede S3 (connesso direttamente su G0/0/1 ↔ F0/5) ma **non vede S4**, che è connesso a S3 e non a R3 direttamente.
>
> Il campo **Capability S** indica che S3 è uno Switch. Il **Platform WS-C2960+** identifica il modello hardware Cisco Catalyst 2960+.

---

### Comando: `show cdp neighbors detail`

**Scopo:** Estende l'output di `show cdp neighbors` aggiungendo l'indirizzo IP del vicino, la versione IOS, il numero di serie e altre informazioni dettagliate.

**Quando si usa:** Quando si sospetta un errore di configurazione IP su un dispositivo vicino, o quando si ha bisogno dell'indirizzo IP del vicino per connettersi ad esso.

```
R3# show cdp neighbors detail
```

**Output simulato:**

```
-------------------------
Device ID: S3
Entry address(es):
  IP address: 192.168.1.2
Platform: cisco WS-C2960+,  Capabilities: Switch
Interface: GigabitEthernet0/0/1,  Port ID (outgoing port): FastEthernet0/5
Holdtime : 148 sec

Version :
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4

advertisement version: 2
Protocol Hello:  OUI=0x00000C, Protocol ID=0x0112; payload len=27, value=...
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
```

> [!WARNING]
> CDP può rappresentare un **rischio per la sicurezza**: fornisce informazioni dettagliate sull'infrastruttura di rete (modelli, versioni IOS, indirizzi IP) che potrebbero essere sfruttate da un attaccante.
>
> **Best practice:**
> - Disabilitare CDP globalmente con `no cdp run` se non necessario
> - Abilitare CDP **solo** sulle interfacce collegate ad altri dispositivi Cisco dell'infrastruttura
> - Disabilitare CDP sulle porte degli utenti con `no cdp enable` a livello di interfaccia

---

## 17.5.7 Comando `show ip interface brief`

### Descrizione

Il comando `show ip interface brief` è uno dei comandi più utilizzati dagli amministratori Cisco. Fornisce un **riepilogo compatto** dello stato di tutte le interfacce del dispositivo, mostrando in una singola riga per ciascuna: nome dell'interfaccia, indirizzo IP assegnato, metodo di configurazione e stato operativo.

---

### Comando su router

```
R1# show ip interface brief
```

**Output simulato:**

```
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0/0   209.165.200.225 YES manual up                    up
GigabitEthernet0/0/1   192.168.10.1    YES manual up                    up
Serial0/1/0            unassigned      NO  unset  down                   down
Serial0/1/1            unassigned      NO  unset  down                   down
GigabitEthernet0       unassigned      YES unset  administratively down  down
```

---

### Interpretazione delle colonne

| Colonna | Significato |
|---|---|
| **Interface** | Nome dell'interfaccia |
| **IP-Address** | Indirizzo IPv4 configurato (o `unassigned`) |
| **OK?** | Se la configurazione IP è valida (YES/NO) |
| **Method** | Come è stato assegnato l'IP (`manual`, `DHCP`, `unset`) |
| **Status** | Stato del Layer 1 — fisico (`up`/`down`/`administratively down`) |
| **Protocol** | Stato del Layer 2 — protocollo (`up`/`down`) |

> [!NOTE]
> La combinazione **Status up / Protocol up** indica che l'interfaccia è completamente operativa. **Status up / Protocol down** suggerisce un problema di Layer 2 (es. mismatch di configurazione). **Administratively down** significa che l'interfaccia è stata spenta manualmente con il comando `shutdown`.

---

### Comando su switch

Il comando funziona anche sugli switch, dove le interfacce fisiche non hanno normalmente un indirizzo IP assegnato (salvo la VLAN di gestione).

```
S1# show ip interface brief
```

**Output simulato:**

```
Interface         IP-Address       OK? Method Status   Protocol
Vlan1             192.168.254.250  YES manual up        up
FastEthernet0/1   unassigned       YES unset  down      down
FastEthernet0/2   unassigned       YES unset  up        up
FastEthernet0/3   unassigned       YES unset  up        up
```

> [!NOTE]
> - **Vlan1** ha l'indirizzo IP di gestione assegnato ed è operativa.
> - **FastEthernet0/1** risulta `down/down`: nessun dispositivo collegato o problema con il dispositivo connesso.
> - **FastEthernet0/2** e **FastEthernet0/3** risultano `up/up`: dispositivi correttamente collegati e operativi.

> [!TIP]
> `show ip interface brief` è il comando ideale per avere una **panoramica rapida** dello stato dell'intero dispositivo in pochi secondi. È spesso il primo comando da eseguire durante un'attività di troubleshooting.

---

## 17.5.8 Il comando `show version`

Il comando `show version` permette di verificare e risolvere problemi relativi a componenti hardware e software del dispositivo. È particolarmente utile durante la procedura di avvio del dispositivo.

Consultare la sezione [17.5.5 — `show version`](#comando-show-version) per l'output dettagliato e la relativa interpretazione.

> [!NOTE]
> Il comando `show version` è disponibile come video nella piattaforma Cisco NetAcad come riferimento per questa sezione.

---

## 17.5.9 Lab — Interpretare l'output del comando `show`

### Obiettivi

- **Parte 1:** Analizzare l'output dei comandi `show`
- **Parte 2:** Rispondere alle domande di riflessione

### Scenario

Questa attività è progettata per consolidare l'utilizzo dei comandi `show` su router Cisco IOS. Non è richiesta alcuna configurazione: l'obiettivo è **leggere e interpretare** l'output dei comandi. La connessione avviene tramite la console di ISPRouter, accessibile da ISP PC → Desktop → Terminal.

---

### Comandi da analizzare

```
ISPRouter# show arp
ISPRouter# show flash:
ISPRouter# show ip route
ISPRouter# show interfaces
ISPRouter# show ip interface brief
ISPRouter# show protocols
ISPRouter# show users
ISPRouter# show version
```

> [!CAUTION]
> Se l'output si interrompe con il prompt `--More--`, premere la **barra spaziatrice** per continuare a scorrere. Premere `q` per uscire. Non premere Invio: fa avanzare di una sola riga alla volta.

---

### Output simulati e commento tecnico

#### `show arp`

```
ISPRouter# show arp
Protocol  Address         Age (min)  Hardware Addr       Type    Interface
Internet  10.0.0.1               -   00:1A:2B:3C:4D:5E   ARPA    GigabitEthernet0/0
Internet  10.0.0.2              12   00:1A:2B:3C:4D:6F   ARPA    GigabitEthernet0/0
Internet  192.168.1.1            -   00:1A:2B:3C:4D:7A   ARPA    GigabitEthernet0/1
```

**📌 Commento tecnico:** Questo output mostra le associazioni IP ↔ MAC note al router. Le voci con Age `-` corrispondono agli indirizzi IP del router stesso. Utile per verificare la raggiungibilità degli host a Layer 2.

---

#### `show flash:`

```
ISPRouter# show flash:
-#- --length-- -----date/time------ path
  1   57336492 Aug  8 2018 10:52:46 +00:00 isr4300-universalk9.03.16.08.S.155-3.S8-ext.SPA.bin

62652416 bytes available (57336492 bytes used)
```

**📌 Commento tecnico:** Mostra il contenuto della memoria flash del router, inclusi i file dell'immagine IOS. Il campo **bytes available** indica lo spazio libero rimanente. Prima di un aggiornamento IOS, verificare che la nuova immagine entri nella flash disponibile.

---

#### `show ip route`

```
ISPRouter# show ip route

Gateway of last resort is 0.0.0.0 to network 0.0.0.0

S*    0.0.0.0/0 [1/0] via 0.0.0.0, GigabitEthernet0/0
C     10.0.0.0/24 is directly connected, GigabitEthernet0/0
L     10.0.0.1/32 is directly connected, GigabitEthernet0/0
C     192.168.1.0/24 is directly connected, GigabitEthernet0/1
L     192.168.1.1/32 is directly connected, GigabitEthernet0/1
```

**📌 Commento tecnico:** La tabella di routing mostra le reti raggiungibili. **C** = reti direttamente connesse, **L** = indirizzi locali delle interfacce, **S*** = rotta statica di default. Se una rete di destinazione non compare, il traffico verrà instradato verso la rotta di default (se presente).

---

#### `show interfaces`

```
ISPRouter# show interfaces GigabitEthernet0/0
GigabitEthernet0/0 is up, line protocol is up
  Hardware is ISR4321-2x1GE, address is 001a.2b3c.4d5e (bia 001a.2b3c.4d5e)
  Internet address is 10.0.0.1/24
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec
  Full Duplex, 1000Mbps, link type is auto, media type is RJ45
  0 input errors, 0 CRC, 0 frame
  0 output errors, 0 collisions, 0 interface resets
```

**📌 Commento tecnico:** Un'interfaccia con stato `up/up`, 0 errori e 0 CRC è in perfetta salute. Valori non nulli nei campi `CRC`, `input errors` o `interface resets` indicano problemi fisici o di configurazione da investigare.

---

#### `show ip interface brief`

```
ISPRouter# show ip interface brief
Interface             IP-Address    OK? Method Status               Protocol
GigabitEthernet0/0    10.0.0.1      YES manual up                   up
GigabitEthernet0/1    192.168.1.1   YES manual up                   up
Serial0/1/0           unassigned    NO  unset  down                  down
```

**📌 Commento tecnico:** Panoramica immediata dello stato delle interfacce. Le due GigabitEthernet sono operative (`up/up`). La Serial0/1/0 è inattiva e senza indirizzo IP — normale se non è in uso in questa topologia.

---

#### `show protocols`

```
ISPRouter# show protocols
Global values:
  Internet Protocol routing is enabled
GigabitEthernet0/0 is up, line protocol is up
  Internet address is 10.0.0.1/24
GigabitEthernet0/1 is up, line protocol is up
  Internet address is 192.168.1.1/24
Serial0/1/0 is down, line protocol is down
```

**📌 Commento tecnico:** Visualizzazione compatta simile a `show ip interface brief` ma focalizzata sui protocolli. Conferma che le due interfacce GigabitEthernet sono attive e che la Serial è inattiva.

---

#### `show users`

```
ISPRouter# show users
    Line       User       Host(s)              Idle       Location
*  0 con 0               idle                 00:00:00
   2 vty 0    admin      idle                 00:02:34    192.168.1.10

Interface    User               Mode         Idle     Peer Address
```

**📌 Commento tecnico:** Mostra le sessioni attive sul dispositivo. La riga con `*` indica la sessione corrente (console). `vty 0` mostra che un secondo utente (`admin`) è connesso via Telnet/SSH dall'indirizzo `192.168.1.10`. Utile per verificare se un collega sta lavorando contemporaneamente sul dispositivo.

---

#### `show version`

*(Output già mostrato in dettaglio nella sezione [17.5.5](#comando-show-version))*

**📌 Commento tecnico:** Fornisce versione IOS, modello hardware, uptime, memoria RAM e Flash disponibile, interfacce fisiche e licenze. Indispensabile prima di un aggiornamento firmware.

---

### Domande di riflessione — Risposte guidate

**1. Quali comandi consentono di determinare l'indirizzo IP e il prefisso di rete delle interfacce?**

`show ip interface brief`, `show interfaces`, `show ip interface`, `show protocols`, `show running-config`

---

**2. Quale comando fornisce l'indirizzo IP e l'assegnazione all'interfaccia, ma NON il prefisso di rete?**

`show arp` — mostra indirizzi IP associati alle interfacce ma non indica la maschera/prefisso.

---

**3. Quali comandi permettono di verificare se un'interfaccia è attiva?**

`show interfaces`, `show ip interface brief`, `show protocols`

---

**4. Quale comando mostra la versione IOS in esecuzione?**

`show version`

---

**5. Quali comandi forniscono informazioni sugli indirizzi delle interfacce del router?**

`show interfaces`, `show ip interface`, `show ip interface brief`, `show protocols`, `show running-config`, `show arp`

---

**6. Si sta valutando un aggiornamento IOS: quale comando mostra la memoria Flash disponibile?**

`show flash:` e `show version` (il campo relativo alla Flash memory)

---

**7. Si vuole verificare se un collega è connesso al router: quale comando usare?**

`show users` — mostra tutte le sessioni attive (console e VTY)

---

**8. Quale comando fornisce statistiche sul traffico delle interfacce?**

`show interfaces` — include contatori di pacchetti RX/TX, errori, CRC, collisioni e bit rate

---

**9. I clienti non riescono a raggiungere un server: quale comando verifica i percorsi di rete disponibili?**

`show ip route` — mostra la tabella di routing e i percorsi verso le reti di destinazione

---

**10. Quali interfacce sono attualmente attive su ISPRouter?**

Basandosi sull'output simulato: **GigabitEthernet0/0** e **GigabitEthernet0/1** risultano `up/up`.

---

## Riepilogo generale

| Comando | Sistema | Scopo principale |
|---|---|---|
| `ipconfig` | Windows | Visualizza configurazione IP base |
| `ipconfig /all` | Windows | Visualizza configurazione IP completa (MAC, DHCP, DNS) |
| `ipconfig /release` + `/renew` | Windows | Rilascia e rinnova lease DHCP |
| `ipconfig /displaydns` | Windows | Mostra cache DNS locale |
| `ifconfig` | Linux/macOS | Visualizza configurazione interfacce di rete |
| `ip address` | Linux | Visualizza e gestisce indirizzi IP (comando moderno) |
| `networksetup` | macOS | Gestisce servizi di rete da riga di comando |
| `arp -a` | Windows/Linux/macOS | Visualizza cache ARP locale |
| `show running-config` | Cisco IOS | Configurazione corrente del dispositivo |
| `show interfaces` | Cisco IOS | Stato e statistiche interfacce |
| `show ip interface` | Cisco IOS | Informazioni Layer 3 delle interfacce |
| `show ip interface brief` | Cisco IOS | Riepilogo compatto stato interfacce |
| `show arp` | Cisco IOS | Tabella ARP del router |
| `show ip route` | Cisco IOS | Tabella di routing |
| `show protocols` | Cisco IOS | Stato protocolli e interfacce |
| `show version` | Cisco IOS | Versione IOS, hardware, memoria, licenze |
| `show cdp neighbors` | Cisco IOS | Dispositivi Cisco vicini (CDP) |
| `show cdp neighbors detail` | Cisco IOS | Dettagli estesi sui vicini CDP |
| `show users` | Cisco IOS | Sessioni attive sul dispositivo |
| `show flash:` | Cisco IOS | Contenuto e spazio della memoria Flash |

---

*© Cisco Systems, Inc. — Materiale didattico per uso interno al corso. Adattato per GitHub da materiale originale Cisco NetAcad.*
