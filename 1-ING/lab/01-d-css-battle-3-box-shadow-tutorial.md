

# Esercizio CSS Battle: Cerchi Concentrici con `box-shadow`

In questo esercizio useremo il sito CSS Battle per imparare a creare **cerchi concentrici** utilizzando la proprietà **CSS `box-shadow`**.

## Come iniziare

1. Apri la pagina:
   👉 [https://cssbattle.dev/play/3](https://cssbattle.dev/play/3)

2. Tieni premuto **CTRL** mentre clicchi sul link per aprirlo in una nuova scheda.

3. In questo modo potrai:

   * vedere il **target** da replicare
   * scrivere il codice nell’editor contemporaneamente

---

## Codice di partenza

Copia questo codice nell’editor:

```html
<div></div>
<style>
  div {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background: #f7c2b5;
    box-shadow:
      0 0 0 15px #f5a3b8,
      0 0 0 30px #9fcac0;
  }
</style>
```

---

## Cos’è `box-shadow`?

La proprietà `box-shadow` serve normalmente per aggiungere **ombre** agli elementi.

👉 In questo esercizio la useremo in modo creativo per creare **cerchi concentrici**.

### Sintassi base

```css
box-shadow: offset-x offset-y blur spread color;
```

Nel nostro caso:

```css
0 0 0 15px #f5a3b8
```

Significa:

* `0 0` → nessuno spostamento (l’ombra è centrata)
* `0` → nessun blur (bordi netti)
* `15px` → espansione → crea un “anello”
* `#f5a3b8` → colore

### Più cerchi

Puoi aggiungere più cerchi separando con una virgola:

```css
box-shadow:
  0 0 0 15px color1,
  0 0 0 30px color2;
```

👉 Ogni riga aggiunge un cerchio più grande.

---

## Spostare il cerchio al centro

Per posizionare il cerchio al centro dello schermo puoi usare:

```css
position: absolute;
top: 50px;
left: 50px;
```

Oppure regolare i valori finché non combaciano con il target.

---

## Aggiungere un rettangolo dietro

Ora aggiungiamo un elemento che sta **sotto il cerchio**.

### Step 1: aggiungi un nuovo div

```html
<div id="rect"></div>
<div id="circle"></div>
```

### Step 2: stile

```css
#rect {
  ...
}

#circle {
  ...
}
```

👉 Il cerchio appare sopra perché viene dichiarato dopo (ordine nel DOM).

---

## Obiettivo finale

* Usare **solo `box-shadow`** per creare cerchi concentrici
* Posizionare gli elementi con `position: absolute`
* Combinare più forme (cerchio + rettangolo)

---

## Suggerimenti

* Pensa ai cerchi come livelli concentrici che crescono
* Usa valori crescenti (15px, 30px, 45px…)
* Gioca con i colori per replicare il target
* L’ordine degli elementi influisce su cosa sta sopra o sotto

