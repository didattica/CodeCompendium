# Sezione Teoria 📚

## Sistema Centralizzato 🖥️

**Definizione (Sistema Centralizzato)**  
Un sistema centralizzato è composto da un solo nodo che esegue tutte le operazioni.

Formalmente, il sistema è definito come:

$$
S_c = (N, E, C) \quad \text{dove} \quad |N| = 1
$$

dove:
- $N$ = insieme dei nodi
- $E$ = insieme degli archi di comunicazione (vuoto in questo caso)
- $C$ = configurazione del sistema

**Proprietà ✨**
- Tutte le funzioni $F = \{f_1, f_2, \dots, f_m\}$ sono eseguite dall'unico nodo
- Non esistono comunicazioni tra nodi interni
- Il sistema comunica solo con entità esterne (client, dispositivi, utenti) tramite I/O

---

## Definizioni fondamentali 📖

### ⏱️ Latenza (Latency)

Tempo totale tra l'invio di una richiesta e la ricezione della risposta.

Per un sistema con **queueing FIFO**, la latenza totale per il client $i$-esimo $C_i$ è data dalla formula:

$$
TC_i = \sum_{j=1}^{i-1} (t_{\text{request},j} + t_{\text{processing},j} + t_{\text{response},j}) + t_{\text{request},i} + t_{\text{processing},i} + t_{\text{response},i}
$$

dove:
- $t_{\text{request},i}$ = tempo di trasmissione della richiesta del client $C_i$
- $t_{\text{processing},i}$ = tempo di elaborazione sul server per $C_i$
- $t_{\text{response},i}$ = tempo di trasmissione della risposta dal server al client $C_i$
- La sommatoria $\sum_{j=1}^{i-1}(\cdot)$ rappresenta la **queue latency** dovuta alle richieste precedenti

**Componenti della latenza:**

1. **Queue Latency** (Latenza di coda): tempo di attesa dovuto alle richieste precedenti

   $$
   \text{Queue Latency}_i = \sum_{j=1}^{i-1} (t_{\text{request},j} + t_{\text{processing},j} + t_{\text{response},j})
   $$

2. **Service Time** (Tempo di servizio): tempo per processare la richiesta corrente

   $$
   \text{Service Time}_i = t_{\text{request},i} + t_{\text{processing},i} + t_{\text{response},i}
   $$

Quindi:

$$
TC_i = \text{Queue Latency}_i + \text{Service Time}_i
$$

---

### 📥 Queue Latency (Latenza di coda)

Tempo di attesa causato dalle richieste precedenti in coda, quando il server gestisce le richieste una alla volta con politica FIFO.

**Esempio concreto:**
- C1 arriva per prima e richiede $30 \text{ ms}$ totali
- C2 arriva subito dopo ma deve attendere che C1 finisca
- **Queue Latency di C2** = $30 \text{ ms}$

---

### 🔄 Politiche di gestione della coda

**➡️ FIFO (First In, First Out)**  
Le richieste sono servite nell'ordine di arrivo.

**Esempio:** Arrivo C1, C2, C3 → Elaborazione C1, C2, C3

**⬅️ LIFO (Last In, First Out)**  
L'ultima richiesta arrivata è la prima servita (comportamento a pila/stack).

**Esempio:** Arrivo C1, C2, C3 → Elaborazione C3, C2, C1

---

## Metriche di prestazione 📊

### 🚀 Throughput

Numero di richieste completate per unità di tempo:

$$
\lambda = \frac{\text{richieste completate}}{\text{tempo}}
$$

**Esempio concreto:**
- Richieste completate: $100$
- Tempo osservato: $10 \text{ secondi}$
- **Throughput:** $\lambda = \frac{100}{10} = 10 \text{ req/s}$

---

### 📨 Tasso di arrivo

Numero di richieste in arrivo per unità di tempo. Indica il carico generato dai client sul sistema.

**Esempio concreto:**
- Arrivano $150$ richieste in $10 \text{ secondi}$
- **Tasso di arrivo:** $\lambda = \frac{150}{10} = 15 \text{ req/s}$

---

# Sezione Problemi 🧩

## Problema 1 – Latenza media ⏱️

Un server centralizzato riceve richieste contemporaneamente da tre client al tempo $t = 0$.

**Dati:**

| Client | $t_{\text{request}}$ (ms) | $t_{\text{processing}}$ (ms) | $t_{\text{response}}$ (ms) |
|--------|---------------------------|------------------------------|----------------------------|
| C1     | 5                         | 30                           | 5                          |
| C2     | 3                         | 20                           | 3                          |
| C3     | 4                         | 40                           | 4                          |

**Politica:** FIFO (First In, First Out)

**Condizioni:**
- Tutte le richieste arrivano al tempo $t = 0$
- Il server gestisce una richiesta alla volta

**Richiesta 🎯**  
Calcolare la latenza media del sistema usando la formula FIFO.

---

### Soluzione 💡

Applichiamo la formula della latenza con queueing FIFO:

$$
TC_i = \sum_{j=1}^{i-1} (t_{\text{request},j} + t_{\text{processing},j} + t_{\text{response},j}) + t_{\text{request},i} + t_{\text{processing},i} + t_{\text{response},i}
$$

---

#### Client C1 (primo in coda, $i=1$)

$$
TC_1 = \sum_{j=1}^{0} (\cdot) + t_{\text{request},1} + t_{\text{processing},1} + t_{\text{response},1}
$$

La sommatoria è vuota (nessuna richiesta precedente):

$$
TC_1 = 0 + 5 + 30 + 5 = 40 \text{ ms}
$$

---

#### Client C2 (secondo in coda, $i=2$)

$$
TC_2 = \sum_{j=1}^{1} (t_{\text{request},j} + t_{\text{processing},j} + t_{\text{response},j}) + t_{\text{request},2} + t_{\text{processing},2} + t_{\text{response},2}
$$

$$
TC_2 = (t_{\text{request},1} + t_{\text{processing},1} + t_{\text{response},1}) + t_{\text{request},2} + t_{\text{processing},2} + t_{\text{response},2}
$$

$$
TC_2 = (5 + 30 + 5) + 3 + 20 + 3
$$

$$
TC_2 = 40 + 26 = 66 \text{ ms}
$$

---

#### Client C3 (terzo in coda, $i=3$)

$$
TC_3 = \sum_{j=1}^{2} (t_{\text{request},j} + t_{\text{processing},j} + t_{\text{response},j}) + t_{\text{request},3} + t_{\text{processing},3} + t_{\text{response},3}
$$

$$
TC_3 = (t_{\text{request},1} + t_{\text{processing},1} + t_{\text{response},1}) + (t_{\text{request},2} + t_{\text{processing},2} + t_{\text{response},2}) + t_{\text{request},3} + t_{\text{processing},3} + t_{\text{response},3}
$$

$$
TC_3 = (5 + 30 + 5) + (3 + 20 + 3) + 4 + 40 + 4
$$

$$
TC_3 = 40 + 26 + 48 = 114 \text{ ms}
$$

---

#### Latenza Media

$$
\text{Latenza media} = \frac{TC_1 + TC_2 + TC_3}{3}
$$

$$
\text{Latenza media} = \frac{40 + 66 + 114}{3} = \frac{220}{3} = 73.33 \text{ ms}
$$

---

### Tabella Riepilogativa 📋

| Client | Queue Latency (ms) | Service Time (ms) | **Latenza Totale $TC_i$ (ms)** |
|--------|-------------------|-------------------|---------------------------------|
| C1     | 0                 | 40                | **40**                          |
| C2     | 40                | 26                | **66**                          |
| C3     | 66                | 48                | **114**                         |

**Dettaglio Service Time:**
- C1: $5 + 30 + 5 = 40 \text{ ms}$
- C2: $3 + 20 + 3 = 26 \text{ ms}$
- C3: $4 + 40 + 4 = 48 \text{ ms}$

**Risposta finale:** ✅ La latenza media del sistema è **73.33 ms**

---

## Problema 2 – Throughput 🚀

Un server centralizzato riceve richieste da più client con le seguenti caratteristiche:

**Dati:**
- Tempo medio di servizio: $T_{\text{serv}} = 40 \text{ ms} = 0.04 \text{ s}$
- Il server gestisce una sola richiesta alla volta ☝️
- Il sistema è stabile ✅

---

### Domanda 1️⃣ – Throughput massimo teorico

**Formula:**

$$
\lambda_{\text{max}} = \frac{1}{T_{\text{serv}}}
$$

**Calcolo:**

$$
\lambda_{\text{max}} = \frac{1}{0.04 \text{ s}} = 25 \text{ req/s}
$$

**Risposta:** ✅ Il throughput massimo teorico è **25 richieste/secondo**

---

### Domanda 2️⃣ – Throughput effettivo

**Dati aggiuntivi:**
- Tasso di arrivo: $\lambda = 15 \text{ req/s}$

**Analisi:**

Poiché $\lambda = 15 \text{ req/s} < \lambda_{\text{max}} = 25 \text{ req/s}$, il server riesce a gestire tutte le richieste in arrivo.

**Throughput effettivo:**

$$
\text{Throughput effettivo} = \min(\lambda, \lambda_{\text{max}}) = \min(15, 25) = 15 \text{ req/s}
$$

**Risposta:** ✅ Il throughput effettivo è **15 richieste/secondo**

---

### Domanda 3️⃣ – Livello di utilizzazione del server

**Formula:**

$$
\rho = \frac{\lambda}{\lambda_{\text{max}}}
$$

**Calcolo:**

$$
\rho = \frac{15}{25} = 0.6 = 60\%
$$

**Interpretazione:**
- Il server è utilizzato al 60% della sua capacità massima
- C'è ancora un 40% di capacità disponibile
- Il sistema è **sottoutilizzato** e può gestire più carico

**Risposta:** ✅ Il livello di utilizzazione del server è **60%** (o **0.6**)

---

## Riepilogo Problema 2 📋

| Metrica | Valore |
|---------|--------|
| Tempo di servizio | 40 ms |
| Throughput massimo | 25 req/s |
| Tasso di arrivo | 15 req/s |
| Throughput effettivo | 15 req/s |
| Utilizzazione server | 60% |
