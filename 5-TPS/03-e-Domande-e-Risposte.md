
## Sistemi Centralizzati, Code, Prestazioni e Load Balancing  
*(Versione rigorosa e priva di ambiguità)*

---

# 🟢 SEZIONE 1 – DOMANDE FACILI (Definizioni precise)

---

### 1) Definizione formale di sistema centralizzato

**Domanda:**  
Fornire una definizione formale di sistema centralizzato utilizzando la notazione $S = (N,E,C)$.

**Risposta:**  

Un sistema è centralizzato se:

$$
S = (N,E,C) \quad \text{con} \quad |N| = 1
$$

dove esiste un unico nodo che esegue tutte le funzioni del sistema e non esistono comunicazioni interne tra nodi distinti.

---

### 2) Cosa significa formalmente $|N| = 1$?

**Risposta:**  
Significa che l’insieme dei nodi contiene un solo elemento: tutte le operazioni del sistema sono eseguite dallo stesso nodo fisico.

---

### 3) Definizione rigorosa di latenza

**Risposta:**  
La latenza totale è il tempo che intercorre tra l’invio di una richiesta da parte del client e la ricezione completa della risposta.

---

### 4) Componenti della latenza

**Risposta:**  
La latenza totale è composta da:

- tempo di trasmissione della richiesta  
- tempo di elaborazione  
- tempo di trasmissione della risposta  
- eventuale tempo di attesa in coda

---

### 5) Definizione di Queue Latency

**Risposta:**  
Tempo di attesa causato dalle richieste precedenti quando il server elabora le richieste sequenzialmente.

---

### 6) Definizione di Service Time

**Risposta:**  

$$
T_{serv} = t_{request} + t_{processing} + t_{response}
$$

È il tempo necessario a completare una singola richiesta, esclusa l’attesa in coda.

---

### 7) Definizione di Throughput

**Risposta:**  

$$
\lambda = \frac{\text{richieste completate}}{\text{tempo}}
$$

Numero di richieste completate per unità di tempo.

---

### 8) Definizione di tasso di arrivo

**Risposta:**  
Numero di richieste che arrivano al sistema per unità di tempo.

---

# 🟡 SEZIONE 2 – DOMANDE MEDIE (Stabilità e Prestazioni)

---

### 9) Formula completa della latenza in FIFO

**Risposta:**

$$
TC_i = \sum_{j=1}^{i-1} (t_{request,j}+t_{processing,j}+t_{response,j}) + t_{request,i}+t_{processing,i}+t_{response,i}
$$

---

### 10) Definizione di throughput massimo teorico

**Risposta:**

Se il tempo medio di servizio è $T_{serv}$:

$$
\lambda_{max} = \frac{1}{T_{serv}}
$$

---

### 11) Definizione di utilizzazione del server

**Risposta:**

Nel modello con capacità massima $\mu$:

$$
\rho = \frac{\lambda}{\mu}
$$

dove $\mu = \lambda_{max}$.

---

### 12) Condizione formale di stabilità

**Risposta:**

Il sistema è stabile se:

$$
\rho < 1
$$

equivalentemente:

$$
\lambda < \mu
$$

---

### 13) Cosa accade se $\rho = 1$?

**Risposta:**  
Il sistema è in saturazione: il server lavora al 100% e qualsiasi incremento del carico genera crescita della coda.

---

### 14) Cosa accade se $\rho > 1$?

**Risposta:**  
Il sistema è instabile: il tasso di arrivo supera la capacità di servizio e la coda cresce senza limite.

---

### 15) Perché la latenza aumenta prima del collasso?

**Risposta:**  
Perché all’aumentare di $\rho$ la coda cresce progressivamente; anche senza superare la capacità massima, l’attesa diventa elevata.

---

# 🔴 SEZIONE 3 – DOMANDE DIFFICILI (Limiti e Analisi Matematica)

---

### 16) Interpretare formalmente:

$$
\lim_{\lambda \to \mu^-} L(\lambda) = +\infty
$$

**Risposta:**  
Quando il tasso di arrivo si avvicina alla capacità massima da valori inferiori, la latenza media cresce senza limite.

---

### 17) Spiegare il significato di asintoto verticale in questo contesto

**Risposta:**  
La retta $\lambda = \mu$ rappresenta un asintoto verticale della funzione latenza: la funzione cresce indefinitamente avvicinandosi alla saturazione.

---

### 18) Differenza tra sistema centralizzato e distribuito (definizione rigorosa)

**Risposta:**  

- Sistema centralizzato: $|N|=1$  
- Sistema distribuito: $|N|>1$ con comunicazione tra nodi distinti  

La distinzione è fisica, non solo logica.

---

### 19) Un sistema con server su macchina A e database su macchina B è centralizzato?

**Risposta:**  
No. È distribuito, perché esistono almeno due nodi fisici che cooperano tramite rete.

---

### 20) Un sistema con client remoto e server unico è centralizzato?

**Risposta:**  
Dal lato server è centralizzato ($|N|=1$).  
Dal punto di vista complessivo client–server è distribuito.

---

# ⚫ SEZIONE 4 – DOMANDE SUPER DIFFICILI (Load Balancing e Scalabilità)

---

### 21) Effetto del Load Balancing su k server identici

**Risposta:**

Con $k$ server di capacità $\mu$ ciascuno:

$$
\rho_k = \frac{\lambda}{k\mu}
$$

---

### 22) Comportamento al limite aumentando i server

**Risposta:**

$$
\lim_{k \to \infty} \rho_k = 0
$$

L’utilizzazione per server tende a zero, assumendo distribuzione uniforme del carico.

---

### 23) Il load balancing elimina la divergenza della latenza?

**Risposta:**  
No. Sposta il punto di saturazione aumentando la capacità totale, ma ogni singolo server mantiene la stessa condizione di stabilità $\rho < 1$.

---

### 24) Perché la stabilità è una proprietà matematica?

**Risposta:**  
Perché dipende dal rapporto tra due tassi ($\lambda$ e $\mu$) e determina formalmente se la coda converge o diverge.

---

### 25) Perché un sistema può essere attivo ma inutilizzabile?

**Risposta:**  
Perché anche con $\rho < 1$, se $\rho$ è molto vicino a 1, la latenza può diventare estremamente elevata pur senza instabilità formale.

---

# 🎯 Copertura completa degli argomenti

Questo documento copre in modo non ambiguo:

- Definizione formale di sistema centralizzato  
- Distinzione fisica tra centralizzato e distribuito  
- Latenza e sue componenti  
- Politiche FIFO  
- Throughput e tasso di arrivo  
- Utilizzazione  
- Stabilità, saturazione, instabilità  
- Limiti matematici  
- Divergenza della latenza  
- Load balancing e scalabilità  

---
