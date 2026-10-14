# Centrale de Bel-Air — supervision

[Ouvrir le site](https://vieux-mbaye.github.io/centrale-bel-air-supervision/)

Ce dépôt contient directement le site statique publié par GitHub Pages : `index.html`, `styles.css`, `app.js` et `assets/`. Les sept vues couvrent le tableau de bord, les équipements, les alarmes, les interventions, les inspections, le Digital Twin et le reporting.

Pour l’ouvrir localement, lancer un serveur HTTP dans ce dossier, par exemple `python -m http.server 8000`, puis visiter `http://localhost:8000`. Le site n’utilise pas de dépendances JavaScript externes.

Les mesures varient toutes les trois secondes. Les nouvelles alarmes simulées apparaissent au maximum une fois par minute. Les actions et le thème clair (`#F9F9F9`) sont enregistrés dans le navigateur local. La vue immersive permet de zoomer et déplacer une image industrielle ; les positions d’équipements sont illustratives et demandent des plans techniques pour validation.

La police Barlow Condensed est fournie sous licence OFL dans `assets/FONT-LICENSE.txt`.
