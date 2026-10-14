# Centrale de Bel-Air — projet de supervision

Application complète côté navigateur en HTML, CSS et JavaScript natif, construite à partir des neuf références fournies. Aucun framework ni service externe n’est nécessaire pour l’exécuter.

## Démarrage

Avec Node.js installé, ouvrir un terminal dans ce dossier :

```sh
npm start
```

Puis ouvrir http://127.0.0.1:8787. Le port peut être changé avec la variable d’environnement `PORT`.

L’ouverture directe de `dist/index.html` fonctionne aussi dans les navigateurs autorisant le stockage local pour les fichiers. Le serveur local est préférable.

## Les sept vues

- Tableau de bord : six groupes, disponibilité, courbe de production, activité, planning et plan interactif.
- Équipements : sélection du groupe, sous-ensembles, mesures et repères sur le visuel industriel.
- Alarmes : filtres combinés, détails, acquittement, notes, création d’intervention et export CSV.
- Interventions : registre partagé de 48 interventions initiales, dont 12 ouvertes ; création, affectation, fiche et clôture avec compte rendu.
- Inspections : points de contrôle, validation, anomalie et ajout d’une photo pendant la session.
- Digital Twin : arborescence, paramètres, historique, maintenance et vue immersive avec zoom/déplacement.
- Reporting : disponibilités, répartition calculée des alarmes, préventif/correctif, rapport par groupe et export.

## Simulation et sauvegarde

Les mesures varient toutes les **3 secondes**. Les alarmes automatiques apparaissent à partir de **60 secondes**, puis à intervalles d’au moins **60 secondes**. Le navigateur peut retarder les minuteries dans les onglets en arrière-plan ; aucune rafale de rattrapage n’est générée.

Les alarmes, interventions, notes, validations et préférence de thème sont enregistrées dans le `localStorage` du navigateur, sous `bel-air-v1`. Les données restent locales à ce navigateur et ne sont pas partagées entre utilisateurs. Pour réinitialiser la démonstration, supprimer cette clé dans les outils de développement du navigateur.

Le mode clair utilise **#F9F9F9** : interprétation de la valeur incomplète `#F9F9F` indiquée dans la demande. Le thème sombre reprend un fond #090F10, des panneaux #0B1112, du turquoise #40C6D2 / #19D7EE et de l’orange #FF6B42.

## Structure

```text
dist/index.html       Document HTML
dist/styles.css       Mise en page responsive et deux thèmes
dist/app.js           Vues, état partagé, simulation et interactions
dist/assets/          Images et police embarquées
server.cjs            Serveur HTTP local sans dépendance
package.json          Commandes de démarrage et de vérification
tests/                Scénarios navigateur de vérification
QA.md                 Résultats des contrôles
ASSET_PROMPTS.txt      Prompts des deux fonds industriels retouchés
```

## Fidélité et limites explicites

Les écrans sont reconstruits avec de vrais éléments HTML et des graphiques SVG ; ce ne sont pas des captures d’écran posées comme interface. Les images industrielles proviennent des références utilisateur. Deux fonds sans annotations, panorama et plan aérien, ont été produits avec l’outil imagegen intégré ; les prompts exacts sont fournis. La police libre Barlow Condensed est embarquée avec sa licence OFL.

La composition, les couleurs et l’iconographie sont rapprochées des références, mais **le rendu n’est pas une reproduction pixel pour pixel**. Les chiffres ont été rendus cohérents entre écrans lorsque les références se contredisaient. Les références présentent des dates historiques d’avril 2026 ; le planning de démonstration conserve ce contexte.

Les vues de centrale, les positions et les raccordements sont **illustratifs**, sans garantie de correspondance à un plan d’implantation constructeur. Les chaudières sont explicitement indiquées hors du groupe. Une photo ne permet pas d’identifier et valider tous les circuits ; des plans P&ID, une nomenclature et un modèle CAO sont nécessaires pour une implantation certifiée.

La vue immersive utilise une image avec zoom/déplacement, **pas un maillage 3D**. L’application n’est pas reliée à une centrale réelle, à un automate ou à un SCADA. Les documents techniques sont des fiches de démonstration clairement identifiées. Une mise en production nécessiterait API de télémétrie, base partagée, authentification, droits et procédures constructeur validées.

## Vérifications

`npm run check` contrôle la syntaxe JavaScript. Les tests navigateur sont dans `tests/` ; ils utilisent Playwright, à installer séparément pour les relancer (`npm install --no-save playwright`, puis `npx playwright install chromium`). Démarrer le serveur dans un premier terminal, puis exécuter :

```sh
node tests/test-interactions.cjs
node tests/qa.cjs
```

Les exports CSV utilisent un séparateur point-virgule et l’encodage UTF-8 avec BOM, adaptés aux tableurs configurés en français.
