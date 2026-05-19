# 🚀 Guida Introduttiva al C++ per Arduino

## 📌 Introduzione

Arduino IDE utilizza una versione semplificata del linguaggio C++ per programmare microcontrollori embedded.

Quando si scrive un programma Arduino, il codice C++ viene:

1. compilato in linguaggio macchina;
2. trasferito sulla scheda;
3. eseguito direttamente dal microcontrollore.

Arduino fornisce librerie hardware che semplificano l’accesso a:

* pin digitali;
* convertitori analogico/digitali;
* comunicazione seriale;
* sensori e attuatori.

---

# ⚡ Architettura di un Programma Arduino

Un programma Arduino è chiamato **sketch**.

Ogni sketch contiene obbligatoriamente due funzioni principali:

```cpp id="n9n4q8"
void setup() {

}

void loop() {

}
```

---

## 🔹 Funzione `setup()`

La funzione `setup()` viene eseguita **una sola volta** all’avvio della scheda o dopo un reset.

È utilizzata per:

* configurare i pin di input/output;
* inizializzare periferiche hardware;
* avviare la comunicazione seriale;
* inizializzare sensori o librerie.

Esempio:

```cpp id="gx3t2m"
void setup() {
    pinMode(13, OUTPUT);
}
```

> [!NOTE]
> `pinMode()` configura il comportamento elettrico di un pin del microcontrollore.

---

## 🔹 Funzione `loop()`

La funzione `loop()` viene eseguita ciclicamente all’infinito finché la scheda rimane alimentata.

Esempio:

```cpp id="1z6v8s"
void loop() {

    digitalWrite(13, HIGH);
    delay(1000);

    digitalWrite(13, LOW);
    delay(1000);
}
```

Questo programma genera un lampeggio del LED integrato con periodo di 2 secondi.

---

# 📘 Variabili e Tipi di Dato

Le variabili permettono di memorizzare informazioni in memoria RAM.

---

## 🔹 `int`

Memorizza numeri interi.

```cpp id="v7x4pd"
int numero = 10;
```

Tipicamente su Arduino Uno:

```text
-32768 → 32767
```

---

## 🔹 `float`

Memorizza numeri in virgola mobile.

```cpp id="4m2c1w"
float temperatura = 23.5;
```

---

## 🔹 `char`

Memorizza un singolo carattere ASCII.

```cpp id="7y2k3p"
char lettera = 'A';
```

---

## 🔹 `bool`

Memorizza valori logici booleani.

```cpp id="8c5n2d"
bool acceso = true;
```

Possibili valori:

```text
true
false
```

---

# 📘 Operatori

## 🔹 Operatori Aritmetici

| Operatore | Descrizione           |
| --------- | --------------------- |
| `+`       | Somma                 |
| `-`       | Sottrazione           |
| `*`       | Moltiplicazione       |
| `/`       | Divisione             |
| `%`       | Resto della divisione |

Esempio:

```cpp id="2r9m5n"
int risultato = 10 + 5;
```

---

## 🔹 Operatori di Confronto

| Operatore | Significato       |
| --------- | ----------------- |
| `==`      | Uguale            |
| `!=`      | Diverso           |
| `>`       | Maggiore          |
| `<`       | Minore            |
| `>=`      | Maggiore o uguale |
| `<=`      | Minore o uguale   |

---

# 📘 Strutture Condizionali

Le strutture condizionali consentono di eseguire codice solo se una determinata condizione è verificata.

---

## 🔹 `if`

```cpp id="0h4q6l"
if (temperatura > 30) {
    Serial.println("Fa caldo");
}
```

---

## 🔹 `if / else`

```cpp id="6b7k2f"
if (temperatura > 30) {

    Serial.println("Fa caldo");

} else {

    Serial.println("Temperatura normale");
}
```

---

# 📘 Cicli Iterativi

---

## 🔹 Ciclo `for`

Ripete un blocco di istruzioni un numero definito di volte.

```cpp id="j8f2w5"
for (int i = 0; i < 5; i++) {
    Serial.println(i);
}
```

---

## 🔹 Ciclo `while`

Esegue il codice finché la condizione rimane vera.

```cpp id="m3v6t1"
while (true) {
    Serial.println("Loop infinito");
}
```

> [!WARNING]
> Un ciclo infinito può bloccare l’esecuzione del programma se non gestito correttamente.

---

# 📘 Funzioni

Le funzioni permettono di organizzare e riutilizzare codice.

---

## 🔹 Definizione di Funzione

```cpp id="a5x8q2"
void saluta() {
    Serial.println("Ciao!");
}
```

Invocazione:

```cpp id="t7d4z3"
saluta();
```

---

## 🔹 Funzione con Parametri

```cpp id="r4u9n1"
void accendiLed(int pin) {
    digitalWrite(pin, HIGH);
}
```

---

# 📘 Comunicazione Seriale

## 🔹 Cos’è la Porta Seriale

La **porta seriale** è un’interfaccia di comunicazione che permette lo scambio di dati tra:

* Arduino e PC;
* Arduino e altri microcontrollori;
* Arduino e moduli esterni (Bluetooth, GPS, Wi-Fi, sensori seriali).

La comunicazione avviene trasmettendo i dati **un bit alla volta** in sequenza temporale.

---

## 🔹 Oggetto `Serial`

In Arduino, `Serial` è un oggetto fornito dalla libreria hardware che gestisce la comunicazione UART/USB seriale.

Esempio:

```cpp id="z5g7v1"
Serial.println("Test");
```

Qui:

* `Serial` → oggetto seriale;
* `.println()` → metodo dell’oggetto.

---

# 📘 `Serial.begin(9600)`

La funzione:

```cpp id="x2n8k7"
Serial.begin(9600);
```

inizializza la comunicazione seriale.

---

## 🔹 Significato Tecnico

`begin()` configura l’hardware UART del microcontrollore definendo:

* velocità di trasmissione;
* sincronizzazione dei dati;
* formato del frame seriale.

---

## 🔹 Significato del Valore `9600`

Il numero `9600` rappresenta il **baud rate**.

Il baud rate indica il numero di simboli/bit trasmessi ogni secondo.

Nel caso di:

```cpp id="f1v3w9"
Serial.begin(9600);
```

la comunicazione avviene a:

```text
9600 bit/s
```

---

> [!IMPORTANT]
> Il baud rate impostato su Arduino deve coincidere con quello configurato nel Monitor Seriale dell’IDE, altrimenti i dati ricevuti risultano corrotti o incomprensibili.

---

## 🔹 Baud Rate Comuni

| Baud Rate | Utilizzo               |
| --------- | ---------------------- |
| `9600`    | Standard e stabile     |
| `19200`   | Comunicazioni moderate |
| `57600`   | Trasmissione veloce    |
| `115200`  | Alta velocità          |

---

## 🔹 Esempio Completo

```cpp id="q8m2v5"
void setup() {

    Serial.begin(9600);

    Serial.println("Sistema avviato");
}

void loop() {

}
```

---

# 📘 Monitor Seriale

Il **Serial Monitor** dell’IDE Arduino consente di:

* visualizzare dati inviati dalla scheda;
* effettuare debug;
* inviare comandi testuali ad Arduino.

---

## 🔹 Stampare Testo

```cpp id="d2w6c9"
Serial.println("Ciao Arduino");
```

---

## 🔹 Stampare Variabili

```cpp id="g4h1s8"
int numero = 5;

Serial.println(numero);
```

---

> [!TIP]
> Il debug seriale è uno degli strumenti più importanti nello sviluppo embedded.

---

# 📘 Input e Output Digitali

---

## 🔹 Configurare un Pin come OUTPUT

```cpp id="p3x7k4"
pinMode(13, OUTPUT);
```

---

## 🔹 Configurare un Pin come INPUT

```cpp id="v1n5r6"
pinMode(2, INPUT);
```

---

# 📘 Controllo di un LED

## 🔹 Accensione

```cpp id="u9k4z2"
digitalWrite(13, HIGH);
```

---

## 🔹 Spegnimento

```cpp id="y2b6f8"
digitalWrite(13, LOW);
```

---

# 📘 Lettura di un Pulsante

```cpp id="e7m2q5"
int pulsante = digitalRead(2);

if (pulsante == HIGH) {
    Serial.println("Premuto");
}
```

---

# 📘 Ingressi Analogici

Arduino possiede convertitori ADC (Analog-to-Digital Converter).

```cpp id="w4x1n9"
int valore = analogRead(A0);
```

Valori acquisibili:

```text
0 → 1023
```

su convertitori ADC a 10 bit.

---

# 📘 PWM (Pulse Width Modulation)

La tecnica PWM consente di simulare una tensione analogica mediante segnali digitali impulsivi.

```cpp id="o8r2k6"
analogWrite(9, 128);
```

Intervallo:

```text
0 → 255
```

---

> [!NOTE]
> PWM viene utilizzato per:
>
> * controllo luminosità LED;
> * velocità motori;
> * controllo di potenza.

---

# 📘 Array

Gli array memorizzano collezioni di dati omogenei.

```cpp id="l3v9m2"
int numeri[5] = {1, 2, 3, 4, 5};
```

Accesso:

```cpp id="h6n2q7"
Serial.println(numeri[0]);
```

---

# 📘 Stringhe

```cpp id="s5c8x1"
String nome = "Arduino";
```

Concatenazione:

```cpp id="b4m7t9"
String frase = "Ciao " + nome;
```

---

> [!WARNING]
> L’uso eccessivo della classe `String` può frammentare la memoria RAM nei microcontrollori con risorse limitate.

---

# 📘 Programmazione a Oggetti

Arduino utilizza concetti base di programmazione orientata agli oggetti (OOP).

Esempio:

```cpp id="n7k5p1"
Serial.println("Test");
```

* `Serial` → oggetto;
* `println()` → metodo;
* l’oggetto incapsula dati e funzionalità.

---

# 📘 Librerie

Le librerie estendono le funzionalità disponibili.

## 🔹 Inclusione di Libreria

```cpp id="q3f9z2"
#include <Servo.h>
```

---

# 📘 Esempio Completo

Sistema con pulsante, LED e debug seriale.

```cpp id="c2w8v5"
int led = 13;
int bottone = 2;

void setup() {

    pinMode(led, OUTPUT);
    pinMode(bottone, INPUT);

    Serial.begin(9600);
}

void loop() {

    int stato = digitalRead(bottone);

    if (stato == HIGH) {

        digitalWrite(led, HIGH);

        Serial.println("LED acceso");

    } else {

        digitalWrite(led, LOW);

        Serial.println("LED spento");
    }
}
```

---

# 📘 Errori Comuni

## ❌ Dimenticare `;`

```cpp id="m8x4k1"
int x = 5;
```

---

## ❌ Confondere `=` con `==`

Errato:

```cpp id="t5q2v8"
if (x = 5)
```

Corretto:

```cpp id="u7k1m3"
if (x == 5)
```

---

# 📘 Differenze tra Arduino e C++ Standard

Arduino introduce alcune semplificazioni:

* il `main()` è nascosto;
* gestione hardware integrata;
* librerie preconfigurate;
* API semplificate per microcontrollori.

Tuttavia il linguaggio rimane C++.

---

# 📘 Risorse Ufficiali

* [Arduino Official Website](https://www.arduino.cc/?utm_source=chatgpt.com)
* [Arduino Documentation](https://docs.arduino.cc/?utm_source=chatgpt.com)

---

# 🎯 Conclusione

Lo studio di Arduino permette di acquisire competenze in:

* programmazione embedded;
* elettronica digitale;
* acquisizione dati;
* automazione;
* sistemi cyber-fisici;
* Internet of Things (IoT).

Con pochi concetti fondamentali è possibile sviluppare:

* robot autonomi;
* sistemi domotici;
* dispositivi IoT;
* sistemi di monitoraggio;
* interfacce sensore-attuatore.
