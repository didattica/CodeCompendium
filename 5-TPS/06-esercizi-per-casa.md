# Esercizi sui Limiti – Sistemi Centralizzati, Code e Latenza $L(\rho)$

Si consideri un **sistema centralizzato** (server unico o cluster visto come risorsa logica) con **carico normalizzato** $\rho \in [0,1)$, dove $\rho$ rappresenta il rapporto tra tasso di arrivo e capacità di servizio.

L’obiettivo è analizzare il comportamento asintotico della **latenza media** al crescere del carico, in scenari tipici di **load balancing, code M/M/1 e sistemi congestionati**.

---

## Esercizio 1 – Latenza normalizzata con overhead di scheduling

$$
L(\rho) = \frac{1 + \rho^2}{1 - \rho}
$$

Calcolare: $\lim_{\rho \to 0.8} L(\rho)$

---

## Esercizio 2 – Sistema centralizzato vicino alla saturazione

$$
L(\rho) = \frac{\log(1 + \rho)}{1 - \rho}
$$

Calcolare:
$\lim_{\rho \to 1^-} L(\rho)$

---

## Esercizio 3 – Latenza con politiche di retry

$$
L(\rho) = \frac{\rho}{(1 - \rho)^2}
$$

Calcolare:
$\lim_{\rho \to 1^-} L(\rho)$

---

## Esercizio 4 – Sistema con backoff esponenziale

$$
L(\rho) = \sqrt{\frac{1 + \rho}{1 - \rho}}
$$

Calcolare:
$\lim_{\rho \to 1^-} L(\rho)$

---

## Esercizio 5 – Ottimizzazione ideale del carico

$$
L(\rho) = \frac{1 - \rho^2}{1 - \rho}
$$

Calcolare:
$\lim_{\rho \to 1^-} L(\rho)$

---

# Risultati (senza svolgimento) ✅

1. $$6.2$$
2. $$+\infty$$
3. $$+\infty$$
4. $$+\infty$$
5. $$2$$
