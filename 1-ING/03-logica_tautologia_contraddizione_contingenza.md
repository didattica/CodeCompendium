# Lezione 3 – Tautologia, Contraddizione e Contingenza 🧠⚙️

---

## 1. Perché questi concetti sono importanti in informatica 💻🤔

In **informatica**, i computer prendono decisioni usando la **logica**.

Ogni volta che un programma usa:

* `if`
* `else`
* condizioni
* confronti

sta valutando una **proposizione logica** che può essere:

* **vera**
* **falsa**

📌 Le proposizioni logiche possono essere di **tre tipi fondamentali**:

* **tautologia**
* **contraddizione**
* **contingenza**

Capire queste differenze aiuta a scrivere:

* programmi più **corretti** ✅
* codice più **semplice** ✨
* software più **efficiente** ⚡

---

## 2. Tautologia 🔁✔️

### Cos’è una tautologia

Una **tautologia** è una proposizione logica **sempre vera**,
in **qualsiasi situazione**.

📌 Non importa quali siano i valori delle variabili:
il risultato è **sempre true**.

---

### Origine della parola 📚

Dal greco:

* **tautó (ταὐτό)** = lo stesso
* **lógos (λόγος)** = discorso, affermazione

👉 *tautología* significa:

* “dire la stessa cosa”
* “ripetere lo stesso concetto”

---

### Forma tipica 🔍

* **A OR NOT A**

---

### Esempio semplice 🧩

> “O piove **oppure** non piove”

✔ Vera se piove
✔ Vera se non piove
➡️ **Sempre vera**

---

### In informatica 💡

Una tautologia in un programma:

* è un **controllo inutile**
* non cambia mai il risultato
* rende il codice più **complicato del necessario**

📌 Esempio concettuale:

```text
if (condizione OR NOT condizione)
```

➡️ Questa condizione è **sempre vera** → non serve controllarla.

---

## 3. Contraddizione ❌⚠️

### Cos’è una contraddizione

Una **contraddizione** è una proposizione logica
che **non può mai essere vera**.

📌 Il risultato è **sempre false**.

---

### Origine della parola 📚

Dal latino:

* **contra** = contro
* **dicere** = dire

👉 *contraddicere* = dire contro, dire l’opposto.

---

### Forma tipica 🔍

* **A AND NOT A**

---

### Esempio semplice 🚦

> “Piove **e** non piove nello stesso momento”

❌ Impossibile
➡️ **Sempre falsa**

---

### Metafora intuitiva 🟥🟩

> “Il semaforo è rosso **e** verde nello stesso istante”

❌ Non può accadere → contraddizione

---

### In informatica 💡

Una contraddizione indica:

* un **errore logico**
* una parte di codice che **non verrà mai eseguita**

📌 Esempio concettuale:

```text
if (x > 10 AND x < 5)
```

➡️ Non esiste nessun valore che soddisfa entrambe le condizioni.

---

## 4. Contingenza 🔄🎯

### Cos’è una contingenza

Una **contingenza** è una proposizione logica che:

* **a volte è vera**
* **a volte è falsa**

📌 Dipende dalla **situazione reale**.

---

### Origine della parola 📚

Dal latino:

* **contingere** = accadere, capitare

👉 Una cosa contingente è qualcosa che **può accadere oppure no**.

---

### Esempio quotidiano ☀️🌧️

> “Domani piove”

✔ Vera se piove
❌ Falsa se non piove
➡️ **Contingenza**

---

### Esempi semplici 🧠

* “Oggi ho fame”
* “Questo numero è pari”
* “Il semaforo è rosso”
* “Studio informatica”

Tutte queste frasi:

* non sono sempre vere
* non sono sempre false

➡️ **Contingenze**

---

### In informatica 💡

La contingenza è il **caso normale** nei programmi.

È ciò che permette di:

* prendere decisioni
* scegliere cosa fare

📌 Esempio tipico:

```text
if (passwordCorretta)
```

Qui la condizione:

* può essere vera
* può essere falsa

➡️ **Contingenza**

---

## 5. Confronto finale 🧩📊

| Tipo               | Risultato                      |
| ------------------ | ------------------------------ |
| **Tautologia**     | Sempre vera ✔️                 |
| **Contraddizione** | Sempre falsa ❌                 |
| **Contingenza**    | A volte vera, a volte falsa 🔄 |

---

## 6. Idea chiave da ricordare 🧠✨

👉 Nei programmi:

* una **tautologia** non serve
* una **contraddizione** è un errore
* una **contingenza** è ciò che fa funzionare le decisioni

Capire questi concetti significa:

* scrivere codice più **chiaro**
* evitare controlli inutili
* evitare parti di codice morte 🧟‍♂️
