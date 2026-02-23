
# Backoff – Definizione, Formalismo e Esempi ⚡🖥️

---

## 📌 Definizione

Il **backoff** è una strategia utilizzata nei sistemi di rete e nei protocolli di comunicazione per **gestire collisioni e retry**.  
Quando due o più nodi tentano di trasmettere dati contemporaneamente e si verifica una collisione, i nodi **attendono un tempo casuale** prima di ritentare, riducendo la probabilità di ulteriori collisioni.

Il backoff è usato in protocolli come **Ethernet (CSMA/CD)** e **Wi-Fi (CSMA/CA)**.

---

## 🔢 Formalismo Matematico

Il **ritardo di backoff** $T_{backoff}$ può essere calcolato come:

$$
T_{backoff} = \text{Random}(0, W) \cdot t_{slot}
$$

dove:

- $W$ = finestra di backoff (in slot)  
- $t_{slot}$ = durata di uno slot di tempo  
- $\text{Random}(0, W)$ = numero casuale uniforme tra 0 e $W$

Per il **backoff esponenziale binario**, tipico di Ethernet:

$$
W = \min(2^k - 1, W_{max})
$$

dove:

- $k$ = numero di tentativi di trasmissione falliti consecutivi  
- $W_{max}$ = finestra massima consentita

---

## 🧮 Esempio Numerico

Supponiamo:

- $t_{slot} = 20 \, \mu s$  
- $W_{min} = 1$  
- $W_{max} = 16$  
- $k = 3$ tentativi falliti

Allora:

$$
W = \min(2^3 - 1, 16) = 7
$$

Il backoff sarà:

$$
T_{backoff} = \text{Random}(0,7) \cdot 20 \, \mu s
$$

Se, ad esempio, $\text{Random}(0,7) = 5$:

$$
T_{backoff} = 5 \cdot 20 = 100 \, \mu s
$$

---

## 📊 Andamento della finestra di backoff

Il grafico seguente mostra come la finestra di backoff $W$ cresce con il numero di tentativi falliti $k$:

```mermaid
xychart-beta
    title "Backoff esponenziale: finestra W in funzione dei tentativi k"
    x-axis ["0","1","2","3","4","5"]
    y-axis "Finestra W" 0 --> 20
    line [1,3,7,15,16,16]
````

📌 **Interpretazione:**

* La finestra di backoff cresce **esponenzialmente** dopo ogni collisione
* Dopo un certo numero di tentativi, la finestra raggiunge $W_{max}$
* L’attesa casuale riduce la probabilità di collisioni successive

---

## 🔑 Concetti Chiave

* **Backoff** = ritardo casuale dopo collisione
* **Backoff esponenziale** riduce le collisioni multiple
* Formula generale:
  $$
  T_{backoff} = \text{Random}(0, W) \cdot t_{slot}
  $$
* Finestra esponenziale:
  $$
  W = \min(2^k -1, W_{max})
  $$

Questa strategia è alla base di molti protocolli di rete a contenuto condiviso, come Ethernet e Wi-Fi.
