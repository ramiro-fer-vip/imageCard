# ImageCard

> **Sprachen:** [English](README.en-US.md) · [Español](README.md) · [Français](README.fr-FR.md) · **Deutsch** · [Italiano](README.it-IT.md)

![ImageCard](images/ImageCard.jpg)

KPI-Karte für Power BI mit Measure, positionierbarem Bild, Einzahl/Mehrzahl-
Beschriftung, regelbasierten bedingten Farben und deterministischer regionaler
Zahlenformatierung.

- **Sprachen des Formatierungsbereichs:** English (en-US), Español (es-ES),
  Français (fr-FR), Deutsch (de-DE), Italiano (it-IT).
- **Aktualisierungshinweis:** Power BI cached das importierte Visual. Um eine neue
  Version zu testen, entfernen Sie das Visual aus dem Bericht und importieren Sie
  das frische `.pbiviz`.

## Funktionen der Steuerung
- **Measure:** ein einzelnes Feld in der Measure-Rolle; erkennt automatisch Zahl,
  Text oder Datum und respektiert das Modellformat.
- **Data labels (Wert):** Schriftart (Größe, Schnitt, Familie), Anzeigeeinheiten
  (Auto, None, Thousands, Millions, Billions, Trillions, Percentage, Currency),
  Dezimalstellen, Dezimal- und Tausendertrennzeichen, Währungssymbol, Textumbruch,
  Ausrichtung (links/mitte/rechts) und Farbe.
- **Datums:** Datumsformat mit oder ohne Uhrzeit (Include time), Power-BI-Wert oder
  eigene sprachunabhängige Darstellung; konfigurierbare Zeitzone.
- **Labels:** Singular- und Plural-Texte mit den Schaltern Show label und Show
  plural; Position (Default, Up, Top, Bottom), Abstand, Schriftart, Ausrichtung,
  Textumbruch und Farbe.
- **Image:** Schalter Show image; Position Left, Right, Top oder Bottom (bei
  Top/Bottom ist das Bild horizontal zentriert); Breite, Polsterung pro Seite
  (top, right, bottom, left) und Deckkraft; Color key schneidet eine Farbe aus
  dem Bild heraus und färbt es mit der Ersetzungsfarbe (oder der Bildfarbe der
  aktiven KPI-Regel); Ersetzen per Klick im Entwurfsmodus, bleibt beim Speichern
  der PBIX erhalten.
- **KPI Color:** Standard-Hintergrundfarbe plus 5 Bereichsregeln (Min/Max mit
  Operator Include/Exclude max), die Hintergrund, Bild, Wert und Beschriftung
  unabhängig einfärben; eine Regel wird allein durch den Bereich aktiviert, auch
  wenn die Hintergrundfarbe leer ist.
- **Card:** Hintergrund, Rahmen (Farbe und Breite), Außen-/Innenradius und
  Polsterung.
- **Tooltip:** Schalter zum Anzeigen der Farb-Measure; Tooltip-Zahlen verwenden
  das Modellformat.
- **Datenrollen:** Measure (1 Feld), Color measure (1 Feld) und Tooltips (bis zu
  10 Felder).

---

## Änderungsprotokoll

### 1.0.0.70 (aktuell)
- KPI-Regelfarben in einer einzigen **KPI Color**-Karte zusammengefasst:
  Jede Regelgruppe enthält nun Background color, Image color, Value color
  und Label color (ersetzt die getrennten KPI Color - BG / Labels /
  Image-Karten). Berichte, die mit den alten Karten gespeichert wurden,
  behalten ihre Farben (geketteter Lese-Fallback).
- Regeln werden allein durch den Bereich aktiviert: Value, Label und Image
  können ohne Hintergrundfarbe gesetzt werden (leerer Hintergrund fällt auf
  die Standard-Hintergrundfarbe zurück).
- „Image replacement color" in jeder Regel in „Image color" umbenannt.
- Bildposition wiederhergestellt: Die Steuerung wendet jetzt die richtige
  CSS-Klasse an (ohne Beachtung der Groß-/Kleinschreibung) und entfernt
  veraltete Klassen bei jedem Rendering. Top zentriert das Bild horizontal
  über dem Text; Bottom platziert es unter dem Text.

### 1.0.0.69
- Korrektur des Bildflackerns: Das `<img>`-Element und seine Quelle werden
  zwischengespeichert und zwischen den Renderings wiederverwendet;
  KPI-Farbänderungen verarbeiten das Bild ohne Flackern neu (Original-URL
  und Ersetzungsfarbe werden getrennt nachverfolgt).
- Korrekturen der Textanpassung (fehlende Klammer, undefinierte
  scope-Variable) in der responsiven Verkleinerungsschleife.

### 1.0.0.46 – 1.0.0.68
- Datumsformatierung automatisch aus der Measure-Rolle erkannt: nur Datum
  oder Datum und Uhrzeit über **Include time**, **Power BI value** und
  **Time Zone**; Modellformat wird respektiert, manuelle formatunabhängige
  Darstellung.
- **Wrap text**-Schalter und Ausrichtungs-Auswahllisten (Links/Mitte/Rechts)
  für Wert und Beschriftung.
- **Show Label**- und **Show Plural**-Schalter (standardmäßig aktiviert).
- **Image padding** pro Seite (oben/rechts/unten/links, Standard 4).
- Sichere Dropdown-Unterklasse verhindert leere Einträge aus unbekannten
  gespeicherten Werten.
- Tooltip-Zahlen mit dem Modellformat formatiert (`valueFormatter`).
- Bildpersistenz per Klick-zum-Ersetzen (nur im Entwurfsmodus).

### 1.0.0.45
- Ohne Tooltip-Inhalt (keine Tooltips-Felder, keine sichtbare Farbkennzahl)
  erscheint keine QuickInfo beim Darüberfahren.

### 1.0.0.44
- QuickInfos im Modellformat (`valueFormatter` pro Spalte + Berichtskultur);
  die Hauptkennzahl erscheint nicht mehr.
- `powerbi-visuals-utils-formattingutils` auf ^6.1.2 fixiert (7.0.0 bricht
  `pbiviz package`: ESM-Locale-Datei scheitert am `localizationLoader`).

### 1.0.0.43
- Hauptschalter Show image (erster in Image, standardmäßig ein): Aus blendet
  das Bild aus, einfache Karte.

### 1.0.0.42
- Einzelne Kennzahl mit Ersetzen (`conditions` max:1) und rollenbasiertes Lesen
  (behebt Farbkennzahl-Verwechslung).
- Mehrfache Tooltips-Rolle (bis 10) + Tooltip-Karte mit Schalter Show color
  measure; Hover-QuickInfos.

### 1.0.0.41
- `powerbi-visuals-utils-formattingmodel` 6.0.4 → ^7.1.0, keine Codeänderungen;
  d3-Reste aus `node_modules` entfernt.

### 1.0.0.40
- Neues Steuerelement **Card border width** (Karte „Card“, unter Card border,
  Bereich 0–20, Standard **1**): Der Rahmen wird nur bei gewählter Farbe und Breite > 0 gezeichnet.

### 1.0.0.39
- **Display Units** erhält **Percentage** (×100 + `%`, ohne K/M-Skalierung) und
  **Currency** (behält Skalierung, stellt das Symbol voran).
- Neues Feld **Currency symbol** (Text, Standard `$`), das **nur erscheint**,
  wenn Currency gewählt ist, ohne dauerhafte redundante Zeilen.

### 1.0.0.38
- Äußerer und innerer Eckenradius standardmäßig **10**.
- Der Außenrahmen (`Card border`, 2 px) ist nun standardmäßig abgerundet.
- Hinweis: Der äußerste eckige graue Rahmen wird von Power BI gezeichnet (nativer
  Hintergrund); kein benutzerdefiniertes Visual kann ihn abrunden. Für die
  abgerundete Optik deaktivieren Sie den nativen Hintergrund und verwenden Sie
  **Card background** + **Card border**.

### 1.0.0.37
- Neues Steuerelement **Image padding** (Karte „Bild“, Standard 4, Bereich 0–50):
  Bild links/rechts → 4 horizontal und 2 vertikal;
  Bild oben/unten → 4 vertikal und 2 horizontal.

### 1.0.0.36
- Neue Karte **Card** (Außenrahmen + Innenkörper):
  **Card background**, **Card border** (2 px), **Outer border radius**,
  **Inner border radius**, **Padding** (Standard 2 auf allen Seiten).
- Der KPI-Hintergrund malt nun den Innenkörper (mit eigenem Radius).
- Die automatische Text-/Bildanpassung misst den Innenkörper.

### 1.0.0.35
- **Decimal separator** erhält die Option **Default**: verwendet die Trennzeichen
  der Berichtssprache (`host.locale`) — es-ES/de-DE/it-IT → `1.234.567,89`,
  en-US → `1,234,567.89`, fr-FR → `1 234 567,89` — mit Rückfall auf englischen
  Stil, wenn die Laufzeit keine Locale-Daten hat.

### 1.0.0.34
- KPI-Regeln mit Standard-Maxima 0,2 / 0,4 / 0,6 / 0,8 / 1,0
  (Regel-1-Minimum bleibt 0; Verkettung unverändert).

### 1.0.0.33
- Die Karte **General** entfällt: Alles zur numerischen Wertanzeige liegt nun in
  **Data labels** (wie bei nativen Steuerelementen). Das interne Objekt heißt
  weiterhin `general`, damit gespeicherte Einstellungen nicht verloren gehen;
  nur sichtbare Texte ändern sich.
- Neuer Schalter **Thousands separator** (standardmäßig ein) in Data labels.
- Übersetzungsaudit: `Card_DataLabels` und lokalisierte Regelpräfixe
  (Règle/Regel/Regola), verwaiste Schlüssel entfernt, DE `Tausender`.
- Die Zahlenformatierung ist deterministisch und browsersprachenunabhängig.

### 1.0.0.32
- KPI aufgeteilt in 3 zusammengesetzte Karten mit einklappbaren Gruppen pro Regel:
  **KPI Color - BG** (Bereiche + Hintergrund, gleiches `kpiBackground`-Objekt, keine Migration),
  **KPI Color - Labels** (neues `kpiLabelColors`-Objekt: Label + Value pro Regel),
  **KPI Color - Image** (neues `kpiImageColors`-Objekt).
- Verkettete Lesereihenfolge (neues Objekt → geerbtes `kpiBackground` → Modell → Original):
  bereits konfigurierte Farben bleiben erhalten.

### 1.0.0.31
- Die Zeile **Image** ist im Bereich ausgeblendet (`visible: false`): Das
  Bereichssteuerelement kann über eine Texteigenschaft keine Dateibytes liefern
  (es zeigte `[object Object]`). Der Upload erfolgt ausschließlich per Klick auf
  Bild/Platzhalter im Bearbeitungsmodus.

### 1.0.0.30
- Der Bereich zeigt den echten Dateinamen statt `"imagen_subida"`.
- Dateinamen ohne URL werden für das Rendern verworfen (Platzhalter im Entwurf,
  nichts in der Ansicht).

### 1.0.0.29
- Klickbarer **Platzhalter** (Inline-SVG), wenn im Entwurfsmodus kein Bild vorhanden ist.
- Nur ladbare URLs werden gerendert (`data:`/`https:`/`blob:`); `error`-Rückfall
  (Platzhalter im Entwurf, ausgeblendet in der Ansicht): nie wieder defektes Symbol mit Text.
- Klick-zum-Ersetzen **nur im Entwurfsmodus** (`ViewMode.View` deaktiviert es):
  Benutzer ändern das Bild in veröffentlichten Dashboards nicht.

### 1.0.0.28
- Bildeigenschaft als **Text** (`{"text": true}`) + Unterklasse `CustomImageUpload`,
  die Zeichenkette oder Objekt akzeptiert: Diese Form überlebt das PBIX-Speichern
  (an einem Referenzprojekt verifiziert; `{"image": true}`-Objekte gehen beim
  Speichern verloren: in der Sitzung vorhanden, in `Report/Layout` fehlend).
- **Klick-zum-Ersetzen**: versteckte Dateiauswahl → `FileReader.readAsDataURL` →
  `persistProperties` mit der `data:`-Zeichenkette.
- Toleranter Leser (Objekt/JSON/SVG/Base64/URL) + `blob:`- → `data:`-Normalisierung.
- Lokalisierte „Klicken zum Ersetzen“-QuickInfo.

### 1.0.0.27
- `blob:`- → `data:`-Normalisierung mit Rückschreiben via `persistProperties`
  (eine Konvertierung pro URL, keine Schleifen).
- Sitzungszwischenspeicher für Updates ohne `metadata.objects`.

### 1.0.0.26
- 15 KPI-Override-Schalter entfernt: Leere Farbe = Original behalten.
- Slices nach Gruppen neu geordnet (Bereiche+Hintergrund, dann Bezeichnung/Wert, dann Bild).

### 1.0.0.25
- KPI-Farben pro Regel für Ersatzbild, numerischen Wert und Bezeichnung.

### 1.0.0.24
- Das Modellbild wird nur bei leerem Wert wiederhergestellt (zerstört nie den
  persistierten Wert).

### 1.0.0.23
- Einzelnes Steuerelement **Decimal separator** (Punkt/Komma, wechselt Tausender
  automatisch) mit deterministischer manueller Formatierung; ersetzt den alten Schalter.

### 1.0.0.22
- Visual-Symbol im Kartenstil (Ziffern + blaues Quadrat).

### 1.0.0.21
- Zahlenformatierung mit `host.locale` (Berichtstrennzeichen, nicht Browser).

### 1.0.0.20
- Responsives Layout: automatische Textverkleinerung und proportional begrenztes Bild.
- Tausendertrennzeichen-Schalter (später in 1.0.0.23 ersetzt).

### 1.0.0.19
- Stellt das Bild aus `dataView.metadata.objects` wieder her (der
  Formatierungsdienst füllt `ImageUpload` nicht).
- Bildbreite Standard 60, Dezimalstellen Standard 0, neues Symbol.

### 1.0.0.18
- Korrekturen: Schutz bei leerer Kennzahl, Bereinigung bei leeren Daten,
  Dropdown-`displayName`, asynchrone Bild-Wettlaufsituation, Dezimalstellen bei
  Ganzzahlen, hexadezimales `NaN`, `package.json`-Bereinigung (ungenutztes `d3` entfernt).
- Vollständige ES/EN/FR/DE/IT-Lokalisierung (`stringResources`, `displayNameKey`,
  `pbiviz.json` mit 5 Locales).

## Unterstützter Bildablauf (Zusammenfassung)
1. Im Bearbeitungsmodus auf Bild oder Platzhalter klicken, um die Dateiauswahl zu öffnen.
2. Die Datei wird als `data:`-URL gelesen und als **Text** via `persistProperties`
   persistiert (überlebt PBIX-Speichern/erneutes Öffnen).
3. Mit `check-pbix-image.ps1` prüfen, dass das Layout das `image`-Objekt mit
   `data:`-Schema enthält.
