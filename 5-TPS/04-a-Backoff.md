# Backoff – Introduzione, Definizione e Casi d'Uso

## 📌 Definizione semplice e chiara

Il **backoff** è una tecnica utilizzata nei sistemi informatici e nelle reti per gestire i **ritentativi dopo un fallimento**.

In pratica, quando un’operazione non va a buon fine (ad esempio un server non risponde o si verifica una collisione di rete), il sistema **non ritenta immediatamente**, ma **attende un certo intervallo di tempo prima di riprovare**.

Questo intervallo:

* serve a **evitare sovraccarichi** o nuove collisioni,
* può **aumentare progressivamente** dopo ogni fallimento,
* può includere una **componente casuale** per evitare tentativi simultanei.

In sintesi:

> **Backoff = aspettare prima di ritentare, e aspettare di più se i fallimenti continuano.**

---

## 📝 Introduzione: metafora intuitiva

Immagina di chiamare un amico al telefono e lui non risponde perché è occupato.
Se provi a richiamarlo **subito**, rischi di intasare la linea.
Invece, aspetti qualche secondo e poi ritenti. Se non risponde ancora, aspetti un po’ di più, e così via.

Questo è esattamente il principio del **backoff**.

---

## 🔢 Backoff esponenziale (server non disponibile)

Quando un server non risponde, il tempo di attesa per il tentativo (k) è:

[
T_{\text{backoff}}^{(k)} = \min(T_{\text{max}}, T_0 \cdot 2^k)
]

Dove:

* (T_0) è il tempo di attesa iniziale
* (k) è il numero di tentativi falliti
* (T_{\text{max}}) è il tempo massimo di attesa

---

## 🔢 Backoff per collisioni in rete

Nelle reti condivise, il backoff include una componente casuale:

[
T_{\text{backoff}} = \text{Random}(0, W) \cdot t_{\text{slot}}
]

con:

[
W = \min(2^k - 1, W_{\text{max}})
]

Il termine casuale riduce la probabilità che più nodi ritentino **nello stesso istante**.

---

## 🔑 Concetti chiave

* Il backoff gestisce i **ritentativi**
* Riduce **congestione** e **collisioni**
* Può essere **deterministico** o **randomizzato**
* È fondamentale in reti, protocolli e sistemi distribuiti
