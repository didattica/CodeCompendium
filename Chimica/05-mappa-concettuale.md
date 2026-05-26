# Mappa concettuale — Proprietà atomiche e legami chimici

## Introduzione

Questo documento presenta una sintesi strutturata delle principali proprietà atomiche e della loro relazione con la formazione dei legami chimici.

La rappresentazione è organizzata in diagrammi di flusso (Mermaid) separati per ciascun concetto fondamentale, al fine di facilitare la comprensione modulare dei contenuti.

---

# 1. Elettronegatività

```mermaid
flowchart TD
    A[Elettronegatività] --> B[Capacità di attrarre<br> elettroni in un <br>legame covalente]
    B --> C[Aumenta da sinistra<br> a destra nel periodo]
    B --> D[Diminuisce dall'alto<br> verso il basso nel gruppo]
    B --> E[Valore massimo: Fluoro]
    B --> F[Determina la polarità <br>del legame]
```

> [!NOTE]
> L’elettronegatività è una proprietà relativa: descrive la capacità di un atomo *all’interno di un legame chimico* di attrarre verso di sé la densità elettronica condivisa.

---

# 2. Affinità elettronica

```mermaid
flowchart TD
    A[Affinità elettronica] --> B[Energia liberata <br>quando un atomo<br> in fase gassosa <br>acquista un elettrone]
    B --> C[X#40;g#41; + e⁻ → X⁻#40;g#41;]
    B --> D[Alta affinità →<br> formazione favorevole di anioni]
    B --> E[Aumenta da sinistra<br> a destra nel periodo]
    B --> F[Diminuisce dall'alto<br> verso il basso nel gruppo]
    B --> G[Eccezioni: gas nobili,<br> gruppi 2 e 15]
```

> [!NOTE]
> L’affinità elettronica descrive un processo energetico isolato su atomi neutri in fase gassosa. Non deve essere confusa con l’elettronegatività, che si riferisce a sistemi legati.

---

# 3. Energia di ionizzazione

```mermaid
flowchart TD
    A[Energia di ionizzazione] --> B[Energia necessaria per<br> rimuovere un elettrone<br> da un atomo neutro]
    B --> C[X#40;g#41; → X⁺#40;g#41; + e⁻]
    B --> D[Alta energia di ionizzazione → <br>elettroni fortemente<br> trattenuti]
    B --> E[Aumenta da sinistra<br> a destra nel periodo]
    B --> F[Diminuisce dall'alto<br> verso il basso nel gruppo]
```

> [!NOTE]
> L’energia di ionizzazione misura la resistenza di un atomo alla perdita di elettroni. È strettamente correlata alla stabilità del guscio elettronico esterno.

---

# 4. Legame covalente puro

```mermaid
flowchart TD
    A[Legame covalente puro] --> B[Condivisione simmetrica<br> della coppia elettronica]
    B --> C[Differenza di <br>elettronegatività ~ 0]
    B --> D[Assenza di dipolo<br> elettrico permanente]
    B --> E[Esempi: H₂, Cl₂]
```

> [!NOTE]
> In un legame covalente puro, la densità elettronica è distribuita uniformemente tra i due atomi coinvolti.

---

# 5. Legame covalente polare

```mermaid
flowchart TD
    A[Legame covalente polare] --> B[Condivisione asimmetrica della coppia elettronica]
    B --> C[Differenza di <br>elettronegatività intermedia]
    B --> D[Formazione di <br>cariche parziali δ⁺ e δ⁻]
    B --> E[Presenza di <br>dipolo elettrico]
    B --> F[Esempi: H₂O, NH₃, HCl]
```

> [!NOTE]
> La polarizzazione del legame deriva dallo spostamento della densità elettronica verso l’atomo più elettronegativo.

---

# 6. Legame ionico

```mermaid
flowchart TD
    A[Legame ionico] --> B[Trasferimento quasi completo di elettroni]
    B --> C[Grande differenza <br>di elettronegatività]
    B --> D[Formazione di <br>cationi e anioni]
    B --> E[Attrazione <br>elettrostatica tra ioni]
    B --> F[Esempi: NaCl, KBr]
```

> [!NOTE]
> Il legame ionico è dominato dall’interazione coulombiana tra cariche opposte, più che dalla condivisione elettronica.

---

# 7. Relazione tra differenza di elettronegatività e tipo di legame

```mermaid
flowchart TD
    A[Differenza di elettronegatività ΔEN] --> B{Valore di ΔEN}

    B -->|≈ 0| C[Legame covalente puro]
    B -->|intermedia| D[Legame covalente polare]
    B -->|grande| E[Legame ionico]

    C --> F[Condivisione simmetrica]
    D --> G[Condivisione asimmetrica]
    E --> H[Trasferimento elettronico]
```

> [!NOTE]
> La classificazione dei legami in funzione di ΔEN è una approssimazione utile. In realtà, esiste un continuum tra carattere covalente e ionico.

---

# 8. Sintesi delle relazioni fondamentali

```mermaid
flowchart TD
    A[Proprietà atomiche] --> B[Elettronegatività]
    A --> C[Affinità elettronica]
    A --> D[Energia di ionizzazione]

    B --> E[Polarità del legame]
    C --> F[Tendenza ad acquisire elettroni]
    D --> G[Tendenza a perdere elettroni]

    E --> H[Tipi di legame chimico]
    H --> I[Covalente puro]
    H --> J[Covalente polare]
    H --> K[Ionico]
```

> [!NOTE]
> Le proprietà atomiche non sono indipendenti: derivano tutte dall’interazione tra carica nucleare efficace, schermaggio elettronico e distanza degli elettroni dal nucleo.

---

# Conclusione

La comprensione dei legami chimici richiede l’integrazione di tre concetti fondamentali: elettronegatività, affinità elettronica ed energia di ionizzazione. La loro variazione periodica consente di prevedere il comportamento chimico degli elementi e il tipo di legame che essi tendono a formare.
