# RadarMapper

RadarMapper est un éditeur HTML/JavaScript autonome pour produire un radar cliquable (zones + popups) à partir d'un visuel radar.

## Fonctionnalités actuelles

- Import visuel radar (`jpg/png/webp/...`).
- Deux types de radar pris en charge, choisis explicitement via le sélecteur **Radar type** de l'onglet Prepare (étape 1) :
  - **Entities / Logos** : entreprises / startups / éditeurs / produits (enrichissement = site officiel + descriptif) ;
  - **Keywords** : mots-clés / tendances tech (enrichissement = descriptif court orienté lecteur CISO).
  - Ce choix pilote la détection, l'enrichissement et le libellé d'export.
- Import facultatif d'un jeu de données (`CSV/TSV/TXT/XLS/XLSX/JSON`). En l'absence de jeu de données, le LLM lit les éléments directement sur l'image et crée la liste automatiquement lors de la détection.
- Exemple préchargé avec un visuel radar et un mapping de zones par défaut.
- Import `PPTX` (option **Alpha** désactivée par défaut) :
  - extraction d'une image de slide (thumbnail/média),
  - tentative d'import des formes/images en zones éditables.
- Mapping LLM :
  - mode externe (copie du prompt + import JSON résultat),
  - mode intégré (Anthropic / OpenAI / Azure OpenAI).
- Édition manuelle des zones (géométrie + contenu).
- Exports :
  - JSON de travail,
  - HTML autonome,
  - snippet CMS,
  - snippet iframe responsive,
  - image map sans script.

## Workflow recommandé

1. **Prepare**
   - Choisir le **Radar type** (Entities / Logos ou Keywords) à l'étape 1.
   - Importer le visuel radar (ou PPTX Alpha si activé).
   - (Facultatif) importer un jeu de données — sinon le LLM crée la liste à partir de l'image.
   - Lancer la détection LLM (intégrée ou externe) puis importer le JSON complété si nécessaire.
   - Lancer l'enrichissement LLM (site officiel pour un radar d'entreprises, descriptif CISO pour un radar de mots-clés).

2. **Edit**
   - Ajuster les zones.
   - Vérifier/compléter le nom et le descriptif (les champs `url`/`logo` restent disponibles mais ne sont pas affichés à l'export s'ils sont vides).

3. **Export**
   - Choisir le format de sortie.
   - Ajuster le style hover/popup.
   - Générer l'artefact final.

## Configuration

- Le **Radar type** (Entities / Logos ou Keywords) se choisit directement dans l'onglet Prepare, étape 1.
- Le menu **Configuration** permet :
  - d'activer **PPTX import (Alpha)**,
  - de configurer le fournisseur LLM,
  - de choisir un profil de prompt LLM (**Default (new)** par défaut, **Simple (archived)**, **Standard**, **Strict**),
  - de gérer l'auto-save.
- Les clés API ne sont pas persistées dans `localStorage` (saisie à chaque session).
