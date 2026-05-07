# 17.8.4 Che cosa ho appreso in questo modulo?
*Cisco CCNA: Introduzione alle reti - 2026*

## 🌐 Dispositivi in una piccola rete
Le reti di piccole dimensioni hanno in genere una singola connessione WAN fornita da DSL, cavo o connessione Ethernet. Le piccole reti sono gestite da un tecnico IT locale o da un professionista appaltato.
- **Fattori di selezione:** costi, velocità, tipi di porte/interfacce, espandibilità e servizi del sistema operativo.
- **Indirizzamento:** Implementare uno schema IP coerente su tutti i dispositivi.
- **Ridondanza:** Ottenuta tramite duplicazione di hardware o link critici.
- **QoS (Quality of Service):** Fondamentale per dare priorità al traffico in tempo reale (voce/video).

## 📂 Applicazioni e protocolli
Esistono due forme di processi software:
1. **Applicazioni di rete:** Implementano direttamente protocolli del layer applicativo (es. browser, client email).
2. **Servizi del layer applicativo:** Assistono programmi per risorse come file transfer o spooling di stampa.

**Accesso remoto:** SSH è l'alternativa sicura a Telnet.
**Protocolli comuni:** HTTP, SMTP, FTP, DHCP, DNS.

## 📈 Scalabilità
Per scalare una rete servono:
- Documentazione e inventario.
- Budget definito.
- Analisi del traffico (acquisizione snapshot durante i picchi).
- Strumenti host: Task Manager, Visualizzatore eventi, Utilizzo dati.

## 🛠 Verifica della connettività
- **Ping:** Verifica Layer 3 e latenza. Esiste la modalità *estesa* su IOS.
- **Traceroute:** Elenca gli hop del percorso (`tracert` su Windows).
- **Baseline:** Archivio dei risultati (ping/trace) per confronti futuri sulle prestazioni.

## 💻 Comandi principali
| Sistema | Comandi Comuni |
| :--- | :--- |
| **Windows** | `ipconfig`, `ipconfig /all`, `arp -a` |
| **Linux** | `ifconfig`, `ip address` |
| **Cisco IOS** | `show running-config`, `show ip interface brief`, `show cdp neighbors detail` |

## 🔍 Risoluzione dei problemi (Troubleshooting)
1. **Identificazione** del problema.
2. **Teoria** sulla causa.
3. **Verifica** della teoria.
4. **Piano d'azione** e soluzione.
5. **Verifica finale** e prevenzione.
6. **Documentazione.**

### Problemi comuni:
- **Duplex Mismatch:** Prestazioni scadenti per incongruenza full/half duplex.
- **Errori IP/Gateway:** Problemi manuali o DHCP; impediscono la comunicazione remota.
- **DNS:** Se il server DNS è irraggiungibile, la navigazione tramite URL fallisce.

---
*Documento generato per CCNA Study Guide.*
