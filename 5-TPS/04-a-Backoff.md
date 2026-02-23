
# Backoff – Introduzione, Formalismo e Casi d'Uso ⚡🖥️

---

## 📝 Introduzione: una metafora semplice

Immagina di dover attraversare un corridoio stretto con **più persone che vogliono passare contemporaneamente**.  
Se tutti provano a passare nello stesso momento, si crea **ingorgo**: nessuno riesce a muoversi.  

Il **backoff** funziona come una strategia per **evitare ingorghi**:

- Chi non riesce a passare aspetta un **tempo casuale** prima di ritentare.  
- Chi aspetta più a lungo ha più probabilità di passare senza scontrarsi con gli altri.  

Questa idea si applica sia alle **collisioni in rete** sia a **server sovraccarichi o giù temporaneamente**.

---

## 🔢 Formalismo Matematico

Il backoff può essere modellato come un **ritardo casuale**:

$$
T_{\text{backoff}} = \text{Random}(0, W) \cdot t_{\text{slot}}
$$

dove:

- $W$ = finestra di backoff (in slot)  
- $t_{\text{slot}}$ = durata di uno slot di tempo  
- $\text{Random}(0, W)$ = numero casuale uniforme tra 0 e $W$

### Backoff esponenziale binario

Tipico in Ethernet e Wi-Fi:

$$
W = \min(2^k - 1, W_{\text{max}})
$$

dove:

- $k$ = numero di tentativi falliti consecutivi  
- $W_{\text{max}}$ = finestra massima consentita  

Per il **retry con server giù**:

$$
T_{\text{backoff}}^{(k)} = \min(T_{\text{max}}, T_0 \cdot 2^k) \cdot \text{Random}(0,1)
$$

- $T_0$ = intervallo base  
- $k$ = tentativo corrente (0,1,2…)  
- $T_{\text{max}}$ = massimo tempo di attesa  
- $\text{Random}(0,1)$ = numero casuale per evitare sincronizzazione tra client  

---

## 🧮 Esempio Numerico

**Caso collisione in rete**:

- $t_{\text{slot}} = 20 \, \mu s$, $k = 3$, $W_{\text{max}} = 16$  
- Calcolo finestra:

$$
W = \min(2^3-1, 16) = 7
$$  
- Se $\text{Random}(0,7) = 5$, allora:
 
$$
T_{\text{backoff}} = 5 \cdot 20 = 100 \, \mu s
$$

**Caso server giù**:

- $T_0 = 100 \, \text{ms}$, $T_{\text{max}} = 1600 \, \text{ms}$, $k = 3$  
- Se $\text{Random}(0,1) = 0.6$, allora:

$$
T_{\text{backoff}}^{(3)} = \min(1600, 100 \cdot 2^3) \cdot 0.6 = \min(1600, 800) \cdot 0.6 = 480 \, \text{ms}
$$

---

## 📊 Andamento della finestra di backoff

Mostriamo come cresce la finestra con il numero di tentativi falliti $k$:

```mermaid
xychart-beta
    title "Backoff esponenziale: finestra W in funzione dei tentativi k"
    x-axis ["0","1","2","3","4","5"]
    y-axis "Finestra W / Tempo di attesa" 0 --> 2000
    line [100,200,400,800,1600,1600]
````

📌 **Interpretazione**:

* La finestra cresce **esponenzialmente** ad ogni tentativo fallito.
* Dopo un certo numero di tentativi, raggiunge il massimo $W_{\text{max}}$ o $T_{\text{max}}$.
* Riduce il rischio di **collisioni in rete** e **sovraccarico dei server**.

---

## ⚙️ Casi d'Uso

1. **Collisioni in rete**

   * Ethernet (CSMA/CD) e Wi-Fi (CSMA/CA)
   * Evita che più nodi trasmettano contemporaneamente

2. **Server giù o sovraccarico**

   * Retry con backoff esponenziale
   * Evita di saturare il server con richieste continue
   * Consente al server di recuperare gradualmente

3. **Altri scenari**

   * API rate-limiting
   * Sistemi distribuiti che condividono risorse
   * Job scheduler con risorse limitate

---

## 🔑 Concetti Chiave

* **Backoff** = ritardo casuale dopo un fallimento
* **Backoff esponenziale** = ritardo crescente ad ogni tentativo
* Riduce **collisioni**, **sovraccarico** e **congestione**
* Formule principali:

$$
T_{\text{backoff}} = \text{Random}(0, W) \cdot t_{\text{slot}}
$$

$$
W = \min(2^k - 1, W_{\text{max}})
$$
$$
T_{\text{backoff}}^{(k)} = \min(T_{\text{max}}, T_0 \cdot 2^k) \cdot \text{Random}(0,1)
$$


