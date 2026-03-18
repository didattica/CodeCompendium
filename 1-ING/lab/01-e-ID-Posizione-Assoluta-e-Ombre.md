# Approfondimento CSS: ID, Posizione Assoluta e Ombre

In questa seconda parte approfondiamo alcune proprietà fondamentali del CSS per controllare **posizione e stile visivo**.

---

## Selettore `id`

Un `id` identifica **un solo elemento** nella pagina.

```html id="1b3g7k"
<div id="box"></div>
```

```css id="z9s1od"
#box {
  width: 100px;
  height: 100px;
  background: red;
}
```

👉 Caratteristiche:

* Unico nella pagina
* Si usa con `#`
* Ha priorità alta rispetto ad altri selettori

---

## `position: absolute`

La proprietà `position: absolute` serve per posizionare un elemento **in modo preciso** nella pagina.

```css id="l5q8jm"
div {
  position: absolute;
  top: 50px;
  left: 100px;
}
```

👉 Significa:

* L’elemento viene posizionato usando coordinate
* `top` → distanza dall’alto
* `left` → distanza da sinistra

---

### Come funziona

Un elemento con `position: absolute`:

* Esce dal flusso normale della pagina
* Non influenza gli altri elementi
* Si posiziona rispetto al contenitore padre (se presente)

---

### Esempio pratico

```html id="q8d2k1"
<div id="box"></div>
```

```css id="5n8x2p"

#box {
  position: absolute;
  top: 20px;
  left: 40px;
  width: 50px;
  height: 50px;
  background: blue;
}
```

👉 Il quadrato blu viene posizionato **dentro il contenitore**.

---

## Proprietà di posizionamento

Funzionano con `position: absolute`:

```css id="3u2k6s"
top
left
right
bottom
```

Esempio:

```css id="m9r4te"
div {
  position: absolute;
  bottom: 10px;
  right: 20px;
}
```

👉 In questo caso l’elemento si posiziona in basso a destra.

---

## Approfondimento `box-shadow`

`box-shadow` permette di creare effetti visivi come ombre e forme.

---

### Ombra base

```css id="2xv9jw"
box-shadow: 10px 10px 20px rgba(0,0,0,0.3);
```

👉 Significa:

* `10px` → spostamento orizzontale
* `10px` → spostamento verticale
* `20px` → sfocatura
* colore → ombra

---

### Più ombre

```css id="8c2v6y"
box-shadow:
  0 0 10px red,
  0 0 20px blue;
```

👉 Puoi combinare più effetti.

---

## Esercizi (senza soluzione)

Rispondi alle seguenti domande:

1. A cosa serve un `id` in CSS?
2. Cosa fa `position: absolute`?
3. A cosa servono le proprietà `top` e `left`?
4. Come si crea un’ombra interna con `box-shadow`?
5. Cosa rappresentano i primi due valori in `box-shadow`?

---

## Obiettivo di questa parte

Dopo questo modulo dovresti essere in grado di:

* Usare correttamente gli `id`
* Posizionare elementi con `position: absolute`
* Creare effetti visivi con `box-shadow`

---

Se vuoi, posso anche trasformarlo in **scheda stampabile per verifica** 👍
