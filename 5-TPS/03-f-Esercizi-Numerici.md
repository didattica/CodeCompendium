# Esercizi Numerici – Difficoltà Crescente  
## Sistemi Centralizzati, Stabilità e Load Balancing

---

# 🟢 ESERCIZIO 1 – Calcolo del Throughput Massimo (Base)

Un server centralizzato ha:

- Tempo medio di servizio  
  $T_{serv} = 50 \text{ ms}$

### Richieste:

1. Calcolare il throughput massimo teorico $\lambda_{max}$  
2. Stabilire se il sistema è stabile per $\lambda = 10 \text{ req/s}$  

---
<!--
### Soluzione

Convertiamo il tempo:

\[
50 \text{ ms} = 0.05 \text{ s}
\]

\[
\lambda_{max} = \frac{1}{T_{serv}} = \frac{1}{0.05} = 20 \text{ req/s}
\]

Poiché:

\[
\lambda = 10 < 20
\]

Il sistema è **stabile**.
-->
---

# 🟡 ESERCIZIO 2 – Utilizzazione e Stato del Sistema

Un server ha:

- $\lambda_{max} = 40 \text{ req/s}$
- $\lambda = 32 \text{ req/s}$

### Richieste:

1. Calcolare l’utilizzazione $\rho$  
2. Determinare lo stato del sistema  

---
<!--
### Soluzione

\[
\rho = \frac{\lambda}{\lambda_{max}} = \frac{32}{40} = 0.8
\]

Interpretazione:

- $\rho = 0.8$  
- Il sistema è stabile  
- Il server è utilizzato all’80%
-->
---

# 🔴 ESERCIZIO 3 – Latenza Media con FIFO

Tre richieste arrivano simultaneamente ($t=0$).  
Il server gestisce una richiesta alla volta (FIFO).

| Client | $t_{request}$ | $t_{processing}$ | $t_{response}$ |
|--------|--------------|-----------------|---------------|
| C1 | 4 ms | 20 ms | 4 ms |
| C2 | 5 ms | 30 ms | 5 ms |
| C3 | 3 ms | 10 ms | 3 ms |

### Richieste:

1. Calcolare $TC_1, TC_2, TC_3$  
2. Calcolare la latenza media  

---
<!--
### Soluzione

Service time:

C1:  
\[
4+20+4=28 \text{ ms}
\]

C2:  
\[
5+30+5=40 \text{ ms}
\]

C3:  
\[
3+10+3=16 \text{ ms}
\]

Latenze totali:

\[
TC_1 = 28
\]

\[
TC_2 = 28 + 40 = 68
\]

\[
TC_3 = 28 + 40 + 16 = 84
\]

Latenza media:

\[
\frac{28 + 68 + 84}{3} = \frac{180}{3} = 60 \text{ ms}
\]
-->
---

# 🔴 ESERCIZIO 4 – Avvicinamento alla Saturazione

Un server ha:

- $T_{serv} = 20 \text{ ms}$

### Richieste:

1. Calcolare $\lambda_{max}$  
2. Calcolare $\rho$ per:
   - $\lambda = 30$
   - $\lambda = 45$
   - $\lambda = 50$

3. Indicare lo stato del sistema in ciascun caso  

---
<!--
### Soluzione

\[
20 \text{ ms} = 0.02 \text{ s}
\]

\[
\lambda_{max} = \frac{1}{0.02} = 50 \text{ req/s}
\]

Caso 1:

\[
\rho = \frac{30}{50} = 0.6
\]

→ stabile

Caso 2:

\[
\rho = \frac{45}{50} = 0.9
\]

→ stabile ma vicino alla saturazione

Caso 3:

\[
\rho = \frac{50}{50} = 1
\]

→ saturazione
-->
---
<!--
# ⚫ ESERCIZIO 5 – Load Balancing e Riduzione del Carico

Un sistema riceve:

\[
\lambda = 120 \text{ req/s}
\]

Ogni server ha:

\[
\mu = 50 \text{ req/s}
\]

### Parte A – Sistema con 1 server

1. Calcolare $\rho$  
2. Determinare lo stato del sistema  

\[
\rho = \frac{120}{50} = 2.4
\]

→ sistema instabile

---

### Parte B – Sistema con 3 server identici

Carico per server:

\[
\rho_3 = \frac{120}{3 \cdot 50} = \frac{120}{150} = 0.8
\]

→ sistema stabile

---

### Parte C – Numero minimo di server per avere $\rho < 0.7$

Condizione:

\[
\frac{120}{k \cdot 50} < 0.7
\]

\[
\frac{120}{50k} < 0.7
\]

\[
\frac{120}{35} < k
\]

\[
3.43 < k
\]

Numero minimo intero:

\[
k = 4
\]
<!--

---

# 🎯 Progressione della difficoltà

1. Calcolo diretto di throughput  
2. Interpretazione di utilizzazione  
3. Calcolo completo della latenza FIFO  
4. Analisi di saturazione  
5. Dimensionamento con load balancing  

---
