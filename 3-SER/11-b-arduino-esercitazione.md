# Introduzione ai Circuiti con Tinkercad

## Dall’LED base ai circuiti interattivi

---

# Obiettivo

Imparare a costruire circuiti elettronici passo dopo passo usando :contentReference[oaicite:0]{index=0}:

- Comprendere i componenti base
- Imparare il cablaggio corretto
- Introdurre logiche di controllo e interazione

---

# Livello 1 — Circuito Base (LED + Resistenza)

## Obiettivo: accendere un LED in sicurezza

### Componenti:
- 1 LED
- 1 resistenza (220Ω o 330Ω)
- Alimentazione (5V)

### Concetto:
- La resistenza limita la corrente per proteggere il LED
- Circuito semplice e chiuso

### Risultato:
- Il LED si accende stabilmente

---

# Livello 2 — Uso della Breadboard

## Obiettivo: organizzare il circuito

### Componenti:
- LED
- Resistenza
- Breadboard
- Cavi jumper
- Alimentazione

### Concetto:
- Comprendere la struttura della breadboard (righe e colonne)
- Collegamenti ordinati e modulari

### Risultato:
- Stesso circuito del livello 1, ma più pulito e scalabile

---

# Livello 3 — LED Lampeggiante

## Obiettivo: far lampeggiare un LED

### Componenti:
- LED
- Resistenza
- Breadboard
- Alimentazione

### Concetto:
- Introduzione al comportamento dinamico del circuito
- Alternanza ON/OFF (manuale o simulata in Tinkercad)

### Risultato:
- Il LED si accende e si spegne a intervalli regolari

### code del Led che lampeggia

// Definiamo i pin
int led = 13;

void setup() {
}

void loop() {
    
    // --- INIZIO SEQUENZA LAMPEGGIO ---
    digitalWrite(led, HIGH); // 1. Accendi il LED
    delay(300);              // 2. Aspetta 0.3 secondi
    digitalWrite(led, LOW);  // 3. Spegni il LED
    delay(300);              // 4. Aspetta 0.3 secondi
    // --- FINE SEQUENZA LAMPEGGIO ---
    

}

---

# Livello 4 — Circuito Interattivo (Pulsante)

## Obiettivo: controllare il LED con un pulsante

### Componenti:
- LED
- Resistenza
- Pulsante
- Breadboard
- Cavi jumper
- Alimentazione

### Concetto:
- Il pulsante funziona come interruttore
- Il circuito si chiude solo quando viene premuto

### Risultato:
- Il LED si accende solo quando il pulsante è premuto

  ### code del pulsante

const int pinPulsante = 2;
const int pinLED = 13;

void setup() {
  pinMode(pinPulsante, INPUT_PULLUP); // Usa la resistenza interna di Arduino
  pinMode(pinLED, OUTPUT);
}

void loop() {
  int statoPulsante = digitalRead(pinPulsante);

  // Se il pulsante è premuto (collegato a GND), lo stato è LOW
  if (statoPulsante == LOW) {
    digitalWrite(pinLED, HIGH);
  } else {
    digitalWrite(pinLED, LOW);
  }
}

---

# Riepilogo

## Competenze acquisite:

- Componenti elettronici base
- Protezione dei circuiti (resistenza)
- Uso della breadboard
- Logica di controllo (lampeggio)
- Input digitale (pulsante)

---

# Prossimi passi

- Aggiungere più LED in sequenza
- Usare sensori (luce, temperatura)
- Introdurre microcontrollori (Arduino)
