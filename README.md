# RadarMapper

RadarMapper est un éditeur HTML/JavaScript autonome pour créer des radars Wavestone cliquables à partir d'une image de radar et d'un jeu de zones.

## Workflow

1. **Initialisation**
   - Charger une image de radar.
   - Lancer une détection locale par `canvas` pour générer des zones rectangulaires candidates.
   - Exporter un JSON d'initialisation contenant l'image, les paramètres de détection et les zones.
   - Compléter ce JSON via un LLM avec l'image et un fichier XLS/CSV de contenus si nécessaire.

2. **Édition**
   - Importer le JSON initial ou enrichi.
   - Ajuster les zones avec l'éditeur visuel existant.
   - Renseigner le nom, l'URL, le logo et le descriptif court de chaque structure.
   - Exporter un JSON de travail ou un HTML autonome intégrable au site principal.

3. **Configuration**
   - Régler les paramètres de détection locale : contraste, taille de composants, marge, fusion de zones et ratio maximal.
   - Définir le titre et le nom de fichier de l'export HTML.

## Notes sur l'OCR

L'application ne dépend d'aucun service externe ni d'aucune librairie tierce. Elle tente d'utiliser l'API navigateur expérimentale `TextDetector` lorsqu'elle est disponible, sinon elle produit des noms génériques (`zone_001`, `zone_002`, etc.) et des champs `ocrCandidate` vides dans le JSON pour faciliter l'enrichissement par LLM.
