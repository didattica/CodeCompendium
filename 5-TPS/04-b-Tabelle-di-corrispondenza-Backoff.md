

# Esercizi – Tabelle di corrispondenza (Backoff)

---

# 🧠 ESERCIZIO 1 – Livello base

## Dato

Tempo iniziale:

```
T0 = 1 secondo
```

Formula del backoff:

```
T(k) = T0 · 2^k
```

---

## Richiesta

Completare la tabella:

| Tentativo k | Tempo T(k) |
| ----------- | ---------- |
| 0           | ?          |
| 1           | ?          |
| 2           | ?          |
| 3           | ?          |
| 4           | ?          |

---

## Soluzione

Calcolo:

```
T(k) = 1 · 2^k
```

| Tentativo k | Calcolo | Tempo |
| ----------- | ------- | ----- |
| 0           | 1·2⁰    | 1 s   |
| 1           | 1·2¹    | 2 s   |
| 2           | 1·2²    | 4 s   |
| 3           | 1·2³    | 8 s   |
| 4           | 1·2⁴    | 16 s  |

---

# 🧠 ESERCIZIO 2 – Livello intermedio

## Dato

```
T0 = 500 ms
Tmax = 4000 ms
```

Formula:

```
T(k) = min(Tmax , T0 · 2^k)
```

---

## Richiesta

Completare la tabella dei tempi di attesa.

| Tentativo k | Tempo T(k) |
| ----------- | ---------- |
| 0           | ?          |
| 1           | ?          |
| 2           | ?          |
| 3           | ?          |
| 4           | ?          |
| 5           | ?          |

---

## Soluzione

Calcolo:

```
T(k) = min(4000 , 500 · 2^k)
```

| k | Calcolo                 | Tempo   |
| - | ----------------------- | ------- |
| 0 | 500·2⁰                  | 500 ms  |
| 1 | 500·2¹                  | 1000 ms |
| 2 | 500·2²                  | 2000 ms |
| 3 | 500·2³ = 4000           | 4000 ms |
| 4 | 500·2⁴ = 8000 → limite  | 4000 ms |
| 5 | 500·2⁵ = 16000 → limite | 4000 ms |

---

# 🧠 ESERCIZIO 3 – Livello avanzato

## Dato

```
T0 = 250 ms
Tmax = 8000 ms
```

Formula:

```
T(k) = min(Tmax , T0 · 2^k)
```

---

## Richiesta

1. Completare la tabella.
2. Indicare **a partire da quale tentativo si raggiunge il limite Tmax**.

| Tentativo k | Tempo T(k) |
| ----------- | ---------- |
| 0           | ?          |
| 1           | ?          |
| 2           | ?          |
| 3           | ?          |
| 4           | ?          |
| 5           | ?          |
| 6           | ?          |

---

## Soluzione

Calcolo:

```
T(k) = min(8000 , 250 · 2^k)
```

| k | Calcolo                 | Tempo   |
| - | ----------------------- | ------- |
| 0 | 250·2⁰                  | 250 ms  |
| 1 | 250·2¹                  | 500 ms  |
| 2 | 250·2²                  | 1000 ms |
| 3 | 250·2³                  | 2000 ms |
| 4 | 250·2⁴                  | 4000 ms |
| 5 | 250·2⁵ = 8000           | 8000 ms |
| 6 | 250·2⁶ = 16000 → limite | 8000 ms |

Limite raggiunto da:

```
k = 5
```
