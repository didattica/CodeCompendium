# Backoff – Introduzione, Formalismo e Casi d'Uso ⚡🖥️

---

## 📝 Introduzione: metafora semplice

Immagina di chiamare un amico al telefono e lui non risponde perché è occupato.  
Se provi a chiamarlo di nuovo **subito**, rischi di intasare la linea.  
Invece, aspetti qualche secondo e poi ritenti. Se non risponde ancora, aspetti un po’ di più, e così via.

Questo è il principio del **backoff**:

- Dopo un fallimento, si **attende un certo intervallo prima di ritentare**  
- Gli intervalli possono crescere con i tentativi, per evitare di **saturare il server**  

---

## 🔢 Backoff per server giù

Quando un server non risponde, il tempo di attesa per il tentativo $k$ è:

$$
T_{\text{backoff}}^{(k)} = \min(T_{\text{max}}, T_0 \cdot 2^k)
$$

dove:

- $T_0$ = intervallo base di attesa (es. 100 ms)  
- $k$ = numero del tentativo corrente (0,1,2…)  
- $T_{\text{max}}$ = massimo tempo di attesa consentito  

### Esempio numerico

- $T_0 = 100 \, \text{ms}$, $T_{\text{max}} = 1600 \, \text{ms}$  

| Tentativo $k$ | $T_{\text{backoff}}^{(k)}$ |
|---------------|----------------------------|
| 0             | 100 ms                     |
| 1             | 200 ms                     |
| 2             | 400 ms                     |
| 3             | 800 ms                     |
| 4             | 1600 ms                    |
| 5             | 1600 ms                    |

---

### Grafico: server giù

```mermaid
xychart
    title "Backoff esponenziale: server giù"
    x-axis ["0","1","2","3","4","5"]
    y-axis "Tempo di attesa (ms)" 0 --> 1800
    line [100,200,400,800,1600,1600]
````

---

## 🔢 Backoff per collisioni in rete

Quando più nodi trasmettono contemporaneamente, si usano **backoff esponenziale con componente casuale**:

$$
T_{\text{backoff}} = \text{Random}(0, W) \cdot t_{\text{slot}}
$$

$$
W = \min(2^k - 1, W_{\text{max}})
$$

* $k$ = numero di tentativi falliti
* $t_{\text{slot}}$ = durata di uno slot di tempo
* $W_{\text{max}}$ = finestra massima

📌 Il **random** serve a ridurre la probabilità che più nodi ritentino **allo stesso momento**, evitando collisioni simultanee.

### Esempio numerico

* $t_{\text{slot}} = 20 , \mu s$, $k = 3$, $W_{\text{max}} = 16$
* Calcolo finestra:

$$
W = \min(2^3-1, 16) = 7
$$
* Se $\text{Random}(0,7) = 5$, allora:

$$
T_{\text{backoff}} = 5 \cdot 20 = 100 , \mu s
$$

---

## 📊 Grafico comparativo

```mermaid
xychart
    title "Backoff: server giù vs collisioni in rete"
    x-axis ["0","1","2","3","4","5"]
    y-axis "Tempo di attesa" 0 --> 1800
    line [100,200,400,800,1600,1600] title "Server giù (ms)"
    line [20,40,80,160,320,320] title "Collisioni in rete (μs)"
```

📌 **Interpretazione:**

* **Server giù:** tempi di attesa crescono esponenzialmente, senza random
* **Collisioni in rete:** tempi di attesa esponenziali ma randomizzati
* Evidente la logica diversa dei due scenari

---

## 🔑 Concetti Chiave

* **Backoff** = ritardo tra tentativi dopo un fallimento
* **Server giù / sovraccarico**: backoff esponenziale semplice, senza random
* **Collisioni in rete**: backoff esponenziale con random, per ridurre ritentativi simultanei
* Formule principali:

**Server giù:**

$$
T_{\text{backoff}}^{(k)} = \min(T_{\text{max}}, T_0 \cdot 2^k)
$$

**Collisioni in rete:**

$$
T_{\text{backoff}} = \text{Random}(0, W) \cdot t_{\text{slot}}, \quad W = \min(2^k - 1, W_{\text{max}})
$$


<!--
```

---

Se vuoi, posso fare una **versione con diagramma a fumetti/metafora visiva** in Mermaid, dove le chiamate al server e i retry vengono mostrati come linee colorate:  
- verde = server giù  
- blu = collisioni in rete  

Così diventa subito molto intuitivo anche per studenti alle prime armi.  

Vuoi che faccia anche questa versione illustrata?
```
-->
