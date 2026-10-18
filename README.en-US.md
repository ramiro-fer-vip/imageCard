# ImageCard

> **Languages:** **English** · [Español](README.md) · [Français](README.fr-FR.md) · [Deutsch](README.de-DE.md) · [Italiano](README.it-IT.md)

![ImageCard](images/ImageCard.jpg)

KPI card for Power BI with a measure, positionable image, singular/plural label,
rule-based conditional colors and deterministic regional number formatting.

- **Format pane languages:** English (en-US), Spanish (es-ES), French (fr-FR),
  German (de-DE), Italian (it-IT).
- **Update note:** Power BI caches the imported visual. To test a new version,
  remove the visual from the report and import the fresh `.pbiviz`.

## Control features
- **Measure:** a single field in the Measure role; automatically detects number,
  text or date and respects the model format.
- **Data labels (value):** font (size, weight, family), display units (Auto, None,
  Thousands, Millions, Billions, Trillions, Percentage, Currency), decimals,
  decimal and thousands separators, currency symbol, wrap text, alignment
  (left/center/right) and color.
- **Dates:** date format with or without time (Include time), Power BI value or
  own locale-independent rendering; configurable time zone.
- **Labels:** Singular and Plural texts with the Show label and Show plural
  toggles; position (Default, Up, Top, Bottom), spacing, font, alignment, wrap
  text and color.
- **Image:** Show image toggle; position Left, Right, Top or Bottom (Top/Bottom
  centers the image horizontally); width, per-side padding (top, right, bottom,
  left) and opacity; Color key cuts one color out of the image and tints it with
  the replacement color (or the active KPI rule's image color); click-to-replace
  in design mode, persisted when the PBIX is saved.
- **KPI Color:** default background color plus 5 range rules (Min/Max with
  Include/Exclude max operator) that color background, image, value and label
  independently; a rule activates by range alone even when the background color
  is empty.
- **Card:** background, border (color and width), outer/inner radius and padding.
- **Tooltip:** toggle to show the color measure; tooltip numbers use the model
  format.
- **Data roles:** Measure (1 field), Color measure (1 field) and Tooltips (up to
  10 fields).

---

## Changelog

### 1.0.0.70 (current)
- KPI color rules consolidated into a single **KPI Color** card: each rule
  group now contains Background color, Image color, Value color and Label
  color (replaces the separate KPI Color - BG / Labels / Image cards).
  Reports saved with the old cards keep their colors (chained read fallback).
- Rules activate by range alone: Value, Label and Image colors can be set
  without defining a background color (empty background falls back to
  Default background color).
- "Image replacement color" renamed to "Image color" in every rule.
- Image position restored: the control now applies the correct CSS class
  (case-insensitive) and clears stale ones on every render. Top centers the
  image horizontally above the text; Bottom places it below the text.

### 1.0.0.69
- Image flicker fix: the `<img>` element and its source are cached and
  reused across renders; KPI color changes reprocess the image without
  flashing (original URL and replacement color tracked separately).
- Text-fit fixes (missing brace, undefined scope variable) in the
  responsive shrink loop.

### 1.0.0.46 – 1.0.0.68
- Date formatting auto-detected from the Measure role: date-only or
  date-time via **Include time**, **Power BI value** and **Time zone**
  controls; model format respected, manual locale-independent formatting.
- **Wrap text** toggles and text alignment dropdowns (Left/Center/Right)
  for value and label.
- **Show Label** and **Show Plural** toggles (on by default).
- Per-side **Image padding** (top/right/bottom/left, default 4).
- Safe dropdown subclass preventing blank entries from unknown persisted
  values.
- Tooltip numbers formatted with the model format (`valueFormatter`).
- Image persistence via click-to-replace (design mode only).

### 1.0.0.45
- With no tooltip content (no Tooltips fields and no visible Color measure),
  no tooltip appears on hover.

### 1.0.0.44
- Tooltips use the model format (`valueFormatter` per column + report culture);
  the main measure no longer appears.
- `powerbi-visuals-utils-formattingutils` pinned to ^6.1.2 (7.0.0 breaks
  `pbiviz package`: its ESM locales file fails the `localizationLoader`).

### 1.0.0.43
- Show image master toggle (first in Image, on by default): off renders
  a plain card with no image.

### 1.0.0.42
- Single measure with replace (`conditions` max:1) and role-based reads
  (fixes Color measure mix-up).
- Multiple Tooltips role (up to 10) + Tooltip card with Show color measure
  toggle; hover tooltips.

### 1.0.0.41
- `powerbi-visuals-utils-formattingmodel` 6.0.4 → ^7.1.0, no code changes;
  d3 leftovers pruned from `node_modules`.

### 1.0.0.40
- New **Card border width** control (Card card, below Card border, range 0–20,
  default **1**): the border draws only when a color is set and width > 0.

### 1.0.0.39
- **Display Units** adds **Percentage** (×100 + `%`, no K/M scaling) and
  **Currency** (keeps scaling, prepends the symbol).
- New **Currency symbol** field (text, default `$`) that **only appears**
  when Currency is selected, with no permanent redundant rows.

### 1.0.0.38
- Outer and inner border radius default to **10**.
- The outer frame border (`Card border`, 2 px) is now rounded by default.
- Note: the outermost square gray frame is drawn by Power BI (native Background);
  no custom visual can round it. For the rounded finish, disable the native
  Background and use **Card background** + **Card border**.

### 1.0.0.37
- New **Image padding** control (Image card, default 4, range 0–50):
  image left/right → 4 horizontal and 2 vertical;
  image top/bottom → 4 vertical and 2 horizontal.

### 1.0.0.36
- New **Card** card (outer frame + inner body):
  **Card background**, **Card border** (2 px), **Outer border radius**,
  **Inner border radius**, **Padding** (default 2 on all sides).
- The KPI background now paints the inner body (with its own radius).
- Text/image auto-fit measures the inner body.

### 1.0.0.35
- **Decimal separator** adds the **Default** option: uses the report language
  separators (`host.locale`) — es-ES/de-DE/it-IT → `1.234.567,89`,
  en-US → `1,234,567.89`, fr-FR → `1 234 567,89` — with fallback to English
  style when the runtime has no locale data.

### 1.0.0.34
- KPI rule defaults: max 0.2 / 0.4 / 0.6 / 0.8 / 1.0
  (Rule 1 min stays 0; chaining unchanged).

### 1.0.0.33
- The **General** card is gone: everything about the numeric value now lives in
  **Data labels** (like native controls). The internal object is still named
  `general` so saved settings are not lost; only visible strings change.
- New **Thousands separator** toggle (on by default) in Data labels.
- Translation audit: `Card_DataLabels` and localized rule prefixes
  (Règle/Regel/Regola), orphan keys removed, DE `Tausender`.
- Number formatting is deterministic and browser-language independent.

### 1.0.0.32
- KPI split into 3 composite cards with collapsible per-rule groups:
  **KPI Color - BG** (ranges + background, same `kpiBackground` object, no migration),
  **KPI Color - Labels** (new `kpiLabelColors` object: Label + Value per rule),
  **KPI Color - Image** (new `kpiImageColors` object).
- Chained reads (new object → legacy `kpiBackground` → model → original):
  already configured colors are preserved.

### 1.0.0.31
- The **Image** row is hidden from the pane (`visible: false`): the pane control
  cannot deliver file bytes through a text property (it showed `[object Object]`).
  Upload happens exclusively by clicking the image/placeholder in edit mode.

### 1.0.0.30
- The pane shows the real file name instead of `"imagen_subida"`.
- File names without URL are discarded for rendering (placeholder in design,
  nothing in view).

### 1.0.0.29
- Clickable **placeholder** (inline SVG) when there is no image in design mode.
- Only loadable URLs render (`data:`/`https:`/`blob:`); `error` fallback
  (placeholder in design, hidden in view): no more broken icon with text.
- Click-to-replace **design mode only** (`ViewMode.View` disables it):
  users cannot change the image in published dashboards.

### 1.0.0.28
- Image property as **text** (`{"text": true}`) + `CustomImageUpload` subclass
  accepting string or object: this is the shape that survives PBIX save
  (verified against a reference project; `{"image": true}` objects are lost on
  save: present in-session, absent from `Report/Layout`).
- **Click-to-replace**: hidden file picker → `FileReader.readAsDataURL` →
  `persistProperties` with the `data:` string.
- Tolerant reader (object/JSON/SVG/base64/URL) + `blob:` → `data:` normalization.
- Localized "click to replace" tooltip.

### 1.0.0.27
- `blob:` → `data:` normalization with `persistProperties` write-back
  (one conversion per URL, no loops).
- Session cache for updates without `metadata.objects`.

### 1.0.0.26
- Removed the 15 KPI Override toggles: empty color = keep the original.
- Slices reordered by group (ranges+background, then label/value, then image).

### 1.0.0.25
- Per-rule KPI colors for replacement image, numeric value and label.

### 1.0.0.24
- The model image is only restored when empty (never destroys the persisted value).

### 1.0.0.23
- Single **Decimal separator** control (Point/Comma, auto-switches thousands)
  with deterministic manual formatting; replaces the previous toggle.

### 1.0.0.22
- Card-style visual icon (numbers + blue square).

### 1.0.0.21
- Number formatting with `host.locale` (report separators, not browser ones).

### 1.0.0.20
- Responsive layout: text auto-shrink and proportionally capped image.
- Thousands separator toggle (later replaced in 1.0.0.23).

### 1.0.0.19
- Restores the image from `dataView.metadata.objects` (the formatting service
  does not populate `ImageUpload`).
- Image width default 60, decimals default 0, new icon.

### 1.0.0.18
- Fixes: empty-measure guards, clearing on empty data, dropdown `displayName`,
  async image race, integers with decimals, hex `NaN`, `package.json` cleanup
  (unused `d3` removed).
- Full ES/EN/FR/DE/IT localization (`stringResources`, `displayNameKey`,
  `pbiviz.json` with 5 locales).

## Supported image flow (summary)
1. In edit mode, click the image or placeholder to open the file picker.
2. The file is read as a `data:` URL and persisted as **text** via
   `persistProperties` (survives PBIX save/reopen).
3. Verify with `check-pbix-image.ps1` that the Layout contains the `image`
   object with a `data:` scheme.
