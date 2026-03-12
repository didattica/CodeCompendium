
# Python Objects, Classes, and Types – Visual Guide with Metaphors

This guide explains **variables, objects, classes, and types** in Python using **simple diagrams** and **easy-to-remember metaphors**.

---

## 1. Key Metaphors

| Concept      | Metaphor                                                      |
| ------------ | ------------------------------------------------------------- |
| **Class**    | Stampino / progetto / blueprint                               |
| **Object**   | Oggetto creato dallo stampino / casa costruita dal progetto   |
| **Variable** | Etichetta o nome che punta all’oggetto                        |
| **Type**     | Classe delle classi / metaclasse (lo stampino dello stampino) |

---

## 2. Example: Integer

Python code:

```python
a = 2
```

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

---

## 8. Built-in Classes in Python

Python has many built-in classes and exceptions. To see **only the classes**, you can filter `__builtins__`:

```python
# List all built-in classes
builtin_classes = [name for name in dir(__builtins__) if isinstance(getattr(__builtins__, name), type)]
print(builtin_classes)
```

Example output:

```text
['bool', 'bytearray', 'bytes', 'complex', 'dict', 'float', 'frozenset', 'int', 'list', 'object', 'range', 'set', 'str', 'tuple', 'type', 'Exception', 'ValueError', 'TypeError', ...]
```

Notes:

* Includes **basic types** (`int`, `str`, `list`, etc.)
* Includes **exceptions** (`Exception`, `ValueError`, `ZeroDivisionError`, etc.)
* All of these are **instances of `type`**, the universal metaclass.

---

## 9. Special Focus: `type`

`type` is **special in Python**:

1. **Metaclass of all classes**
   Every class you define (`int`, `Dog`, `MyClass`) is an **instance of `type`**.

2. **Itself an object**
   In Python, `type` is also an **object**. That means:

   ```python
   print(type(int))  # <class 'type'>
   print(type(Dog))  # <class 'type'>
   print(type(type)) # <class 'type'>  <- auto-referenziale!
   ```

3. **Why this is powerful**

   * `type` unifica Python: classi e oggetti seguono lo stesso schema.
   * Puoi creare classi dinamicamente usando `type(name, bases, dict)`.

**Diagram:**

```text
object (2, d1) ──> class (int, Dog)
class ──> type  (stampino supremo)
type ──> type  (auto-referenziale)
```

---

## 10. Python Objects, Classes, and Type – Visual Diagram

```mermaid
flowchart TD
    %% Oggetti concreti
    A[Variable: a<br/>etichetta] --> B[Object: 2<br/>oggetto concreto]
    C[Variable: d1<br/>etichetta] --> D[Object: d1<br/>oggetto Dog]

    %% Classi
    B --> E[Class: int<br/>stampino dei numeri interi]
    D --> F[Class: Dog<br/>stampino del cane]

    %% Metaclasse universale
    E --> G[Metaclass: type<br/>stampino supremo delle classi]
    F --> G
    G --> G[auto-referenziale<br/>type è classe e oggetto allo stesso tempo]

    %% Stile
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#9f9,stroke:#333,stroke-width:2px
    style C fill:#f9f,stroke:#333,stroke-width:2px
    style D fill:#9f9,stroke:#333,stroke-width:2px
    style E fill:#9cf,stroke:#333,stroke-width:2px
    style F fill:#9cf,stroke:#333,stroke-width:2px
    style G fill:#fc9,stroke:#333,stroke-width:2px
```

---

### Metafore intuitive

| Concetto | Metafora                                                              |
| -------- | --------------------------------------------------------------------- |
| Variable | Etichetta sul tavolo che punta a un oggetto                           |
| Object   | Oggetto concreto costruito con uno stampino                           |
| Class    | Stampino / blueprint che definisce come creare oggetti                |
| Type     | Stampino supremo delle classi, **classe e oggetto allo stesso tempo** |

---

### Spiegazione passo passo

1. **Oggetti concreti** (`2`, `d1`) → istanze di classi (`int`, `Dog`)
2. **Classi** → istanze di `type`
3. **Metaclasse `type`** → auto-referenziale, chiude il ciclo
4. Tutto il sistema è coerente e permette a Python di trattare **classi come oggetti**, rendendo tutto uniforme
