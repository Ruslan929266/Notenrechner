# 📊 Notenrechner

Ein Notenrechner als **einzelne HTML-Datei**. Du trägst deine Prüfungsnoten pro Fach ein und siehst sofort Durchschnitte, Zeugnisnoten, Mangelpunkte und den Notenverlauf in einem Diagramm. Es braucht keine Installation, keinen Server und kein Konto.

Fächer, Durchschnitte (Gruppen von Fächern) und die Anzahl Prüfungen legst du selbst fest. Deine Einstellungen kannst du als **Presets** in Dateien speichern und später wieder laden.

---

## Inhaltsverzeichnis

- [Funktionen](#funktionen)
- [Schnellstart](#schnellstart)
- [Bedienung](#bedienung)
- [Berechnungen](#berechnungen)
- [Kompensationen](#kompensationen)
- [Presets](#presets)
- [Datenspeicherung und Datenschutz](#datenspeicherung-und-datenschutz)
- [Technische Details](#technische-details)
- [Veröffentlichen mit GitHub Pages](#veröffentlichen-mit-github-pages)
- [Lizenz](#lizenz)

---

## Funktionen

- **Freie Fächer**: Fächer hinzufügen und löschen, jedes Fach hat eine eigene Farbe, die nur einmal vorkommt
- **Freie Durchschnitte**: beliebig viele Durchschnitte anlegen, umbenennen, mit Fächern verknüpfen und löschen
- **Anzahl Prüfungen einstellbar** (1 bis 10)
- **Liniendiagramm** des Notenverlaufs mit gestrichelter roter Linie bei 4.0
- **Zeugnisnote** (auf halbe Noten gerundet) und **Mangelpunkte** pro Fach, farbig markiert
- **Kompensationen**: Prüfung, ob ungenügende Fächer durch andere Fächer ausgeglichen werden können
- **Presets**: Einstellungen als Datei speichern, laden und aus einem ganzen Ordner auswählen
- **Automatisches Speichern** im Browser
- **Heller und dunkler Modus**, passend zur Systemeinstellung
- Geeignet für **Computer und Smartphone**

---

## Schnellstart

1. Die Datei `notenrechner.html` herunterladen oder das Repository klonen:
   ```bash
   git clone https://github.com/<dein-benutzername>/<dein-repository>.git
   ```
2. `notenrechner.html` im Browser öffnen.
3. Noten eintragen.

> Für das Diagramm wird [Chart.js](https://www.chartjs.org/) von cdnjs geladen. Beim ersten Öffnen ist deshalb eine Internetverbindung nötig.

---

## Bedienung

### Durchschnitte

Oben stehen die Durchschnitte als Kacheln. Jede Kachel zeigt den Namen, den Durchschnitt und die Mangelpunkte.

| Aktion | So geht es |
|---|---|
| Hinzufügen | Auf **+ Durchschnitt hinzufügen** klicken. Im Fenster Namen eingeben und die passenden Fächer ankreuzen |
| Bearbeiten | Auf die **drei Punkte (⋮)** in der Kachel klicken. Dort lassen sich Name und verknüpfte Fächer ändern |
| Löschen | Auf das **✕** in der Kachel klicken und zur Bestätigung ein zweites Mal klicken |

### Diagramm

Über dem Diagramm stehen Auswahlknöpfe für die Durchschnitte und für jedes einzelne Fach.

- **Ein Fach anklicken** zeigt die einzelnen Noten dieses Fachs, also den Verlauf über alle Prüfungen.
- **Mehrere Fächer vergleichen**: Aktiviere diese Option, dann kannst du mehrere Fächer gleichzeitig anklicken. Das Diagramm zeigt jedes Fach mit seiner Farbe und zusätzlich die gestrichelte **Gesamtbewertung** über alle gewählten Fächer.
- **Einen Durchschnitt anklicken** wählt alle zugehörigen Fächer aus.
- Neben dem Diagramm steht der Durchschnitt jedes Fachs, fett und auf der Höhe der letzten Note.
- Prüfungen ohne Note werden nicht angezeigt.

### Noten und Prüfungen

In der Tabelle trägst du die Noten (1 bis 6) pro Prüfung ein. Eingaben werden auf **eine Nachkommastelle** gerundet. Mit **−** und **+** bei «Prüfungen» änderst du die Anzahl der Prüfungen. Unter der Tabelle fügst du neue Fächer hinzu, das **✕** in der Zeile löscht ein Fach.

### Zurücksetzen

Der Knopf **Zurücksetzen** fragt nach, was gelöscht werden soll:

- **Nur Noten löschen**: Fächer und Durchschnitte bleiben
- **Alles löschen**: auch Fächer und Durchschnitte werden entfernt

---

## Berechnungen

Alle Werte werden im Browser berechnet.

**Durchschnitt eines Fachs**: Mittelwert aller eingetragenen Noten, mit einer Nachkommastelle. Ab 4.0 grün, darunter rot.

**Zeugnisnote**: der Durchschnitt, auf eine halbe Note gerundet (4.3 ergibt 4.5, 4.2 ergibt 4.0).

**Mangelpunkte eines Fachs**: `4 − Durchschnitt` (auf eine Nachkommastelle). Ein Wert über 0 bedeutet Mangelpunkte und ist rot, sonst grün.

**Durchschnitt einer Kachel**: Mittelwert der Fachdurchschnitte der verknüpften Fächer. Fächer ohne Note zählen nicht mit.

**Mangelpunkte einer Kachel**: Summe von `4 − Zeugnisnote` über alle verknüpften Fächer, deren Zeugnisnote unter 4.0 liegt. Gibt es keine ungenügenden Fächer, ist der Wert 0.0 und grün.

---

## Kompensationen

Unter dem Diagramm gibt es den aufklappbaren Bereich **Kompensationen anzeigen**.

1. Wähle den **Durchschnitt**, dessen Fächer geprüft werden sollen, oder «Alle Fächer».
2. Wähle durch Anklicken, welche **Fächer** davon in die Prüfung einbezogen werden.

Für jedes ungenügende Fach zeigt die Seite den Mangel (Zeugnisnote 3.5 hat 0.5 Punkte Mangel) und alle Fächer über 4 mit ihren Pluspunkten (Zeugnisnote 4.5 hat +0.5). Es steht dabei, ob ein Fach den Mangel allein kompensiert. Am Ende zeigt eine Gesamtaussage, ob die Pluspunkte aller geprüften Fächer für alle Mängel reichen.

> Die Gesamtaussage geht davon aus, dass mehrere Fächer gemeinsam kompensieren dürfen. Gelten andere Regeln, muss die Funktion `komp()` angepasst werden.

---

## Presets

Ein Preset enthält Fächer, Durchschnitte und die Anzahl Prüfungen, auf Wunsch auch die Noten. **Jedes Preset hat einen Namen.** Im Bereich **Presets** unten auf der Seite gibt es:

| Knopf | Funktion |
|---|---|
| **Aktuelles Preset speichern** | Fragt nach einem Namen und ob die Noten mitgespeichert werden. Das Preset kommt in die Liste und kann zusätzlich als Datei gespeichert werden |
| **Datei laden** | Lädt eine oder mehrere Preset-Dateien (`.json`) in die Liste |
| **Ordner wählen** | Liest alle Preset-Dateien eines ganzen Ordners ein, danach wählst du aus der Liste |
| **Laden** (in der Liste) | Wendet ein Preset an und ersetzt dabei Fächer und Durchschnitte |
| **Als Datei** (in der Liste) | Speichert ein Preset aus der Liste als Datei |
| **✕** (in der Liste) | Entfernt ein Preset aus der Liste (die Datei bleibt erhalten) |

Preset-Dateien sind lesbares JSON mit dem Feld `"format": "notenrechner-preset"`. Dateien ohne dieses Feld werden beim Import übersprungen.

---

## Datenspeicherung und Datenschutz

- Noten, Fächer, Durchschnitte und die Preset-Liste liegen im **`localStorage` des Browsers**.
- Es werden **keine Daten an einen Server gesendet.**
- Die Daten gelten pro Gerät und Browser. Beim Löschen der Browserdaten gehen sie verloren. Sichere wichtige Einstellungen deshalb als Preset-Datei.

---

## Technische Details

- Reines HTML, CSS und JavaScript in einer Datei, ohne Build-Schritt
- Diagramm mit Chart.js 4.4.1 (von `cdnjs.cloudflare.com`) und einem eigenen Plugin für die Durchschnitte neben dem Diagramm
- Fächerfarben werden mit dem Goldenen Winkel erzeugt, damit sich keine Farbe wiederholt
- Farben als CSS-Variablen, mit eigenen Werten für den dunklen Modus
- Unterstützt aktuelle Versionen von Chrome, Firefox, Safari und Edge. Die Ordnerauswahl für Presets braucht einen Browser mit Unterstützung für `webkitdirectory`

---

## Veröffentlichen mit GitHub Pages

1. `notenrechner.html` in `index.html` umbenennen.
2. Im Repository **Settings → Pages** öffnen.
3. Bei **Source** den Branch (zum Beispiel `main`) und den Ordner `/ (root)` wählen und speichern.
4. Die Seite ist danach unter `https://<dein-benutzername>.github.io/<dein-repository>/` erreichbar.

---

## Lizenz

Noch keine Lizenz festgelegt. Füge eine `LICENSE`-Datei hinzu (zum Beispiel MIT), wenn andere das Projekt verwenden dürfen.