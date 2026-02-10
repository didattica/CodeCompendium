# Esercizi sui Limiti – Load Balancing e Latenza $L(\rho)$ ⚖️🌐

In questi esercizi studiamo l’andamento della **latenza** $L(\rho)$ in funzione del **carico normalizzato** (utilizzazione) $\rho$.

Ricordiamo che:

$$
\rho = \frac{\lambda}{\mu}
\qquad\text{e}\qquad
0 \le \rho < 1
$$

Quando $\rho \to 1^-$ il sistema si avvicina alla **saturazione**, e la latenza tende a crescere senza limite.

---

## Esercizio 1 (Facile) – Limite in un punto interno

### Traccia
Sia:

$$
L(\rho) = \frac{1}{1-\rho}
$$

Calcolare:

$$
\lim_{\rho \to 0.5} L(\rho)
$$

---

### Soluzione
Sostituiamo direttamente $\rho = 0.5$:

$$
L(0.5) = \frac{1}{1-0.5} = \frac{1}{0.5} = 2
$$

Quindi:

$$
\lim_{\rho \to 0.5} \frac{1}{1-\rho} = 2
$$

---

## Esercizio 2 (Facile) – Limite verso saturazione

### Traccia
Sia:

$$
L(\rho) = \frac{1}{1-\rho}
$$

Calcolare:

$$
\lim_{\rho \to 1^-} L(\rho)
$$

---

### Soluzione
Quando $\rho \to 1^-$, il denominatore $1-\rho \to 0^+$.

Quindi:

$$
\frac{1}{1-\rho} \to +\infty
$$

Conclusione:

$$
\lim_{\rho \to 1^-} \frac{1}{1-\rho} = +\infty
$$

---

## Esercizio 3 (Medio) – Confronto tra due divergenze

### Traccia
Siano:

$$
f(\rho) = \frac{1}{1-\rho}
\qquad
g(\rho) = \frac{1}{(1-\rho)^2}
$$

Calcolare:

1. $\displaystyle \lim_{\rho\to 1^-} f(\rho)$  
2. $\displaystyle \lim_{\rho\to 1^-} g(\rho)$  
3. Quale funzione diverge più velocemente?

---

### Soluzione
1. Come già visto:

$$
\lim_{\rho\to 1^-} \frac{1}{1-\rho} = +\infty
$$

2. Anche in questo caso $1-\rho \to 0^+$, ma elevato al quadrato:

$$
(1-\rho)^2 \to 0^+
$$

Quindi:

$$
\lim_{\rho\to 1^-} \frac{1}{(1-\rho)^2} = +\infty
$$

3. $g(\rho)$ diverge più velocemente perché il denominatore tende a zero più rapidamente (quadratico).

---

## Esercizio 4 (Medio) – Limite con radice

### Traccia
Sia:

$$
L(\rho) = \frac{1}{\sqrt{1-\rho}}
$$

Calcolare:

$$
\lim_{\rho \to 1^-} L(\rho)
$$

---

### Soluzione
Quando $\rho \to 1^-$, allora $1-\rho \to 0^+$ e quindi:

$$
\sqrt{1-\rho} \to 0^+
$$

Allora:

$$
\frac{1}{\sqrt{1-\rho}} \to +\infty
$$

Conclusione:

$$
\lim_{\rho \to 1^-} \frac{1}{\sqrt{1-\rho}} = +\infty
$$

---

## Esercizio 5 (Medio) – Limite di una funzione normalizzata

### Traccia
Sia:

$$
L(\rho) = \frac{1}{1-\rho}
$$

Definiamo:

$$
H(\rho) = (1-\rho)\cdot L(\rho)
$$

Calcolare:

$$
\lim_{\rho \to 1^-} H(\rho)
$$

---

### Soluzione
Sostituiamo $L(\rho)$:

$$
H(\rho) = (1-\rho)\cdot \frac{1}{1-\rho}
$$

Semplificando:

$$
H(\rho) = 1
$$

Quindi:

$$
\lim_{\rho \to 1^-} H(\rho) = 1
$$

📌 Interpretazione: abbiamo eliminato la divergenza tramite una normalizzazione.

---

## Esercizio 6 (Medio-Difficile) – Forma indeterminata $0 \cdot \infty$

### Traccia
Calcolare il limite:

$$
\lim_{\rho \to 1^-} \left( (1-\rho)\cdot \frac{5}{(1-\rho)^2} \right)
$$

---

### Soluzione
Riscriviamo l’espressione:

$$
(1-\rho)\cdot \frac{5}{(1-\rho)^2}
=
\frac{5(1-\rho)}{(1-\rho)^2}
$$

Semplificando:

$$
\frac{5}{1-\rho}
$$

Ora calcoliamo il limite:

$$
\lim_{\rho \to 1^-} \frac{5}{1-\rho} = +\infty
$$

Quindi:

$$
\lim_{\rho \to 1^-} \left( (1-\rho)\cdot \frac{5}{(1-\rho)^2} \right)=+\infty
$$

---

## Esercizio 7 (Difficile) – Limite con logaritmo

### Traccia
Sia:

$$
L(\rho) = \frac{\ln\left(\frac{1}{1-\rho}\right)}{1-\rho}
$$

Calcolare:

$$
\lim_{\rho \to 1^-} L(\rho)
$$

---

### Soluzione
Quando $\rho \to 1^-$, allora $1-\rho \to 0^+$.

Quindi:

- $\frac{1}{1-\rho} \to +\infty$
- $\ln\left(\frac{1}{1-\rho}\right) \to +\infty$

L’espressione diventa:

$$
\frac{+\infty}{0^+}
$$

che tende a:

$$
+\infty
$$

Conclusione:

$$
\lim_{\rho \to 1^-} \frac{\ln\left(\frac{1}{1-\rho}\right)}{1-\rho} = +\infty
$$

📌 Interpretazione: la latenza cresce ancora più rapidamente rispetto a un logaritmo semplice.

---

## Esercizio 8 (Molto Difficile) – Limite con parametro $k$ (Load Balancing)

### Traccia
Un sistema di Load Balancing distribuisce il carico su $k$ server identici.

Il carico normalizzato per server è:

$$
\rho_k = \frac{\lambda}{k\mu}
$$

La latenza su ciascun server è modellata come:

$$
L(\rho_k) = \frac{1}{1-\rho_k}
$$

Calcolare:

$$
\lim_{k \to \infty} L(\rho_k)
$$

---

### Soluzione
Sostituiamo $\rho_k$ nella latenza:

$$
L(\rho_k) = \frac{1}{1-\frac{\lambda}{k\mu}}
$$

Ora valutiamo il limite per $k \to \infty$.

Poiché:

$$
\frac{\lambda}{k\mu} \to 0
\quad\text{quando}\quad k\to\infty
$$

allora:

$$
1 - \frac{\lambda}{k\mu} \to 1
$$

Quindi:

$$
\lim_{k \to \infty} L(\rho_k)
=
\frac{1}{1}
=
1
$$

Conclusione:

$$
\lim_{k \to \infty} \frac{1}{1-\frac{\lambda}{k\mu}} = 1
$$

📌 Interpretazione: aumentando molto il numero di server, il carico su ciascun server tende a zero e la latenza tende al valore minimo teorico.

---

# Fine esercizi ✅
