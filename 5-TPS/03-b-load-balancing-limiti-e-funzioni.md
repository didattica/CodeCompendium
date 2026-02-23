
# Load Balancing - Limiti e Funzioni ⚖️🌐

*(Introduzione teorica e primi esercizi)*

## Prerequisiti matematici e concetti di sistema 🧮

Prima di affrontare i calcoli di Load Balancing, è utile comprendere alcuni concetti matematici fondamentali legati al **limite di una funzione**.

In particolare, in ambito di sistemi e reti, ci interessa studiare come varia la **latenza** al crescere del **carico**.

---

### Concetti preliminari sul carico

Per descrivere il comportamento di un server, definiamo:

- **$\lambda$** = tasso di arrivo delle richieste (requests/sec)  
- **$\mu$** = tasso di servizio massimo del server (requests/sec)  

Da questi parametri definiamo il **carico normalizzato** o **utilizzazione**:

$$
\rho = \frac{\lambda}{\mu}, \quad 0 \le \rho < 1
$$

📌 Interpretazione:

- se $\rho = 0.2$ → il server è usato al 20%  
- se $\rho = 0.9$ → il server è quasi saturo  
- se $\rho \ge 1$ → il sistema non riesce più a smaltire le richieste (instabile)

La latenza $L$ dipende dal carico: più il server è saturo, maggiore è $L(\rho)$.

---

### Concetti base di matematica

| Concetto                     | Definizione / Nota                                                                 | Esempio intuitivo |
| ---------------------------- | ---------------------------------------------------------------------------------- | ----------------- |
| **Funzione**                 | Relazione che associa a ogni valore di input $x$ un unico valore di output $f(x)$ | Latenza $L$ in funzione del carico $\rho$: $L = f(\rho)$ |
| **Limite di una funzione**   | Valore a cui $f(x)$ tende quando $x$ si avvicina a un certo punto $a$             | $\lim_{x \to a} f(x)$ descrive cosa succede vicino a $a$ |
| **Limite destro / sinistro** | Limite osservato avvicinandosi al punto da destra ($x \to a^+$) o da sinistra ($x \to a^-$) | Utile per descrivere cosa succede quando $\rho$ tende a 1 |
| **Limite infinito**          | Quando $f(x)$ cresce senza bound all’avvicinarsi di $x$ a un valore               | Latenza che diverge quando $\rho \to 1$ |
| **Asintoto verticale**       | Retta verticale che la funzione tende ad avvicinare senza mai raggiungerla        | $L(\rho)$ cresce molto rapidamente quando $\rho$ tende a 1 |

---

## Applicazione al Load Balancing 🔁

Consideriamo la **latenza** $L(\rho)$ come funzione crescente del carico normalizzato $\rho$.

La condizione di stabilità del sistema si esprime tramite il limite:

$$
\lim_{\rho \to 1^-} L(\rho) = \infty
$$

Questo formalizza il concetto che **quando l’utilizzazione tende a 1 (saturazione), la latenza diverge e il sistema collassa**.

---

### Effetto del Load Balancing

Se distribuiamo il carico su $k$ server equivalenti, il carico medio per server diventa circa:

$$
\rho_k = \frac{\lambda}{k\mu}
$$

Quindi, aumentando $k$:

$$
\lim_{k \to \infty} \rho_k = 0
$$

📌 Significa che aumentando il numero di server, l’utilizzazione di ciascun server diminuisce, e la latenza può ridursi (entro limiti pratici come overhead, sincronizzazione, rete, ecc.).

---

📌 Questi concetti matematici saranno fondamentali per comprendere e calcolare stabilità, throughput e latenza nelle sezioni successive della lezione.

---

## Andamento della latenza in funzione del carico normalizzato

Nel contesto del Load Balancing, la **latenza** $L(\rho)$ è una funzione crescente del carico normalizzato $\rho$.

Quando $\rho$ si avvicina a 1 (saturazione), la latenza cresce rapidamente fino a divergere:

$$
\lim_{\rho \to 1^-} L(\rho) = \infty
$$

Il comportamento tipico è illustrato nel grafico seguente.

```mermaid
xychart-beta
    title "Latenza L in funzione del carico normalizzato ρ"
    x-axis ["0", "0.1", "0.2", "0.3", "0.4", "0.5", "0.6", "0.7", "0.8", "0.85", "0.9", "0.95", "0.98", "0.99"]
    y-axis "Latenza L" 0 --> 100
    line [1, 1.2, 1.4, 1.7, 2.1, 2.8, 3.8, 5.5, 9, 12, 20, 40, 70, 95]
````

📌 **Osservazione**: la curva mostra che per carichi bassi la latenza cresce lentamente, mentre vicino alla saturazione ($\rho \to 1$) aumenta rapidamente fino a diventare non gestibile.
