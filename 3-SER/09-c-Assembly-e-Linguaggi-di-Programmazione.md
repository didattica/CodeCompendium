# Assembly e Linguaggi di Programmazione
### Una visione ad alto livello per chi inizia

---

## Indice

1. [Cosa sono i linguaggi di programmazione?](#1-cosa-sono-i-linguaggi-di-programmazione)
2. [La gerarchia dei linguaggi](#2-la-gerarchia-dei-linguaggi)
3. [Cosa è l'Assembly?](#3-cosa-è-lassembly)
4. [Dal linguaggio naturale alla macchina](#4-dal-linguaggio-naturale-alla-macchina)
5. [Assembly e logica formale](#5-assembly-e-logica-formale)
6. [Logica Booleana: il ponte verso l'hardware](#6-logica-booleana-il-ponte-verso-lhardware)
7. [Il ruolo storico dell'Assembly](#7-il-ruolo-storico-dellassembly)
8. [Come l'Assembly ha influenzato i linguaggi moderni](#8-come-lassembly-ha-influenzato-i-linguaggi-moderni)
9. [Schema riassuntivo](#9-schema-riassuntivo)
10. [Conclusione](#10-conclusione)

---

## 1. Cosa sono i linguaggi di programmazione?

Prima di capire cos'è l'Assembly, è utile chiedersi: *perché esistono i linguaggi di programmazione?*

I computer capiscono solo **sequenze di 0 e 1** — il cosiddetto *codice macchina*. Un essere umano che voglia comunicare istruzioni a un computer ha bisogno di un intermediario: un **linguaggio di programmazione**.

Un linguaggio di programmazione è, in sostanza, un sistema di comunicazione tra l'intelligenza umana e l'hardware. Come ogni sistema di comunicazione, è fatto di:

- **Sintassi** (*syntax*): le regole su come scrivere le istruzioni
- **Semantica** (*semantics*): il significato di quelle istruzioni

> **Analogia:** Pensate a una ricetta di cucina. La ricetta ha una sintassi (elenco ingredienti, poi procedimento, poi tempi) e una semantica (ogni azione produce un effetto fisico reale). Un programma è la stessa cosa: una serie di istruzioni con un significato preciso.

---

## 2. La gerarchia dei linguaggi

I linguaggi di programmazione non sono tutti uguali. Si distinguono per quanto siano **vicini al linguaggio umano** (alto livello) o **vicini al linguaggio della macchina** (basso livello).

```mermaid
graph TD
    A["🗣️ Linguaggio Naturale<br/><i>italiano, inglese...</i>"]
    B["📐 Linguaggi ad Alto Livello<br/><i>Python, Java, C#...</i>"]
    C["⚙️ Linguaggi a Medio Livello<br/><i>C, C++</i>"]
    D["🔩 Assembly<br/><i>linguaggio simbolico della macchina</i>"]
    E["💻 Codice Macchina<br/><i>sequenze di 0 e 1</i>"]
    F["🔌 Hardware<br/><i>transistor, circuiti</i>"]

    A -->|"astrazione crescente ⬆"| B
    B --> C
    C --> D
    D --> E
    E --> F

    style A fill:#d4edda,stroke:#28a745
    style B fill:#cce5ff,stroke:#004085
    style C fill:#cce5ff,stroke:#004085
    style D fill:#fff3cd,stroke:#856404
    style E fill:#f8d7da,stroke:#721c24
    style F fill:#e2e3e5,stroke:#6c757d
```

Più si scende nella gerarchia, più le istruzioni sono **potenti ma difficili da leggere per un umano**. Più si sale, più il codice **somiglia al linguaggio naturale**, ma perde contatto diretto con l'hardware.

L'Assembly occupa una posizione cruciale: è il linguaggio più vicino all'hardware che un essere umano può ancora leggere e scrivere in modo ragionevole.

---

## 3. Cosa è l'Assembly?

L'**Assembly** (o linguaggio assemblativo) è un linguaggio di programmazione a basso livello in cui ogni istruzione corrisponde, quasi sempre in modo diretto, a una singola operazione eseguita dal processore.

A differenza del codice macchina (fatto di soli numeri binari), l'Assembly usa **parole simboliche** leggibili dall'uomo, chiamate *mnemonici*:

| Codice macchina | Assembly | Significato |
|:---:|:---:|:---|
| `10110000 01100001` | `MOV AL, 97` | Sposta il valore 97 nel registro AL |
| `00000011 11000011` | `ADD EAX, EBX` | Somma EBX a EAX |
| `11101011 00001010` | `JMP fine` | Salta all'etichetta "fine" |

> **Nota:** Il mnemonico `MOV` viene da *move* (sposta), `ADD` da *add* (somma), `JMP` da *jump* (salta). Questa scelta non è casuale: i progettisti dell'Assembly volevano rendere il codice *minimamente* leggibile.

### Come funziona la traduzione?

Un programma chiamato **assembler** traduce il codice Assembly in codice macchina. È il primo esempio storico di "compilazione".

```mermaid
flowchart LR
    A["📝 Codice Assembly\n(leggibile dall'umano)"]
    B["🔧 Assembler\n(programma traduttore)"]
    C["💻 Codice Macchina\n(leggibile dalla CPU)"]

    A -->|"testo simbolico"| B
    B -->|"sequenze binarie"| C

    style A fill:#cce5ff,stroke:#004085
    style B fill:#fff3cd,stroke:#856404
    style C fill:#f8d7da,stroke:#721c24
```

---

## 4. Dal linguaggio naturale alla macchina

C'è una catena di trasformazioni che va dal pensiero umano all'esecuzione fisica. Ogni passaggio traduce il messaggio in una forma più precisa e meno ambigua.

### Un esempio concreto

Immaginiamo di voler esprimere un'idea semplice: *"Se ho più di 18 anni, posso votare."*

Vediamo come questa stessa idea si esprime a livelli diversi:

**Linguaggio naturale (italiano):**
```
Se la mia età è maggiore di 18, allora posso votare.
```

**Pseudocodice (linguaggio ad alto livello):**
```python
if eta > 18:
    print("Puoi votare")
```

**Assembly (basso livello):**
```asm
CMP EAX, 18      ; confronta EAX (età) con 18
JLE non_votare   ; se minore o uguale, salta a "non_votare"
; ... codice per "puoi votare"
non_votare:
; ... codice per "non puoi votare"
```

**Codice macchina (binario):**
```
00111101 00010010 00000000 00000000 00000000
01111110 00001000
...
```

```mermaid
flowchart TD
    NL["💬 <b>Linguaggio Naturale</b><br/><i>Se ho più di 18 anni, posso votare</i>"]
    HL["🐍 <b>Alto livello</b><br/><code>if eta > 18: print(...)</code>"]
    ASM["🔩 <b>Assembly</b><br/><code>CMP EAX, 18 / JLE non_votare</code>"]
    MC["01 <b>Codice Macchina</b><br/><code>00111101 00010010 ...</code>"]
    HW["🔌 <b>Hardware</b><br/><i>circuiti che eseguono la comparazione</i>"]

    NL -->|"rimozione ambiguità"| HL
    HL -->|"compilazione"| ASM
    ASM -->|"assemblaggio"| MC
    MC -->|"esecuzione"| HW

    style NL fill:#d4edda,stroke:#28a745
    style HL fill:#cce5ff,stroke:#004085
    style ASM fill:#fff3cd,stroke:#856404
    style MC fill:#f8d7da,stroke:#721c24
    style HW fill:#e2e3e5,stroke:#6c757d
```

Ogni passaggio **elimina ambiguità** e **aggiunge precisione**, fino a ottenere istruzioni che l'hardware può eseguire senza alcuna interpretazione.

---

## 5. Assembly e logica formale

L'Assembly non è solo un linguaggio tecnico: è anche un **linguaggio logico**. Ogni programma Assembly descrive una sequenza di trasformazioni su dati, esattamente come la logica matematica descrive trasformazioni su proposizioni.

Ma per capire davvero cosa rende l'Assembly speciale, partiamo da un posto inaspettato: la **poesia italiana**.

---

### Sintassi e Semantica: dalla poesia all'Assembly

> [!NOTE]
> **Sintassi** = le regole su *come* scrivere le istruzioni (la forma).
> **Semantica** = il *significato* di quelle istruzioni (il contenuto).
> Tutti i linguaggi hanno entrambe — ma con gradi molto diversi di rigidità e precisione.

#### La licenza poetica: quando la sintassi si piega

Leopardi, ne *L'Infinito* (1819), scrive:

> *"Sempre caro mi fu quest'ermo colle"*

In italiano standard diremmo: *"Questo colle solitario mi fu sempre caro"*. Leopardi sposta il soggetto in fondo, anticipa gli avverbi, inverte l'ordine naturale — e lo fa deliberatamente, per creare ritmo e suggestione.

Manzoni, nel *5 Maggio* (1821), apre con:

> *"Ei fu. Siccome immobile"*

Due parole per descrivere la morte di Napoleone. La frase è sintatticamentte sospesa, incompleta secondo le regole standard — eppure potentissima.

> [!TIP]
> Questo si chiama **licenza poetica**: i poeti possono *piegare* le regole sintattiche per effetto estetico. Non le eliminano — le violano consapevolmente. Il lettore capisce proprio perché conosce le regole di base e riconosce la deviazione.

---

### Il quadro completo: tutti i linguaggi a confronto

```mermaid
quadrantChart
    title Sintassi vs Semantica nei linguaggi
    x-axis "Semantica vaga" --> "Semantica precisa"
    y-axis "Sintassi flessibile" --> "Sintassi rigida"
    quadrant-1 Formali e precisi
    quadrant-2 Grammaticali ma ambigui
    quadrant-3 Licenza e ambiguita'
    quadrant-4 Precisi ma informali
    Poesia - Leopardi: [0.10, 0.20]
    Poesia - Manzoni: [0.12, 0.25]
    Italiano: [0.18, 0.75]
    Inglese: [0.22, 0.70]
    LIS - Lingua dei Segni: [0.16, 0.72]
    Python: [0.80, 0.75]
    C: [0.88, 0.85]
    Assembly: [0.93, 0.92]
    Logica Mat.: [0.91, 0.60]
```

> [!TIP]
> **Come leggere il grafico:**
> - In basso a sinistra (*Licenza e ambiguità*): la **Poesia** — sintassi volutamente piegata, semantica aperta e plurima. L'unico linguaggio che abita questo quadrante.
> - In alto a sinistra (*Grammaticali ma ambigui*): i **linguaggi naturali** — grammatica rigida, ma il significato dipende dal contesto
> - In alto a destra (*Formali e precisi*): **Python, C, Assembly** — sintassi rigida *e* semantica univoca
> - In basso a destra (*Precisi ma informali*): la **Logica Matematica** — semantica assoluta, ma la notazione può variare

> [!IMPORTANT]
> La poesia è il punto **più lontano** dall'Assembly nell'intero spettro: ha sia sintassi flessibile che semantica volutamente ambigua. È impossibile "eseguire" una poesia su una macchina — non per limite tecnologico, ma per sua natura intrinseca.

---

### L'ambiguità nei linguaggi naturali

> [!WARNING]
> L'ambiguità non è un difetto dei linguaggi naturali: è una caratteristica **voluta**. Gli esseri umani sfruttano il contesto, il tono, la cultura per comunicare in modo efficiente — e i poeti la usano come strumento artistico. Una macchina non può fare altrettanto.

Considera questa frase in italiano:

> *"Vedo l'uomo con il telescopio."*

Chi usa il telescopio? Io, o l'uomo? La frase è grammaticalmente corretta ma **semanticamente ambigua**. Un essere umano risolve l'ambiguità con il contesto. Un processore non ha contesto: ha bisogno di istruzioni inequivocabili.

---

### L'Assembly elimina ogni ambiguità

In Assembly, ogni operazione deve essere espressa in modo completamente esplicito. Non esiste contesto, non esiste interpretazione, non esiste licenza poetica:

```asm
MOV EAX, [eta]      ; carica il valore dell'età nel registro EAX
CMP EAX, 18         ; confronta con 18
JG  puo_votare      ; se maggiore, salta a "puo_votare"
JMP non_puo_votare  ; altrimenti salta a "non_puo_votare"
```

Mentre Leopardi poteva scrivere *"Sempre caro mi fu quest'ermo colle"* mettendo il soggetto dove voleva, in Assembly **l'ordine delle istruzioni è legge**: cambiare l'ordine cambia il significato, o produce un errore.

> [!IMPORTANT]
> In Assembly non esiste ambiguità interpretativa. Ogni istruzione specifica **esattamente** quale dato usare, quale operazione eseguire, e dove mettere il risultato. Non c'è spazio per il contesto, il tono, o l'interpretazione — e tanto meno per la licenza poetica.

---

### Il flusso di controllo come logica

In logica esistono strutture fondamentali: *se… allora*, *ripeti finché*, *scegli tra*. L'Assembly le implementa in modo esplicito:

| Struttura logica | In linguaggio naturale | In poesia | In Assembly |
|:---|:---|:---|:---|
| Condizione | "Se A è vero, fai X" | *"Ei fu"* — tutto il resto è conseguenza | `CMP` + `JE` / `JNE` |
| Ciclo | "Ripeti X fino a quando Y" | il ritornello, la terzina | `LOOP` + `JMP` |
| Sequenza | "Prima A, poi B, poi C" | la strofa | istruzioni in ordine |

> [!NOTE]
> L'istruzione `JE equal` (*Jump if Equal*) non è altro che la realizzazione fisica di **"se i valori sono uguali, allora salta"**. La struttura logica condizionale più elementare — che Manzoni esprimeva in versi e Leopardi in immagini — diventa un'operazione concreta sul processore.


---

## 6. Logica Booleana: il ponte verso l'hardware

Alla base di tutto c'è la **logica booleana**, inventata dal matematico George Boole nel 1847, decenni prima dei computer. La sua intuizione fu che il ragionamento logico poteva essere ridotto a operazioni su soli due valori: **vero** e **falso**, o equivalentemente **1** e **0**.

### Le operazioni fondamentali

```mermaid
flowchart LR
    subgraph AND["AND (E)"]
        direction TB
        a1["1"] & b1["1"] --> r1["1 ✓"]
        a2["1"] & b2["0"] --> r2["0 ✗"]
    end
    subgraph OR["OR (O)"]
        direction TB
        a3["1"] & b3["0"] --> r3["1 ✓"]
        a4["0"] & b4["0"] --> r4["0 ✗"]
    end
    subgraph NOT["NOT (NON)"]
        direction TB
        a5["1"] --> r5["0"]
        a6["0"] --> r6["1"]
    end
```

Queste tre operazioni sono abbastanza potenti da costruire qualsiasi calcolo possibile. Nei circuiti digitali, sono implementate fisicamente tramite componenti chiamati **porte logiche** (*logic gates*).

In Assembly, la logica booleana è direttamente accessibile:

```asm
AND R1, R2    ; R1 = R1 AND R2 (bit per bit)
OR  R1, R3    ; R1 = R1 OR R3
NOT R1        ; R1 = NOT R1 (inverte tutti i bit)
XOR R1, R1    ; trucco classico: mette R1 a zero
```

```mermaid
flowchart LR
    BOOL["📐 Logica Booleana\n<i>AND, OR, NOT</i>"]
    GATE["🔌 Porte Logiche\n<i>circuiti fisici</i>"]
    ASM["🔩 Istruzioni Assembly\n<i>AND, OR, NOT, XOR</i>"]
    CPU["💻 CPU\n<i>esecuzione reale</i>"]

    BOOL -->|"implementata in"| GATE
    BOOL -->|"espressa in"| ASM
    GATE -->|"compone la"| CPU
    ASM -->|"controlla la"| CPU

    style BOOL fill:#d4edda,stroke:#28a745
    style GATE fill:#e2e3e5,stroke:#6c757d
    style ASM fill:#fff3cd,stroke:#856404
    style CPU fill:#f8d7da,stroke:#721c24
```

La logica booleana è il punto in cui **la matematica astratta diventa fisica reale**.

---

## 7. Il ruolo storico dell'Assembly

Per capire davvero l'Assembly, bisogna conoscere il contesto in cui è nato.

### Le origini: il codice macchina puro

Nei primissimi computer degli anni '40 (ENIAC, UNIVAC, ecc.), i programmatori scrivevano direttamente in **codice macchina binario**, inserendo i programmi tramite schede perforate o interruttori fisici. Era un lavoro lentissimo, erroratissimo e privo di qualsiasi astrazione.

```mermaid
timeline
    title Evoluzione dei linguaggi di programmazione
    1940s : Codice Macchina Binario
          : Programmazione tramite schede perforate
          : Nessuna astrazione
    1950s : Assembly
          : Mnemonici simbolici
          : Primi assembler automatici
    1957  : FORTRAN
          : Primo linguaggio ad alto livello
          : Compilatori automatici
    1960s : COBOL e LISP
          : Linguaggi specializzati
          : Crescente astrazione
    1970s : C
          : "Basso livello ad alto livello"
          : Eredità diretta di Assembly
    1980s-oggi : Java Python JavaScript...
              : Linguaggi moderni
              : Portabilità e sicurezza
```

### Perché l'Assembly fu rivoluzionario

L'introduzione dell'Assembly, a metà degli anni '50, fu una svolta epocale per tre ragioni:

1. **Leggibilità:** `ADD EAX, EBX` è incomparabilmente più chiaro di `00000011 11000011`.
2. **Produttività:** I programmatori potevano scrivere e correggere codice molto più velocemente.
3. **Astrazione:** Per la prima volta, il programmatore poteva *pensare* al problema senza gestire ogni bit manualmente.

> **Analogia:** Immaginate di dover costruire una casa usando direttamente gli atomi. Poi qualcuno inventa i mattoni. L'Assembly è l'invenzione del mattone: non elimina la complessità di fondo, ma la rende gestibile.

---

## 8. Come l'Assembly ha influenzato i linguaggi moderni

L'Assembly non è "morto": vive nei linguaggi moderni attraverso concetti, strutture e paradigmi che ha introdotto o consolidato.

### Eredità concettuale

```mermaid
mindmap
  root((Assembly))
    Concetti fondamentali
      Registri e variabili
      Stack e funzioni
      Puntatori e indirizzi
      Flusso di controllo
    Influenza su C/C++
      Puntatori diretti
      Gestione manuale della memoria
      Compilazione nativa
      Inline Assembly
    Influenza su linguaggi moderni
      Modello di esecuzione
      Tipi di dati primitivi
      Operatori bitwise
      Ottimizzazione del compilatore
    Ancora in uso oggi
      Kernel di sistemi operativi
      Driver hardware
      Crittografia e sicurezza
      Videogiochi e grafica 3D
```

### Il C: figlio diretto dell'Assembly

Il linguaggio C, creato da Dennis Ritchie negli anni '70, fu progettato esplicitamente come un "Assembly leggibile". Molte costruzioni di C mappano quasi direttamente su istruzioni Assembly:

| Concetto | In C | In Assembly |
|:---|:---|:---|
| Variabile intera | `int x = 5;` | `MOV EAX, 5` |
| Condizione | `if (x > 0)` | `CMP EAX, 0 / JLE ...` |
| Ciclo | `for (int i=0; i<10; i++)` | `MOV ECX, 0 / CMP/JGE/INC` |
| Operazione bit | `x & 0xFF` | `AND EAX, 0xFF` |

Questa relazione non è casuale: il compilatore C, quando genera il codice eseguibile, **produce Assembly** come passaggio intermedio.

### La catena di compilazione moderna

```mermaid
flowchart LR
    PY["🐍 Python\n<code>if x > 18:</code>"]
    C["⚙️ C\n<code>if (x > 18)</code>"]
    ASM["🔩 Assembly\n<code>CMP EAX, 18</code>"]
    MC["💻 Codice Macchina\n<code>0x3D 0x12...</code>"]
    CPU["🔌 CPU"]

    PY -->|"interprete/compilatore"| C
    C -->|"compilatore GCC/Clang"| ASM
    ASM -->|"assembler"| MC
    MC -->|"esecuzione"| CPU

    style PY fill:#d4edda,stroke:#28a745
    style C fill:#cce5ff,stroke:#004085
    style ASM fill:#fff3cd,stroke:#856404
    style MC fill:#f8d7da,stroke:#721c24
    style CPU fill:#e2e3e5,stroke:#6c757d
```

Ogni volta che eseguite un programma Python o Java, da qualche parte nella catena c'è dell'Assembly — generato automaticamente dal compilatore, invisibile ma presente.

### Dove si usa ancora oggi

L'Assembly non è un reperto museale. Viene ancora usato in contesti dove le prestazioni e il controllo diretto sull'hardware sono critici:

- **Kernel dei sistemi operativi** (Linux, Windows): le primissime istruzioni eseguite all'avvio di un computer sono scritte in Assembly
- **Driver hardware**: la comunicazione a basso livello con periferiche
- **Crittografia**: algoritmi ottimizzati al massimo per la velocità
- **Videogiochi e grafica 3D**: shader e ottimizzazioni per GPU
- **Sistemi embedded**: microcontroller con risorse limitate (automobili, elettrodomestici, dispositivi medici)

---

## 9. Schema riassuntivo

### I concetti chiave in sintesi

```mermaid
graph TB
    subgraph Linguaggi["🗂️ Gerarchia dei Linguaggi"]
        NL["Linguaggio Naturale<br/><i>ambiguo, espressivo</i>"]
        FL["Linguaggio Formale<br/><i>preciso, strutturato</i>"]
        ASM["Assembly<br/><i>simbolico, vicino all'hardware</i>"]
        MC["Codice Macchina<br/><i>binario, eseguibile</i>"]
        NL --> FL --> ASM --> MC
    end

    subgraph Logica["📐 Fondamenti Logici"]
        BOOL["Logica Booleana<br/><i>AND, OR, NOT</i>"]
        GATE["Porte Logiche<br/><i>hardware fisico</i>"]
        BOOL --> GATE
    end

    subgraph Storia["📅 Evoluzione Storica"]
        S1["Anni '40: Codice Macchina"]
        S2["Anni '50: Assembly"]
        S3["Anni '70: C"]
        S4["Oggi: Python, Java..."]
        S1 --> S2 --> S3 --> S4
    end

    ASM --- BOOL
    ASM --- S2

    style ASM fill:#fff3cd,stroke:#856404,stroke-width:3px
```

### Cosa ricordare

| Domanda | Risposta |
|:---|:---|
| Cos'è l'Assembly? | Un linguaggio simbolico a basso livello, un passo sopra il codice macchina |
| A cosa serve? | A dare istruzioni dirette alla CPU, con il minimo di astrazione |
| Perché è importante? | Fu il primo linguaggio leggibile dall'uomo e gettò le basi di tutti i successivi |
| È ancora usato? | Sì, in kernel, driver, crittografia e sistemi embedded |
| Qual è il suo legame con la logica? | Ogni istruzione è un'operazione logica; implementa direttamente la logica booleana |
| Qual è il suo legame con i linguaggi moderni? | Tutti i linguaggi compilati generano Assembly come passaggio intermedio |

---

## 10. Conclusione

L'Assembly non è solo un vecchio linguaggio di programmazione. È il **punto di incontro** tra tre mondi:

- Il mondo dell'**astrazione umana** — linguaggio, logica, matematica
- Il mondo della **computazione** — algoritmi, strutture dati, flusso di controllo
- Il mondo della **fisica** — transistor, circuiti, segnali elettrici

Capire l'Assembly significa capire come un'idea — espressa in un linguaggio naturale — possa trasformarsi, passo dopo passo, in un'azione concreta eseguita da un processore a miliardi di operazioni al secondo.

I linguaggi moderni che usate ogni giorno — Python, JavaScript, Java, C# — sono costruiti sulle spalle dell'Assembly. Le loro astrazioni (variabili, funzioni, cicli, condizioni) nascono tutte da operazioni che, a basso livello, l'Assembly implementa in modo esplicito.

> **Messaggio finale:** Imparare i concetti dell'Assembly, anche senza scrivere una sola riga di codice Assembly, vi rende programmatori più consapevoli. Vi insegna a capire cosa succede *davvero* quando il vostro codice gira.



