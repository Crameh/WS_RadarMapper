# RadarMapper

RadarMapper est un éditeur HTML/JavaScript autonome pour créer des radars Wavestone cliquables à partir d'une image de radar et d'un jeu de zones. L'exemple embarqué est séparé dans `assets/example-radar.js` afin de garder `RadarMapper.html` lisible tout en conservant une démo prête à ouvrir.

## Workflow

1. **Initialisation**
   - Charger une image de radar.
   - Lancer une détection locale par `canvas` pour générer des zones candidates.
   - Utiliser, si autorisé, le bouton **OCR + mapping LLM** pour compléter automatiquement les noms et métadonnées.
   - Exporter un JSON d'initialisation contenant l'image, les paramètres de détection, les zones, des exemples et des consignes de format pour LLM.

2. **Édition**
   - Importer le JSON initial ou enrichi.
   - Ajuster les zones avec l'éditeur visuel. Le radar n'est éditable que dans ce mode.
   - Renseigner le nom, l'URL, le logo et le descriptif court de chaque structure.
   - Sauvegarder localement les corrections dans le navigateur.

3. **Exportation**
   - Définir le titre, le nom de fichier et le format d'intégration.
   - Régler le hover des zones et le rendu de la popup, puis les tester en live sur le radar à gauche.
   - Exporter un JSON de travail, une page HTML autonome, un snippet CMS, un iframe responsive ou une image map sans script.

4. **Configuration**
   - Choisir un fournisseur LLM : Anthropic, OpenAI ou Azure OpenAI.
   - Renseigner le modèle, la clé API et, pour Azure, l'endpoint et le déploiement.
   - Cocher l'approbation écrite requise avant tout appel externe.
   - La clé API n'est pas sauvegardée dans le navigateur ; elle doit être ressaisie à chaque session.

## Notes sur l'OCR

Sans configuration LLM, l'application reste entièrement locale : la détection utilise uniquement `canvas` et JavaScript navigateur pour isoler les pixels saillants, regrouper les fragments de logos/textes, puis générer des zones candidates rectangulaires, circulaires ou polygonales. Elle tente aussi d'utiliser l'API navigateur expérimentale `TextDetector` lorsqu'elle est disponible. Sinon elle produit des noms génériques (`zone_001`, `zone_002`, etc.) et des champs `ocrCandidate` vides.

Avec une configuration LLM, le bouton **OCR + mapping LLM** envoie l'image et le JSON courant au fournisseur choisi depuis le navigateur. Cette fonction doit être utilisée uniquement après validation explicite de l'organisation concernée.

## Sécurité des clés API

RadarMapper ne persiste pas les clés API. Le bouton **Sauver la configuration** stocke uniquement les paramètres non secrets dans `localStorage` : fournisseur, modèle, endpoint Azure, déploiement, version d'API, langue et validation d'usage. La clé saisie dans le champ mot de passe reste disponible uniquement dans la page ouverte et est vidée au rechargement.

Si une ancienne version a déjà enregistré une clé dans `localStorage`, le chargement de l'application la supprime automatiquement de la configuration sauvegardée.

## Intégration web

Les pages Wavestone Insights et RiskInsight sont des pages WordPress chargées avec leurs propres thèmes, scripts et gestionnaires de consentement. Pour éviter les collisions CSS/JS, l'onglet **Exportation** propose plusieurs formats :

- **Page autonome** : fichier HTML complet avec l'image et les zones intégrées. C'est le format à héberger tel quel, puis à afficher dans une iframe.
- **Snippet iframe responsive** : bloc HTML très court à coller dans une page WordPress après avoir renseigné l'URL du HTML hébergé. C'est l'option recommandée pour Wavestone Insights et RiskInsight, car elle isole le radar du thème WordPress.
- **Snippet CMS** : bloc HTML avec CSS préfixé et script léger. À utiliser si l'éditeur WordPress autorise les scripts dans les blocs HTML personnalisés.
- **Image map sans script** : fallback compatible avec les CMS qui filtrent JavaScript. Les zones restent cliquables, mais les popups enrichies ne sont pas disponibles.

Recommandation pratique : publier d'abord la **page autonome** sur un espace statique ou média validé, renseigner son URL dans le champ dédié, puis copier le **snippet iframe responsive** dans l'article. Le JSON reste l'archive de travail à conserver pour rééditer le radar plus tard.

Les paramètres de rendu export contrôlent l'effet de survol, la forme de la popup, ses couleurs, son ombre, sa largeur et les contenus affichés. Ces réglages sont visibles immédiatement dans l'onglet **Exportation** en survolant ou cliquant une zone du radar.
