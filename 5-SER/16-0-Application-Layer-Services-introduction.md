# 🌐 Introduction to Application Layer Services

## 📌 Obiettivo del modulo
Questo modulo introduce il **livello applicativo** delle reti, ovvero il livello in cui gli utenti interagiscono direttamente con i servizi di rete (web, email, file transfer, ecc.).

L’obiettivo è comprendere:
- come funzionano le applicazioni di rete
- il ruolo dei protocolli applicativi
- la relazione tra client e server
- i principali servizi utilizzati su Internet

---

## 🧠 Cos'è il livello applicativo?

Il **livello applicativo** è il livello più alto nei modelli di rete (TCP/IP e OSI).

È responsabile di:
- fornire servizi direttamente alle applicazioni
- permettere la comunicazione tra software su dispositivi diversi

### 📊 Modelli di riferimento

| Modello OSI        | Modello TCP/IP       |
|--------------------|---------------------|
| Application        | Application         |
| Presentation       |                     |
| Session            |                     |
| Transport          | Transport           |
| Network            | Internet            |
| Data Link          | Network Access      |
| Physical           |                     |

👉 Nel modello TCP/IP, i livelli Application, Presentation e Session sono unificati.

---

## 🔗 Ruolo del livello applicativo

Il livello applicativo:
- definisce **come le applicazioni comunicano**
- stabilisce **regole (protocolli)**
- gestisce **formato e scambio dei dati**

### 📦 Esempi di servizi

| Servizio        | Descrizione                         | Protocollo |
|----------------|----------------------------------|------------|
| Web            | Navigazione internet              | HTTP/HTTPS |
| Email          | Invio e ricezione messaggi        | SMTP, POP, IMAP |
| File Transfer  | Trasferimento file                | FTP        |
| Naming         | Traduzione nomi → IP              | DNS        |
| Remote Access  | Accesso remoto                    | SSH/Telnet |

---

## 🖥️ Architettura Client-Server

Le applicazioni di rete si basano principalmente su questo modello:

### 🔄 Schema

```

[ Client ]  ---> richiesta --->  [ Server ]
[ Client ]  <--- risposta ----  [ Server ]

```

### 📊 Differenze principali

| Client                          | Server                          |
|---------------------------------|---------------------------------|
| Richiede servizi                | Fornisce servizi                |
| Inizia la comunicazione         | Risponde alle richieste         |
| Esempio: browser                | Esempio: web server             |

---

## 🌍 Comunicazione nelle applicazioni

Per comunicare, le applicazioni utilizzano:
- **Protocolli** (regole)
- **Indirizzi IP** (identificazione dispositivi)
- **Porte** (identificazione servizi)

### 📊 Esempio

| Elemento        | Esempio              |
|----------------|----------------------|
| IP Address     | 192.168.1.1          |
| Porta          | 80 (HTTP)            |
| Protocollo     | HTTP                 |

---

## ⚙️ Concetti chiave

### 🔹 Protocollo
Insieme di regole che definiscono:
- formato dei dati
- modalità di trasmissione
- gestione degli errori

### 🔹 Servizio
Funzionalità offerta dalla rete (es. accesso web)

### 🔹 Applicazione
Software che utilizza i servizi (es. browser, client email)

---

## 🧩 Schema riassuntivo

```

Utente
↓
Applicazione (browser, email client)
↓
Livello Applicativo (HTTP, SMTP, DNS)
↓
Livello Trasporto (TCP/UDP)
↓
Rete

```

---

## 🎯 Perché è importante?

Il livello applicativo è fondamentale perché:
- è quello **più vicino all’utente**
- permette l’utilizzo reale della rete
- è alla base dello sviluppo web e backend

---

## ✅ Conclusione

In questo modulo studieremo:
- come funzionano i servizi di rete
- i principali protocolli applicativi
- il modello client-server
- le applicazioni più utilizzate su Internet

👉 Questo rappresenta il punto di incontro tra:
- **reti (Sistemi)**
- **sviluppo software (TPSIT)**





<!--
Se vuoi, nel prossimo step posso prepararti anche **16.1 Client-Server** mantenendo lo stesso stile (molto chiaro + pronto per spiegazione in classe).

Module 16: Application Layer Services
16.0. Introduction
16.1. The Client Server Relationship
16.2. Network Application Services
16.3. Domain Name System
16.4. Web Clients and Servers
16.5. FTP Clients and Servers
16.6. Virtual Terminals
16.7. Email and Messaging
16.8. Application Layer Services Summary
Module 17: Network Testing Utilities
17.0. Introduction
17.1. Troubleshooting Commands
17.2. Network Testing Utilities Summary
-->
