
# Python Objects, Classes, and Types – Visual Guide with Metaphors

This guide explains **variables, objects, classes, and types** in Python using **simple diagrams** and **easy-to-remember metaphors**.

---

## 1. Key Metaphors

| Concept  | Metaphor |
|----------|----------|
| **Class** | Stampino / progetto / blueprint |
| **Object** | Oggetto creato dallo stampino / casa costruita dal progetto |
| **Variable** | Etichetta o nome che punta all’oggetto |
| **Type** | Classe delle classi / metaclasse (lo stampino dello stampino) |

---

## 2. Example: Integer

Python code:

```python
a = 2
````

Diagram:

```text
variable: a
     │
     ▼
   object: 2  ──── instance of ───► class: int (stampino dei numeri interi)
                               │
                               ▼
                           metaclass: type (stampino delle classi)
```

**Explanation:**

* `a` → variable, come un’etichetta che punta all’oggetto `2`
* `2` → object, è un’istanza della classe `int`
* `int` → class, lo stampino che definisce come è fatto un numero intero
* `type` → metaclass, lo stampino di tutti gli stampini

---

## 3. Example: Custom Class

Python code:

```python
class Dog:
    pass

d1 = Dog()
```

Diagram:

```text
variable: d1
     │
     ▼
   object: d1 ──── instance of ───► class: Dog (stampino di un cane)
                                   │
                                   ▼
                               metaclass: type (stampino delle classi)
```

**Metaphor Explanation:**

* `Dog` = classe = stampino del cane
* `d1` = object = cane costruito con quello stampino
* `d2 = Dog()` → nuovo cane, altro oggetto dello stesso stampino
* Tutte le classi derivano da `type`, il **meta-stampino**

---

## 4. General Concept Diagram

```text
variable (etichetta)
      │
      ▼
object (oggetto creato dallo stampino)
      │
      ▼
class (stampino / blueprint)
      │
      ▼
type (stampino delle classi)
```

---

## 5. Quick Summary

1. **Variable** → nome / etichetta che punta a un oggetto
2. **Object** → l’istanza concreta, ciò che esiste realmente in memoria
3. **Class** → modello / stampino per creare oggetti
4. **Type** → classe delle classi, lo stampino che definisce gli stampini

---

## 6. Student-Friendly Phrases

* “Una **class è lo stampino**, un object è l’oggetto costruito con quello stampino”
* “Una **variable è un’etichetta** che punta all’oggetto, non lo contiene”
* “Tutti gli oggetti hanno un **tipo**, che è la loro classe”
* “Anche le classi stesse sono oggetti, il loro tipo è `type`”

---

## 7. Example in Python with Types

```python
a = 2
print(type(a))   # <class 'int'>

d1 = Dog()
print(type(d1))  # <class '__main__.Dog'>

print(type(int)) # <class 'type'>
print(type(Dog)) # <class 'type'>
```


