# RadarMapper

RadarMapper est un éditeur HTML/JavaScript autonome pour produire un radar cliquable (zones + popups) à partir d'un visuel radar.

## Fonctionnalités actuelles

- Import visuel radar (`jpg/png/webp/...`).
- Import d'organisations (`CSV/TSV/TXT/XLS/XLSX/JSON`) pour enrichir les zones.
- Exemple préchargé avec un visuel radar, un jeu d'organisations et un mapping de zones par défaut.
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
   - Importer le visuel radar (ou PPTX Alpha si activé).
   - Importer le fichier d'organisations.
   - Lancer le mapping LLM (intégré ou externe) puis importer le JSON complété si nécessaire.

2. **Edit**
   - Ajuster les zones.
   - Vérifier/compléter `name`, `url`, `logo`, `description`.
   - Confirmer les liens zone ↔ organisation.

3. **Export**
   - Choisir le format de sortie.
   - Ajuster le style hover/popup.
   - Générer l'artefact final.

## Configuration

- Le menu **Configuration** permet :
  - d'activer **PPTX import (Alpha)**,
  - de configurer le fournisseur LLM,
  - de choisir un profil de prompt LLM (**Default (new)** par défaut, **Simple (archived)**, **Standard**, **Strict**),
  - de gérer l'auto-save.
- Les clés API ne sont pas persistées dans `localStorage` (saisie à chaque session).
