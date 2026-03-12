# Chat Log Analysis Tool

Dieses Python-Skript wertet Chat-Logdateien aus einer ZIP-Datei aus und erstellt automatisch eine strukturierte **Excel-Auswertungsdatei**.

Das Tool wurde entwickelt, um Chatinteraktionen zwischen **User (z. B. Schüler:innen)** und einem **Assistant (KI-System)** quantitativ auszuwerten.

Die Ergebnisse werden in einer übersichtlichen Excel-Datei zusammengefasst und enthalten:

* eine **Gesamtauswertung über alle Versuchspersonen**
* **Auswertungsblätter pro User**
* **Rohdatenblätter pro User**

---

# Funktionsübersicht

Das Skript führt folgende Schritte aus:

1. Öffnet einen **Explorer-Dialog zur Auswahl einer ZIP-Datei**
2. Liest **alle `.txt` Logdateien** in der ZIP
3. Extrahiert die Chat-Ereignisse
4. Berechnet quantitative Kennwerte
5. Erstellt eine strukturierte **Excel-Datei (.xlsx)**

---

# Erwartetes Logformat

Die Logdateien müssen folgendes Format besitzen:

```
TYPE: USER_MESSAGE
TIME: 2026-03-12T09:14:12.250Z
URL: /LampenAi/2
USER: username
THREAD_ID: thread_id
CONTENT: Text der Nachricht
```

Mögliche Eventtypen:

* `USER_MESSAGE`
* `ASSISTANT_MESSAGE`

Mehrzeilige Inhalte werden automatisch korrekt verarbeitet.

---

# Berechnete Kennwerte

Für jede Seite (`URL`) werden folgende Parameter berechnet:

| Parameter          | Beschreibung                                                     |
| ------------------ | ---------------------------------------------------------------- |
| URL                | Seite innerhalb der Anwendung                                    |
| User_Messages      | Anzahl der User-Nachrichten                                      |
| User_Words         | Anzahl der Wörter der User                                       |
| Assistant_Messages | Anzahl der Assistant-Nachrichten                                 |
| Assistant_Words    | Anzahl der Wörter des Assistants                                 |
| Turns              | Anzahl der Dialogturns (User → Assistant)                        |
| Duration_Seconds   | Zeitspanne zwischen erster und letzter Interaktion auf der Seite |

---

# Aufbau der Excel-Datei

Die generierte Excel-Datei enthält mehrere Tabellenblätter.

## 1. Gesamtauswertung

Erstes Tabellenblatt der Datei.

Enthält:

### Werte pro Versuchsperson

| USER | User_Messages | User_Words | Assistant_Messages | Assistant_Words | Turns | Duration_Seconds |

### Statistische Kennwerte über alle VP

* N
* Mittelwert
* Median
* Minimum
* Maximum
* Standardabweichung

---

## 2. Auswertungsblätter pro User

Blattname:

```
Username_Auswertung
```

Enthält die Kennwerte **pro Seite (URL)**.

Beispiel:

| URL | User_Messages | User_Words | Assistant_Messages | Assistant_Words | Turns | Duration_Seconds |

Am Ende befindet sich eine **TOTAL-Zeile**.

---

## 3. Rohdatenblätter pro User

Blattname:

```
Username_Rohdaten
```

Spalten:

| USER | TYPE | TIME | URL | THREAD_ID | CONTENT |

Diese Tabelle enthält die **unveränderten Logdaten**.

---

# Installation

Python ≥ 3.8 wird empfohlen.

Benötigte Bibliothek:

```
pip install openpyxl
```

`tkinter` wird für die Dateiauswahl verwendet und ist bei den meisten Python-Installationen bereits enthalten.

---

# Nutzung

Script starten:

```
python log_analysis.py
```

Danach erscheinen zwei Explorer-Dialoge:

1. **ZIP-Datei auswählen**

   Die ZIP-Datei muss mehrere `.txt` Logdateien enthalten.

2. **Speicherort der Excel-Datei wählen**

   Hier kannst du Dateiname und Speicherort festlegen.

---

# Beispielstruktur der ZIP-Datei

```
logs.zip
│
├── user_01.txt
├── user_02.txt
├── user_03.txt
```

Jede Datei repräsentiert eine **Versuchsperson**.

---

# Hinweise zur Interpretation der Dauer

Die Variable

```
Duration_Seconds
```

berechnet:

```
letzter Zeitstempel − erster Zeitstempel
```

auf einer Seite.

Damit wird die **beobachtbare Interaktionsdauer** gemessen.
Reine Lesezeiten ohne Interaktion können damit nicht erfasst werden.

---

# Typische Anwendungsfälle

Das Tool eignet sich besonders für:

* Analyse von **KI-gestützten Lernsystemen**
* Evaluation von **Chatbot-Interaktionen**
* Quantitative Analyse von **Dialogverhalten**
* Forschung im Bereich **Educational Technology**

---

# Lizenz

Dieses Skript kann frei für Forschungszwecke verwendet und angepasst werden.
