# ImageCard — Registro delle modifiche

![Tarjeta con gráfico y texto](images/ImageCard.jpg)

Scheda KPI per Power BI con misura, immagine posizionabile, etichetta
singolare/plurale, sfondo condizionale basato su regole e formattazione numerica
regionale deterministica.

- **Lingue del riquadro di formattazione:** English (en-US), Español (es-ES),
  Français (fr-FR), Deutsch (de-DE), Italiano (it-IT).
- **Nota di aggiornamento:** Power BI memorizza nella cache l'oggetto visivo
  importato. Per testare una nuova versione, rimuovilo dal report e importa
  il `.pbiviz` aggiornato.

---

## 1.0.0.45 (corrente)
- Senza contenuto tooltip (nessun campo Tooltips né Color measure visibile),
  nessun tooltip al passaggio.

## 1.0.0.44
- Tooltip nel formato del modello (`valueFormatter` per colonna + cultura del
  report); la misura principale non appare più.
- `powerbi-visuals-utils-formattingutils` fissato a ^6.1.2 (la 7.0.0 rompe
  `pbiviz package`: il file locales ESM fallisce il `localizationLoader`).

## 1.0.0.43
- Interruttore principale Show image (primo in Image, attivo per impostazione):
  disattivo, scheda semplice senza immagine.

## 1.0.0.42
- Misura singola con sostituzione (`conditions` max:1) e letture per ruolo
  (corregge confusione Color measure).
- Ruolo Tooltips multiplo (fino a 10) + scheda Tooltip con interruttore
  Show color measure; tooltip al passaggio.

## 1.0.0.41
- `powerbi-visuals-utils-formattingmodel` 6.0.4 → ^7.1.0, nessuna modifica
  al codice; resti d3 rimossi da `node_modules`.

## 1.0.0.40
- Nuovo controllo **Card border width** (scheda Card, sotto Card border, intervallo 0–20,
  predefinito **1**): il bordo si disegna solo con colore scelto e larghezza > 0.

## 1.0.0.39
- **Display Units** aggiunge **Percentage** (×100 + `%`, senza scala K/M) e
  **Currency** (conserva la scala, antepone il simbolo).
- Nuovo campo **Currency symbol** (testo, predefinito `$`) che **appare solo**
  quando si sceglie Currency, senza righe ridondanti permanenti.

## 1.0.0.38
- Raggio bordo esterno e interno predefiniti a **10**.
- Il bordo della cornice esterna (`Card border`, 2 px) ora nasce arrotondato.
- Nota: la cornice grigia quadrata più esterna è disegnata da Power BI (sfondo
  nativo); nessun oggetto visivo può arrotondarla. Per la finitura arrotondata,
  disattiva lo sfondo nativo e usa **Card background** + **Card border**.

## 1.0.0.37
- Nuovo controllo **Image padding** (scheda Immagine, predefinito 4, intervallo 0–50):
  immagine a sinistra/destra → 4 orizzontale e 2 verticale;
  immagine sopra/sotto → 4 verticale e 2 orizzontale.

## 1.0.0.36
- Nuova scheda **Card** (cornice esterna + corpo interno):
  **Card background**, **Card border** (2 px), **Outer border radius**,
  **Inner border radius**, **Padding** (predefinito 2 su tutti i lati).
- Lo sfondo KPI ora dipinge il corpo interno (con il proprio raggio).
- L'adattamento automatico di testo/immagine misura il corpo interno.

## 1.0.0.35
- **Decimal separator** aggiunge l'opzione **Default**: usa i separatori della
  lingua del report (`host.locale`) — es-ES/de-DE/it-IT → `1.234.567,89`,
  en-US → `1,234,567.89`, fr-FR → `1 234 567,89` — con ripiego allo stile
  inglese se il runtime non ha i dati della lingua.

## 1.0.0.34
- Regole KPI con massimi predefiniti 0,2 / 0,4 / 0,6 / 0,8 / 1,0
  (minimo della regola 1 sempre 0; concatenamento invariato).

## 1.0.0.33
- La scheda **General** scompare: tutto ciò che riguarda il valore numerico si
  trova in **Data labels** (come i controlli nativi). L'oggetto interno si chiama
  ancora `general` per non perdere le impostazioni salvate; cambiano solo i testi visibili.
- Nuovo interruttore **Thousands separator** (attivo per impostazione) in Data labels.
- Revisione traduzioni: `Card_DataLabels` e prefissi di regola localizzati
  (Règle/Regel/Regola), chiavi orfane rimosse, DE `Tausender`.
- La formattazione numerica è deterministica e indipendente dalla lingua del browser.

## 1.0.0.32
- KPI diviso in 3 schede composite con gruppi comprimibili per regola:
  **KPI Color - BG** (intervalli + sfondo, stesso oggetto `kpiBackground`, nessuna migrazione),
  **KPI Color - Labels** (nuovo oggetto `kpiLabelColors`: Label + Value per regola),
  **KPI Color - Image** (nuovo oggetto `kpiImageColors`).
- Letture concatenate (nuovo oggetto → `kpiBackground` precedente → modello → originale):
  i colori già configurati vengono conservati.

## 1.0.0.31
- La riga **Image** è nascosta dal riquadro (`visible: false`): il controllo del
  riquadro non può fornire i byte del file tramite una proprietà di testo
  (mostrava `[object Object]`). Il caricamento avviene esclusivamente facendo clic
  sull'immagine/segnaposto in modalità di modifica.

## 1.0.0.30
- Il riquadro mostra il vero nome del file invece di `"imagen_subida"`.
- I nomi senza URL vengono scartati per il rendering (segnaposto in progettazione,
  niente in visualizzazione).

## 1.0.0.29
- **Segnaposto** cliccabile (SVG inline) quando non c'è immagine in modalità progettazione.
- Solo URL caricabili (`data:`/`https:`/`blob:`); ripiego `error`
  (segnaposto in progettazione, nascosto in visualizzazione): mai più icona rotta con testo.
- Clic-per-sostituire **solo in modalità progettazione** (`ViewMode.View` lo disattiva):
  gli utenti non cambiano l'immagine nelle dashboard pubblicate.

## 1.0.0.28
- Proprietà immagine come **testo** (`{"text": true}`) + sottoclasse `CustomImageUpload`
  che accetta stringa o oggetto: è la forma che sopravvive al salvataggio PBIX
  (verificato su un progetto di riferimento; gli oggetti `{"image": true}` si perdono
  al salvataggio: presenti in sessione, assenti da `Report/Layout`).
- **Clic-per-sostituire**: selettore file nascosto → `FileReader.readAsDataURL` →
  `persistProperties` con la stringa `data:`.
- Lettore tollerante (oggetto/JSON/SVG/base64/URL) + normalizzazione `blob:` → `data:`.
- Tooltip localizzato «fai clic per sostituire».

## 1.0.0.27
- Normalizzazione `blob:` → `data:` con riscrittura via `persistProperties`
  (una conversione per URL, senza cicli).
- Cache di sessione per update senza `metadata.objects`.

## 1.0.0.26
- Rimossi i 15 interruttori Override KPI: colore vuoto = conserva l'originale.
- Slice riordinate per gruppi (intervalli+sfondo, poi etichetta/valore, poi immagine).

## 1.0.0.25
- Colori KPI per regola per immagine sostitutiva, valore numerico ed etichetta.

## 1.0.0.24
- L'immagine del modello viene ripristinata solo se vuota (non distrugge mai il
  valore persistito).

## 1.0.0.23
- Singolo controllo **Decimal separator** (Punto/Virgola, alterna le migliaia
  automaticamente) con formattazione manuale deterministica; sostituisce il precedente.

## 1.0.0.22
- Icona del oggetto visivo stile scheda (numeri + quadrato blu).

## 1.0.0.21
- Formattazione numerica con `host.locale` (separatori del report, non del browser).

## 1.0.0.20
- Layout responsive: riduzione automatica del testo e immagine proporzionale limitata.
- Interruttore separatore migliaia (sostituito poi in 1.0.0.23).

## 1.0.0.19
- Ripristina l'immagine da `dataView.metadata.objects` (il servizio di formattazione
  non compila `ImageUpload`).
- Larghezza immagine predefinita 60, decimali predefiniti 0, nuova icona.

## 1.0.0.18
- Correzioni: protezioni misura vuota, pulizia con dati vuoti, `displayName` dei
  menu, corsa asincrona immagine, decimali sugli interi, `NaN` esadecimale,
  pulizia di `package.json` (`d3` inutilizzato rimosso).
- Localizzazione completa ES/EN/FR/DE/IT (`stringResources`, `displayNameKey`,
  `pbiviz.json` con 5 lingue).

## Flusso immagine supportato (riepilogo)
1. In modalità modifica, fai clic sull'immagine o sul segnaposto per aprire il selettore.
2. Il file viene letto come URL `data:` e persistito come **testo** via
   `persistProperties` (sopravvive a salvataggio/riapertura del PBIX).
3. Verifica con `check-pbix-image.ps1` che il layout contenga l'oggetto `image`
   con schema `data:`.
