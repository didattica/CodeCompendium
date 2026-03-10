# Spiegazione della Soluzione – CSSBattle #1

Questo documento spiega in modo semplice la soluzione del seguente esercizio:

[https://cssbattle.dev/play/1](https://cssbattle.dev/play/1)

Codice soluzione:

```html
<div></div>
<style>
  body {
    background: #5d3a3a;
    margin: 0px;
  }
  div {
    width: 200px;
    height: 200px;
    background: #b5e0ba;
  }
</style>
```

---

# 1️⃣ Prima idea: cosa stiamo facendo?

Stiamo costruendo una pagina web molto semplice.

Immagina una pagina web come un foglio bianco.
Dentro questo foglio possiamo mettere degli "oggetti".
In questo caso mettiamo solo un quadrato.

---

# 2️⃣ Cos’è `<div>`?

```html
<div></div>
```

Un `div` è come una scatola vuota.

Pensa a una scatola di cartone:

* all’inizio è vuota
* non ha colore
* non ha dimensione

Con il CSS noi decidiamo:

* quanto è grande la scatola
* che colore ha
* dove si trova

---

# 3️⃣ Cos’è `<style>`?

```html
<style>
  ...
</style>
```

La parte `<style>` contiene le regole di stile.

Se HTML è la struttura (le scatole),
CSS è la parte estetica (colori, grandezze, posizione).

È come dire:

* HTML = scheletro
* CSS = vestiti e aspetto

---

# 4️⃣ Il `body`

```css
body {
  background: #5d3a3a;
  margin: 0px;
}
```

Il `body` è tutto il foglio della pagina.

Immagina il body come il tavolo su cui appoggi le scatole.

## 🔹 background

```css
background: #5d3a3a;
```

`background` significa colore di sfondo.

Qui stiamo dicendo:

"Colora tutto il foglio di marrone scuro."

Il valore `#5d3a3a` è un colore espresso in formato esadecimale.
Non è importante sapere ora come funziona: è semplicemente un codice colore.

---

## 🔹 margin

```css
margin: 0px;
```

Il `margin` è lo spazio esterno.

Immagina una cornice invisibile attorno al foglio.

Di default, il browser mette un piccolo spazio attorno alla pagina.
Se non lo togliamo, vedremmo un bordo chiaro attorno al colore.

Con:

```css
margin: 0px;
```

stiamo dicendo:

"Non lasciare nessuno spazio. Voglio che il colore arrivi fino ai bordi della pagina."

È come dire: niente distanza tra il foglio e il bordo dello schermo.

---

# 5️⃣ Il `div`

```css
div {
  width: 200px;
  height: 200px;
  background: #b5e0ba;
}
```

Qui stiamo modificando la scatola che abbiamo creato prima.

---

## 🔹 width

```css
width: 200px;
```

`width` significa larghezza.

Stiamo dicendo:

"La scatola deve essere larga 200 pixel."

Un pixel è una piccola unità dello schermo.

---

## 🔹 height

```css
height: 200px;
```

`height` significa altezza.

Quindi la scatola è:

* 200 pixel di larghezza
* 200 pixel di altezza

Se larghezza e altezza sono uguali → otteniamo un quadrato.

---

## 🔹 background (del div)

```css
background: #b5e0ba;
```

Qui coloriamo solo la scatola.

Il foglio è marrone scuro.
La scatola sopra è verde chiaro.

---

# 6️⃣ Perché il quadrato è in alto a sinistra?

Perché non abbiamo specificato nessuna posizione.

Quando non diciamo dove mettere un elemento,
il browser lo mette automaticamente:

* in alto
* a sinistra
* nel primo spazio disponibile

È il comportamento di default.

---

# 7️⃣ Riassunto logico

Abbiamo fatto 4 cose:

1. Creato una scatola (`div`)
2. Colorato il foglio (`body background`)
3. Tolto lo spazio automatico (`margin: 0`)
4. Dato dimensione e colore alla scatola (`width`, `height`, `background`)

Tutto qui.

---

# 8️⃣ Concetto chiave da ricordare

HTML crea gli oggetti.
CSS decide come appaiono.

Se pensi in modo logico:

Struttura → poi Stile.

Prima costruisci la scatola.
Poi la dipingi e le dai dimensione.

---

