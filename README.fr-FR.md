# ImageCard

> **Langues:** [English](README.en-US.md) · [Español](README.md) · **Français** · [Deutsch](README.de-DE.md) · [Italiano](README.it-IT.md)

![ImageCard](images/ImageCard.jpg)

Carte KPI pour Power BI avec mesure, image positionnable, libellé singulier/pluriel,
couleurs conditionnelles par règles et format numérique régional déterministe.

- **Langues du volet de mise en forme :** English (en-US), Español (es-ES),
  Français (fr-FR), Deutsch (de-DE), Italiano (it-IT).
- **Note de mise à jour :** Power BI met en cache le visuel importé. Pour tester
  une nouvelle version, retirez le visuel du rapport et importez le `.pbiviz` frais.

## Caractéristiques du contrôle
- **Measure (mesure) :** un seul champ dans le rôle Measure ; détecte
  automatiquement nombre, texte ou date et respecte le format du modèle.
- **Data labels (valeur) :** police (taille, graisse, famille), unités d'affichage
  (Auto, None, Thousands, Millions, Billions, Trillions, Percentage, Currency),
  décimales, séparateurs décimal et de milliers, symbole monétaire, retour à la
  ligne, alignement (gauche/centre/droite) et couleur.
- **Dates :** format de date avec ou sans heure (Include time), valeur Power BI ou
  rendu propre indépendant de la langue ; fuseau horaire configurable.
- **Labels :** textes Singular et Plural avec les bascules Show label et Show
  plural ; position (Default, Up, Top, Bottom), espacement, police, alignement,
  retour à la ligne et couleur.
- **Image :** bascule Show image ; position Left, Right, Top ou Bottom (avec
  Top/Bottom l'image est centrée horizontalement) ; largeur, marge par côté
  (top, right, bottom, left) et opacité ; Color key découpe une couleur de
  l'image et la teinte avec la couleur de remplacement (ou la couleur d'image de
  la règle KPI active) ; remplacement par clic en mode conception, persistant à
  l'enregistrement du PBIX.
- **KPI Color :** couleur de fond par défaut et 5 règles de plage (Min/Max avec
  opérateur Include/Exclude max) qui colorent séparément fond, image, valeur et
  libellé ; une règle s'active par la plage seule, même si la couleur de fond
  est vide.
- **Card :** fond, bordure (couleur et épaisseur), rayons extérieur/intérieur et
  marge intérieure.
- **Tooltip :** bascule pour afficher la mesure de couleur ; les nombres de
  l'infobulle utilisent le format du modèle.
- **Rôles de données :** Measure (1 champ), Color measure (1 champ) et Tooltips
  (jusqu'à 10 champs).

---

## Journal des modifications

### 1.0.0.70 (actuelle)
- Règles KPI regroupées dans une seule carte **KPI Color** : chaque groupe
  de règle contient désormais Background color, Image color, Value color et
  Label color (remplace les cartes séparées KPI Color - BG / Labels /
  Image). Les rapports enregistrés avec les anciennes cartes conservent
  leurs couleurs (lecture en chaîne avec repli).
- Les règles s'activent par la plage seule : Value, Label et Image peuvent
  être définis sans couleur de fond (fond vide renvoie à la couleur de fond
  par défaut).
- « Image replacement color » renommé « Image color » dans chaque règle.
- Position de l'image restaurée : le contrôle applique maintenant la classe
  CSS correcte (sans tenir compte de la casse) et nettoie les classes
  obsolètes à chaque rendu. Top centre l'image horizontalement au-dessus du
  texte ; Bottom la place sous le texte.

### 1.0.0.69
- Correction du scintillement de l'image : l'élément `<img>` et sa source
  sont mis en cache et réutilisés entre les rendus ; les changements de
  couleur KPI retraitent l'image sans clignotement (URL d'origine et
  couleur de remplacement suivis séparément).
- Corrections d'ajustement du texte (accolade manquante, variable scope
  indéfinie) dans la boucle de réduction responsive.

### 1.0.0.46 – 1.0.0.68
- Format de date détecté automatiquement depuis le rôle Mesure : date seule
  ou date-heure via **Include time**, **Power BI value** et **Time zone** ;
  format du modèle respecté, formatage manuel indépendant de la langue.
- Bascules **Wrap text** et listes d'alignement (Gauche/Centre/Droite)
  pour la valeur et le libellé.
- Bascules **Show Label** et **Show Plural** (activées par défaut).
- **Image padding** par côté (haut/droite/bas/gauche, défaut 4).
- Sous-classe sûre des listes déroulantes évitant les entrées vides
  issues de valeurs persistées inconnues.
- Nombres des infobulles formatés avec le format du modèle
  (`valueFormatter`).
- Persistance de l'image par clic-à-remplacer (uniquement en mode
  conception).

### 1.0.0.45
- Sans contenu d'infobulle (aucun champ Tooltips ni Color measure visible),
  aucune infobulle au survol.

### 1.0.0.44
- Infobulles au format du modèle (`valueFormatter` par colonne + culture du
  rapport) ; la mesure principale n'apparaît plus.
- `powerbi-visuals-utils-formattingutils` fixé à ^6.1.2 (la 7.0.0 casse
  `pbiviz package` : son fichier de locales ESM échoue au `localizationLoader`).

### 1.0.0.43
- Interrupteur maître Show image (premier dans Image, activé par défaut) :
  désactivé, carte simple sans image.

### 1.0.0.42
- Mesure unique avec remplacement (`conditions` max:1) et lectures par rôle
  (corrige la confusion Color measure).
- Rôle Tooltips multiple (jusqu'à 10) + carte Tooltip avec interrupteur
  Show color measure ; infobulles au survol.

### 1.0.0.41
- `powerbi-visuals-utils-formattingmodel` 6.0.4 → ^7.1.0, sans changement
  de code ; restes d3 purgés de `node_modules`.

### 1.0.0.40
- Nouveau contrôle **Card border width** (carte Card, sous Card border, plage 0–20,
  défaut **1**) : la bordure ne se dessine que si une couleur est choisie et largeur > 0.

### 1.0.0.39
- **Display Units** ajoute **Percentage** (×100 + `%`, sans échelle K/M) et
  **Currency** (conserve l'échelle, préfixe le symbole).
- Nouveau champ **Currency symbol** (texte, défaut `$`) qui **n'apparaît** que
  si Currency est sélectionné, sans lignes redondantes permanentes.

### 1.0.0.38
- Rayons de bordure extérieur et intérieur par défaut à **10**.
- La bordure du cadre extérieur (`Card border`, 2 px) est désormais arrondie par défaut.
- Remarque : le cadre gris carré le plus externe est dessiné par Power BI
  (arrière-plan natif) ; aucun visuel ne peut l'arrondir. Pour la finition
  arrondie, désactivez l'arrière-plan natif et utilisez
  **Card background** + **Card border**.

### 1.0.0.37
- Nouveau contrôle **Image padding** (carte Image, défaut 4, plage 0–50) :
  image à gauche/droite → 4 horizontal et 2 vertical ;
  image en haut/bas → 4 vertical et 2 horizontal.

### 1.0.0.36
- Nouvelle carte **Card** (cadre extérieur + corps interne) :
  **Card background**, **Card border** (2 px), **Outer border radius**,
  **Inner border radius**, **Padding** (défaut 2 de tous les côtés).
- L'arrière-plan KPI peint désormais le corps interne (avec son propre rayon).
- L'ajustement auto du texte/de l'image mesure le corps interne.

### 1.0.0.35
- **Decimal separator** ajoute l'option **Default** : utilise les séparateurs de la
  langue du rapport (`host.locale`) — es-ES/de-DE/it-IT → `1.234.567,89`,
  en-US → `1,234,567.89`, fr-FR → `1 234 567,89` — avec repli vers le style
  anglais si le runtime n'a pas les données de locale.

### 1.0.0.34
- Règles KPI avec max par défaut 0,2 / 0,4 / 0,6 / 0,8 / 1,0
  (min de la règle 1 toujours 0 ; chaînage inchangé).

### 1.0.0.33
- La carte **General** disparaît : tout ce qui concerne la valeur numérique se
  trouve dans **Data labels** (comme les contrôles natifs). L'objet interne
  s'appelle toujours `general` pour ne pas perdre les réglages enregistrés ;
  seuls les textes visibles changent.
- Nouveau commutateur **Thousands separator** (activé par défaut) dans Data labels.
- Audit des traductions : `Card_DataLabels` et préfixes de règle localisés
  (Règle/Regel/Regola), clés orphelines supprimées, DE `Tausender`.
- Le format numérique est déterministe et indépendant de la langue du navigateur.

### 1.0.0.32
- KPI divisé en 3 cartes composites avec groupes repliables par règle :
  **KPI Color - BG** (plages + fond, même objet `kpiBackground`, sans migration),
  **KPI Color - Labels** (nouvel objet `kpiLabelColors` : Label + Value par règle),
  **KPI Color - Image** (nouvel objet `kpiImageColors`).
- Lectures en chaîne (nouvel objet → `kpiBackground` hérité → modèle → original) :
  les couleurs déjà configurées sont conservées.

### 1.0.0.31
- La ligne **Image** est masquée du volet (`visible: false`) : le contrôle du volet
  ne peut pas fournir les octets du fichier via une propriété texte
  (il affichait `[object Object]`). L'envoi se fait exclusivement en cliquant
  l'image/le placeholder en mode édition.

### 1.0.0.30
- Le volet affiche le vrai nom du fichier au lieu de `"imagen_subida"`.
- Les noms sans URL sont écartés pour le rendu (placeholder en conception,
  rien en affichage).

### 1.0.0.29
- **Placeholder** cliquable (SVG inline) quand il n'y a pas d'image en mode conception.
- Seules les URL chargeables sont rendues (`data:`/`https:`/`blob:`) ; repli `error`
  (placeholder en conception, masqué en affichage) : plus jamais d'icône cassée avec texte.
- Clic-pour-remplacer **en mode conception uniquement** (`ViewMode.View` le désactive) :
  les utilisateurs ne changent pas l'image dans les tableaux publiés.

### 1.0.0.28
- Propriété image en **texte** (`{"text": true}`) + sous-classe `CustomImageUpload`
  acceptant chaîne ou objet : c'est la forme qui survit à l'enregistrement PBIX
  (vérifié sur un projet de référence ; les objets `{"image": true}` sont perdus
  à l'enregistrement : présents en session, absents de `Report/Layout`).
- **Clic-pour-remplacer** : sélecteur de fichier masqué → `FileReader.readAsDataURL` →
  `persistProperties` avec la chaîne `data:`.
- Lecteur tolérant (objet/JSON/SVG/base64/URL) + normalisation `blob:` → `data:`.
- Infobulle localisée « cliquer pour remplacer ».

### 1.0.0.27
- Normalisation `blob:` → `data:` avec réécriture via `persistProperties`
  (une conversion par URL, sans boucles).
- Cache de session pour les updates sans `metadata.objects`.

### 1.0.0.26
- 15 commutateurs Override KPI supprimés : couleur vide = conserve l'original.
- Tranches réordonnées par groupe (plages+fond, puis étiquette/valeur, puis image).

### 1.0.0.25
- Couleurs KPI par règle pour l'image de remplacement, la valeur numérique et l'étiquette.

### 1.0.0.24
- L'image du modèle n'est restaurée que si elle est vide (ne détruit jamais la
  valeur persistée).

### 1.0.0.23
- Contrôle unique **Decimal separator** (Point/Virgule, alterne les milliers
  automatiquement) avec format manuel déterministe ; remplace l'ancien commutateur.

### 1.0.0.22
- Icône du visuel style carte (chiffres + carré bleu).

### 1.0.0.21
- Format numérique avec `host.locale` (séparateurs du rapport, pas du navigateur).

### 1.0.0.20
- Mise en page responsive : réduction auto du texte et image proportionnelle plafonnée.
- Commutateur de séparateur de milliers (remplacé ensuite en 1.0.0.23).

### 1.0.0.19
- Restaure l'image depuis `dataView.metadata.objects` (le service de format ne
  remplit pas `ImageUpload`).
- Largeur d'image par défaut 60, décimales par défaut 0, nouvelle icône.

### 1.0.0.18
- Corrections : gardes de mesure vide, nettoyage sur données vides, `displayName`
  des listes, course async d'image, décimales sur entiers, `NaN` hexadécimal,
  nettoyage de `package.json` (`d3` inutilisé supprimé).
- Localisation complète ES/EN/FR/DE/IT (`stringResources`, `displayNameKey`,
  `pbiviz.json` avec 5 locales).

## Flux d'image pris en charge (résumé)
1. En mode édition, cliquez l'image ou le placeholder pour ouvrir le sélecteur.
2. Le fichier est lu comme URL `data:` et persisté en **texte** via
   `persistProperties` (survit à l'enregistrement/réouverture du PBIX).
3. Vérifiez avec `check-pbix-image.ps1` que le Layout contient l'objet `image`
   avec un schéma `data:`.
