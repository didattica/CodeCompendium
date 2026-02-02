## Concetti di base 📌

### ⏱️ Tempo medio di servizio

Indichiamo con:

$$
T_{\text{serv}}
$$

il **tempo medio** necessario al server per completare **una richiesta**  
(invio richiesta + elaborazione + invio risposta).

---

### 🚀 Throughput massimo teorico

Se il server impiega in media $T_{\text{serv}}$ secondi per ogni richiesta,  
il **numero massimo di richieste** che può completare in un secondo è:

$$
\lambda_{\text{max}} = \frac{1}{T_{\text{serv}}}
$$

📌 Questo valore rappresenta **il limite fisico del sistema**:  
il server **non può andare oltre**.

---

### 📨 Tasso di arrivo

Indichiamo con:

$$
\lambda
$$

il **numero di richieste che arrivano al server per secondo**.

---

## Utilizzazione del server 🔄

Definiamo il **livello di utilizzazione** del server come:

$$
\rho = \frac{\lambda}{\lambda_{\text{max}}}
$$

📊 Interpretazione:

| Valore di $\rho$ | Significato |
|------------------|-------------|
| $\rho < 1$ | Il server ha tempo libero |
| $\rho = 1$ | Il server è saturo |
| $\rho > 1$ | Le richieste arrivano troppo velocemente |

---

## Metafora: il casello autostradale 🚗🚗🚗

Immagina:
- **un solo casello** → il server
- **auto in arrivo** → le richieste
- **tempo per ogni auto** → $T_{\text{serv}}$

### Caso 1️⃣ – Poche auto  
Il casello smaltisce tutto → **nessuna coda**

### Caso 2️⃣ – Troppe auto  
Le auto arrivano più velocemente → **la coda cresce**

👉 Il casello funziona, ma **gli automobilisti restano bloccati**

---

## Condizione di stabilità ✅

Un sistema è **stabile** se:

$$
\lambda < \lambda_{\text{max}}
$$

equivalentemente:

$$
\rho < 1
$$

📌 Significato:
- il server riesce a gestire il carico
- la coda resta limitata
- i tempi di risposta sono accettabili

---

## Punto di saturazione ⚠️

Il **punto di saturazione** si ha quando:

$$
\lambda = \lambda_{\text{max}}
$$

ovvero:

$$
\rho = 1
$$

In questa situazione:
- il server lavora sempre al 100%
- non ha margine di recupero
- **basta una richiesta in più per creare coda**

---

## Instabilità del sistema ❌

Se:

$$
\lambda > \lambda_{\text{max}}
$$

allora:

$$
\rho > 1
$$

📌 Conseguenze:
- la coda cresce senza limite
- il tempo di attesa aumenta continuamente
- il sistema diventa **instabile**

Anche se il server è acceso 🔌,  
gli utenti lo percepiscono come **non funzionante**.

---

## Latenza e divergenza 📈♾️

Indichiamo con:

$$
L(\lambda)
$$

la **latenza media del sistema** in funzione del carico.

Quando il tasso di arrivo si avvicina al massimo:

$$
\lim_{\lambda \to \lambda_{\text{max}}^-} L(\lambda) = +\infty
$$

### Interpretazione intuitiva 🧠

- Il server non è ancora fermo
- Ma l’attesa cresce sempre di più
- Il sistema diventa inutilizzabile **prima** di bloccarsi

👉 La **latenza** è il primo segnale di collasso 🚨

---

## Riepilogo 🧩

| Stato del sistema | Condizione |
|------------------|------------|
| Stabile | $\lambda < \lambda_{\text{max}}$ |
| Saturo | $\lambda = \lambda_{\text{max}}$ |
| Instabile | $\lambda > \lambda_{\text{max}}$ |

---

## Esercizi numerici 🧮

### Esercizio 1 – Stabilità del sistema

Un server ha:
- $T_{\text{serv}} = 40 \text{ ms}$

1. Calcolare $\lambda_{\text{max}}$
2. Stabilire se il sistema è stabile per:
   - $\lambda = 10 \text{ req/s}$
   - $\lambda = 20 \text{ req/s}$
   - $\lambda = 30 \text{ req/s}$

---

### Esercizio 2 – Saturazione

Dato un server con:
- $\lambda_{\text{max}} = 25 \text{ req/s}$

Calcolare $\rho$ e indicare lo stato del sistema per:
- $\lambda = 15$
- $\lambda = 25$
- $\lambda = 28$

---

### Esercizio 3 – Interpretazione del limite

Sapendo che:

$$
\lim_{\lambda \to \lambda_{\text{max}}^-} L(\lambda) = +\infty
$$

spiegare **a parole** cosa succede al sistema  
quando il carico si avvicina al valore massimo.

---

## Idee chiave 🎯

- Un sistema può essere **attivo ma inutilizzabile**
- La stabilità è una **condizione matematica**
- La latenza cresce **prima** del blocco totale
- Non basta aumentare la potenza: serve equilibrio ⚖️

## Collegamento con i server web reali 🌐🖥️

Il modello matematico studiato finora non è astratto:  
è una **semplificazione diretta del comportamento dei server web reali**.

Quando accediamo a:
- un sito web
- una piattaforma cloud
- un servizio di streaming
- un’API REST

stiamo inviando **richieste HTTP** a un server che:
- le riceve
- le mette in coda
- le elabora
- restituisce una risposta

---

## Corrispondenza modello ↔ realtà 🔁

| Modello teorico | Server web reale |
|-----------------|------------------|
| Richiesta | HTTP request |
| Server centralizzato | Web server (Apache, Nginx, Node.js, ecc.) |
| Coda FIFO | Request queue |
| $T_{\text{serv}}$ | Tempo di elaborazione della richiesta |
| $\lambda$ | Numero di richieste al secondo |
| Latenza | Tempo di risposta percepito dall’utente |

---

## Perché i siti “vanno lenti” 🐌

Quando molti utenti accedono contemporaneamente:
- $\lambda$ aumenta
- $\rho$ si avvicina a 1
- la coda cresce
- la latenza aumenta

Anche se il server:
- è acceso
- non ha errori
- continua a rispondere

👉 l’utente percepisce il servizio come **lento o inutilizzabile**

Questo accade **prima** del blocco totale del sistema.

---

## Esempio concreto 🧠

Un server web può gestire al massimo:

$$
\lambda_{\text{max}} = 100 \text{ req/s}
$$

Durante un picco di traffico:
- arrivano 95–98 richieste al secondo
- il server non è ancora saturo
- ma i tempi di risposta crescono molto

📌 Il problema non è il crash,  
ma la **latenza che diverge**.

---

## Messaggio chiave 💡

- I server web **non collassano all’improvviso**
- Prima diventano lenti
- La matematica spiega **perché succede**
- La stabilità è più importante della potenza pura ⚖️

---

👉 Nei sistemi reali, per evitare la saturazione, si introducono:
- più server
- bilanciamento del carico
- code limitate
- meccanismi di controllo

(che vedremo solo se deciderai di approfondire 😉)

