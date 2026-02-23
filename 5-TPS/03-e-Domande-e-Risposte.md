# 🟢 DOMANDE FACILI (0-6)

### 1) Definizione di sistema centralizzato
**Risposta (max 30 parole):**  
Sistema composto da un unico nodo che esegue tutte le operazioni e gestisce tutte le richieste senza comunicazione interna tra nodi.

---

### 2) Cosa rappresenta $|N| = 1$ in un sistema centralizzato?
**Risposta:**  
Indica che l’insieme dei nodi contiene un solo elemento: esiste un unico nodo che svolge tutte le funzioni del sistema.

---

### 3) Definizione di latenza (max 30 parole)
**Risposta:**  
Tempo totale che intercorre tra l’invio di una richiesta da parte del client e la ricezione della risposta dal server.

---

### 4) Cos’è la Queue Latency?
**Risposta:**  
È il tempo di attesa in coda dovuto alle richieste precedenti quando il server gestisce le richieste una alla volta.

---

### 5) Cos’è il Service Time?
**Risposta:**  
È il tempo necessario per trasmettere la richiesta, elaborarla sul server e inviare la risposta al client.

---

### 6) Definizione di Throughput (max 30 parole)
**Risposta:**  
Numero di richieste completate dal sistema per unità di tempo.

---

### 7) Cos’è il tasso di arrivo $\lambda$?
**Risposta:**  
Numero di richieste che arrivano al server per unità di tempo.

---

### 8) Differenza tra FIFO e LIFO
**Risposta:**  
FIFO serve le richieste in ordine di arrivo; LIFO serve prima l’ultima richiesta arrivata.

---

# 🟡 DOMANDE MEDIE (7)

### 9) Scrivere la formula della latenza totale $TC_i$ in un sistema FIFO
**Risposta:**

$$
TC_i = \sum_{j=1}^{i-1}(t_{request,j}+t_{processing,j}+t_{response,j}) + t_{request,i}+t_{processing,i}+t_{response,i}
$$

---

### 10) Cosa succede se $\lambda < \lambda_{\text{max}}$?
**Risposta:**  
Il sistema è stabile, il server riesce a smaltire le richieste e la coda rimane limitata.

---

### 11) Cosa succede quando $\lambda = \lambda_{\text{max}}$?
**Risposta:**  
Il server è saturo (ρ = 1). Lavora al 100% e basta una richiesta in più per generare coda crescente.

---

### 12) Cosa accade se $\lambda > \lambda_{\text{max}}$?
**Risposta:**  
Il sistema diventa instabile: la coda cresce senza limite e la latenza aumenta continuamente.

---

### 13) Definire l’utilizzazione del server
**Risposta:**

$$
\rho = \frac{\lambda}{\lambda_{\text{max}}}
$$

Indica la percentuale di capacità utilizzata.

---

### 14) Interpretazione di $\rho = 0.6$
**Risposta:**  
Il server è utilizzato al 60% della sua capacità massima e dispone ancora del 40% di margine.

---

### 15) Perché un sito web può essere lento anche se non è in crash?
**Risposta:**  
Perché il carico si avvicina alla saturazione, la coda cresce e la latenza aumenta prima del collasso totale.

---

# 🔴 DOMANDE DIFFICILI (8)

### 16) Dimostrare perché $\lambda_{\text{max}} = \frac{1}{T_{serv}}$
**Risposta:**  
Se una richiesta richiede $T_{serv}$ secondi, in un secondo il server può completare al massimo $\frac{1}{T_{serv}}$ richieste.

---

### 17) Spiegare il significato di:

$$
\lim_{\lambda \to \lambda_{\text{max}}^-} L(\lambda) = +\infty
$$

**Risposta:**  
Quando il tasso di arrivo si avvicina al massimo teorico da sinistra, la latenza cresce senza limite pur senza blocco immediato del sistema.

---

### 18) Perché la latenza diverge prima del crash?
**Risposta:**  
Perché la coda accumula richieste sempre più rapidamente; anche un piccolo eccesso di carico genera attese crescenti.

---

### 19) Definire $\rho = \frac{\lambda}{\mu}$ nel modello con $\mu$ tasso di servizio
**Risposta:**  
ρ rappresenta il carico normalizzato: rapporto tra richieste in arrivo e capacità massima di servizio del server.

---

### 20) Spiegare il concetto di asintoto verticale nel grafico della latenza
**Risposta:**  
Quando $\rho \to 1$, la latenza cresce senza bound: la retta $\rho = 1$ si comporta come asintoto verticale della funzione $L(\rho)$.

---

# ⚫ DOMANDE SUPER DIFFICILI (9 - 10)

### 21) Dimostrare l’effetto del load balancing su k server identici
**Risposta:**

Carico per server:

$$
\rho_k = \frac{\lambda}{k\mu}
$$

All’aumentare di $k$:

$$
\lim_{k \to \infty} \rho_k = 0
$$

Quindi l’utilizzazione per server diminuisce.

---

### 22) Perché aumentare k non elimina completamente la latenza?
**Risposta:**  
Esistono overhead di rete, sincronizzazione, coordinamento e costi di bilanciamento che impediscono latenza nulla.

---

### 23) Spiegare formalmente la condizione di stabilità
**Risposta:**  

Il sistema è stabile se:

$$
\rho < 1
$$

cioè il carico è inferiore alla capacità massima. In caso contrario la coda diverge.

---

### 24) Confrontare sistema centralizzato e sistema con load balancing in termini di limite
**Risposta:**  
Sistema centralizzato: un unico punto di saturazione con divergenza rapida della latenza.  
Sistema distribuito: saturazione spostata, carico ripartito, crescita più lenta della latenza.

---

### 25) Perché la stabilità è più importante della potenza pura?
**Risposta:**  
Perché anche un server molto potente diventa inutilizzabile se il carico supera la capacità. La stabilità garantisce tempi di risposta accettabili.

---

# 🎯 Obiettivo didattico

Le domande coprono:

- Modello formale del sistema centralizzato  
- Latenza e sue componenti  
- Politiche di coda  
- Throughput e tasso di arrivo  
- Utilizzazione e stabilità  
- Saturazione e divergenza  
- Interpretazione dei limiti  
- Collegamento ai server web reali  
- Introduzione formale al Load Balancing  

---
```
