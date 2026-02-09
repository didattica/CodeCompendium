# Lezione 4 – Tavole di Verità (approfondimento) 🧠📊

---

## 1. Perché studiare le tavole di verità ❓💡

Le **tavole di verità** sono uno strumento fondamentale della **logica** perché permettono di:

- analizzare **tutte le possibili situazioni**
- verificare se un’espressione è corretta
- capire in modo preciso **come funziona una formula logica**

📌 In informatica e nei sistemi digitali, le tavole di verità servono per:

- controllare condizioni (`if`)
- progettare circuiti logici
- verificare se una formula è:
  - una **tautologia**
  - una **contraddizione**
  - una **contingenza**

👉 Le tavole di verità sono il collegamento tra:

- logica classica (Aristotele) 🏛️
- logica booleana e informatica ⚙️💻

---

## 2. Cos’è una tavola di verità 📋🧩

Una **tavola di verità** è una tabella che mostra:

- **tutte le combinazioni possibili** delle variabili logiche
- il **risultato finale** di un’espressione logica

📌 Le variabili logiche possono assumere solo due valori:

- **Vero (V oppure 1)**
- **Falso (F oppure 0)**

---

## 3. Tavola di verità con una variabile 🔢

Consideriamo una sola proposizione:

**A**

| A | NOT A |
|---|-------|
| V | F     |
| F | V     |

📌 Con **una variabile** ci sono sempre:

> **2 possibilità**

---

## 4. Tavola di verità con due variabili 🔁

Con **due proposizioni** (A e B) le combinazioni possibili sono:

> **2² = 4**

| A | B |
|---|---|
| V | V |
| V | F |
| F | V |
| F | F |

Questa è la **base** per costruire qualsiasi tavola più complessa.

---

## 5. Tavole di verità complete 🧠📊

Vediamo ora come costruire una **tavola di verità completa**, passo per passo.

---

### Esempio 1 – A AND B ✖️

| A | B | A AND B |
|---|---|---------|
| V | V | V       |
| V | F | F       |
| F | V | F       |
| F | F | F       |

📌 L’operatore **AND** è vero **solo se entrambe** le proposizioni sono vere.

---

### Esempio 2 – A OR B ➕

| A | B | A OR B |
|---|---|--------|
| V | V | V      |
| V | F | V      |
| F | V | V      |
| F | F | F      |

📌 L’operatore **OR** è vero se **almeno una** proposizione è vera.

---

### Esempio 3 – NOT A 🔄

| A | NOT A |
|---|-------|
| V | F     |
| F | V     |

📌 L’operatore **NOT** inverte sempre il valore logico.

---

## 6. Come costruire una tavola di verità passo per passo 🪜✍️

Metodo consigliato (molto importante per gli studenti):

### Passo 1
Scrivere **tutte le combinazioni** delle variabili.

### Passo 2
Calcolare prima tutte le negazioni (**NOT**).

### Passo 3
Calcolare gli operatori (**AND / OR**) seguendo l’ordine corretto.

### Passo 4
Compilare la tabella **una colonna alla volta**, senza saltare passaggi.

📌 Non bisogna mai improvvisare:
la logica richiede **precisione**, non intuizione.

---

## 7. Tavole di verità e classificazione delle proposizioni 🏷️

Le tavole di verità permettono di **classificare** una formula logica.

---

### Tautologia 🔁

Una formula è una **tautologia** se:

👉 l’ultima colonna è **sempre vera**

#### Esempio: A OR NOT A

| A | NOT A | A OR NOT A |
|---|-------|------------|
| V | F     | V          |
| F | V     | V          |

✔ Sempre vera → **tautologia**

---

### Contraddizione ❌

Una formula è una **contraddizione** se:

👉 l’ultima colonna è **sempre falsa**

#### Esempio: A AND NOT A

| A | NOT A | A AND NOT A |
|---|-------|-------------|
| V | F     | F           |
| F | V     | F           |

❌ Sempre falsa → **contraddizione**

---

### Contingenza 🔄

Una formula è una **contingenza** se:

👉 l’ultima colonna contiene **sia V che F**

#### Esempio: A AND B

| A | B | A AND B |
|---|---|---------|
| V | V | V       |
| V | F | F       |
| F | V | F       |
| F | F | F       |

🔄 A volte vera, a volte falsa → **contingenza**

---

## 8. Collegamento con informatica e sistemi 💻⚙️

📌 Nei programmi:

- una **tautologia** → condizione inutile (sempre vera)
- una **contraddizione** → codice che non verrà mai eseguito
- una **contingenza** → condizione reale che dipende dai dati

📌 Nei circuiti digitali:

- la tavola di verità descrive **esattamente** il comportamento del circuito

---

## 9. Idea chiave da ricordare 🧠✨

👉 Le tavole di verità:

- rendono la logica **oggettiva**
- eliminano ambiguità
- permettono di dimostrare se una formula è vera:
  - **sempre**
  - **mai**
  - **solo in alcuni casi**

Senza tavole di verità:
❌ non esiste una verifica logica rigorosa.
