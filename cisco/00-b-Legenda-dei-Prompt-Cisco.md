
# 🖥️ Legenda dei Prompt Cisco IOS
> I prompt del terminale Cisco non sono casuali — ogni simbolo indica **dove sei** nel sistema e **cosa puoi fare**.

---

> [!IMPORTANT]
> ### 🔑 Concetto chiave
> Cisco IOS è organizzato in **livelli di accesso gerarchici**. Più scendi nella gerarchia, più hai potere — e più devi essere autorizzato. Il prompt cambia ad ogni livello per ricordarti sempre in quale "stanza" ti trovi.

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
   └── router ospf 1     →  Router(config-router)# 🗺️
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
