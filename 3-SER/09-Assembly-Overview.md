
# Assembly Overview

## Cos'è Assembly

Assembly è un linguaggio di programmazione **a basso livello** (*low-level*). Un linguaggio a basso livello è vicino al funzionamento fisico del processore, con poca o nessuna astrazione rispetto all'hardware.

Ogni istruzione Assembly corrisponde a una singola operazione eseguita dalla CPU. Questa corrispondenza è spesso uno-a-uno.

Assembly espone direttamente i componenti interni del processore:

- I **registri** (*registers*) sono piccole celle di memoria dentro la CPU, usate per calcoli immediati.
- Gli **indirizzi di memoria** (*memory addresses*) sono identificatori numerici che indicano dove un dato è memorizzato nella RAM.
- Il **set di istruzioni** (*instruction set*) è l'insieme di tutte le operazioni che una specifica CPU sa eseguire.

Assembly si colloca tra il codice binario e i linguaggi ad alto livello come Python o C.

---

## Contesto Storico

Nei primi anni '40 e '50, i computer non avevano linguaggi di programmazione. I programmatori scrivevano le istruzioni direttamente in formato binario o esadecimale.

Assembly ha risolto questo problema. Ha sostituito i codici numerici con parole simboliche chiamate **mnemonici**. Un mnemonico è una parola breve che rappresenta un'operazione della CPU.

Esempi di mnemonici:

| Mnemonico | Significato |
|-----------|-------------|
| `MOV` | Sposta un valore da un registro a un altro |
| `ADD` | Somma due valori |
| `JMP` | Salta a un'altra istruzione nel programma |

I codici numerici sostituiti dai mnemonici si chiamano **opcode** (*operation code*). Un opcode è il numero binario che la CPU legge per capire quale operazione eseguire. Assembly traduce i mnemonici leggibili negli opcode binari corrispondenti.

Con l'arrivo di linguaggi come C e Fortran, l'uso di Assembly nella programmazione generale è diminuito. Assembly è però rimasto fondamentale in tre aree:

- **Programmazione di sistema** (*systems programming*): sviluppo di sistemi operativi e driver.
- **Sistemi embedded** (*embedded systems*): dispositivi con risorse limitate come microcontrollori, elettrodomestici intelligenti o sensori industriali.
- **Applicazioni critiche per le prestazioni**: codice dove la velocità di esecuzione è prioritaria.

---

## Collegamento con la Matematica e i Linguaggi Formali

Assembly ha radici nella matematica e nella logica.

### Macchine a stati finiti

Una **macchina a stati finiti** (*finite state machine*, FSM) è un modello matematico che descrive un sistema con un numero limitato di stati possibili. Il sistema si trova sempre in uno stato alla volta. Ogni evento o istruzione causa una **transizione**: il passaggio da uno stato al successivo.

La CPU funziona secondo questo principio. Ogni istruzione Assembly rappresenta una transizione di stato: la CPU legge un'istruzione, cambia il proprio stato interno (registri, memoria, program counter) e si prepara all'istruzione successiva.

### Aritmetica binaria e algebra booleana

Assembly opera su **aritmetica binaria**: tutti i dati sono rappresentati come sequenze di 0 e 1. Questa rappresentazione è governata dall'**algebra booleana** (*Boolean algebra*), un sistema matematico basato su valori vero/falso e operatori logici (AND, OR, NOT). L'algebra booleana è il fondamento della logica digitale e dei circuiti elettronici.

### Sistemi formali

Un **sistema formale** (*formal system*) è un insieme di regole precise e non ambigue che governano la manipolazione di simboli. I linguaggi di programmazione sono sistemi formali: ogni istruzione ha una sintassi esatta e un significato deterministico. Assembly è uno dei sistemi formali più vicini all'hardware: le sue regole corrispondono direttamente alle operazioni fisiche della CPU.

---

## Assembly nello Stack Tecnologico

Lo **stack tecnologico** (*technology stack*) è la gerarchia di livelli software e hardware che cooperano per eseguire un programma.

```
Applicazioni
     ↓
Linguaggi ad Alto Livello (C, Python, Java)
     ↓
Assembly
     ↓
Codice Macchina (Machine Code)
     ↓
Hardware (CPU, Memoria)
```

Ogni livello comunica con quello adiacente:

| Livello | Descrizione |
|--------|-------------|
| **Hardware** | Componenti fisici. Eseguono segnali elettrici. |
| **Codice Macchina** | Sequenze di bit. La CPU le legge direttamente. |
| **Assembly** | Versione leggibile del codice macchina. Un assemblatore (*assembler*) la converte in codice macchina. |
| **Linguaggi ad Alto Livello** | Linguaggi come C o Python. Un compilatore (*compiler*) li traduce in Assembly o codice macchina. |
| **Applicazioni** | Software usato dall'utente finale. |

Assembly occupa una posizione strategica in questo stack. I compilatori di linguaggi come C producono spesso Assembly come fase intermedia. Assembly permette inoltre un controllo preciso su prestazioni e memoria, utile nel debugging, nel reverse engineering e nei sistemi embedded.

---

## Conclusione

Assembly è il livello più vicino all'hardware che un programmatore può leggere e scrivere direttamente. Non è usato per la maggior parte delle applicazioni moderne. È però essenziale per capire come il software interagisce con la macchina.

Studiare Assembly fornisce tre competenze fondamentali:

1. **Comprensione delle prestazioni**: si impara perché alcune operazioni sono più veloci di altre.
2. **Gestione della memoria**: si capisce come i dati vengono letti, scritti e organizzati fisicamente.
3. **Fondamenti della computazione**: si acquisisce una visione chiara di come una CPU esegue le istruzioni.

Queste competenze restano rilevanti anche nei contesti di programmazione moderni.
