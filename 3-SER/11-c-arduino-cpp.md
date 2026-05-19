# 🚀 Guida Base al C++ per Arduino

## 📌 Introduzione

Arduino utilizza una versione semplificata del linguaggio **C++**.

Quando programmi una scheda Arduino, stai scrivendo codice C++ che viene compilato ed eseguito sul microcontrollore.

Questa guida spiega:

- Le basi del C++
- Come funziona Arduino
- Variabili
- Funzioni
- Condizioni
- Cicli
- Input/Output
- Sensori e attuatori
- Programmazione orientata agli oggetti base

---

# ⚡ Come Funziona Arduino

Ogni programma Arduino è chiamato **sketch**.

Uno sketch ha sempre due funzioni principali:

```cpp
void setup() {

}

void loop() {

}
```

---

## 🔹 setup()

Viene eseguita **una sola volta** all'accensione.

Serve per:

- inizializzare pin
- avviare comunicazioni seriali
- configurare sensori

Esempio:

```cpp
void setup() {
    pinMode(13, OUTPUT);
}
```

---

## 🔹 loop()

Viene eseguita continuamente all'infinito.

Esempio:

```cpp
void loop() {
    digitalWrite(13, HIGH);
    delay(1000);

    digitalWrite(13, LOW);
    delay(1000);
}
```

Questo fa lampeggiare il LED integrato.

---

# 📘 Variabili

Le variabili servono a memorizzare dati.

---

## 🔹 int

Numeri interi.

```cpp
int numero = 10;
```

---

## 🔹 float

Numeri decimali.

```cpp
float temperatura = 23.5;
```

---

## 🔹 char

Singolo carattere.

```cpp
char lettera = 'A';
```

---

## 🔹 bool

Valori veri o falsi.

```cpp
bool acceso = true;
```

---

# 📘 Operatori

## 🔹 Matematici

```cpp
+   somma
-   sottrazione
*   moltiplicazione
/   divisione
%   resto
```

Esempio:

```cpp
int risultato = 10 + 5;
```

---

## 🔹 Confronto

```cpp
==   uguale
!=   diverso
>    maggiore
<    minore
>=   maggiore uguale
<=   minore uguale
```

---

# 📘 Condizioni

Le condizioni permettono di prendere decisioni.

## 🔹 if

```cpp
if (temperatura > 30) {
    Serial.println("Fa caldo");
}
```

---

## 🔹 if / else

```cpp
if (temperatura > 30) {
    Serial.println("Fa caldo");
} else {
    Serial.println("Temperatura normale");
}
```

---

# 📘 Cicli

## 🔹 for

Ripete un'operazione un numero preciso di volte.

```cpp
for (int i = 0; i < 5; i++) {
    Serial.println(i);
}
```

---

## 🔹 while

Ripete finché la condizione è vera.

```cpp
while (true) {
    Serial.println("Loop infinito");
}
```

---

# 📘 Funzioni

Le funzioni servono per riutilizzare codice.

## 🔹 Creare una funzione

```cpp
void saluta() {
    Serial.println("Ciao!");
}
```

Uso:

```cpp
saluta();
```

---

## 🔹 Funzione con parametri

```cpp
void accendiLed(int pin) {
    digitalWrite(pin, HIGH);
}
```

---

# 📘 Serial Monitor

Il monitor seriale permette di comunicare con il PC.

---

## 🔹 Avvio seriale

```cpp
void setup() {
    Serial.begin(9600);
}
```

---

## 🔹 Stampare testo

```cpp
Serial.println("Ciao Arduino");
```

---

## 🔹 Stampare variabili

```cpp
int numero = 5;

Serial.println(numero);
```

---

# 📘 Input e Output

---

## 🔹 OUTPUT

```cpp
pinMode(13, OUTPUT);
```

---

## 🔹 INPUT

```cpp
pinMode(2, INPUT);
```

---

# 📘 Controllare un LED

## 🔹 Accendere

```cpp
digitalWrite(13, HIGH);
```

---

## 🔹 Spegnere

```cpp
digitalWrite(13, LOW);
```

---

# 📘 Leggere un Pulsante

```cpp
int pulsante = digitalRead(2);

if (pulsante == HIGH) {
    Serial.println("Premuto");
}
```

---

# 📘 Sensori Analogici

Arduino può leggere valori analogici.

```cpp
int valore = analogRead(A0);
```

Valori possibili:

```text
0 → 1023
```

---

# 📘 PWM

PWM permette di simulare tensioni analogiche.

```cpp
analogWrite(9, 128);
```

Valori:

```text
0 → 255
```

---

# 📘 Array

Gli array contengono più valori.

```cpp
int numeri[5] = {1, 2, 3, 4, 5};
```

Accesso:

```cpp
Serial.println(numeri[0]);
```

---

# 📘 Stringhe

```cpp
String nome = "Arduino";
```

Concatenazione:

```cpp
String frase = "Ciao " + nome;
```

---

# 📘 Oggetti nel C++

Arduino usa molto la programmazione a oggetti.

Esempio:

```cpp
Serial.println("Test");
```

Qui:

- `Serial` è un oggetto
- `.println()` è un metodo

---

# 📘 Librerie

Le librerie aggiungono funzionalità.

## 🔹 Includere libreria

```cpp
#include <Servo.h>
```

---

# 📘 Esempio Completo

Lampeggio LED con pulsante.

```cpp
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

# 📘 Consigli per Imparare

## 🔹 Parti da progetti semplici

- LED
- Pulsanti
- Sensori
- Servo motori

---

## 🔹 Impara il debug seriale

Usa spesso:

```cpp
Serial.println();
```

---

## 🔹 Leggi esempi ufficiali

Nell'IDE Arduino:

```text
File → Examples
```

---

# 📘 Errori Comuni

## ❌ Dimenticare il `;`

```cpp
int x = 5;
```

---

## ❌ Usare `=` invece di `==`

SBAGLIATO:

```cpp
if (x = 5)
```

CORRETTO:

```cpp
if (x == 5)
```

---

# 📘 Differenze tra Arduino e C++ Standard

Arduino semplifica alcune cose:

- non serve il `main()`
- alcune librerie sono automatiche
- gestione hardware integrata

Ma il linguaggio rimane C++.

---

# 📘 Risorse Utili

## 🔹 Sito ufficiale Arduino

https://www.arduino.cc/

---

## 🔹 Documentazione ufficiale

https://docs.arduino.cc/

---

# 🎯 Conclusione

Imparare Arduino significa imparare:

- elettronica
- logica
- programmazione C++

Con pochi concetti puoi già creare:

- robot
- sistemi domotici
- sensori
- display
- automazioni

Buono studio 🚀
