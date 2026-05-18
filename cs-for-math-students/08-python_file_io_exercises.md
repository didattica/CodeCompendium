# Python — File I/O · Exercises
## `python_file_io_exercises.md`

> **Dataset:** `studenti_matematica.csv`
> **Obiettivo:** Leggere, analizzare e scrivere file CSV usando solo Python puro.
> **Difficoltà:** Crescente (da base a intermedio-avanzato).

---

## Esercizio 1: Prima lettura (Livello: Principiante)

**Traccia:**
Apri il file `studenti_matematica.csv` e stampa:
1. Il numero totale di righe nel file (intestazione inclusa).
2. La prima riga (l'intestazione).
3. L'ultima riga.

> [!TIP]
> Per l'ultima riga, `readlines()` ti restituisce una lista — come accedi all'ultimo elemento?

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
with open("studenti_matematica.csv", "r", encoding="utf-8") as f:
    righe = f.readlines()

print(f"Numero di righe: {len(righe)}")
print(f"Intestazione: {righe[0].strip()}")
print(f"Ultima riga:  {righe[-1].strip()}")
```

**Output atteso:**
```
Numero di righe: 11
Intestazione: matricola,nome,cognome,analisi,algebra,geometria
Ultima riga:  110,Luca,Ferrari,16,18,17
```

**Spiegazione:**
`readlines()` carica tutte le righe in una lista. L'accesso per indice (`[0]` e `[-1]`) è $O(1)$ sulla lista. `.strip()` rimuove il `\n` finale che altrimenti apparirebbe nell'output.
</details>

---

## Esercizio 2: Stampa formattata (Livello: Principiante)

**Traccia:**
Leggi il file e stampa ogni studente nel formato:

```
[101] Alice Rossi — Analisi: 28, Algebra: 30, Geometria: 27
```

Salta l'intestazione.

> [!TIP]
> Usa `readline()` per leggere e scartare la prima riga prima del loop.

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
with open("studenti_matematica.csv", "r", encoding="utf-8") as f:
    f.readline()  # salta l'intestazione

    for riga in f:
        campi = riga.strip().split(",")
        matricola, nome, cognome = campi[0], campi[1], campi[2]
        analisi, algebra, geometria = campi[3], campi[4], campi[5]
        
        print(f"[{matricola}] {nome} {cognome} — "
              f"Analisi: {analisi}, Algebra: {algebra}, Geometria: {geometria}")
```

**Spiegazione:**
Chiamare `f.readline()` una volta avanza il cursore interno del file oltre la prima riga. Le chiamate successive (nel `for`) partono quindi dalla riga 2. L'**unpacking** multiplo `a, b, c = lista[0], lista[1], lista[2]` rende il codice più leggibile.
</details>

---

## Esercizio 3: Calcolo della media per studente (Livello: Principiante)

**Traccia:**
Per ogni studente, calcola la media aritmetica dei tre voti e stampala con due decimali:

```
Alice Rossi        media: 28.33
Bruno Verdi        media: 21.33
...
```

Ricorda di convertire i voti da `str` a `int` prima di fare la somma.

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
with open("studenti_matematica.csv", "r", encoding="utf-8") as f:
    f.readline()  # salta intestazione

    for riga in f:
        campi = riga.strip().split(",")
        nome     = campi[1]
        cognome  = campi[2]
        voti     = [int(campi[3]), int(campi[4]), int(campi[5])]
        media    = sum(voti) / len(voti)

        print(f"{nome} {cognome:<12} media: {media:.2f}")
```

**Spiegazione:**
La conversione `int(campi[3])` è essenziale: senza di essa `"28" + "30"` produce `"2830"` (concatenazione di stringhe), non `58`. Il format specifier `{media:.2f}` arrotonda a due cifre decimali — equivalente a $\lfloor media \cdot 100 \rfloor / 100$.
</details>

---

## Esercizio 4: Media della classe per materia (Livello: Intermedio)

**Traccia:**
Calcola la media della classe per ciascuna delle tre materie (Analisi, Algebra, Geometria) e stampa i risultati.

$$\bar{v}_{materia} = \frac{1}{n} \sum_{i=1}^{n} v_i$$

> [!NOTE]
> Accumula le somme in tre variabili separate, poi dividi per il numero di studenti alla fine.

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
somma_analisi   = 0
somma_algebra   = 0
somma_geometria = 0
n_studenti      = 0

with open("studenti_matematica.csv", "r", encoding="utf-8") as f:
    f.readline()  # salta intestazione

    for riga in f:
        campi = riga.strip().split(",")
        somma_analisi   += int(campi[3])
        somma_algebra   += int(campi[4])
        somma_geometria += int(campi[5])
        n_studenti      += 1

print(f"Media Analisi:   {somma_analisi / n_studenti:.2f}")
print(f"Media Algebra:   {somma_algebra / n_studenti:.2f}")
print(f"Media Geometria: {somma_geometria / n_studenti:.2f}")
```

**Output atteso:**
```
Media Analisi:   23.90
Media Algebra:   24.70
Media Geometria: 24.10
```

**Spiegazione:**
Usiamo il pattern classico dell'**accumulatore** — una variabile inizializzata a zero che viene incrementata a ogni iterazione. Questo è esattamente il calcolo che `numpy.mean()` farà per noi nella prossima lezione, con una sintassi molto più compatta.
</details>

---

## Esercizio 5: Trovare il migliore studente (Livello: Intermedio)

**Traccia:**
Trova lo studente con la media più alta e stampa nome, cognome e media.
In caso di parità, restituisci il primo in ordine di riga.

> [!TIP]
> Tieni traccia del massimo con due variabili: `miglior_studente` e `media_massima`.

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
miglior_studente = None
media_massima    = -1

with open("studenti_matematica.csv", "r", encoding="utf-8") as f:
    f.readline()  # salta intestazione

    for riga in f:
        campi = riga.strip().split(",")
        nome    = campi[1]
        cognome = campi[2]
        media   = (int(campi[3]) + int(campi[4]) + int(campi[5])) / 3

        if media > media_massima:
            media_massima    = media
            miglior_studente = (nome, cognome)

nome, cognome = miglior_studente
print(f"Miglior studente: {nome} {cognome} con media {media_massima:.2f}")
```

**Output atteso:**
```
Miglior studente: Irene Romano con media 29.67
```

**Spiegazione:**
Il pattern `massimo = -1 / if valore > massimo` è un algoritmo classico di ricerca del massimo in una sequenza — equivalente a $\max_{i} a_i$. La variabile `miglior_studente` è una **tupla** `(nome, cognome)`, struttura appropriata per un record immutabile con due campi.
</details>

---

## Esercizio 6: Scrivere i risultati in un nuovo file (Livello: Intermedio)

**Traccia:**
Crea un nuovo file `risultati_medie.csv` con il seguente formato:

```
matricola,nome,cognome,media
101,Alice,Rossi,28.33
102,Bruno,Verdi,21.33
...
```

Il file deve contenere l'intestazione seguita da una riga per ogni studente con la media calcolata.

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
with open("studenti_matematica.csv", "r", encoding="utf-8") as f_in, \
     open("risultati_medie.csv", "w", encoding="utf-8") as f_out:

    f_in.readline()  # salta intestazione originale

    # Scriviamo la nuova intestazione
    f_out.write("matricola,nome,cognome,media\n")

    for riga in f_in:
        campi    = riga.strip().split(",")
        matricola = campi[0]
        nome      = campi[1]
        cognome   = campi[2]
        media     = (int(campi[3]) + int(campi[4]) + int(campi[5])) / 3

        f_out.write(f"{matricola},{nome},{cognome},{media:.2f}\n")

print("File 'risultati_medie.csv' creato con successo.")
```

**Spiegazione:**
Il costrutto `with ... as f_in, ... as f_out` apre **due file contemporaneamente** nello stesso blocco — è sintassi Python valida e idiomatica. Entrambi vengono chiusi automaticamente all'uscita dal blocco. L'`\n` in `f.write()` è obbligatorio: senza di esso tutte le righe verrebbero scritte in una riga sola.
</details>

---

## Esercizio 7: Filtrare per soglia (Livello: Intermedio)

**Traccia:**
Leggi il CSV e stampa solo gli studenti che hanno una media **strettamente superiore a 25**.
Poi stampa quanti studenti soddisfano questa condizione.

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
studenti_promossi = []

with open("studenti_matematica.csv", "r", encoding="utf-8") as f:
    f.readline()

    for riga in f:
        campi  = riga.strip().split(",")
        media  = (int(campi[3]) + int(campi[4]) + int(campi[5])) / 3

        if media > 25:
            studenti_promossi.append((campi[1], campi[2], media))

print(f"Studenti con media > 25: {len(studenti_promossi)}\n")
for nome, cognome, media in studenti_promossi:
    print(f"  {nome} {cognome}: {media:.2f}")
```

**Output atteso:**
```
Studenti con media > 25: 5

  Alice Rossi: 28.33
  Carla Bianchi: 29.67
  Elena Greco: 26.00
  Giulia Marino: 26.67
  Irene Romano: 29.67
```

**Spiegazione:**
Ogni studente che supera la soglia viene aggiunto a `studenti_promossi` come **tupla** `(nome, cognome, media)` — struttura immutabile adatta a un record di risultato che non verrà modificato. L'unpacking `for nome, cognome, media in ...` nel loop di stampa rende il codice molto leggibile.
</details>

---

## Esercizio 8: Gestione di file corrotto (Livello: Avanzato)

**Traccia:**
Il file `studenti_corrotto.csv` contiene alcune righe malformate (un campo numerico sostituito da `"N/A"`). Scrivi una funzione `carica_robusto(nome_file)` che:
1. Salta le righe con valori non convertibili.
2. Stampa un avviso per ogni riga saltata con il relativo numero di riga.
3. Restituisce la lista degli studenti validi.

Prima di tutto, crea il file corrotto con questo codice:

```python
# Creazione del file di test corrotto
righe_corrotte = [
    "matricola,nome,cognome,analisi,algebra,geometria\n",
    "101,Alice,Rossi,28,30,27\n",
    "102,Bruno,Verdi,22,N/A,24\n",   # ← algebra mancante
    "103,Carla,Bianchi,30,29,30\n",
    "104,Davide,Neri,18,20\n",        # ← geometria mancante (campo assente)
    "105,Elena,Greco,25,27,26\n",
]

with open("studenti_corrotto.csv", "w", encoding="utf-8") as f:
    f.writelines(righe_corrotte)
```

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
def carica_robusto(nome_file):
    """
    Legge un CSV con possibili errori.
    Salta le righe malformate e avvisa l'utente.
    Restituisce la lista degli studenti validi.
    """
    studenti_validi = []

    try:
        with open(nome_file, "r", encoding="utf-8") as f:
            intestazione = f.readline().strip().split(",")

            for n_riga, riga in enumerate(f, start=2):
                try:
                    campi = riga.strip().split(",")

                    # Verifica che ci siano abbastanza campi
                    if len(campi) != len(intestazione):
                        raise ValueError(
                            f"attesi {len(intestazione)} campi, trovati {len(campi)}"
                        )

                    studente = {
                        "matricola": int(campi[0]),
                        "nome":      campi[1],
                        "cognome":   campi[2],
                        "analisi":   int(campi[3]),
                        "algebra":   int(campi[4]),
                        "geometria": int(campi[5]),
                    }
                    studenti_validi.append(studente)

                except (ValueError, IndexError) as e:
                    print(f"⚠️  Riga {n_riga} saltata: {e}")

    except FileNotFoundError:
        print(f"Errore: '{nome_file}' non trovato.")

    return studenti_validi


# Test
studenti = carica_robusto("studenti_corrotto.csv")
print(f"\nStudenti caricati correttamente: {len(studenti)}")
for s in studenti:
    print(f"  [{s['matricola']}] {s['nome']} {s['cognome']}")
```

**Output atteso:**
```
⚠️  Riga 3 saltata: invalid literal for int() with base 10: 'N/A'
⚠️  Riga 5 saltata: attesi 6 campi, trovati 5

Studenti caricati correttamente: 3
  [101] Alice Rossi
  [103] Carla Bianchi
  [105] Elena Greco
```

**Spiegazione:**
La struttura `try/except` **annidata** gestisce due livelli di errore distinti:
- Il `try` esterno cattura `FileNotFoundError` — il file non esiste.
- Il `try` interno (nel `for`) cattura `ValueError` e `IndexError` — la riga è malformata.

Questo è il pattern corretto per operazioni I/O robuste: separare gli errori di accesso al file dagli errori di parsing dei dati.
</details>

---

## Esercizio 9: Analisi completa con output su file (Livello: Avanzato)

**Traccia:**
Scrivi una funzione `analisi_completa(file_input, file_output)` che legge `studenti_matematica.csv` e produce un file di testo `report_analisi.txt` con il seguente contenuto:

```
===== REPORT ANALISI VOTI =====

Numero studenti: 10

Medie per materia:
  Analisi:   23.90
  Algebra:   24.70
  Geometria: 24.10

Miglior studente:  Irene Romano (29.67)
Peggior studente:  Luca Ferrari (17.00)

Studenti sopra la media generale (23.90):
  Alice Rossi       28.33
  Carla Bianchi     29.67
  ...
```

> [!NOTE]
> La media generale è la media delle tre medie per materia, oppure la media di tutte le medie individuali — entrambe le interpretazioni sono accettabili. Scegli quella che ti sembra più significativa e documentala nel codice.

<details>
<summary>👉 Soluzione e Spiegazione</summary>

```python
def analisi_completa(file_input, file_output):
    """
    Legge il CSV, calcola statistiche aggregate e scrive un report testuale.
    La media generale è calcolata come media delle medie individuali.
    """
    studenti = []

    # --- Lettura e parsing ---
    with open(file_input, "r", encoding="utf-8") as f:
        f.readline()
        for riga in f:
            campi = riga.strip().split(",")
            studenti.append({
                "nome":      campi[1],
                "cognome":   campi[2],
                "analisi":   int(campi[3]),
                "algebra":   int(campi[4]),
                "geometria": int(campi[5]),
            })

    n = len(studenti)

    # --- Calcolo statistiche ---
    for s in studenti:
        s["media"] = (s["analisi"] + s["algebra"] + s["geometria"]) / 3

    media_analisi   = sum(s["analisi"]   for s in studenti) / n
    media_algebra   = sum(s["algebra"]   for s in studenti) / n
    media_geometria = sum(s["geometria"] for s in studenti) / n
    media_generale  = sum(s["media"]     for s in studenti) / n

    migliore = max(studenti, key=lambda s: s["media"])
    peggiore = min(studenti, key=lambda s: s["media"])

    sopra_media = [s for s in studenti if s["media"] > media_generale]

    # --- Scrittura report ---
    with open(file_output, "w", encoding="utf-8") as f:
        f.write("===== REPORT ANALISI VOTI =====\n\n")
        f.write(f"Numero studenti: {n}\n\n")

        f.write("Medie per materia:\n")
        f.write(f"  Analisi:   {media_analisi:.2f}\n")
        f.write(f"  Algebra:   {media_algebra:.2f}\n")
        f.write(f"  Geometria: {media_geometria:.2f}\n\n")

        f.write(f"Miglior studente:  {migliore['nome']} {migliore['cognome']}"
                f" ({migliore['media']:.2f})\n")
        f.write(f"Peggior studente:  {peggiore['nome']} {peggiore['cognome']}"
                f" ({peggiore['media']:.2f})\n\n")

        f.write(f"Studenti sopra la media generale ({media_generale:.2f}):\n")
        for s in sopra_media:
            f.write(f"  {s['nome']} {s['cognome']:<12} {s['media']:.2f}\n")

    print(f"Report salvato in '{file_output}'.")


# Esecuzione
analisi_completa("studenti_matematica.csv", "report_analisi.txt")
```

**Spiegazione:**
Questo esercizio integra tutti i concetti della lezione:
- Lettura con `with open(..., "r")` e parsing manuale
- Scrittura con `with open(..., "w")`
- Utilizzo di **lambda** come chiave per `max()` e `min()`
- **List comprehension** per filtrare studenti sopra la media

Il pattern di separare la fase di lettura, calcolo e scrittura in tre blocchi distinti è una buona pratica: rende il codice più facile da testare e da modificare.
</details>

---

> [!TIP]
> **Sfida per casa:** modifica `analisi_completa` per aggiungere al report anche la **deviazione standard** dei voti per ogni materia, calcolata manualmente con la formula:
> $$\sigma = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (v_i - \bar{v})^2}$$
> Poi, nella prossima lezione, verifica che il risultato coincida con `numpy.std()`.
