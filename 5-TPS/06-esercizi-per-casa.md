# Esercizi sui Limiti – Load Balancing e Latenza $L(\rho)$ ⚖️🌐

In questi esercizi consideriamo la latenza $L(\rho)$ come funzione crescente del carico normalizzato $\rho$, con:

$$
0 \le \rho < 1
$$

L’obiettivo è calcolare limiti tipici che descrivono il comportamento del sistema quando il carico aumenta.

---

## Esercizio 1

### Traccia
Sia:

$$
L(\rho) = \frac{1}{1-\rho}
$$

Calcolare:

$$
\lim_{\rho \to 0.25} L(\rho)
$$

---

## Esercizio 2

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

## Esercizio 3

### Traccia
Sia:

$$
L(\rho) = \frac{5}{(1-\rho)^2}
$$

Calcolare:

$$
\lim_{\rho \to 1^-} L(\rho)
$$

---

## Esercizio 4

### Traccia
Sia:

$$
L(\rho) = \sqrt{\frac{1}{1-\rho}}
$$

Calcolare:

$$
\lim_{\rho \to 1^-} L(\rho)
$$

---

## Esercizio 5

### Traccia
Sia:

$$
L(\rho) = \frac{1-\rho}{1-\rho}
$$

Calcolare:

$$
\lim_{\rho \to 1^-} L(\rho)
$$

---

# Risultati (senza svolgimento) ✅

1. $$\lim_{\rho \to 0.25} \frac{1}{1-\rho} = \frac{4}{3}$$  
2. $$\lim_{\rho \to 1^-} \frac{1}{1-\rho} = +\infty$$  
3. $$\lim_{\rho \to 1^-} \frac{5}{(1-\rho)^2} = +\infty$$  
4. $$\lim_{\rho \to 1^-} \sqrt{\frac{1}{1-\rho}} = +\infty$$  
5. $$\lim_{\rho \to 1^-} \frac{1-\rho}{1-\rho} = 1$$  
