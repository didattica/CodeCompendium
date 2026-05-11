# Cisco IOS — Come leggere `show interfaces`

## Idea fondamentale

Cisco IOS utilizza una **UI testuale gerarchica**.
Non usa colori o elementi grafici moderni, ma organizza le informazioni tramite:

* indentazione,
* spazi bianchi,
* ordine costante,
* gruppi logici.

> [!NOTE]
> In Cisco IOS la posizione del testo rispetto al margine sinistro è importante.
> L'indentazione indica relazione gerarchica tra le informazioni.

---

# Struttura generale dell'output

```text
GigabitEthernet0/0 is up, line protocol is up
  Hardware is ...
  Internet address is ...
  MTU ...
     reliability ...
```

---

# Livelli di indentazione

## 1. Nessuna indentazione → nuova sezione

```text
GigabitEthernet0/0 is up, line protocol is up
```

Questa riga rappresenta:

* una nuova interfaccia,
* l'inizio di un nuovo blocco logico.

> [!TIP]
> Gli amministratori Cisco leggono prima il margine sinistro per individuare rapidamente le interfacce.

---

## 2. Due spazi → proprietà dell'interfaccia

```text
  Hardware is ...
  Internet address is ...
```

Queste righe descrivono l'interfaccia dichiarata sopra.

---

## 3. Indentazione maggiore → sotto-dettagli

```text
     reliability 255/255
```

Questa riga è un dettaglio della riga precedente (`MTU`, `BW`, `DLY`).

---

# Ordine logico delle informazioni

Cisco IOS organizza quasi sempre l'output in questo ordine:

| Ordine | Contenuto                  |
| ------ | -------------------------- |
| 1      | Stato interfaccia          |
| 2      | Identità hardware          |
| 3      | Configurazione IP          |
| 4      | Parametri prestazioni      |
| 5      | Protocollo / encapsulation |
| 6      | Statistiche traffico       |
| 7      | Errori                     |

---

# Esempi importanti

## Stato dell'interfaccia

```text
is up, line protocol is up
```

Significa:

* collegamento fisico OK,
* protocollo Layer 2 OK.

> [!NOTE]
> `up/up` = interfaccia funzionante.

---

## Interfaccia disabilitata

```text
administratively down
```

L'interfaccia è stata spenta manualmente con:

```text
shutdown
```

> [!WARNING]
> `administratively down` NON significa guasto fisico.
> Significa che l'interfaccia è stata disabilitata da configurazione.

---

## Errori

Verso la fine dell'output trovi:

```text
CRC
frame
collisions
overrun
```

Questi campi servono per troubleshooting.

> [!CAUTION]
> Errori CRC o collisioni elevate possono indicare:
>
> * problemi di cavo,
> * duplex mismatch,
> * congestione,
> * problemi hardware.

---

# Filosofia Cisco IOS

Cisco IOS nasce per:

* terminali seriali,
* connessioni lente,
* amministrazione remota.

Per questo:

* tutto è testuale,
* l'output è compatto,
* la struttura è sempre coerente.

> [!TIP]
> Dopo un po', gli amministratori Cisco non leggono tutto il testo:
> riconoscono i pattern visivi e le keyword importanti.

---

# Concetto chiave finale

Cisco IOS usa una vera e propria "grammatica visuale":

* margine sinistro = livello principale,
* indentazione = relazione gerarchica,
* ordine delle righe = logica diagnostica.

L'output va quindi interpretato non solo leggendo il testo, ma anche osservando la struttura visiva.
