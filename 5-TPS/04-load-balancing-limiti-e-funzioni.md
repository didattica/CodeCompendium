# Load Balancing - Limiti e Funzioni ⚖️🌐

*(Introduzione teorica e primi esercizi)*

## Prerequisiti matematici 🧮

Prima di affrontare i calcoli di Load Balancing, è utile comprendere alcuni concetti matematici fondamentali legati al **limite di una funzione**.

| Concetto                     | Definizione / Nota                                                                          | Esempio intuitivo                                                                 |
| ---------------------------- | ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| **Funzione**                 | Relazione che associa a ogni valore di input $x$ un unico valore di output $f(x)$           | Latenza $L$ in funzione del carico $\lambda$: $L = f(\lambda)$                    |
| **Limite di una funzione**   | Valore a cui $f(x)$ tende quando $x$ si avvicina a un certo punto $a$                       | $\lim_{x \to a} f(x) = L$ significa che $f(x)$ si avvicina a $L$ quando $x \to a$ |
| **Limite destro / sinistro** | Limite osservato avvicinandosi al punto da destra ($x \to a^+$) o da sinistra ($x \to a^-$) | Utile per capire cosa succede quando il carico tende al massimo dal basso         |
| **Limite infinito**          | Quando $f(x)$ cresce senza bound all’avvicinarsi di $x$ a un valore                         | Latenza che diverge quando $\lambda \to \lambda_{\text{max}}$                     |
| **Asintoto**                 | Retta che la funzione “tende a toccare” ma non raggiunge mai                                | Latenza cresce senza bound avvicinandosi alla saturazione                         |

### Applicazione al Load Balancing 🔁

* Consideriamo la **latenza** $L(\lambda)$ come funzione crescente del carico $\lambda$.
* La condizione di stabilità del sistema si esprime con il limite:

$\lim_{\lambda \to \lambda_{\text{max}}^-} L(\lambda) = \infty$

* Questo formalizza il concetto che **superando $\lambda_{\text{max}}$, la latenza diverge e il sistema collassa**.
* Aggiungendo server con Load Balancing, possiamo osservare che:

$\lim_{k \to \infty} \rho = 0$

* Dove $\rho$ è l’utilizzazione di ciascun server. Significa che aumentando il numero di server, la latenza teoricamente si riduce, pur restando vincolata da fattori pratici.

📌 Questi concetti matematici saranno fondamentali per comprendere e calcolare stabilità, throughput e latenza nelle sezioni successive della lezione.

---

## Andamento della latenza in funzione del carico

Nel contesto del Load Balancing, la **latenza** $(L(\lambda))$ è una funzione crescente del carico $(\lambda)$.
Quando il carico si avvicina alla capacità massima del sistema $(\lambda_{max})$, la latenza cresce rapidamente fino a divergere.

Formalmente:

$$
\lim_{\lambda \to \lambda_{max}^{-}} L(\lambda) = \infty
$$

Il comportamento tipico è illustrato nel grafico seguente.

```mermaid
xychart-beta
    title "Latenza L in funzione del carico λ"
    x-axis ["0", "0.1", "0.2", "0.3", "0.4", "0.5", "0.6", "0.7", "0.8", "0.85", "0.9", "0.95", "0.98", "0.99"]
    y-axis "Latenza L" 0 --> 100
    line [1, 1.2, 1.4, 1.7, 2.1, 2.8, 3.8, 5.5, 9, 12, 20, 40, 70, 95]
````

📌 **Osservazione**: la curva mostra che per carichi bassi la latenza cresce lentamente, mentre vicino alla saturazione aumenta rapidamente fino a diventare non gestibile.



