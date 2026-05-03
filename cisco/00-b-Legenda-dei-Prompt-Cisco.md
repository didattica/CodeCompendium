
# 🖥️ Legenda dei Prompt Cisco IOS
> I prompt del terminale Cisco non sono casuali — ogni simbolo indica **dove sei** nel sistema e **cosa puoi fare**.

---

> [!IMPORTANT]
> ### 🔑 Concetto chiave
> Cisco IOS è organizzato in **livelli di accesso gerarchici**. Più scendi nella gerarchia, più hai potere — e più devi essere autorizzato. Il prompt cambia ad ogni livello per ricordarti sempre in quale "stanza" ti trovi.

---

## 📋 Comandi Base e Sicurezza (Tabella Riassuntiva)
Questa tabella illustra i comandi fondamentali per configurare e proteggere il dispositivo, suddivisi per il livello in cui devono essere impartiti.

| Livello Prompt | Comando | Esempio Pratico | Cosa fa / A cosa serve |
|:---|:---|:---|:---|
| **User** `>` | `enable` | `Router> enable` | **Attiva i privilegi:** Ti porta nel modo Privileged EXEC (richiede psw se impostata). |
| **Privileged** `#` | `show ip int bri` | `Router# sh ip int bri` | **Verifica rapida:** Mostra lo stato di tutte le interfacce e i relativi IP. |
| **Privileged** `#` | `copy run start` | `Router# copy run start` | **Salvataggio:** Copia la config corrente nella memoria permanente (NVRAM). |
| **Global** `(config)#` | `hostname` | `Router(config)# hostname R1` | **Identità:** Cambia il nome del dispositivo nel prompt (es. da Router a R1). |
| **Global** `(config)#` | `enable secret` | `Router(config)# enable secret cisco123` | **Password di Sistema:** Imposta una password cifrata per passare da `>` a `#`. |
| **Global** `(config)#` | `service password-encryption` | `Router(config)# service password-encryption` | **Cifratura:** Cifra tutte le password visualizzabili (es. quelle delle linee) nel file di testo. |
| **Global** `(config)#` | `banner motd` | `Router(config)# banner motd #Accesso vietato#` | **Avviso Legale:** Mostra un messaggio a chiunque tenti di connettersi. |
| **Interface** `(config-if)#` | `ip address` | `Router(config-if)# ip add 192.168.1.1 255.255.255.0` | **Indirizzamento:** Assegna un indirizzo IP e una maschera alla porta. |
| **Interface** `(config-if)#` | `no shutdown` | `Router(config-if)# no shutdown` | **Accensione:** Attiva fisicamente l'interfaccia (di default sono "spente"). |
| **Line** `(config-line)#` | `password` | `Router(config-line)# password cisco` | **Password di Accesso:** Imposta la password per la specifica linea (Console o VTY). |
| **Line** `(config-line)#` | `login` | `Router(config-line)# login` | **Attivazione Controllo:** Dice al router di chiedere effettivamente la password all'utente. |

---

## Gerarchia dei Prompt

| Prompt | Emoji | Nome del Modo | Cosa puoi fare | Esempi di comandi | Come si entra |
|---|---|---|---|---|---|
| `Router>` | 👁️ | **User EXEC** | Solo visualizzazione di base — comandi limitati, nessuna modifica | `ping 8.8.8.8` `show version` `traceroute 192.168.1.1` | Accesso iniziale al dispositivo |
| `Router#` | ⚡ | **Privileged EXEC** | Visualizzazione completa, diagnostica, salvataggio config, riavvio | `show running-config` `copy running-config startup-config` `reload` `debug ip route` | `enable` (da `>`) |
| `Router(config)#` | 🔧 | **Global Configuration** | Modifica della configurazione globale del dispositivo | `hostname R1` `enable secret cisco` `ip domain-name lab.it` `service password-encryption` | `configure terminal` (da `#`) |
| `Router(config-if)#` | 🔌 | **Interface Configuration** | Configurazione di una singola interfaccia (es. `Fa0/0`, `vlan 1`) | `ip address 192.168.1.1 255.255.255.0` `no shutdown` `description LAN-principale` | `interface <nome>` (da `config`) |
| `Router(config-line)#` | 📡 | **Line Configuration** | Configurazione delle linee di accesso (console, VTY, AUX) | `password cisco` `login local` `transport input ssh` `exec-timeout 5 30` | `line <tipo> <numero>` (da `config`) |
| `Router(config-router)#` | 🗺️ | **Router Configuration** | Configurazione dei protocolli di routing (RIP, OSPF, EIGRP) | `network 192.168.1.0` `passive-interface fa0/1` `default-information originate` | `router <protocollo>` (da `config`) |

---

## Come si scende (e come si risale)

```
Router>          👁️  User EXEC
   │
   │  enable
   ▼
Router#          ⚡  Privileged EXEC
   │
   │  configure terminal
   ▼
Router(config)#  🔧  Global Configuration
   │
   ├── interface fa0/0   →  Router(config-if)#    🔌
   ├── line vty 0 4      →  Router(config-line)#  📡
   └── router ospf 1      →  Router(config-router)# 🗺️
```

> [!NOTE]
> ### ⬆️ Come si risale
>
> | Comando | Effetto |
> |---|---|
> | `exit` | Torna al livello precedente (un gradino su) |
> | `end` oppure `Ctrl+Z` | Torna direttamente a `Router#` da qualsiasi livello |
> | `disable` | Torna da `Router#` a `Router>` |

---

> [!TIP]
> ### 🧠 Metafora — I livelli di accesso di un edificio
>
> | Livello IOS | Analogia |
> |---|---|
> | `Router>` 👁️ | **Ingresso** — puoi guardare la lobby, non entrare negli uffici |
> | `Router#` ⚡ | **Reception con badge** — puoi accedere alle aree comuni, vedere tutto |
> | `Router(config)#` 🔧 | **Sala server** — puoi modificare le impostazioni dell'edificio |
> | `Router(config-if)#` 🔌 | **Quadro elettrico** — stai lavorando su un impianto specifico |
> | `Router(config-line)#` 📡 | **Centralino** — stai configurando le linee telefoniche di accesso |

---

> [!WARNING]
> ### ⚠️ Errori comuni
>
> * Digitare `configure terminal` da `Router>` → **errore**: devi prima fare `enable`
> * Dimenticare `exit` tra un sotto-modo e l'altro → i comandi del modo sbagliato danno errore
> * Usare `end` quando vuoi uscire di un solo livello → torni subito a `#`, saltando tutti i livelli intermedi

---

## Differenza tra `enable password` e `enable secret`

> [!NOTE]
> ### 🔐 Accesso a `Router#` — quale comando usare?
>
> | Comando | Sicurezza | Archiviazione |
> |---|---|---|
> | `enable password` | ❌ Bassa — salvata in chiaro | Leggibile nel `running-config` |
> | `enable secret` | ✅ Alta — cifrata con MD5 | Illeggibile nel `running-config` |
>
> Usa **sempre** `enable secret`. Se sono presenti entrambi, `enable secret` ha la precedenza.

---
*Documento creato come supporto didattico per le lezioni Cisco CCNA 2026.*
