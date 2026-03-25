

# Creare angoli arrotondati negli elementi HTML con CSS

## Introduzione

In questa guida vedremo come creare **angoli arrotondati** negli elementi HTML usando CSS, prendendo come esempio una soluzione tratta da CSSBattle.

L’obiettivo è costruire una figura composta da tre blocchi con alcune parti arrotondate.

---

## Il codice di partenza

```html
<div id="centro"></div>
<div id="destra"></div>
<div id="sinistra"></div>

<style>
  body {
    background: #62306D;
  }
  div#centro {
    position: absolute;
    top: 50px;
    left: 150px;
    width: 100px;
    height: 100px;
    background: #F7EC7D;
    border-radius: 50px 50px 0 0;
  }
  div#destra {
    position: absolute;
    top: 150px;
    left: 50px;
    width: 100px;
    height: 100px;
    background: #F7EC7D;
    border-radius: 0 0 50px 50px;
  }
  div#sinistra {
    position: absolute;
    top: 150px;
    left: 250px;
    width: 100px;
    height: 100px;
    background: #F7EC7D;
    border-radius: 0 0 50px 50px;
  }
</style>
```

---

## Struttura HTML

Abbiamo tre elementi `<div>`:

* `centro`
* `destra`
* `sinistra`

Questi rappresentano tre blocchi che verranno posizionati manualmente nella pagina.

---

## Sfondo della pagina

```css
body {
  background: #62306D;
}
```

Serve semplicemente a impostare il colore di sfondo viola.

---

## Posizionamento degli elementi

Tutti i div usano:

```css
position: absolute;
```

Questo significa che possiamo posizionarli liberamente usando:

* `top` → distanza dall’alto
* `left` → distanza da sinistra

Esempio:

```css
top: 50px;
left: 150px;
```

---

## Dimensioni e colore

Ogni blocco ha:

```css
width: 100px;
height: 100px;
background: #F7EC7D;
```

Quindi sono quadrati gialli di 100x100 pixel.

---

## Il concetto chiave: `border-radius`

La proprietà più importante è:

```css
border-radius
```

Serve per arrotondare gli angoli.

---

## Come funziona `border-radius`

Può avere **4 valori**, uno per ogni angolo:

```css
border-radius: alto-sinistra alto-destra basso-destra basso-sinistra;
```

---

## Analisi dei tre elementi

### 1. Blocco centrale

```css
border-radius: 50px 50px 0 0;
```

Significa:

* alto sinistra → arrotondato
* alto destra → arrotondato
* basso destra → non arrotondato
* basso sinistra → non arrotondato

👉 Risultato: forma con la parte superiore arrotondata.

---

### 2. Blocco destro

```css
border-radius: 0 0 50px 50px;
```

Significa:

* alto sinistra → non arrotondato
* alto destra → non arrotondato
* basso destra → arrotondato
* basso sinistra → arrotondato

👉 Risultato: parte inferiore arrotondata.

---

### 3. Blocco sinistro

È identico al blocco destro:

```css
border-radius: 0 0 50px 50px;
```

👉 Anche qui abbiamo la parte inferiore arrotondata.

---

## Effetto finale

Combinando i tre blocchi:

* uno sopra con curva verso l’alto
* due sotto con curve verso il basso

si crea una figura simmetrica.

---

## Riassunto

* `border-radius` permette di arrotondare gli angoli
* puoi controllare ogni angolo separatamente
* valori alti (es. 50px su un box da 100px) creano forme semicircolari
* combinando più elementi puoi creare figure complesse

---

## Esercizi (da copiare sul quaderno)

Rispondi alle seguenti domande scrivendo sia la domanda che la risposta:

1. Cos’è la proprietà `border-radius` e a cosa serve?
2. Cosa succede se uso `border-radius: 50px 50px 0 0;`?
3. Come posso creare un cerchio perfetto usando `border-radius`?
