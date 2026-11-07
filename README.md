# 📊 Notenrechner

Ein Notenrechner für die Schule, der komplett im Browser läuft. Du trägst Prüfungsnoten pro Fach ein und siehst sofort Durchschnitte, Zeugnisnoten, Mangelpunkte und den Notenverlauf in verschiedenen Diagrammen. Dazu gibt es Semester und Jahre, eine Prognose für die nächste Prüfung und Presets zum Speichern deiner Einstellungen.

Es braucht keine Installation, keinen Server und kein Konto. Alle Daten bleiben in deinem Browser.

---

## Inhaltsverzeichnis

- [Funktionen im Überblick](#funktionen-im-überblick)
- [Schnellstart](#schnellstart)
- [Projektstruktur](#projektstruktur)
- [Bedienung](#bedienung)
  - [Semester, Gesamt- und Jahresansicht](#semester-gesamt--und-jahresansicht)
  - [Durchschnitte](#durchschnitte)
  - [Diagramm und Ansichten](#diagramm-und-ansichten)
  - [Kompensationen](#kompensationen)
  - [Noten, Sperren und Note erfassen](#noten-sperren-und-note-erfassen)
  - [Selbstbewertung und Prognose](#selbstbewertung-und-prognose)
  - [Presets](#presets)
- [Berechnungen](#berechnungen)
- [Datenspeicherung und Datenschutz](#datenspeicherung-und-datenschutz)
- [Technische Details](#technische-details)
- [Veröffentlichen mit GitHub Pages](#veröffentlichen-mit-github-pages)
- [Lizenz](#lizenz)

---

## Funktionen im Überblick

| Bereich                | Was es kann                                                                       |
| ---------------------- | --------------------------------------------------------------------------------- |
| **Fächer**             | Hinzufügen und löschen, jedes Fach hat eine eigene Farbe, die nur einmal vorkommt |
| **Prüfungen**          | 1 bis 10 Prüfungen pro Fach einstellbar, mit Prüfungsnamen                        |
| **Durchschnitte**      | Beliebig viele Gruppen von Fächern mit Durchschnitt und Mangelpunkten             |
| **Diagramme**          | Linien, Fläche, Balken, horizontale Balken, Punkte und Netzdiagramm               |
| **Ansichten**          | Mehrere Diagramm-Ansichten als Tabs, wie in Notion                                |
| **Semester und Jahre** | Mehrere Semester, Gesamtansicht und Jahresansicht mit Entwicklung                 |
| **Kompensationen**     | Prüft, ob ungenügende Fächer durch andere ausgeglichen werden können              |
| **Noten sperren**      | Noten nur über «Note erfassen», auch aus Punktzahlen berechnet                    |
| **Prognose**           | Erwartete Note der nächsten Prüfung mit Selbstbewertung und Kerzendiagramm        |
| **Presets**            | Einstellungen als Datei speichern, laden und aus einem Ordner auswählen           |
| **Darstellung**        | Heller und dunkler Modus, geeignet für Computer und Smartphone                    |

---

## Schnellstart

1. Das Repository klonen oder die drei Dateien herunterladen:
   ```bash
   git clone https://github.com/<dein-benutzername>/<dein-repository>.git
   ```
2. `index.html` im Browser öffnen.
3. Noten eintragen.

> Für die Diagramme wird [Chart.js](https://www.chartjs.org/) von cdnjs geladen. Beim ersten Öffnen ist deshalb eine Internetverbindung nötig.

Beim ersten Start sind Beispielnoten und zwei Beispiel-Durchschnitte angelegt. Du kannst alles ändern oder mit **Zurücksetzen** löschen.

---

## Projektstruktur

```
.
├── index.html   # Aufbau der Seite
├── style.css    # Design, auch der dunkle Modus
├── script.js    # die komplette Logik
└── README.md
```

Alle drei Dateien müssen im **selben Ordner** liegen.

---

## Bedienung

### Semester, Gesamt- und Jahresansicht

Ganz oben steht eine Tab-Leiste mit deinen Semestern.

- **+** legt ein neues Semester an. Du gibst Name und Jahr ein (zum Beispiel 2026/27). Optional übernimmt es Fächer und Durchschnitte des aktuellen Semesters, aber ohne Noten.
- **⋮** (beim aktiven Semester) ändert Name und Jahr, **✕** löscht das Semester mit Rückfrage. Das letzte Semester kann nicht gelöscht werden.
- Jedes Semester hat **eigene Fächer, Noten, Ansichten und Selbstbewertungen**.
- **Gesamtansicht**: Entwicklung über alle Semester als Diagramm und Tabelle. Du wählst per Knopf, welche Werte angezeigt werden: den Gesamtdurchschnitt, deine Durchschnitte oder einzelne Fächer.
- **Jahresansicht**: wie die Gesamtansicht, aber ein Wert pro Jahr. Semester mit demselben Jahr werden zusammengefasst (Mittelwert, bei den Mangelpunkten die Summe).

### Durchschnitte

Die Kacheln oben zeigen deine Durchschnitte. Ein Durchschnitt ist eine frei gewählte Gruppe von Fächern.

| Aktion     | So geht es                                                                      |
| ---------- | ------------------------------------------------------------------------------- |
| Hinzufügen | **+ Durchschnitt hinzufügen**: Name eingeben, Fächer ankreuzen                  |
| Bearbeiten | **⋮** in der Kachel: Name, Fächer und die Option «Mangelpunkte anzeigen» ändern |
| Löschen    | **✕** in der Kachel, zur Bestätigung ein zweites Mal klicken                    |

Jede Kachel zeigt den Durchschnitt (grün ab 4.0, sonst rot) und auf Wunsch die Mangelpunkte.

### Diagramm und Ansichten

Über dem Diagramm steht eine Leiste mit **Ansichten**. Jede Ansicht merkt sich ihre eigenen Einstellungen.

- **+** legt eine Ansicht an (Name, Diagrammtyp, welche Prüfungen betrachtet werden).
- **⋮** bearbeitet die aktive Ansicht, **✕** löscht sie. Die letzte Ansicht bleibt bestehen.
- Das Auswahlfeld **Diagrammtyp** oben links gilt für die geöffnete Ansicht.

**Diagrammtypen**

| Typ                | Beschreibung                                                                                   |
| ------------------ | ---------------------------------------------------------------------------------------------- |
| Linien             | Verlauf der Noten über die Prüfungen                                                           |
| Fläche             | Wie Linien, mit eingefärbter Fläche                                                            |
| Balken             | Eine Note pro Balken und Prüfung                                                               |
| Horizontale Balken | Durchschnitt pro Fach, sortiert vom besten zum schlechtesten                                   |
| Punkte             | Nur die einzelnen Noten ohne Verbindung                                                        |
| Netzdiagramm       | Jedes Fach ist eine Achse. Zeigt die Noten einzelner Prüfungen und auf Wunsch den Durchschnitt |

**Auswahl und Anzeige**

- Ein **Fach anklicken** zeigt dessen Noten. Mit dem Schalter **Mehrere Fächer gleichzeitig vergleichen** wählst du mehrere Fächer.
- Ein **Durchschnitt** (Knopf mit gestricheltem Rand) oder **Alle** wählt gleich mehrere Fächer aus.
- **Gesamtbewertung anzeigen**: gestrichelte Linie über alle gewählten Fächer (bei mindestens zwei Fächern).
- **Linie bei 4.0 anzeigen**: rote gestrichelte Linie als Grenze zwischen genügend und ungenügend.
- Neben dem Diagramm steht der Durchschnitt jedes Fachs, grün oder rot, auf der Höhe der letzten Note.
- Die linke Achse zeigt halbe Noten von 1 bis 6.
- Horizontale Balken und Netzdiagramm zeigen alle Fächer, wenn weniger als zwei ausgewählt sind.
- Beim **Netzdiagramm** blenden Knöpfe über dem Diagramm einzelne Prüfungen und den Durchschnitt ein oder aus.

### Kompensationen

Der aufklappbare Bereich **Kompensationen anzeigen** unter dem Diagramm prüft, ob ungenügende Fächer ausgeglichen werden können.

1. Wähle den **Durchschnitt**, dessen Fächer geprüft werden sollen, oder «Alle Fächer».
2. Klicke an, welche **Fächer** davon einbezogen werden.

Für jedes ungenügende Fach siehst du den Mangel (Zeugnisnote 3.5 hat 0.5 Punkte Mangel) und alle Fächer über 4 mit ihren Pluspunkten, auch ob ein Fach den Mangel allein kompensiert. Am Ende zeigt eine Gesamtaussage, ob die Pluspunkte für alle Mängel reichen.

> Die Gesamtaussage geht davon aus, dass mehrere Fächer gemeinsam kompensieren dürfen. Gelten andere Regeln, muss die Funktion `komp()` in `script.js` angepasst werden.

### Noten, Sperren und Note erfassen

In der Tabelle trägst du die Noten (1 bis 6) pro Prüfung ein. Eingaben werden auf **eine Nachkommastelle** gerundet.

- **Prüfungen**: Mit **−** und **+** stellst du 1 bis 10 Prüfungen ein.
- **Fächer**: Unter der Tabelle fügst du Fächer hinzu, das **✕** in der Zeile löscht ein Fach.
- **Prüfungsnamen**: Unter jeder eingetragenen Note steht der Name der Prüfung, sonst blass «Prüfung 1», «Prüfung 2» und so weiter. Beim Darüberfahren erscheint ein Stift (✎), mit dem du den Namen überschreibst. Leer lassen setzt den Standardnamen zurück.
- **Sperren (🔓/🔒)**: Gesperrt kannst du Noten nicht mehr direkt eintippen. Das Umbenennen der Prüfungen geht weiterhin.
- **+ Note erfassen**: Öffnet ein Fenster mit Fach, Prüfungsnummer und Name (Testthema). Du gibst entweder die Note direkt ein oder die Punktzahlen:

  ```
  Note = erreichte Punkte ÷ maximale Punkte × 5 + 1
  ```

- **Zurücksetzen**: Fragt nach, ob nur die Noten oder alles (auch Fächer und Durchschnitte) gelöscht werden soll.

### Selbstbewertung und Prognose

Ein System, das aus deinen bisherigen Prüfungen eine erwartete Note für die nächste berechnet.

**Ablauf mit «Prognose berechnen»**

1. Fach und Prüfung wählen.
2. Für jede **frühere Prüfung** ohne Selbstbewertung erscheint ein Block. Du trägst Prüfungstyp, Schwierigkeit (1 bis 5), investierte Stunden sowie erwartete und erhaltene Note nach. Steht die Note schon in der Tabelle, wird sie von dort übernommen.
3. Für die gewählte Prüfung gibst du Typ, geplante Lernzeit und erwartete Schwierigkeit an.
4. Beim Berechnen werden die nachgetragenen Selbstbewertungen gespeichert, und die erwartete Note erscheint, zusammen mit der **tiefsten und höchsten möglichen Note**.

Bei einer Prognose unter 4.0 erscheint eine rote Meldung, dass du dich besser vorbereiten musst, mit einer Schätzung der nötigen Lernzeit.

**Prüfungstypen**: Schreiben (entspricht Schriftlich), Reden, Hören, Lesen und Exam.net.

**Reihenfolge pro Fach**: Im Abschnitt «Prüfungstypen nach Schwierigkeit» steht oben die schwerste, unten die einfachste Prüfung. Du verschiebst die Typen per **Ziehen** oder über die **drei Punkte (⋮)**. Jedes Fach hat seine eigene Reihenfolge.

**Diagramm «Erwartete Noten»**: Es zeigt die bisherigen Noten als Linie und die Prognose als **Kerze**.

- Der dünne Strich reicht von der tiefsten bis zur höchsten möglichen Note.
- Der Körper reicht von der letzten Note bis zur erwarteten Note, der Querstrich markiert die erwartete Note.
- Grün bedeutet genügend, rot ungenügend.
- Mit den **Schaltern** pro Fach vergleichst du mehrere Fächer gleichzeitig.
- Darunter fasst eine Tabelle alle Fächer zusammen.

Alle gespeicherten Selbstbewertungen stehen in einem aufklappbaren Bereich und lassen sich dort löschen.

### Presets

Ein Preset enthält Fächer, Durchschnitte und die Anzahl Prüfungen, auf Wunsch auch die Noten. **Jedes Preset hat einen Namen.**

| Knopf                          | Funktion                                                                                                               |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
| **Aktuelles Preset speichern** | Fragt nach Name und ob die Noten mitgespeichert werden. Das Preset kommt in die Liste, auf Wunsch zusätzlich als Datei |
| **Datei laden**                | Lädt eine oder mehrere Preset-Dateien (`.json`) in die Liste                                                           |
| **Ordner wählen**              | Liest alle Preset-Dateien eines Ordners ein, danach wählst du aus der Liste                                            |
| **Laden**                      | Wendet ein Preset auf das aktive Semester an und ersetzt Fächer und Durchschnitte                                      |
| **Als Datei**                  | Speichert ein Preset aus der Liste als Datei                                                                           |
| **✕**                          | Entfernt ein Preset aus der Liste (die Datei bleibt erhalten)                                                          |

Preset-Dateien sind lesbares JSON mit dem Feld `"format": "notenrechner-preset"`. Andere Dateien werden beim Import übersprungen. Ansichten, Semester und Selbstbewertungen sind nicht Teil eines Presets.

---

## Berechnungen

Alle Werte werden im Browser berechnet.

**Durchschnitt eines Fachs**: Mittelwert der eingetragenen Noten, mit einer Nachkommastelle. Ab 4.0 grün, darunter rot.

**Zeugnisnote**: Der Durchschnitt, auf eine halbe Note gerundet (4.3 ergibt 4.5, 4.2 ergibt 4.0).

**Mangelpunkte eines Fachs** (Tabelle): `4 − Durchschnitt`, auf eine Nachkommastelle. Über 0 bedeutet Mangelpunkte (rot), sonst grün.

**Durchschnitt einer Kachel**: Mittelwert der Fachdurchschnitte der verknüpften Fächer. Fächer ohne Note zählen nicht mit.

**Mangelpunkte einer Kachel**: Summe von `4 − Zeugnisnote` über alle verknüpften Fächer mit einer Zeugnisnote unter 4.0.

**Prognose**: Die erwartete Note beginnt beim Durchschnitt des Fachs vor der gewählten Prüfung. Gibt es noch keine Note, nimmt die Seite den Durchschnitt der anderen Fächer. Dazu kommen vier Anpassungen:

| Anpassung     | Wirkung                                                                                                                                            |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Prüfungstyp   | Die Reihenfolge der Typen verschiebt die Note um bis zu ±0.3. Eigene Ergebnisse zu diesem Typ zählen mit der Zeit stärker                          |
| Lernzeit      | Mehr Stunden als üblich erhöhen die Note, höchstens um 1.0. Mit mindestens drei Selbstbewertungen wird der Zusammenhang aus deinen Daten geschätzt |
| Schwierigkeit | Jeder Punkt über deinem Durchschnitt senkt die Note um 0.25                                                                                        |
| Erwartung     | Schätzt du dich meist zu hoch oder zu tief ein, wird das zur Hälfte ausgeglichen                                                                   |

**Spannweite**: Sie wird grösser, wenn deine Noten im Fach stark schwanken, und kleiner, je mehr Selbstbewertungen vorliegen (mindestens ±0.3, höchstens ±1.5).

**Nötige Lernzeit**: Bei einer Prognose unter 4.0 rechnet die Seite mit mindestens 0.2 Notenpunkten pro zusätzlicher Stunde und empfiehlt höchstens 3 Stunden mehr als geplant.

**Programm-Schwierigkeit** (0 bis 100, in der Liste der Selbstbewertungen): zu 50 % deine eingeschätzte Schwierigkeit, zu 30 % wie viel schlechter die Note als erwartet war, zu 20 % die Lernzeit (10 Stunden zählen als Maximum).

> Die Prognose ist eine einfache, nachvollziehbare Schätzung und kein trainiertes Modell. Mit wenig Daten ist sie ungenau, das zeigt die Seite an.

---

## Datenspeicherung und Datenschutz

- Alles liegt im **`localStorage` des Browsers**: deine Semester mit Fächern, Noten und Einstellungen unter `noten_v2` und die Preset-Liste unter `noten_presets`.
- Es werden **keine Daten an einen Server gesendet.**
- Daten einer früheren Version (`noten_v1`) werden automatisch übernommen.
- Die Daten gelten pro Gerät und Browser. Beim Löschen der Browserdaten oder im privaten Modus gehen sie verloren. Sichere wichtige Einstellungen deshalb als Preset-Datei.

---

## Technische Details

- Reines **HTML, CSS und JavaScript**, ohne Build-Schritt und ohne Framework
- Diagramme mit **Chart.js 4.4.1** (von `cdnjs.cloudflare.com`) und eigenen Plugins für die Durchschnitte am Diagrammrand, die Prognose-Kerzen und die senkrechte Linie bei den horizontalen Balken
- Fächerfarben werden mit dem Goldenen Winkel erzeugt, damit sich keine Farbe wiederholt
- Farben als CSS-Variablen, mit eigenen Werten für den dunklen Modus (`prefers-color-scheme`)
- Die Reihenfolge der Prüfungstypen funktioniert per Ziehen mit Pointer-Events, also auch mit dem Finger
- Unterstützt aktuelle Versionen von Chrome, Firefox, Safari und Edge. Die Ordnerauswahl für Presets braucht einen Browser mit Unterstützung für `webkitdirectory`

---

## Veröffentlichen mit GitHub Pages

1. Alle drei Dateien (`index.html`, `style.css`, `script.js`) ins Repository legen.
2. Im Repository **Settings → Pages** öffnen.
3. Bei **Source** den Branch (zum Beispiel `main`) und den Ordner `/ (root)` wählen und speichern.
4. Die Seite ist danach unter `https://<dein-benutzername>.github.io/<dein-repository>/` erreichbar.

---

## Lizenz

Noch keine Lizenz festgelegt. Füge eine `LICENSE`-Datei hinzu (zum Beispiel MIT), wenn andere das Projekt verwenden dürfen.
