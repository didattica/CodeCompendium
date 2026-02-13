# Dalla Logica alla Rappresentazione Grafica

## Introduzione

Nella logica proposizionale abbiamo studiato operatori come:

* **AND**
* **OR**
* **NOT**

Abbiamo visto come funzionano attraverso le **tavole della verità**.

Ora facciamo un passo avanti.

L’idea fondamentale è questa:

> Le operazioni logiche possono essere rappresentate graficamente utilizzando gli insiemi.

Questo passaggio ci permette di **vedere la logica**, non solo calcolarla.

---

# 1. Dalla proposizione all’insieme

Una proposizione logica può essere interpretata come un insieme.

### Esempio

Consideriamo l’universo U = insieme di tutti gli studenti di una classe.

Definiamo:

* A = studenti che praticano sport
* B = studenti che suonano uno strumento musicale

Qui A e B non sono più frasi, ma **insiemi di elementi**.

---

# 2. Corrispondenza tra Logica e Insiemi

Le operazioni logiche hanno un equivalente negli insiemi.

| Logica  | Insiemi | Significato                       |
| ------- | ------- | --------------------------------- |
| A AND B | A ∩ B   | Elementi che stanno in entrambi   |
| A OR B  | A ∪ B   | Elementi che stanno in almeno uno |
| NOT A   | Aᶜ      | Elementi che non stanno in A      |

---

## 2.1 AND → Intersezione (∩)

**Logica:**
A AND B è vera solo se entrambe sono vere.

**Insiemi:**
A ∩ B contiene gli elementi comuni.

### Metafora

Immaginiamo due cerchi che si sovrappongono.

La parte centrale è come una zona condivisa:
chi sta lì appartiene sia ad A sia a B.

Esempio:
Studenti che praticano sport **e** suonano uno strumento.

---

## 2.2 OR → Unione (∪)

**Logica:**
A OR B è vera se almeno una è vera.

**Insiemi:**
A ∪ B contiene tutti gli elementi di A e di B.

### Metafora

Se A è un cerchio rosso e B è un cerchio blu,
l’unione è tutta l’area coperta dai due cerchi.

Non importa se un elemento sta in uno solo o in entrambi:
fa comunque parte dell’unione.

---

## 2.3 NOT → Complementare

**Logica:**  
NOT A è vera quando A è falsa.

**Insiemi:**  
Il complemento di A è l’insieme di tutti gli elementi dell’universo che non appartengono ad A.

Notazioni equivalenti per indicare il complemento di A:

- Aᶜ  
- Ā  
- U − A  
- C(A)  (meno usata, ma possibile)

Formalmente:

Aᶜ = { x ∈ U | x ∉ A }

Significa: l’insieme di tutti gli elementi x appartenenti all’universo U che non appartengono ad A.

### Metafora

Se l’universo è l’intera classe,
e A è l’insieme degli studenti che praticano sport,

il complemento di A (Aᶜ, Ā, U − A) è l’insieme degli studenti che non praticano sport.


---

# 3. I Diagrammi di Venn

Per rappresentare graficamente gli insiemi si usano i **diagrammi di Venn**.

Sono rappresentazioni in cui:

* L’insieme universo è un rettangolo.
* Gli insiemi sono cerchi all’interno del rettangolo.
* Le sovrapposizioni mostrano le intersezioni.

---

## 3.1 Due insiemi

Con due insiemi possiamo rappresentare:

* A
* B
* A ∩ B
* A ∪ B
* Aᶜ
* Bᶜ

La zona centrale dei due cerchi rappresenta l’intersezione.

---

## 3.2 Tre insiemi

Con tre insiemi il diagramma diventa più complesso:

* Ogni coppia ha una zona comune.
* Esiste una zona centrale comune a tutti e tre.

Questa rappresentazione è utile per visualizzare espressioni logiche come:

(A AND B) OR C

---

# 4. Perché questo passaggio è importante?

La logica lavora con valori di verità (vero/falso).
Gli insiemi lavorano con appartenenza (∈ / ∉).

Il collegamento è profondo:

* Vero ↔ appartiene all’insieme
* Falso ↔ non appartiene all’insieme

Questo significa che:

> La logica può essere tradotta in linguaggio insiemistico.

E questo sarà fondamentale quando parleremo di:

* Sottoinsiemi
* Insieme vuoto
* Insiemi numerici
* Strutture matematiche più avanzate

---

# 5. Esempio Completo

Sia:

U = {1,2,3,4,5,6}
A = {1,2,3}
B = {3,4,5}

Allora:

* A ∩ B = {3}
* A ∪ B = {1,2,3,4,5}
* Aᶜ = {4,5,6}

Nel diagramma di Venn:

* Il numero 3 sta nella zona centrale.
* Il numero 6 sta fuori da entrambi i cerchi.

---

# 6. Sintesi Concettuale

Possiamo riassumere così:

Logica → Valori di verità
Insiemi → Appartenenza
Diagrammi di Venn → Visualizzazione della logica

La rappresentazione grafica non è solo un disegno,
ma uno strumento per comprendere strutture astratte.
