# Load Balancing ⚖️🌐  
*(Introduzione teorica e primi esercizi)*

Nel capitolo precedente abbiamo visto che un **server centralizzato** diventa:
- lento quando si avvicina alla saturazione
- instabile quando il carico supera il limite

Una soluzione reale e molto usata è il **Load Balancing**.

---

## Cos’è il Load Balancing 🔁

Il **Load Balancing** consiste nel:
- distribuire le richieste
- su **più server**
- in modo da evitare la saturazione di uno solo

📌 Dal punto di vista matematico, significa **dividere il carico totale**.

---

## Architettura di riferimento 🖥️🖥️🖥️

Consideriamo:
- un **bilanciatore di carico**
- \( k \) server identici
- ogni server gestisce una richiesta alla volta

Le richieste arrivano con tasso totale:

$$
\lambda
$$

---

## Metafora: più casse al supermercato 🛒🧾

- Client → clienti del supermercato
- Server → casse
- Load balancer → addetto che manda i clienti alla cassa libera

Con:
- **1 cassa** → coda lunga
- **più casse** → attesa più breve

👉 Non cambiano i clienti,  
cambia **come vengono distribuiti**.

---

## Distribuzione del carico ⚖️

Se il carico è distribuito **uniformemente** su \( k \) server:

$$
\lambda_i = \frac{\lambda}{k}
$$

dove:
- \( \lambda_i \) è il tasso di arrivo sul singolo server

---

## Throughput massimo con Load Balancing 🚀

Ogni server ha:
- tempo medio di servizio \( T_{\text{serv}} \)

Quindi:

$$
\lambda_{\text{max,1}} = \frac{1}{T_{\text{serv}}}
$$

Con \( k \) server:

$$
\lambda_{\text{max,tot}} = k \cdot \lambda_{\text{max,1}}
$$

📌 Il throughput massimo **cresce linearmente** con il numero di server.

---

## Utilizzazione dei server 🔄

Il livello di utilizzazione di **ogni server** è:

$$
\rho = \frac{\lambda_i}{\lambda_{\text{max,1}}}
$$

Sostituendo:

$$
\rho = \frac{\lambda}{k \cdot \lambda_{\text{max,1}}}
$$

👉 Aumentare \( k \) **riduce l’utilizzazione**  
👉 Ridurre \( \rho \) **riduce la latenza**

---

## Stabilità con Load Balancing ✅

Il sistema è stabile se **ogni server** è stabile:

$$
\lambda_i < \lambda_{\text{max,1}}
$$

cioè:

$$
\lambda < k \cdot \lambda_{\text{max,1}}
$$

📌 Con più server:
- aumenta il carico massimo sostenibile
- il punto di saturazione si sposta più in alto

---

## Effetto sulla latenza 📉

Senza Load Balancing:
- un solo server
- \( \lambda \to \lambda_{\text{max}} \)
- latenza che diverge

Con Load Balancing:
- carico diviso
- \( \rho \) più basso
- latenza **molto più contenuta**

👉 Non si elimina la latenza,  
👉 si **ritarda il collasso del sistema**.

---

## Riepilogo concettuale 🧩

| Aspetto | Senza LB | Con LB |
|-------|----------|--------|
| Numero server | 1 | \( k \) |
| Carico per server | \( \lambda \) | \( \lambda / k \) |
| Saturazione | Rapida | Ritardata |
| Scalabilità | Assente | Presente |

---

## Esercizi numerici 🧮

### Esercizio 1 – Throughput totale

Ogni server ha:
- \( T_{\text{serv}} = 50 \text{ ms} \)

1. Calcolare \( \lambda_{\text{max,1}} \)
2. Calcolare il throughput massimo totale con:
   - \( k = 2 \) server
   - \( k = 4 \) server

---

### Esercizio 2 – Utilizzazione dei server

Un sistema ha:
- \( k = 3 \) server
- \( T_{\text{serv}} = 40 \text{ ms} \)
- \( \lambda = 45 \text{ req/s} \)

1. Calcolare \( \lambda_i \)
2. Calcolare \( \rho \) di ogni server
3. Stabilire se il sistema è stabile

---

### Esercizio 3 – Confronto diretto

Un sistema riceve:
- \( \lambda = 30 \text{ req/s} \)

Confrontare:
- **1 server**
- **3 server con Load Balancing**

Sapendo che:

$$
T_{\text{serv}} = 40 \text{ ms}
$$

Indicare:
- quale sistema è stabile
- quale ha latenza minore (qualitativamente)

---

## Messaggio chiave 🎯

- Il Load Balancing **non rende i server più veloci**
- Riduce il carico su ciascun server
- Migliora stabilità e tempi di risposta
- È alla base di tutti i servizi web moderni 🌍
