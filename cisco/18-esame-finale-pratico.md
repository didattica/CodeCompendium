# 🖧 Esercitazione Packet Tracer – Routing Statico e Accesso Remoto Telnet

**Livello:** Base
**Strumento:** Cisco Packet Tracer
**Tempo stimato:** ~1 ora

---

# 📋 Obiettivi

Al termine dell’esercitazione sarai in grado di:

* Costruire una semplice rete con router, switch e PC
* Configurare indirizzi IPv4
* Configurare routing statico
* Verificare la connettività con `ping`
* Accedere da remoto via Telnet
* Configurare SSH (opzionale)

---

# 🗺️ Topologia

```text
 PC-A ---- S1 ---- R1 ===== R2 ---- S2 ---- PC-B
```

---

# 📐 Schema di Indirizzamento

| Dispositivo | Interfaccia | IP Address   | Subnet Mask     |
| ----------- | ----------- | ------------ | --------------- |
| R1          | G0/0        | 192.168.1.1  | 255.255.255.0   |
| R1          | S0/0/0      | 10.0.0.1     | 255.255.255.252 |
| R2          | G0/0        | 192.168.2.1  | 255.255.255.0   |
| R2          | S0/0/0      | 10.0.0.2     | 255.255.255.252 |
| PC-A        | NIC         | 192.168.1.10 | 255.255.255.0   |
| PC-B        | NIC         | 192.168.2.10 | 255.255.255.0   |

Gateway PC-A → `192.168.1.1`
Gateway PC-B → `192.168.2.1`

---

# 🔧 PARTE 1 – Configurazione Fisica

## Dispositivi richiesti

| Dispositivo | Quantità |
| ----------- | -------- |
| Router 2911 | 2        |
| Switch 2960 | 2        |
| PC          | 2        |

---

## Collegamenti

| Da   | A  | Tipo di cavo            |
| ---- | -- | ----------------------- |
| PC-A | S1 | Copper Straight-Through |
| S1   | R1 | Copper Straight-Through |
| PC-B | S2 | Copper Straight-Through |
| S2   | R2 | Copper Straight-Through |
| R1   | R2 | Serial DCE              |

> [!WARNING]
> Il cavo seriale deve essere collegato partendo da **R1** usando **Serial DCE**.
> Solo il lato DCE configura il comando `clock rate`.

---

# ⚙️ PARTE 2 – Configurazione Logica

## Configurazione Router R1

Apri la CLI di R1.

```ios
Router> enable
Router# configure terminal

Router(config)# hostname R1

R1(config)# interface g0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface s0/0/0
R1(config-if)# ip address 10.0.0.1 255.255.255.252
R1(config-if)# clock rate 64000
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

> [!IMPORTANT]
> Il comando `no shutdown` è obbligatorio.
> Senza di esso l’interfaccia rimane disattivata (`administratively down`).

> [!IMPORTANT]
>
> ## Come funziona una Route Statica
>
> Il comando:
>
> ```ios id="wvl8s5"
> ip route 192.168.1.0 255.255.255.0 10.0.0.1
> ```
>
> significa:
>
> > “Per raggiungere la rete `192.168.1.0/24`, invia i pacchetti al router `10.0.0.1`.”
>
> Una route statica ha sempre questa struttura:
>
> ```ios id="7m4v5s"
> ip route [rete-destinazione] [subnet-mask] [next-hop]
> ```
>
> Dove:
>
> * `rete-destinazione` → rete che vogliamo raggiungere
> * `subnet-mask` → maschera della rete
> * `next-hop` → IP del router vicino a cui inoltrare i pacchetti
>
> Senza una route statica, il router non saprebbe dove inviare i pacchetti destinati a reti remote.


---

## Configurazione Router R2

```ios
Router> enable
Router# configure terminal

Router(config)# hostname R2

R2(config)# interface g0/0
R2(config-if)# ip address 192.168.2.1 255.255.255.0
R2(config-if)# no shutdown
R2(config-if)# exit

R2(config)# interface s0/0/0
R2(config-if)# ip address 10.0.0.2 255.255.255.252
R2(config-if)# no shutdown
R2(config-if)# exit

R2(config)# ip route 192.168.1.0 255.255.255.0 10.0.0.1
```

---

## Configurazione PC-A

Desktop → IP Configuration

```text
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
```

---

## Configurazione PC-B

```text
IP Address: 192.168.2.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.2.1
```

---

# 🧪 PARTE 3 – Test dei Ping

## Ping da PC-A verso R1

Desktop → Command Prompt

```text
C:\> ping 192.168.1.1
```

---

## Ping da PC-A verso R2

```text
C:\> ping 10.0.0.2
```

---

## Ping da PC-A verso PC-B

```text
C:\> ping 192.168.2.10
```

Output atteso:

```text
Reply from 192.168.2.10: bytes=32 time<1ms TTL=126
```

> [!TIP]
> Se il ping non funziona:
>
> * controlla gli IP
> * verifica i gateway
> * verifica le route statiche
> * usa `show ip interface brief`

---

# 🌐 PARTE 4 – Accesso Remoto via Telnet

## Configurazione Telnet su R1

```ios
R1# configure terminal

R1(config)# line vty 0 4
R1(config-line)# password cisco
R1(config-line)# login
R1(config-line)# transport input telnet
R1(config-line)# exit
```

---

## Configurazione Telnet su R2

```ios
R2# configure terminal

R2(config)# line vty 0 4
R2(config-line)# password cisco
R2(config-line)# login
R2(config-line)# transport input telnet
R2(config-line)# exit
```

> [!IMPORTANT]
> Senza il comando `login`, Telnet non richiederà la password e l’accesso verrà negato.

---

## Test Telnet verso R1

Da PC-A:

```text
C:\> telnet 192.168.1.1
```

Password:

```text
cisco
```

---

## Test Telnet verso R2

```text
C:\> telnet 10.0.0.2
```

Password:

```text
cisco
```

---

# 🔐 PARTE 5 – Opzionale: Accesso SSH

## Configurazione SSH su R1

```ios
R1# configure terminal

R1(config)# ip domain-name lab.local
R1(config)# username admin secret admin123

R1(config)# crypto key generate rsa
How many bits in the modulus [512]: 1024

R1(config)# ip ssh version 2

R1(config)# line vty 0 4
R1(config-line)# login local
R1(config-line)# transport input ssh
R1(config-line)# exit
```

> [!NOTE]
> SSH richiede:
>
> * domain-name
> * username locale
> * chiavi RSA

---

## Test SSH

Da PC-A:

```text
C:\> ssh -l admin 192.168.1.1
```

Password:

```text
admin123
```

---

# ✅ Checklist Finale

* [ ] Topologia completata
* [ ] IP configurati correttamente
* [ ] Interfacce attive
* [ ] Routing statico funzionante
* [ ] Ping riusciti
* [ ] Telnet funzionante
* [ ] SSH funzionante (opzionale)

---

# 📖 Comandi Utili

| Comando                              | Funzione             |
| ------------------------------------ | -------------------- |
| `show ip interface brief`            | Stato interfacce     |
| `show ip route`                      | Tabella routing      |
| `ping`                               | Test connettività    |
| `copy running-config startup-config` | Salva configurazione |
