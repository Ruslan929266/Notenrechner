# 📊 Notenrechner

Ein einfacher Notenrechner als **einzelne HTML-Datei**. Man trägt seine Prüfungsnoten pro Fach ein und sieht sofort Durchschnitte, Zeugnisnoten, Mangelpunkte und den Notenverlauf in einem Diagramm. Es braucht keine Installation, keinen Server und kein Konto.

---

## Inhaltsverzeichnis

- [Funktionen](#funktionen)
- [Schnellstart](#schnellstart)
- [Bedienung](#bedienung)
- [Berechnungen](#berechnungen)
- [Kompensationen](#kompensationen)
- [Fächer und Gruppen anpassen](#fächer-und-gruppen-anpassen)
- [Datenspeicherung und Datenschutz](#datenspeicherung-und-datenschutz)
- [Technische Details](#technische-details)
- [Projektstruktur](#projektstruktur)
- [Veröffentlichen mit GitHub Pages](#veröffentlichen-mit-github-pages)
- [Lizenz](#lizenz)

---

## Funktionen

- **Noteneingabe** für bis zu 4 Prüfungen pro Fach, mit einer Nachkommastelle
- **Liniendiagramm** über Prüfung 1 bis Prüfung 4, mit
  - einzelnen Fächern oder mehreren Fächern gleichzeitig,
  - Schnellauswahl für **Alle**, **FMZ** und **BBZW**,
  - einer gestrichelten roten Linie bei **4.0** (Grenze zwischen genügend und ungenügend),
  - den Durchschnitten jedes Fachs, fett und in der Höhe der letzten Note direkt neben dem Diagramm
- **Prüfungen ohne Note** werden nicht angezeigt
- **Durchschnitt pro Fach**, grün (genügend) oder rot (ungenügend)
- **Zeugnisnote**, auf halbe Noten gerundet und farbig markiert
- **Mangelpunkte** pro Fach und als Total für die FMZ-Fächer, rot bei Mangelpunkten, sonst grün
- **Kennzahlen oben**: Durchschnitt FMZ, Durchschnitt BBZW, Durchschnitt aller Fächer, Total Mangelpunkte
- **Kompensationen**: Ein aufklappbarer Bereich zeigt, ob ungenügende FMZ-Fächer durch andere Fächer ausgeglichen werden können
- **Automatisches Speichern** im Browser
- **Heller und dunkler Modus**, passend zur Systemeinstellung
- Geeignet für **Desktop und Smartphone**

---

## Schnellstart

1. Datei `notenrechner.html` herunterladen oder das Repository klonen:
   ```bash
   git clone https://github.com/<dein-benutzername>/<dein-repository>.git
   cd <dein-repository>
   ```
2. `notenrechner.html` mit einem Doppelklick im Browser öffnen.
3. Noten eintragen. Fertig.

> **Hinweis:** Für das Diagramm wird [Chart.js](https://www.chartjs.org/) von cdnjs geladen. Beim ersten Öffnen ist deshalb eine Internetverbindung nötig.

---

## Bedienung

### Diagramm

Über dem Diagramm stehen Auswahlknöpfe:

| Knopf | Wirkung |
|---|---|
| **Alle** | Zeigt alle Fächer, ein zweiter Klick blendet alle aus |
| **FMZ** | Zeigt nur die FMZ-Fächer |
| **BBZW** | Zeigt nur die BBZW-Fächer |
| **Einzelnes Fach** | Fach ein- oder ausblenden, beliebig kombinierbar |

- Ist **ein einzelnes Fach** gewählt, ist die Linie grün und in der Legende als «Gesamtbewertung» beschriftet.
- Sind **mehrere Fächer** gewählt, hat jedes Fach eine eigene Farbe und neben dem Diagramm steht das Fachkürzel vor dem Durchschnitt.
- Der Satz «Aktueller Durchschnitt» zeigt den Durchschnitt des gewählten Fachs, bei mehreren Fächern den Durchschnitt über diese Fächer.
- Die **rote gestrichelte Linie bei 4.0** zeigt auf einen Blick, ob eine Note genügend oder ungenügend ist.

### Tabelle

Pro Fach gibt es vier Felder für **Prüfung 1 bis 4**. Das Diagramm, die Durchschnitte und alle Kennzahlen aktualisieren sich sofort bei jeder Eingabe.

- Erlaubt sind Noten von 1 bis 6.
- Eingaben werden auf **eine Nachkommastelle** gerundet (4.39 wird zu 4.4).
- Ein leeres Feld bedeutet, dass die Prüfung noch nicht geschrieben wurde.

Mit **Zurücksetzen** unter der Tabelle stellst du die Startwerte wieder her.

---

## Berechnungen

Alle Werte werden direkt im Browser berechnet.

### Durchschnitt

Mittelwert aller eingetragenen Noten eines Fachs, mit einer Nachkommastelle angezeigt. Ab **4.0** ist er grün, darunter rot.

### Zeugnisnote

Der Durchschnitt wird auf eine **halbe Note** gerundet:

| Durchschnitt | Zeugnisnote |
|---|---|
| 4.2 | 4.0 |
| 4.3 | 4.5 |
| 4.7 | 4.5 |
| 4.8 | 5.0 |

### Mangelpunkte pro Fach

```
Mangelpunkte = 4 − Durchschnitt   (auf eine Nachkommastelle gerundet)
```

Ein positiver Wert (Durchschnitt unter 4) bedeutet Mangelpunkte und wird **rot** angezeigt. Ein Wert von 0 oder weniger wird **grün** angezeigt. Beispiel: Durchschnitt 3.2 ergibt 0.8 Mangelpunkte.

### Total Mangelpunkte

Das Total gilt nur für die **FMZ-Fächer**. Es zählt nur, wer eine **ungenügende Zeugnisnote** (unter 4.0) hat:

```
Total = Summe über alle FMZ-Fächer mit Zeugnisnote < 4 von (4 − Zeugnisnote)
```

Beispiel: Zeugnisnote 3.5 ergibt 0.5 Mangelpunkte. Gibt es keine ungenügenden FMZ-Fächer, ist das Total 0.0 und grün.

> Das Total ist bewusst nicht die Summe der Spalte «Mangelpunkte» in der Tabelle. Die Tabelle rechnet mit dem gerundeten Durchschnitt, das Total mit der Zeugnisnote.

### Durchschnitt FMZ, BBZW und alle Fächer

Mittelwert der **Fachdurchschnitte** der jeweiligen Gruppe. Fächer ohne Note zählen nicht mit.

---

## Kompensationen

Unter dem Diagramm gibt es den Bereich **«Kompensationen anzeigen»**. Er betrifft nur die **FMZ-Fächer** und rechnet mit den Zeugnisnoten.

Für jedes ungenügende FMZ-Fach steht dort:

- die Zeugnisnote und der **Mangel** in Punkten (Zeugnisnote 3.5 hat 0.5 Punkte Mangel),
- alle FMZ-Fächer mit einer Note über 4 mit ihren **Pluspunkten** (zum Beispiel GP 4.5 hat +0.5),
- ob ein Fach den Mangel **allein kompensiert** (Pluspunkte ≥ Mangel) oder dafür nicht reicht.

Am Ende steht eine Gesamtaussage: Mangel total gegenüber Pluspunkten total, also ob sich alle Mängel zusammen ausgleichen lassen.

> Die Gesamtaussage geht davon aus, dass mehrere Fächer gemeinsam kompensieren dürfen. Gelten an deiner Schule andere Regeln, muss die Funktion `komp()` angepasst werden.

---

## Fächer und Gruppen anpassen

Alle Einstellungen stehen am Anfang des Skripts in `notenrechner.html`:

```js
const FMZ  = ["DE","EN","FR","FRW","GP","MA","WR"];
const BBZW = ["IPT-1","M117","M122","M162","M319"];
const INIT = { DE:[3.9,4.7], EN:[5.1], /* ... */ SP:[4], U187:[], WR:[5] };
```

| Konstante | Bedeutung |
|---|---|
| `FMZ` | Fächer der Gruppe FMZ (Kennzahlen, Total Mangelpunkte, Kompensationen) |
| `BBZW` | Fächer der Gruppe BBZW |
| `INIT` | Alle Fächer mit den Startnoten (leere Liste = noch keine Note) |

Fächer, die in `INIT` stehen, aber in keiner Gruppe (hier **SP** und **U187**), erscheinen in Tabelle und Diagramm und zählen beim Durchschnitt aller Fächer mit, gehören aber nicht zu FMZ oder BBZW.

Nach Änderungen an den Fächern kann es nötig sein, den gespeicherten Stand zu löschen (Zurücksetzen-Knopf oder Browserdaten der Seite löschen).

---

## Datenspeicherung und Datenschutz

- Die Noten werden im **`localStorage` des Browsers** unter dem Schlüssel `noten_v1` gespeichert.
- Es werden **keine Daten an einen Server gesendet**. Alles bleibt auf deinem Gerät.
- Die Daten gelten pro Gerät und Browser. Ein anderer Browser oder ein anderes Gerät startet wieder mit den Startwerten.
- Löschst du die Browserdaten oder nutzt den privaten Modus, gehen die Eingaben verloren.

---

## Technische Details

- Reines **HTML, CSS und JavaScript** in einer Datei, ohne Build-Schritt
- Diagramm mit **Chart.js 4.4.1** (UMD-Build, geladen von `cdnjs.cloudflare.com`)
- Eigenes Chart.js-Plugin (`endLabels`), das die Durchschnitte neben dem Diagramm zeichnet und sich überlappende Beschriftungen auseinanderschiebt
- Farben als **CSS-Variablen**, mit eigenen Werten für den dunklen Modus (`prefers-color-scheme`)
- Responsive Layout, die Tabelle scrollt auf schmalen Bildschirmen seitlich
- Unterstützt aktuelle Versionen von Chrome, Firefox, Safari und Edge

---

## Projektstruktur

```
.
├── notenrechner.html   # die komplette Anwendung
├── Noten.xlsx          # optional: Excel-Vorlage mit den ursprünglichen Daten
└── README.md
```

---

## Veröffentlichen mit GitHub Pages

1. Datei `notenrechner.html` in `index.html` umbenennen (oder im Repository so ablegen).
2. Im Repository auf **Settings → Pages** gehen.
3. Bei **Source** den Branch (zum Beispiel `main`) und den Ordner `/ (root)` auswählen und speichern.
4. Nach kurzer Zeit ist die Seite unter `https://<dein-benutzername>.github.io/<dein-repository>/` erreichbar.

---

## Lizenz

Noch keine Lizenz festgelegt. Füge eine `LICENSE`-Datei hinzu (zum Beispiel MIT), wenn andere das Projekt verwenden oder weiterentwickeln dürfen.
