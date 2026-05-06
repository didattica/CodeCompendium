
# Python — Native Data Structures · Exercises
## `python_native_data_structures_exercises.md`

> **Obiettivo:** Padroneggiare la scelta e l'uso di tuple, dizionari e set.
> **Difficoltà:** Crescente (da base a intermedio-avanzato).

---

## Esercizio 1: Geometria Immutabile (Livello: Principiante)

**Traccia:**
Definisci due punti nel piano $\mathbb{R}^2$ come tuple: $A = (3, 4)$ e $B = (0, 0)$. 
1. Calcola la distanza euclidea tra i due punti usando la formula: 
   $$d = \sqrt{(x_A - x_B)^2 + (y_A - y_B)^2}$$
2. Prova a modificare la coordinata $x$ del punto $A$ portandola a $10$. Cosa succede?

> [!TIP]
> Per la radice quadrata puoi usare `math.sqrt()` oppure l'elevamento a potenza `** 0.5`.

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
import math

A = (3, 4)
B = (0, 0)

# 1. Calcolo distanza
distanza = math.sqrt((A[0] - B[0])**2 + (A[1] - B[1])**2)
print(f"Distanza: {distanza}") # Output: 5.0

# 2. Tentativo di modifica
try:
    A[0] = 10
except TypeError as e:
    print(f"Errore previsto: {e}")
```

**Spiegazione Teorica:**
Le tuple sono perfette per modellare concetti matematici come i vettori in $\mathbb{R}^n$ perché sono **immutabili**. Se un punto cambia coordinata, non è più "quel" punto, ma un nuovo oggetto matematico. L'errore `TypeError` garantisce l'integrità dei dati nel tempo.
</details>

---

## Esercizio 2: Il Set come Filtro (Livello: Principiante)

**Traccia:**
Hai una lista di numeri che rappresenta i risultati di un esperimento: `campione = [1, 2, 2, 3, 4, 4, 4, 5, 1, 6]`.
1. Ottieni una collezione di soli valori distinti.
2. Verifica se il numero `7` è presente nel campione in tempo $O(1)$.

> [!NOTE]
> Ricorda che la conversione da `list` a `set` ha un costo di $O(n)$, ma rende ogni ricerca successiva istantanea.

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
campione = [1, 2, 2, 3, 4, 4, 4, 5, 1, 6]

# 1. Valori distinti
distinti = set(campione)
print(f"Insieme A: {distinti}") # {1, 2, 3, 4, 5, 6}

# 2. Ricerca efficiente
print(7 in distinti) # False
```

**Spiegazione Teorica:**
In matematica, un insieme non ammette duplicati ($\{1,1\} = \{1\}$). Python usa le **Hash Table** per implementare i set: questo significa che non deve scorrere tutta la lista per trovare un numero, ma "calcola" direttamente la sua posizione in memoria.
</details>


### ⚡ Analisi delle Performance: List vs Set

Questo esperimento dimostra la differenza computazionale tra la ricerca in una **Lista** ($O(n)$) e in un **Set** ($O(1)$) utilizzando il modulo `time.perf_counter()`.

#### 🧪 Il Codice

Ho raggruppato la logica in una funzione `measure_time` per rendere il codice più pulito e modulare.
```python
import time

def measure_time(container, element, label):
    start = time.perf_counter()
    _ = element in container
    end = time.perf_counter()
    tempo = end - start
    print(f"{label:<20} | Completata in: {tempo:.8f}s")
    return tempo

# Configurazione test
GRANDEZZA = 10_000_000
target = -1  # Caso peggiore: elemento non presente

# Preparazione dati
campione_list = list(range(GRANDEZZA))
campione_set = set(campione_list)

print(f"Test su {GRANDEZZA:,} elementi:\n" + "-"*45)

# Esecuzione test
t_list = measure_time(campione_list, target, "Ricerca in Lista")
t_set = measure_time(campione_set, target, "Ricerca in Set")

# Risultato finale
print("-"*45)
print(f"🚀 Il Set è circa {int(t_list/t_set):,} volte più veloce!")
```

#### 📉 Analisi Tecnica



##### 1. Lista: Ricerca Lineare $O(n)$
Nella lista, Python deve controllare ogni elemento uno per uno partendo dall'inizio. 
- **Tempo:** Cresce proporzionalmente al numero di elementi.
- **Operazione:** "Sei tu l'elemento? No. E tu? No..." fino alla fine.

##### 2. Set: Hash Look-up $O(1)$
Il Set utilizza una **Hash Table**. Python calcola l'hash del valore cercato e "salta" direttamente all'indirizzo di memoria corrispondente.
- **Tempo:** Costante. Non importa se ci sono 10 o 10 milioni di elementi, l'accesso richiede sempre un singolo calcolo.
- **Operazione:** Calcolo Hash -> Accesso diretto alla cella.

> [!IMPORTANT]
> Sebbene il Set sia infinitamente più veloce nella ricerca, ricorda che la sua creazione (`set(lista)`) richiede tempo e memoria aggiuntiva. È una strategia vincente quando devi effettuare **molteplici ricerche** sulla stessa collezione di dati.


---

## Esercizio 3: Algebra degli Insiemi (Livello: Intermedio)

**Traccia:**
Siano $A$ l'insieme dei numeri pari tra 1 e 20 e $B$ l'insieme dei multipli di 3 tra 1 e 20.
Utilizzando i `set` di Python e le *set comprehension*:
1. Rappresenta $A$ e $B$.
2. Calcola $C = A \cap B$ (intersezione).
3. Calcola $D = A \triangle B$ (differenza simmetrica).

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
A = {x for x in range(1, 21) if x % 2 == 0}
B = {x for x in range(1, 21) if x % 3 == 0}

print(f"A (Pari): {A}")
print(f"B (Mult. 3): {B}")

# Intersezione (numeri pari E multipli di 3, ovvero multipli di 6)
intersezione = A & B 
print(f"A ∩ B: {intersezione}")

# Differenza simmetrica (numeri che sono solo in A o solo in B)
diff_simm = A ^ B
print(f"A △ B: {diff_simm}")
```

**Spiegazione Teorica:**
L'operatore `&` corrisponde al connettivo logico `AND`, mentre `^` corrisponde allo `XOR`. Notate come il codice Python sia quasi una trascrizione diretta della simbologia matematica.
</details>

---

## Esercizio 4: Dizionario come Funzione (Livello: Intermedio)

**Traccia:**
Data una stringa `testo = "scienza delle costruzioni"`, crea un dizionario che rappresenti la **frequenza** di ogni carattere (escluso lo spazio).
Esempio: `{'s': 2, 'c': 2, ...}`.

> [!IMPORTANT]
> Questo esercizio modella una funzione $f: \text{Carattere} \to \mathbb{N}$ (frequenza).

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
testo = "scienza delle costruzioni"
frequenze = {}

for char in testo:
    if char == " ": 
        continue
    # Usiamo .get() per gestire il caso in cui la chiave non esista ancora
    frequenze[char] = frequenze.get(char, 0) + 1

print(frequenze)
```

**Spiegazione Teorica:**
L'uso di `.get(char, 0)` è una tecnica fondamentale. Matematicamente, stiamo definendo una funzione parziale e la stiamo estendendo su tutto il dominio dei caratteri possibili, assegnando valore $0$ a quelli non ancora incontrati.
</details>

---

## Esercizio 5: Slicing e Proiezioni (Livello: Intermedio)

**Traccia:**
Data la sequenza $S = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)$:
1. Estrai la sottosequenza dei numeri nelle posizioni dispari (indice 1, 3, ...).
2. Inverti la sequenza originale usando lo slicing.
3. Ottieni gli ultimi 3 elementi.

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
S = tuple(range(10))

# 1. Indici dispari (start=1, stop=default, step=2)
dispari = S[1::2]
print(f"Indici dispari: {dispari}") # (1, 3, 5, 7, 9)

# 2. Inversione
inversa = S[::-1]
print(f"Inversa: {inversa}")

# 3. Ultimi tre
ultimi = S[-3:]
print(f"Ultimi tre: {ultimi}")
```
</details>

---

## Esercizio 6: Strutture Composte e Lookup (Livello: Avanzato)

**Traccia:**
Immagina di dover gestire un database di studenti. Ogni studente è identificato da una matricola (univoca). Per ogni studente vogliamo memorizzare: Nome, Cognome e un Insieme di esami superati.

1. Crea una struttura dati `database` con 3 studenti.
2. Scrivi una funzione `ha_superato(matricola, esame)` che restituisca un booleano in tempo $O(1)$ (assumendo di conoscere la matricola).
3. Aggiungi l'esame "Analisi 1" allo studente con matricola `101`.

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
# Struttura: Dict[int, Dict] -> all'interno del valore usiamo un Set per gli esami
database = {
    101: {"nome": "Mario", "cognome": "Rossi", "esami": {"Fisica", "Chimica"}},
    102: {"nome": "Anna", "cognome": "Verdi", "esami": {"Algebra"}},
    103: {"nome": "Luca", "cognome": "Blu", "esami": set()}
}

def ha_superato(matricola, esame):
    # O(1) per il dict delle matricole + O(1) per il set degli esami
    studente = database.get(matricola)
    if studente:
        return esame in studente["esami"]
    return False

# 3. Aggiunta esame
database[101]["esami"].add("Analisi 1")

print(f"Mario ha superato Analisi 1? {ha_superato(101, 'Analisi 1')}")
```

**Spiegazione Teorica:**
Questa è una **struttura dati composta**. La combinazione di `dict` e `set` permette di scalare su milioni di record mantenendo le prestazioni quasi istantanee. Se avessimo usato una lista di liste, controllare un esame avrebbe richiesto di scorrere tutti gli studenti E tutti i loro esami ($O(N \cdot M)$).
</details>

---

> [!TIP]
> **Sfida per casa:** Prova a modificare l'Esercizio 6 in modo che il database possa restituire rapidamente tutti gli studenti che hanno superato un determinato esame. Quale nuova struttura dati dovresti creare per rendere questa ricerca $O(1)$? (Suggerimento: Inversione della funzione).
