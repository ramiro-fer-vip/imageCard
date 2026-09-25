# ImageCard — Journal des modifications

Carte KPI pour Power BI avec mesure, image positionnable, étiquette
singulier/pluriel, arrière-plan conditionnel par règles et format numérique
régional déterministe.

- **Langues du volet de format :** English (en-US), Español (es-ES),
  Français (fr-FR), Deutsch (de-DE), Italiano (it-IT).
- **Note de mise à jour :** Power BI met en cache le visuel importé. Pour tester
  une nouvelle version, supprimez le visuel du rapport et importez le `.pbiviz` récent.

---

## 1.0.0.45 (actuelle)
- Sans contenu d'infobulle (aucun champ Tooltips ni Color measure visible),
  aucune infobulle au survol.

## 1.0.0.44
- Infobulles au format du modèle (`valueFormatter` par colonne + culture du
  rapport) ; la mesure principale n'apparaît plus.
- `powerbi-visuals-utils-formattingutils` fixé à ^6.1.2 (la 7.0.0 casse
  `pbiviz package` : son fichier de locales ESM échoue au `localizationLoader`).

## 1.0.0.43
- Interrupteur maître Show image (premier dans Image, activé par défaut) :
  désactivé, carte simple sans image.

## 1.0.0.42
- Mesure unique avec remplacement (`conditions` max:1) et lectures par rôle
  (corrige la confusion Color measure).
- Rôle Tooltips multiple (jusqu'à 10) + carte Tooltip avec interrupteur
  Show color measure ; infobulles au survol.

## 1.0.0.41
- `powerbi-visuals-utils-formattingmodel` 6.0.4 → ^7.1.0, sans changement
  de code ; restes d3 purgés de `node_modules`.

## 1.0.0.40
- Nouveau contrôle **Card border width** (carte Card, sous Card border, plage 0–20,
  défaut **1**) : la bordure ne se dessine que si une couleur est choisie et largeur > 0.

## 1.0.0.39
- **Display Units** ajoute **Percentage** (×100 + `%`, sans échelle K/M) et
  **Currency** (conserve l'échelle, préfixe le symbole).
- Nouveau champ **Currency symbol** (texte, défaut `$`) qui **n'apparaît** que
  si Currency est sélectionné, sans lignes redondantes permanentes.

## 1.0.0.38
- Rayons de bordure extérieur et intérieur par défaut à **10**.
- La bordure du cadre extérieur (`Card border`, 2 px) est désormais arrondie par défaut.
- Remarque : le cadre gris carré le plus externe est dessiné par Power BI
  (arrière-plan natif) ; aucun visuel ne peut l'arrondir. Pour la finition
  arrondie, désactivez l'arrière-plan natif et utilisez
  **Card background** + **Card border**.

## 1.0.0.37
- Nouveau contrôle **Image padding** (carte Image, défaut 4, plage 0–50) :
  image à gauche/droite → 4 horizontal et 2 vertical ;
  image en haut/bas → 4 vertical et 2 horizontal.

## 1.0.0.36
- Nouvelle carte **Card** (cadre extérieur + corps interne) :
  **Card background**, **Card border** (2 px), **Outer border radius**,
  **Inner border radius**, **Padding** (défaut 2 de tous les côtés).
- L'arrière-plan KPI peint désormais le corps interne (avec son propre rayon).
- L'ajustement auto du texte/de l'image mesure le corps interne.

## 1.0.0.35
- **Decimal separator** ajoute l'option **Default** : utilise les séparateurs de la
  langue du rapport (`host.locale`) — es-ES/de-DE/it-IT → `1.234.567,89`,
  en-US → `1,234,567.89`, fr-FR → `1 234 567,89` — avec repli vers le style
  anglais si le runtime n'a pas les données de locale.

## 1.0.0.34
- Règles KPI avec max par défaut 0,2 / 0,4 / 0,6 / 0,8 / 1,0
  (min de la règle 1 toujours 0 ; chaînage inchangé).

## 1.0.0.33
- La carte **General** disparaît : tout ce qui concerne la valeur numérique se
  trouve dans **Data labels** (comme les contrôles natifs). L'objet interne
  s'appelle toujours `general` pour ne pas perdre les réglages enregistrés ;
  seuls les textes visibles changent.
- Nouveau commutateur **Thousands separator** (activé par défaut) dans Data labels.
- Audit des traductions : `Card_DataLabels` et préfixes de règle localisés
  (Règle/Regel/Regola), clés orphelines supprimées, DE `Tausender`.
- Le format numérique est déterministe et indépendant de la langue du navigateur.

## 1.0.0.32
- KPI divisé en 3 cartes composites avec groupes repliables par règle :
  **KPI Color - BG** (plages + fond, même objet `kpiBackground`, sans migration),
  **KPI Color - Labels** (nouvel objet `kpiLabelColors` : Label + Value par règle),
  **KPI Color - Image** (nouvel objet `kpiImageColors`).
- Lectures en chaîne (nouvel objet → `kpiBackground` hérité → modèle → original) :
  les couleurs déjà configurées sont conservées.

## 1.0.0.31
- La ligne **Image** est masquée du volet (`visible: false`) : le contrôle du volet
  ne peut pas fournir les octets du fichier via une propriété texte
  (il affichait `[object Object]`). L'envoi se fait exclusivement en cliquant
  l'image/le placeholder en mode édition.

## 1.0.0.30
- Le volet affiche le vrai nom du fichier au lieu de `"imagen_subida"`.
- Les noms sans URL sont écartés pour le rendu (placeholder en conception,
  rien en affichage).

## 1.0.0.29
- **Placeholder** cliquable (SVG inline) quand il n'y a pas d'image en mode conception.
- Seules les URL chargeables sont rendues (`data:`/`https:`/`blob:`) ; repli `error`
  (placeholder en conception, masqué en affichage) : plus jamais d'icône cassée avec texte.
- Clic-pour-remplacer **en mode conception uniquement** (`ViewMode.View` le désactive) :
  les utilisateurs ne changent pas l'image dans les tableaux publiés.

## 1.0.0.28
- Propriété image en **texte** (`{"text": true}`) + sous-classe `CustomImageUpload`
  acceptant chaîne ou objet : c'est la forme qui survit à l'enregistrement PBIX
  (vérifié sur un projet de référence ; les objets `{"image": true}` sont perdus
  à l'enregistrement : présents en session, absents de `Report/Layout`).
- **Clic-pour-remplacer** : sélecteur de fichier masqué → `FileReader.readAsDataURL` →
  `persistProperties` avec la chaîne `data:`.
- Lecteur tolérant (objet/JSON/SVG/base64/URL) + normalisation `blob:` → `data:`.
- Infobulle localisée « cliquer pour remplacer ».

## 1.0.0.27
- Normalisation `blob:` → `data:` avec réécriture via `persistProperties`
  (une conversion par URL, sans boucles).
- Cache de session pour les updates sans `metadata.objects`.

## 1.0.0.26
- 15 commutateurs Override KPI supprimés : couleur vide = conserve l'original.
- Tranches réordonnées par groupe (plages+fond, puis étiquette/valeur, puis image).

## 1.0.0.25
- Couleurs KPI par règle pour l'image de remplacement, la valeur numérique et l'étiquette.

## 1.0.0.24
- L'image du modèle n'est restaurée que si elle est vide (ne détruit jamais la
  valeur persistée).

## 1.0.0.23
- Contrôle unique **Decimal separator** (Point/Virgule, alterne les milliers
  automatiquement) avec format manuel déterministe ; remplace l'ancien commutateur.

## 1.0.0.22
- Icône du visuel style carte (chiffres + carré bleu).

## 1.0.0.21
- Format numérique avec `host.locale` (séparateurs du rapport, pas du navigateur).

## 1.0.0.20
- Mise en page responsive : réduction auto du texte et image proportionnelle plafonnée.
- Commutateur de séparateur de milliers (remplacé ensuite en 1.0.0.23).

## 1.0.0.19
- Restaure l'image depuis `dataView.metadata.objects` (le service de format ne
  remplit pas `ImageUpload`).
- Largeur d'image par défaut 60, décimales par défaut 0, nouvelle icône.

## 1.0.0.18
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
