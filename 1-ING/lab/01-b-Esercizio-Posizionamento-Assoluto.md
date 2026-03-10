# Esercizio CSS Battle: Posizionamento Assoluto con 4 Div

In questo esercizio useremo il sito [CSS Battle](https://cssbattle.dev/play/2) per imparare a posizionare elementi HTML usando **CSS**.  

## Obiettivo

Partiamo dal seguente codice di base:

```html
<div id="a"></div>
<div id="b"></div>
<div id="c"></div>

<style>
  body {
    background: #fdc57b;
  }
  #a, #b, #c {
    width: 50px;
    height: 50px;
    position: absolute; /* li posizioniamo nello schermo */
  }
  /* Colori diversi per distinguerli */
  #a { background: red; top: 0; left: 0; }
  #b { background: blue; top: 0; left: 100px; }
  #c { background: green; top: 0; left: 200px; }
</style>
````

### Cosa vedrai

* Tre quadrati colorati:

  * **rosso** (#a) a sinistra
  * **blu** (#b) al centro
  * **verde** (#c) a destra

* I quadrati sono posizionati usando `position: absolute` rispetto al **body**.

### Come funziona `top` e `left`

* `top` indica la distanza tra il bordo superiore del quadrato e il bordo superiore del contenitore (body).
* `left` indica la distanza tra il bordo sinistro del quadrato e il bordo sinistro del contenitore.

> Pensa a un **sistema di coordinate** come in matematica:
>
> * l'angolo in alto a sinistra è `(0, 0)`
> * `top` è simile alla coordinata **y**
> * `left` è simile alla coordinata **x**

### Esercizio aggiornato

1. Aggiungi un **quarto div**:

```html
<div id="d"></div>
```

2. Modifica i div in modo da replicare il target:

   * Cambia **colore** dei div se necessario.
   * Modifica le **coordinate `top` e `left`** per posizionarli correttamente.
3. Copia il codice nel [CSS Battle Editor](https://cssbattle.dev/play/2) e osserva il risultato.
4. L’obiettivo è replicare l’immagine target usando **solo questi quattro div**.

### Suggerimento

* Usa valori numerici di `top` e `left` per posizionare ciascun quadrato.
* Ricorda il concetto di coordinate: l’altezza (`top`) aumenta scendendo verso il basso, e la larghezza (`left`) aumenta spostandosi verso destra.


```
