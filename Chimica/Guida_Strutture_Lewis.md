# Guida alle Strutture di Lewis: Molecole Neutre e Ioni Poliatomici

Questa guida fornisce un'analisi dettagliata e sistematica per la costruzione delle strutture di Lewis di 20 specie chimiche differenti, suddivise equamente tra molecole neutre (senza ioni) e ioni poliatomici. Ogni esempio è corredato da una descrizione, dal conteggio degli elettroni, dalla rappresentazione grafica bidimensionale (tramite tabelle HTML compatibili con GitHub) e da una spiegazione approfondita sulla natura dei legami presenti (puri, polari o dativi).

---

## 🚀 Metodologia per il Disegno delle Strutture di Lewis

Per determinare correttamente la disposizione degli elettroni in una molecola o in uno ione, si raccomanda di seguire rigorosamente i seguenti passaggi fisici e matematici:

1. **Calcolo degli Elettroni di Valenza Totali ($E_{tot}$):** Sommare gli elettroni di valenza di tutti gli atomi coinvolti (corrispondenti al gruppo della tavola periodica).
2. **Aggiustamento per la Carica (solo per Ioni):** * Per gli anioni (carica negativa), **sommare** il valore assoluto della carica al totale degli elettroni.
   * Per i cationi (carica positiva), **sottrarre** il valore assoluto della carica dal totale degli elettroni.
3. **Identificazione dell'Atomo Centrale:** Di norma è l'atomo meno elettronegativo (escludendo sempre l'Idrogeno, che può formare un solo legame).
4. **Distribuzione degli Ottetti:** Disporre i legami singoli tra l'atomo centrale e gli atomi periferici, quindi completare gli ottetti degli atomi esterni. Gli elettroni rimanenti vanno posizionati sull'atomo centrale come doppietti solitari (*lone pairs*).
5. **Verifica dell'Ottetto e Legami Multipli:** Se l'atomo centrale non raggiunge l'ottetto, spostare coppie solitarie dagli atomi esterni per formare legami doppi o tripli (o dativi).

> [!NOTE]
> Un **legame covalente dativo** (o di coordinazione) si verifica quando la coppia di elettroni condivisa proviene interamente da uno solo dei due atomi (il donatore), mentre l'altro (l'accettore) mette a disposizione un orbitale vuoto.

---

## ⚛️ Sezione 1: Molecole Senza Ioni (Neutre)

In questa sezione vengono esaminate 10 molecole elettricamente neutre, analizzando la polarità dei legami in base alle differenze di elettronegatività.

### Esempio 1: Acqua ($H_2O$)
* **Descrizione:** Molecola polare fondamentale, costituente principale dei fluidi biologici. Presenta una geometria piegata (VSEPR: $AX_2E_2$).
* **Input (Calcolo Elettroni):**
  * $H: 1 	imes 2 = 2$ elettroni
  * $O: 6 	imes 1 = 6$ elettroni
  * **Totale:** 8 elettroni (4 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center"><b>H</b></td>
  <td align="center">—</td>
  <td align="center"><b>O••</b></td>
  <td align="center">—</td>
  <td align="center"><b>H</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** L'atomo centrale di ossigeno forma due legami singoli con i due idrogeni e mantiene due coppie solitarie. I legami sono **covalenti polari** a causa della forte differenza di elettronegatività tra $O$ e $H$. Non sono presenti legami dativi.

---

### Esempio 2: Anidride Carbonica ($CO_2$)
* **Descrizione:** Gas serra lineare ($AX_2$), prodotto dai processi di combustione e respirazione cellulare.
* **Input (Calcolo Elettroni):**
  * $C: 4 	imes 1 = 4$ elettroni
  * $O: 6 	imes 2 = 12$ elettroni
  * **Totale:** 16 elettroni (8 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
</tr>
<tr>
  <td align="center"><b>O</b></td>
  <td align="center">=</td>
  <td align="center"><b>C</b></td>
  <td align="center">=</td>
  <td align="center"><b>O</b></td>
</tr>
<tr>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
</tr>
</table>

* **Spiegazione:** Il carbonio centrale forma due doppi legami con gli atomi di ossigeno per completare il proprio ottetto. I legami singoli sono **covalenti polari**, ma la simmetria lineare della molecola annulla i vettori di dipolo elettrico, rendendo la molecola globalmente apolare. Nessun legame dativo.

---

### Esempio 3: Azoto Molecolare ($N_2$)
* **Descrizione:** Gas biatomico inerte che costituisce circa il 78% dell'atmosfera terrestre.
* **Input (Calcolo Elettroni):**
  * $N: 5 	imes 2 = 10$ elettroni (5 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center"><b>••N</b></td>
  <td align="center">≡</td>
  <td align="center"><b>N••</b></td>
</tr>
</table>

* **Spiegazione:** Per soddisfare la regola dell'ottetto per entrambi gli atomi, l'azoto condivide tre coppie elettroniche formando un **triplo legame covalente puro** (o omopolare). L'elettronegatività identica dei due atomi rende il legame perfettamente simmetrico e non polare.

---

### Esempio 4: Monossido di Carbonio ($CO$)
* **Descrizione:** Gas tossico, inodore e incolore, noto per la sua elevata affinità con l'emoglobina.
* **Input (Calcolo Elettroni):**
  * $C: 4 	imes 1 = 4$ elettroni
  * $O: 6 	imes 1 = 6$ elettroni
  * **Totale:** 10 elettroni (5 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center"><b>••C</b></td>
  <td align="center">←</td>
  <td align="center"><b>O••</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center"><b>(=)</b></td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** Questo è un caso classico che include **1 legame covalente dativo** coordinato insieme a 2 legami covalenti standard (formando un triplo legame complessivo). L'ossigeno funge da donatore del doppietto per consentire al carbonio di raggiungere l'ottetto, generando una carica formale negativa sul carbonio e positiva sull'ossigeno. I legami sono polari.

---

### Esempio 5: Anidride Solforosa ($SO_2$)
* **Descrizione:** Gas pungente generato dalle eruzioni vulcaniche e dai processi industriali, avente geometria piegata.
* **Input (Calcolo Elettroni):**
  * $S: 6 	imes 1 = 6$ elettroni
  * $O: 6 	imes 2 = 12$ elettroni
  * **Totale:** 18 elettroni (9 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>S</b></td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
</tr>
<tr>
  <td align="center"><b>O</b></td>
  <td align="center">=</td>
  <td align="center">&nbsp;</td>
  <td align="center">→</td>
  <td align="center"><b>O••</b></td>
</tr>
<tr>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
</tr>
</table>

* **Spiegazione:** Nella sua formulazione classica rispettosa dell'ottetto fisso, lo zolfo forma un doppio legame covalente polare con un ossigeno e **1 legame covalente dativo** (rappresentato dalla freccia) con il secondo ossigeno, trasferendo idealmente la densità di una sua coppia solitaria. Tutti i legami sono polari.

---

### Esempio 6: Ammoniaca ($NH_3$)
* **Descrizione:** Composto base industriale con geometria piramidale trigonale ($AX_3E$), caratterizzato da un forte odore pungente.
* **Input (Calcolo Elettroni):**
  * $N: 5 	imes 1 = 5$ elettroni
  * $H: 1 	imes 3 = 3$ elettroni
  * **Totale:** 8 elettroni (4 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center"><b>N</b></td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>H</b> —</td>
  <td align="center">|</td>
  <td align="center">— <b>H</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center"><b>H</b></td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** L'azoto si lega tramite tre legami singoli **covalenti polari** ad altrettanti atomi di idrogeno, mantenendo un doppietto solitario sulla sommità. Non sono presenti legami dativi.

---

### Esempio 7: Trifluoruro di Boro ($BF_3$)
* **Descrizione:** Lewis acid per eccellenza, molecola planare trigonale che costituisce un'eccezione alla regola dell'ottetto per difetto (ottetto incompleto).
* **Input (Calcolo Elettroni):**
  * $B: 3 	imes 1 = 3$ elettroni
  * $F: 7 	imes 3 = 21$ elettroni
  * **Totale:** 24 elettroni (12 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••F••</b></td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">|</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>••••F</b> —</td>
  <td align="center"><b>B</b></td>
  <td align="center">— <b>F••••</b></td>
</tr>
</table>

* **Spiegazione:** Il boro centrale si stabilizza con soli 6 elettroni di valenza condivisi. I tre legami $B-F$ sono **altamente covalenti polari** a causa dell'altissima elettronegatività del fluoro. Non ci sono legami dativi.

---

### Esempio 8: Acido Cloridrico ($HCl$)
* **Descrizione:** Idracido forte, un gas altamente corrosivo che in soluzione acquosa forma l'acido muriatico.
* **Input (Calcolo Elettroni):**
  * $H: 1 	imes 1 = 1$ elettrone
  * $Cl: 7 	imes 1 = 7$ elettroni
  * **Totale:** 8 elettroni (4 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>H</b> —</td>
  <td align="center"><b>Cl••</b></td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** Presenta un unico legame singolo **covalente polare**. Il cloro, più elettronegativo, attrae fortemente la coppia di legame e si circonda di tre doppietti solitari. Nessun legame dativo.

---

### Esempio 9: Cloro Molecolare ($Cl_2$)
* **Descrizione:** Gas tossico di colore verde-giallastro appartenente al gruppo degli alogeni.
* **Input (Calcolo Elettroni):**
  * $Cl: 7 	imes 2 = 14$ elettroni (7 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>••Cl</b></td>
  <td align="center">—</td>
  <td align="center">&nbsp;</td>
  <td align="center">—</td>
  <td align="center"><b>Cl••</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** I due atomi identici condividono una sola coppia legante, generando un legame **covalente puro**. Entrambi completano l'ottetto conservando ciascuno tre coppie solitarie.

---

### Esempio 10: Esacloruro di Zolfo ($SF_6$)
* **Descrizione:** Gas inerte utilizzato come isolante elettrico, classico esempio di ottetto espanso (ipervalenza).
* **Input (Calcolo Elettroni):**
  * $S: 6 	imes 1 = 6$ elettroni
  * $Cl: 7 	imes 6 = 42$ elettroni
  * **Totale:** 48 elettroni (24 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center"><b>Cl</b></td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>Cl</b></td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>Cl</b></td>
  <td align="center">\</td>
  <td align="center">|</td>
  <td align="center">/</td>
  <td align="center"><b>Cl</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">—</td>
  <td align="center"><b>S</b></td>
  <td align="center">—</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>Cl</b></td>
  <td align="center">/</td>
  <td align="center">|</td>
  <td align="center">\</td>
  <td align="center"><b>Cl</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center"><b>Cl</b></td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>Cl</b></td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** Lo zolfo espande il proprio guscio di valenza sfruttando gli orbitali $d$ vuoti per ospitare 12 elettroni periferici. Tutti e 6 i legami generati sono **covalenti polari**. Nota: per motivi di spazio e pulizia del diagramma, i tre doppietti solitari attorno a ciascun atomo di $Cl$ sono stati omessi dal disegno, ma vanno conteggiati nell'ottetto esterno.

> [!IMPORTANT]
> L'espansione dell'ottetto (ipervalenza) è possibile solo per gli elementi a partire dal terzo periodo della tavola periodica (come $S$, $P$, $Cl$), in quanto possiedono orbitali $d$ energeticamente accessibili.

---

## 🔋 Sezione 2: Ioni Poliatomici

Questa sezione analizza 10 cariche ioniche racchiuse in strutture molecolari complessive. Il calcolo include la variazione elettronica dovuta al bilancio di carica.

### Esempio 11: Ione Ammonio ($NH_4^+$)
* **Descrizione:** Catione simmetrico derivante dalla protonazione dell'ammoniaca, componente dei sali d'ammonio.
* **Input (Calcolo Elettroni):**
  * $N: 5 	imes 1 = 5$ elettroni
  * $H: 1 	imes 4 = 4$ elettroni
  * Carica ($+$): Sottrare 1 elettrone $ightarrow -1$
  * **Totale:** $5 + 4 - 1 = 8$ elettroni (4 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>H</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center" rowspan="5" valign="middle"><b><font size="5">]</font> ⁺</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">|</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>[</b></td>
  <td align="center"><b>H</b> —</td>
  <td align="center"><b>N</b></td>
  <td align="center">— <b>H</b></td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">|</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>H</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** L'azoto condivide il suo doppietto solitario nativo con uno ione idrogeno ($H^+$) privo di elettroni, realizzando **1 legame covalente dativo**. Tutti e quattro i legami finali sono polari ed energeticamente equivalenti per risonanza geometrica.

---

### Esempio 12: Ione Idronio ($H_3O^+$)
* **Descrizione:** Catione caratteristico delle soluzioni acquose acide, responsabile del valore del pH.
* **Input (Calcolo Elettroni):**
  * $O: 6 	imes 1 = 6$ elettroni
  * $H: 1 	imes 3 = 3$ elettroni
  * Carica ($+$): Sottrare 1 elettrone $ightarrow -1$
  * **Totale:** $6 + 3 - 1 = 8$ elettroni (4 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center" rowspan="4" valign="middle"><b><font size="5">]</font> ⁺</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>O</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>[</b></td>
  <td align="center"><b>H</b> —</td>
  <td align="center">|</td>
  <td align="center">— <b>H</b></td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>H</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** Una molecola d'acqua coordina un protone esterno utilizzando uno dei doppietti liberi dell'ossigeno, dando origine a **1 legame covalente dativo**. I legami residui mantengono la loro natura di covalenti polari.

---

### Esempio 13: Ione Idrossido ($OH^-$)
* **Descrizione:** Anione tipico delle soluzioni basiche e degli idrossidi metallici.
* **Input (Calcolo Elettroni):**
  * $O: 6 	imes 1 = 6$ elettroni
  * $H: 1 	imes 1 = 1$ elettrone
  * Carica ($-$): Aggiungere 1 elettrone $ightarrow +1$
  * **Totale:** $6 + 1 + 1 = 8$ elettroni (4 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
  <td align="center" rowspan="3" valign="middle"><b><font size="5">]</font> ⁻</b></td>
</tr>
<tr>
  <td align="center"><b>[</b></td>
  <td align="center"><b>H</b> —</td>
  <td align="center"><b>O••</b></td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** L'ossigeno completa l'ottetto accogliendo l'elettrone supplementare della carica negativa. Il legame tra ossigeno e idrogeno è un legame singolo **covalente polari**. Nessun legame dativo presente.

---

### Esempio 14: Ione Solfato ($SO_4^{2-}$)
* **Descrizione:** Anione poliatomico altamente stabile, presente nell'acido solforico e in molti composti minerali.
* **Input (Calcolo Elettroni):**
  * $S: 6 	imes 1 = 6$ elettroni
  * $O: 6 	imes 4 = 24$ elettroni
  * Carica ($2-$): Aggiungere 2 elettroni $ightarrow +2$
  * **Totale:** $6 + 24 + 2 = 32$ elettroni (16 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>O</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center" rowspan="5" valign="middle"><b><font size="5">]</font> ²⁻</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">↑</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>[</b></td>
  <td align="center"><b>O</b> ←</td>
  <td align="center"><b>S</b></td>
  <td align="center">→</td>
  <td align="center"><b>O</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">↓</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>O</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** Nella struttura canonica rigida ad ottetti atomici singoli, lo zolfo centrale completa l'ottetto legandosi a due ossigeni esterni (che acquisiscono formalmente gli elettroni della carica), e attiva **2 legami covalenti dativi** verso i restanti due ossigeni neutri. Tutti i legami sono polari. *(Nota: i doppietti esterni degli ossigeni non sono mostrati nel diagramma).*

---

### Esempio 15: Ione Nitrato ($NO_3^-$)
* **Descrizione:** Anione planare trigonale, forte ossidante presente nei fertilizzanti e nei composti esplosivi.
* **Input (Calcolo Elettroni):**
  * $N: 5 	imes 1 = 5$ elettroni
  * $O: 6 	imes 3 = 18$ elettroni
  * Carica ($-$): Aggiungere 1 elettrone $ightarrow +1$
  * **Totale:** $5 + 18 + 1 = 24$ elettroni (12 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>O</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center" rowspan="5" valign="middle"><b><font size="5">]</font> ⁻</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">||</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>[</b></td>
  <td align="center"><b>O</b> —</td>
  <td align="center"><b>N</b></td>
  <td align="center">→</td>
  <td align="center"><b>O</b></td>
</tr>
</table>

* **Spiegazione:** L'azoto centrale esibisce un doppio legame covalente polare con un ossigeno, un legame singolo polare con il secondo ossigeno (carico negativamente) e **1 legame covalente dativo** verso il terzo ossigeno. La struttura reale è un ibrido di risonanza.

---

### Esempio 16: Ione Carbonato ($CO_3^{2-}$)
* **Descrizione:** Anione costituente dei minerali calcarei e fondamentale per il tamponamento del pH del sangue umano.
* **Input (Calcolo Elettroni):**
  * $C: 4 	imes 1 = 4$ elettroni
  * $O: 6 	imes 3 = 18$ elettroni
  * Carica ($2-$): Aggiungere 2 elettroni $ightarrow +2$
  * **Totale:** $4 + 18 + 2 = 24$ elettroni (12 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>O</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center" rowspan="5" valign="middle"><b><font size="5">]</font> ²⁻</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">||</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>[</b></td>
  <td align="center"><b>O</b> —</td>
  <td align="center"><b>C</b></td>
  <td align="center">— <b>O</b></td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** Il carbonio forma un doppio legame e due legami singoli con i tre ossigeni periferici. Tutti i legami risultano **covalenti polari**. Non si riscontrano legami dativi poiché il carbonio distribuisce normalmente i suoi quattro elettroni originari.

---

### Esempio 17: Ione Fosfato ($PO_4^{3-}$)
* **Descrizione:** Anione biologico cruciale per la costituzione dello scheletro del DNA, dell'RNA e dell'ATP.
* **Input (Calcolo Elettroni):**
  * $P: 5 	imes 1 = 5$ elettroni
  * $O: 6 	imes 4 = 24$ elettroni
  * Carica ($3-$): Aggiungere 3 elettroni $ightarrow +3$
  * **Totale:** $5 + 24 + 3 = 32$ elettroni (16 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>O</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center" rowspan="5" valign="middle"><b><font size="5">]</font> ³⁻</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">|</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>[</b></td>
  <td align="center"><b>O</b> —</td>
  <td align="center"><b>P</b></td>
  <td align="center">→</td>
  <td align="center"><b>O</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">|</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>O</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** Il fosforo centrale genera tre legami singoli polari con gli ossigeni carichi negativamente e **1 legame covalente dativo** verso l'atomo di ossigeno neutro, portando a compimento l'ottetto strutturale in forma polare.

---

### Esempio 18: Ione Perclorato ($ClO_4^-$)
* **Descrizione:** Anione energetico derivante dall'acido perclorato, utilizzato nei propellenti solidi per razzi.
* **Input (Calcolo Elettroni):**
  * $Cl: 7 	imes 1 = 7$ elettroni
  * $O: 6 	imes 4 = 24$ elettroni
  * Carica ($-$): Aggiungere 1 elettrone $ightarrow +1$
  * **Totale:** $7 + 24 + 1 = 32$ elettroni (16 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>O</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center" rowspan="5" valign="middle"><b><font size="5">]</font> ⁻</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">↑</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center"><b>[</b></td>
  <td align="center"><b>O</b> ←</td>
  <td align="center"><b>Cl</b></td>
  <td align="center">→</td>
  <td align="center"><b>O</b></td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center">↓</td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>O</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
</tr>
</table>

* **Spiegazione:** Il cloro condivide un legame singolo normale con l'ossigeno recante la carica netta e impegna le proprie rimanenti tre coppie solitarie per attivare **3 legami covalenti dativi** indipendenti con gli altri tre ossigeni. Legami fortemente polari.

---

### Esempio 19: Ione Cianuro ($CN^-$)
* **Descrizione:** Anione tossico lineare, noto per inibire la catena di trasporto degli elettroni mitocondriale.
* **Input (Calcolo Elettroni):**
  * $C: 4 	imes 1 = 4$ elettroni
  * $N: 5 	imes 1 = 5$ elettroni
  * Carica ($-$): Aggiungere 1 elettrone $ightarrow +1$
  * **Totale:** $4 + 5 + 1 = 10$ elettroni (5 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center"><b>[</b></td>
  <td align="center"><b>••C</b></td>
  <td align="center">≡</td>
  <td align="center"><b>N••</b></td>
  <td align="center" rowspan="1" valign="middle"><b><font size="5">]</font> ⁻</b></td>
</tr>
</table>

* **Spiegazione:** L'elettrone aggiuntivo stabilizza l'ottetto permettendo la formazione di un **triplo legame covalente polare** tra il carbonio e l'azoto. Ciascun elemento conserva un doppietto elettronico solitario. Nessun legame dativo.

---

### Esempio 20: Ione Nitrito ($NO_2^-$)
* **Descrizione:** Anione piegato impiegato nella conservazione alimentare per prevenire il botulismo.
* **Input (Calcolo Elettroni):**
  * $N: 5 	imes 1 = 5$ elettroni
  * $O: 6 	imes 2 = 12$ elettroni
  * Carica ($-$): Aggiungere 1 elettrone $ightarrow +1$
  * **Totale:** $5 + 12 + 1 = 18$ elettroni (9 coppie)
* **Output (Struttura di Lewis):**

<table>
<tr>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center"><b>••</b></td>
  <td align="center">&nbsp;</td>
  <td align="center">&nbsp;</td>
  <td align="center" rowspan="4" valign="middle"><b><font size="5">]</font> ⁻</b></td>
</tr>
<tr>
  <td align="center"><b>[</b></td>
  <td align="center"><b>O</b></td>
  <td align="center">=</td>
  <td align="center"><b>N</b></td>
  <td align="center">→</td>
  <td align="center"><b>O</b></td>
</tr>
</table>

* **Spiegazione:** L'azoto centrale mantiene una coppia solitaria e si connette alla periferia tramite un doppio legame covalente standard e **1 legame covalente dativo**. L'intera struttura sperimenta delocalizzazione per risonanza chimica.

---

## ⚠️ Avvertenze Tecniche e Casi Limite

> [!WARNING]
> La teoria di Lewis non tiene conto della geometria tridimensionale reale delle molecole (esplicitata dalla teoria VSEPR) né della delocalizzazione elettronica reale degli orbitali molecolari.

> [!CAUTION]
> Quando si disegnano gli ioni poliatomici, l'omissione delle parentesi quadre o della carica esterna rende la struttura di Lewis formalmente errata, poiché il conteggio elettronico non corrisponderebbe al sistema grafico rappresentato.

> [!TIP]
> Per verificare l'accuratezza di una struttura, calcolare sempre la **carica formale** ($CF$) di ciascun atomo con la formula:
> $$CF = E_{valenza} - E_{solitari} - \frac{1}{2}E_{condivisi}$$
> La somma delle cariche formali deve coincidere con la carica complessiva della specie chimica analizzata.
