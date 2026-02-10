# Shift nei sistemi di numerazione

## Cos’è lo shift
Lo **shift** è un’operazione che consiste nello spostare tutte le cifre di un numero verso **sinistra** o verso **destra** di una o più posizioni.  
Lo shift è strettamente legato alle **moltiplicazioni e divisioni per la base** del sistema di numerazione.

---

## Shift a sinistra (moltiplicazione)
Lo **shift a sinistra** equivale a una **moltiplicazione per la base** del sistema.

Ogni posizione spostata a sinistra moltiplica il numero per:
- **2** nel sistema binario  
- **10** nel sistema decimale  
- **16** nel sistema esadecimale  

Se lo shift è di più posizioni, la moltiplicazione avviene per una potenza della base.

### Esempi
- Binario:  
  `1011₂ << 1 = 10110₂`  (×2)  
  `1011₂ << 2 = 101100₂` (×4)

- Decimale:  
  `123 << 1 = 1230`  (×10)  
  `123 << 2 = 12300` (×100)

- Esadecimale:  
  `A3₁₆ << 1 = A30₁₆`  (×16)  
  `A3₁₆ << 2 = A300₁₆` (×256)

---

## Shift a destra (divisione)
Lo **shift a destra** equivale a una **divisione per la base** del sistema.

Ogni posizione spostata a destra divide il numero per:
- **2** nel sistema binario  
- **10** nel sistema decimale  
- **16** nel sistema esadecimale  

Le cifre che escono a destra vengono **scartate** (divisione intera).

### Esempi
- Binario:  
  `11010₂ >> 1 = 1101₂`  (÷2)  
  `11010₂ >> 2 = 110₂`   (÷4)

- Decimale:  
  `456 >> 1 = 45`   (÷10)  
  `456 >> 2 = 4`    (÷100)

- Esadecimale:  
  `7C₁₆ >> 1 = 7₁₆`  (÷16)  
  `7C₁₆ >> 2 = 0₁₆`  (÷256)

---

## Riepilogo
- Shift a sinistra → **moltiplicazione per la base**
- Shift a destra → **divisione per la base**
- Lo shift può essere di **una o più posizioni**
- Il valore cambia secondo una **potenza della base**
