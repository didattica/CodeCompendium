
# CSS Battle n.2 - Soluzione, Spiegazione e Domande

Questo documento serve per:

1. Mostrare **una possibile soluzione** dell’esercizio https://cssbattle.dev/play/2 .
2. Spiegare **i concetti di base di HTML e CSS** usati.
3. Proporre **domande di teoria**.

Gli studenti devono **copiare le domande sul quaderno e rispondere con frasi complete**.

---

# 1. Soluzione

Una possibile soluzione di https://cssbattle.dev/play/2 consiste nell’aggiungere il quarto `div` e posizionare i quadrati con valori diversi di `top` e `left`.

```html
<div id="a"></div>
<div id="b"></div>
<div id="c"></div>
<div id="d"></div>

<style>
body {
  background: #fdc57b;
}

#a, #b, #c, #d {
  width: 50px;
  height: 50px;
  position: absolute;
}

#a {
  background: red;
  top: 0;
  left: 0;
}

#b {
  background: blue;
  top: 0;
  left: 100px;
}

#c {
  background: green;
  top: 100px;
  left: 0;
}

#d {
  background: purple;
  top: 100px;
  left: 100px;
}
</style>
````

In questo modo i quattro quadrati formano una **figura 2 × 2**.

---

# 2. Spiegazione

## Il linguaggio HTML

HTML è il linguaggio usato per **strutturare una pagina web**.

Con HTML possiamo creare elementi come:

* titoli
* paragrafi
* immagini
* contenitori

Uno dei contenitori più usati è il **tag `div`**.

Esempio:

```html
<div></div>
```

Un `div` è un **contenitore vuoto** che possiamo riempire o modificare con il CSS.

---

## Il linguaggio CSS

CSS è il linguaggio che serve per **cambiare l’aspetto grafico** della pagina.

Con il CSS possiamo modificare:

* colori
* dimensioni
* posizione
* sfondi

Esempio:

```css
#a {
  background: red;
}
```

Questo codice cambia il colore di sfondo dell’elemento.

---

## Gli ID

In HTML possiamo dare un **nome unico** a un elemento usando `id`.

Esempio:

```html
<div id="a"></div>
```

Nel CSS possiamo selezionarlo usando `#`.

```css
#a {
  background: red;
}
```

---

## Dimensione degli elementi

La dimensione di un elemento si controlla con:

```css
width
height
```

Esempio:

```css
width: 50px;
height: 50px;
```

Questo crea un quadrato largo **50 pixel** e alto **50 pixel**.

---

## Colore di sfondo

Per cambiare colore si usa:

```css
background
```

Esempio:

```css
background: blue;
```

---

# 3. Domande di teoria (da copiare sul quaderno)

Copia le domande sul quaderno e rispondi con una frase completa.

---

### Domanda 1

Che cos'è **HTML**?

---

### Domanda 2

A cosa serve il linguaggio **CSS**?

---

### Domanda 3

Che cos'è un **tag `div`**?

---

### Domanda 4

A cosa serve la proprietà CSS:

```
background
```

---

### Domanda 5

Quali proprietà CSS servono per definire la **dimensione di un elemento**?

---

### Domanda 6

Che cosa rappresenta un **id** in HTML?

---

### Domanda 7

Come si seleziona un elemento con `id` nel CSS?

Scrivi un esempio.

---

### Domanda 8

Nel codice seguente:

```css
#a {
  background: red;
}
```

che cosa fa questo codice?

---

### Domanda 9

Se un elemento ha:

```
width: 50px
height: 50px
```

che forma ha?


