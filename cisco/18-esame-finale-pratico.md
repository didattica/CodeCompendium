# 🖧 Esercitazione Packet Tracer – CCNA Introduction to Networks
**Livello:** Base-Intermedio | **Tempo stimato:** ~2 ore | **Strumento:** Cisco Packet Tracer 8.x

---

## 📋 Obiettivi dell'esercitazione

Al termine di questa esercitazione sarai in grado di:

- Costruire una topologia di rete con router, switch e PC
- Configurare indirizzamento IPv4 su tutti i dispositivi
- Abilitare il routing statico tra due reti diverse
- Configurare accesso remoto sicuro via SSH
- Verificare la connettività end-to-end con `ping` e `show`

---

## 🗺️ Topologia di Rete

```
  PC-A              PC-B
  |                  |
[S1]              [S2]
  |                  |
[R1]---[seriale]---[R2]
  |                  |
  LAN-A             LAN-B
192.168.1.0/24    192.168.2.0/24
```

### Dispositivi richiesti in Packet Tracer

| Dispositivo | Modello consigliato | Quantità |
|-------------|---------------------|----------|
| Router      | Cisco 2911          | 2        |
| Switch      | Cisco 2960          | 2        |
| PC          | Generic PC-PT       | 2        |
| Cavi        | Copper Straight-Through + Serial DCE | vari |

---

## 📐 Schema di Indirizzamento

| Dispositivo   | Interfaccia      | Indirizzo IP      | Subnet Mask       | Gateway           |
|---------------|------------------|-------------------|-------------------|-------------------|
| R1            | GigabitEthernet0/0 | 192.168.1.1     | 255.255.255.0     | —                 |
| R1            | Serial0/0/0      | 10.0.0.1          | 255.255.255.252   | —                 |
| R2            | GigabitEthernet0/0 | 192.168.2.1     | 255.255.255.0     | —                 |
| R2            | Serial0/0/0      | 10.0.0.2          | 255.255.255.252   | —                 |
| S1            | VLAN 1           | 192.168.1.2       | 255.255.255.0     | 192.168.1.1       |
| S2            | VLAN 1           | 192.168.2.2       | 255.255.255.0     | 192.168.2.1       |
| PC-A          | NIC              | 192.168.1.10      | 255.255.255.0     | 192.168.1.1       |
| PC-B          | NIC              | 192.168.2.10      | 255.255.255.0     | 192.168.2.1       |

> [!NOTE]
> La rete **10.0.0.0/30** è usata per il collegamento seriale (WAN) tra i due router.
> Una /30 fornisce esattamente **2 indirizzi host** — perfetta per un link punto-punto.

---

## 🔧 PARTE 1 – Costruzione della Topologia (⏱ ~20 min)

### Passo 1.1 – Aggiungere i dispositivi

1. Apri Packet Tracer e crea un nuovo progetto vuoto.
2. Dalla barra **Network Devices**, trascina nell'area di lavoro:
   - 2× Router 2911
   - 2× Switch 2960
   - 2× PC
3. Rinomina i dispositivi cliccando sull'etichetta: `R1`, `R2`, `S1`, `S2`, `PC-A`, `PC-B`.

### Passo 1.2 – Collegare i dispositivi

Usa lo strumento **Connections** (icona fulmine) per i seguenti cavi:

| Da          | Porta            | A           | Porta              | Tipo cavo                  |
|-------------|------------------|-------------|--------------------|----------------------------|
| PC-A        | FastEthernet0    | S1          | FastEthernet0/1    | Copper Straight-Through    |
| S1          | GigabitEthernet0/1 | R1        | GigabitEthernet0/0 | Copper Straight-Through    |
| PC-B        | FastEthernet0    | S2          | FastEthernet0/1    | Copper Straight-Through    |
| S2          | GigabitEthernet0/1 | R2        | GigabitEthernet0/0 | Copper Straight-Through    |
| R1          | Serial0/0/0      | R2          | Serial0/0/0        | Serial DCE (lato R1)       |

> [!WARNING]
> Per il cavo seriale, scegli **Serial DCE** e collegalo **partendo da R1**.
> Il lato DCE deve configurare il **clock rate** — se lo invertisci il link non si alza.

---

## ⚙️ PARTE 2 – Configurazione dei Router (⏱ ~40 min)

### Passo 2.1 – Configurazione base di R1

Clicca su R1 → tab **CLI** → premi Invio per accedere alla console.

```ios
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# enable secret cisco123
R1(config)# no ip domain-lookup
R1(config)# banner motd # Accesso autorizzato soltanto! #
R1(config)# line console 0
R1(config-line)# password consolepwd
R1(config-line)# login
R1(config-line)# exit
R1(config)# line vty 0 4
R1(config-line)# transport input ssh
R1(config-line)# login local
R1(config-line)# exit
R1(config)# service password-encryption
```

> [!TIP]
> Il comando `no ip domain-lookup` evita che il router tenti di risolvere DNS ogni volta che digiti un comando errato — ti risparmia lunghe attese in sala esame.

### Passo 2.2 – Configurazione interfacce di R1

```ios
R1(config)# interface GigabitEthernet0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# description LAN-A
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface Serial0/0/0
R1(config-if)# ip address 10.0.0.1 255.255.255.252
R1(config-if)# description WAN link to R2
R1(config-if)# clock rate 64000
R1(config-if)# no shutdown
R1(config-if)# exit
```

> [!WARNING]
> Il comando `clock rate` va inserito **solo sul lato DCE** del cavo seriale (R1 in questo caso).
> Se non lo configuri, la Serial rimarrà in stato `down/down`.

### Passo 2.3 – Configurazione SSH su R1

```ios
R1(config)# ip domain-name ccna.lab
R1(config)# username admin privilege 15 secret adminpwd
R1(config)# crypto key generate rsa
  How many bits in the modulus [512]: 1024
R1(config)# ip ssh version 2
```

> [!NOTE]
> SSH richiede **obbligatoriamente** tre cose per funzionare:
> 1. Un `ip domain-name` configurato
> 2. Una coppia di chiavi RSA generata con `crypto key generate rsa`
> 3. Un utente locale creato con `username`
>
> Senza uno di questi tre elementi, SSH non sarà abilitato.

### Passo 2.4 – Configurazione base di R2

```ios
Router> enable
Router# configure terminal
Router(config)# hostname R2
R2(config)# enable secret cisco123
R2(config)# no ip domain-lookup
R2(config)# banner motd # Accesso autorizzato soltanto! #
R2(config)# line console 0
R2(config-line)# password consolepwd
R2(config-line)# login
R2(config-line)# exit
R2(config)# line vty 0 4
R2(config-line)# transport input ssh
R2(config-line)# login local
R2(config-line)# exit
R2(config)# service password-encryption
```

### Passo 2.5 – Configurazione interfacce di R2

```ios
R2(config)# interface GigabitEthernet0/0
R2(config-if)# ip address 192.168.2.1 255.255.255.0
R2(config-if)# description LAN-B
R2(config-if)# no shutdown
R2(config-if)# exit

R2(config)# interface Serial0/0/0
R2(config-if)# ip address 10.0.0.2 255.255.255.252
R2(config-if)# description WAN link to R1
R2(config-if)# no shutdown
R2(config-if)# exit
```

### Passo 2.6 – Configurazione SSH su R2

```ios
R2(config)# ip domain-name ccna.lab
R2(config)# username admin privilege 15 secret adminpwd
R2(config)# crypto key generate rsa
  How many bits in the modulus [512]: 1024
R2(config)# ip ssh version 2
```

---

## ⚙️ PARTE 3 – Configurazione degli Switch (⏱ ~20 min)

### Passo 3.1 – Configurazione S1

```ios
Switch> enable
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# enable secret cisco123
S1(config)# no ip domain-lookup
S1(config)# interface vlan 1
S1(config-if)# ip address 192.168.1.2 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# exit
S1(config)# ip default-gateway 192.168.1.1
S1(config)# line console 0
S1(config-line)# password consolepwd
S1(config-line)# login
S1(config-line)# exit
S1(config)# service password-encryption
S1(config)# end
S1# copy running-config startup-config
```

> [!IMPORTANT]
> Lo switch di livello 2 **non ha routing**, quindi ha bisogno del comando `ip default-gateway` per poter essere raggiunto (ad esempio via SSH) da reti diverse dalla sua.
> Senza di esso, i pacchetti di risposta non sapranno dove andare.

### Passo 3.2 – Configurazione S2

```ios
Switch> enable
Switch# configure terminal
Switch(config)# hostname S2
S2(config)# enable secret cisco123
S2(config)# no ip domain-lookup
S2(config)# interface vlan 1
S2(config-if)# ip address 192.168.2.2 255.255.255.0
S2(config-if)# no shutdown
S2(config-if)# exit
S2(config)# ip default-gateway 192.168.2.1
S2(config)# line console 0
S2(config-line)# password consolepwd
S2(config-line)# login
S2(config-line)# exit
S2(config)# service password-encryption
S2(config)# end
S2# copy running-config startup-config
```

---

## ⚙️ PARTE 4 – Configurazione dei PC (⏱ ~10 min)

### Passo 4.1 – Configurazione PC-A

1. Clicca su **PC-A** → tab **Desktop** → **IP Configuration**
2. Imposta:
   - IP Address: `192.168.1.10`
   - Subnet Mask: `255.255.255.0`
   - Default Gateway: `192.168.1.1`

### Passo 4.2 – Configurazione PC-B

1. Clicca su **PC-B** → tab **Desktop** → **IP Configuration**
2. Imposta:
   - IP Address: `192.168.2.10`
   - Subnet Mask: `255.255.255.0`
   - Default Gateway: `192.168.2.1`

> [!TIP]
> In Packet Tracer puoi anche usare **DHCP** automatico se hai configurato un server DHCP, ma in questa esercitazione usiamo indirizzi **statici** per avere il pieno controllo — come richiesto tipicamente all'esame.

---

## 🌐 PARTE 5 – Configurazione del Routing Statico (⏱ ~15 min)

Senza routing, i due router non sanno come raggiungere le reti remote. Dobbiamo configurare **route statiche**.

### Passo 5.1 – Route statica su R1

R1 deve sapere come raggiungere la rete `192.168.2.0/24` (LAN-B), tramite R2:

```ios
R1# configure terminal
R1(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2
R1(config)# end
R1# copy running-config startup-config
```

### Passo 5.2 – Route statica su R2

R2 deve sapere come raggiungere la rete `192.168.1.0/24` (LAN-A), tramite R1:

```ios
R2# configure terminal
R2(config)# ip route 192.168.1.0 255.255.255.0 10.0.0.1
R2(config)# end
R2# copy running-config startup-config
```

> [!IMPORTANT]
> La sintassi del routing statico è:
> ```
> ip route [rete-destinazione] [subnet-mask] [next-hop o interfaccia-uscita]
> ```
> Il **next-hop** è l'indirizzo IP dell'interfaccia del router vicino, non della rete di destinazione.
> Confonderli è uno degli errori più frequenti all'esame pratico.

---

## ✅ PARTE 6 – Verifica della Configurazione (⏱ ~15 min)

### Passo 6.1 – Verifica interfacce su R1

```ios
R1# show ip interface brief
```

Output atteso:

```
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0    192.168.1.1     YES manual up                    up
Serial0/0/0           10.0.0.1        YES manual up                    up
```

> [!WARNING]
> Se una interfaccia mostra `administratively down`, significa che non hai eseguito `no shutdown`.
> Se mostra `down/down`, controlla il cavo fisico o il clock rate sul seriale.

### Passo 6.2 – Verifica routing su R1

```ios
R1# show ip route
```

Dovresti vedere:

```
C    10.0.0.0/30 is directly connected, Serial0/0/0
C    192.168.1.0/24 is directly connected, GigabitEthernet0/0
S    192.168.2.0/24 [1/0] via 10.0.0.2
```

La `S` indica una rotta **statica** (Static). La `C` indica reti **direttamente connesse** (Connected).

### Passo 6.3 – Test ping da PC-A a PC-B

1. Clicca su **PC-A** → **Desktop** → **Command Prompt**
2. Esegui:

```
C:\> ping 192.168.2.10
```

Output atteso:

```
Pinging 192.168.2.10 with 32 bytes of data:
Reply from 192.168.2.10: bytes=32 time=1ms TTL=126
Reply from 192.168.2.10: bytes=32 time=1ms TTL=126
Reply from 192.168.2.10: bytes=32 time=1ms TTL=126
Reply from 192.168.2.10: bytes=32 time=1ms TTL=126

Ping statistics for 192.168.2.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

> [!TIP]
> Il valore **TTL=126** (non 128) è normale: ogni router decrementa il TTL di 1.
> Partendo da 128 (default Windows), passando per 2 router → 128 - 2 = 126. ✓

### Passo 6.4 – Verifica SSH da PC-A verso R1

1. Su **PC-A** → **Desktop** → **Command Prompt**

```
C:\> ssh -l admin 192.168.1.1
```

2. Inserisci la password: `adminpwd`
3. Dovresti accedere alla CLI di R1 con il banner configurato.

### Passo 6.5 – Verifica completa con traceroute

Da PC-A, esegui:

```
C:\> tracert 192.168.2.10
```

Output atteso:

```
Tracing route to 192.168.2.10 over a maximum of 30 hops:
  1    1 ms    192.168.1.1    (R1 - GigabitEthernet0/0)
  2    1 ms    10.0.0.2       (R2 - Serial0/0/0)
  3    2 ms    192.168.2.10   (PC-B)
Trace complete.
```

---

## 🧪 PARTE 7 – Sfida Aggiuntiva (Opzionale) (⏱ ~10 min)

Se hai completato tutto in anticipo, prova queste configurazioni extra:

### 7.1 – Configura un messaggio MOTD diverso su R2

```ios
R2(config)# banner motd $
========================================
  ATTENZIONE: Sistema privato aziendale
  Accesso non autorizzato e' vietato!
========================================
$
```

### 7.2 – Verifica la cifratura delle password

```ios
R1# show running-config | include password
```

Dovresti vedere solo password cifrate (es. `7 08026F6028`) e non in chiaro — grazie a `service password-encryption`.

### 7.3 – Salva e verifica la startup-config

```ios
R1# show startup-config
```

Confronta con `show running-config`. Devono essere identiche dopo `copy run start`.

---

## 📊 Checklist Finale

Usa questa lista per verificare di aver completato tutto:

- [ ] Topologia costruita correttamente in Packet Tracer
- [ ] R1 configurato con hostname, password, interfacce e SSH
- [ ] R2 configurato con hostname, password, interfacce e SSH
- [ ] S1 configurato con IP VLAN1 e default-gateway
- [ ] S2 configurato con IP VLAN1 e default-gateway
- [ ] PC-A e PC-B configurati con IP statico e gateway
- [ ] Route statica su R1 verso 192.168.2.0/24
- [ ] Route statica su R2 verso 192.168.1.0/24
- [ ] `ping` da PC-A a PC-B: 0% loss ✓
- [ ] `show ip route` mostra la route `S` su entrambi i router ✓
- [ ] SSH funzionante da PC-A verso R1 ✓
- [ ] Configurazione salvata con `copy run start` su tutti i dispositivi ✓

---

## 📖 Riepilogo Comandi Chiave

| Comando | Descrizione |
|---------|-------------|
| `enable` | Entra in modalità privilegiata |
| `configure terminal` | Entra in modalità di configurazione globale |
| `hostname <nome>` | Imposta il nome del dispositivo |
| `enable secret <pwd>` | Imposta password enable cifrata |
| `no shutdown` | Attiva un'interfaccia |
| `ip address <ip> <mask>` | Assegna indirizzo IP a un'interfaccia |
| `ip route <rete> <mask> <next-hop>` | Configura una rotta statica |
| `ip default-gateway <ip>` | Imposta il gateway di default (switch L2) |
| `show ip interface brief` | Verifica stato e IP delle interfacce |
| `show ip route` | Mostra la tabella di routing |
| `show running-config` | Mostra la configurazione attiva |
| `copy running-config startup-config` | Salva la configurazione |
| `crypto key generate rsa` | Genera chiavi per SSH |

---

## 🔗 Risorse Utili

- [Cisco NetAcad – CCNA ITN](https://www.netacad.com/courses/ccna-introduction-networks)
- [Cisco IOS Command Reference](https://www.cisco.com/c/en/us/support/ios-nx-os-software/ios-15-4m-t/products-command-reference-list.html)
- [Packet Tracer Download](https://www.netacad.com/cisco-packet-tracer)

---

*Esercitazione basata sul curriculum CCNA: Introduction to Networks v7.02 — NetAcad Cisco*
