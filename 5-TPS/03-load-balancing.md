

## Prerequisiti per la lezione 📚

Gli studenti devono conoscere e memorizzare i concetti base legati a **tassi di arrivo, tempo di servizio e utilizzo del server**.

| Simbolo                    | Definizione                             | Note                                                                                     |
| -------------------------- | --------------------------------------- | ---------------------------------------------------------------------------------------- |
| $\lambda$                  | Tasso di arrivo delle richieste         | Numero di richieste per unità di tempo (req/s)                                           |
| $T_{\text{serv}}$          | Tempo medio di servizio di un server    | Tempo necessario al server per completare una richiesta                                  |
| $\lambda_i$                | Tasso di arrivo sul singolo server      | $\lambda_i = \lambda / k$ se il carico è distribuito uniformemente                       |
| $\lambda_{\text{max,1}}$   | Throughput massimo di un singolo server | $\lambda_{\text{max,1}} = 1 / T_{\text{serv}}$                                           |
| $\lambda_{\text{max,tot}}$ | Throughput massimo totale del sistema   | $\lambda_{\text{max,tot}} = k \cdot \lambda_{\text{max,1}}$                              |
| $\rho$                     | Livello di utilizzazione del server     | $\rho = \lambda_i / \lambda_{\text{max,1}} = \lambda / (k \cdot \lambda_{\text{max,1}})$ |

📌 Questi concetti saranno fondamentali per calcolare throughput, stabilità e latenza durante la lezione e gli esercizi.

# Load Balancing ⚖️🌐

*(Introduzione teorica e primi esercizi)*
*(Introduzione teorica e primi esercizi)*

Nel capitolo precedente abbiamo visto che un **server centralizzato** può diventare:

* lento quando si avvicina alla saturazione
* instabile quando il carico supera il limite

Una soluzione reale e molto usata è il **Load Balancing**.

---

## Cos’è il Load Balancing 🔁

Il **Load Balancing** consiste nel:

* distribuire le richieste
* su **più server**
* in modo da evitare la saturazione di uno solo

📌 Dal punto di vista matematico, significa **dividere il carico totale**.

---

## Architettura di riferimento 🖥️🖥️🖥️

Consideriamo:

* un **bilanciatore di carico**
* $k$ server identici
* ogni server gestisce una richiesta alla volta

Le richieste arrivano con tasso totale $\lambda$.

---

## Metafora: più casse al supermercato 🛒🧾

* Client → clienti del supermercato
* Server → casse
* Load balancer → addetto che manda i clienti alla cassa libera

Con:

* **1 cassa** → coda lunga
* **più casse** → attesa più breve

👉 Non cambiano i clienti, cambia **come vengono distribuiti**.

---

## Distribuzione del carico ⚖️

Se il carico è distribuito **uniformemente** su $k$ server:

$\lambda_i = \frac{\lambda}{k}$

dove:

* $\lambda_i$ è il tasso di arrivo sul singolo server

---

## Throughput massimo con Load Balancing 🚀

Ogni server ha:

* tempo medio di servizio $T_{\text{serv}}$

Quindi:

$\lambda_{\text{max,1}} = \frac{1}{T_{\text{serv}}}$

Con $k$ server:

$\lambda_{\text{max,tot}} = k \cdot \lambda_{\text{max,1}}$

📌 Il throughput massimo **cresce linearmente** con il numero di server.

---

## Utilizzazione dei server 🔄

Il livello di utilizzazione di **ogni server** è:

$\rho = \frac{\lambda_i}{\lambda_{\text{max,1}}}$

Sostituendo:

$\rho = \frac{\lambda}{k \cdot \lambda_{\text{max,1}}}$

👉 Aumentare $k$ **riduce l’utilizzazione**
👉 Ridurre $\rho$ **riduce la latenza**

---

## Stabilità con Load Balancing ✅

Il sistema è stabile se **ogni server** è stabile:

$\lambda_i < \lambda_{\text{max,1}}$

cioè:

$\lambda < k \cdot \lambda_{\text{max,1}}$

📌 Con più server:

* aumenta il carico massimo sostenibile
* il punto di saturazione si sposta più in alto

---

## Effetto sulla latenza 📉

Senza Load Balancing:

* un solo server
* $(\lambda \to \lambda_{\text{max}})$
* latenza che diverge

Con Load Balancing:

* carico diviso
* $(\rho)$ più basso
* latenza **molto più contenuta**

👉 Non si elimina la latenza,
👉 si **ritarda il collasso del sistema**

---

## Riepilogo concettuale 🧩

| Aspetto           | Senza LB  | Con LB        |
| ----------------- | --------- | ------------- |
| Numero server     | 1         | $k$           |
| Carico per server | $\lambda$ | $\lambda / k$ |
| Saturazione       | Rapida    | Ritardata     |
| Scalabilità       | Assente   | Presente      |

---
## Esercizi numerici 🧮

Di seguito la traccia degli esercizi suddivisa in **dati e domande** e in una sezione separata di **risoluzione passo passo**.

---

## Traccia degli esercizi

### Esercizio 1 – Throughput totale

**Dati:**

* $T_{\text{serv}} = 50 \text{ ms}$ per server
* Numero di server: $k = 2$ e $k = 4$

**Domande:**

1. Calcolare $\lambda_{\text{max,1}}$ per un singolo server.
2. Calcolare il throughput massimo totale per $k = 2$ server.
3. Calcolare il throughput massimo totale per $k = 4$ server.

---

### Esercizio 2 – Utilizzazione dei server

**Dati:**

* $k = 3$ server
* $T_{\text{serv}} = 40 \text{ ms}$
* $\lambda = 45 \text{ req/s}$

**Domande:**

1. Calcolare $\lambda_i$ per ciascun server.
2. Calcolare l’utilizzazione $\rho$ di ogni server.
3. Determinare se il sistema è stabile.

---

### Esercizio 3 – Confronto diretto

**Dati:**

* $\lambda = 30 \text{ req/s}$
* $T_{\text{serv}} = 40 \text{ ms}$
* Confronto tra 1 server e 3 server con Load Balancing

**Domande:**

1. Determinare quale sistema è stabile.
2. Indicare qualitativamente quale sistema ha latenza minore.

---

## Risoluzione passo passo 🛠️

### Esercizio 1 – Throughput totale

**Passo 1: Calcolare $\lambda_{\text{max,1}}$**

$$\lambda_{\text{max,1}} = \frac{1}{T_{\text{serv}}} = \frac{1}{0.05} = 20 \text{ req/s}$$

*Metafora*: il server è come una cassa di supermercato che serve clienti: 50 ms a cliente = 20 clienti/s.

**Passo 2: Throughput totale con $k$ server**

* $k=2$: $X_{\text{max}} = 2*20 = 40$ req/s
* $k=4$: $X_{\text{max}} = 4*20 = 80$ req/s
  
  *Metafora*: più casse aperte, più clienti serviti contemporaneamente.

### Esercizio 2 – Utilizzazione dei server

**Passo 1: Calcolare $\lambda_i$**

$$\lambda_i = \frac{\lambda}{k} = 45/3 = 15 \text{ req/s}$$

*Metafora*: distribuire 45 mele in 3 cestini → 15 mele ciascuno.

**Passo 2: Calcolare $\rho$**

$$\rho = \lambda_i * T_{\text{serv}} = 15*0.04 = 0.6$$

*Metafora*: ogni server è occupato il 60% del tempo.

**Passo 3: Verifica stabilità**

* $\rho<1$ → sistema stabile.
  
  *Metafora*: il server non è mai sovraccarico, quindi la coda non cresce all’infinito.

### Esercizio 3 – Confronto diretto

**1 server:**

* $\lambda_{\text{max,1}} = 1/0.04 = 25$ req/s
* $\lambda = 30$ req/s > 25 → **instabile**

**3 server con Load Balancing:**

* $\lambda_i = 30/3 = 10$ req/s
* $\rho = 10*0.04 = 0.4 < 1$ → **stabile**
* Latenza qualitativa minore perché il carico è distribuito
  
  *Metafora*: più casse aperte → attesa minore in fila e sistema stabile.

---

## Messaggio chiave 🎯

* Il Load Balancing **non rende i server più veloci**
* Riduce il carico su ciascun server
* Migliora stabilità e tempi di risposta
* È alla base di tutti i servizi web moderni 🌍
