# Comparaison Pièces

Outil HTML autonome pour comparer finement **une paire** de photos de pièces horlogères avant/après essai de laboratoire.

## Description brève

En contrôle qualité horloger, les photos « avant » et « après » d'une pièce ne sont jamais cadrées exactement de la même façon. Cet outil recale l'image **Après** sur l'image **Avant** pour que les pièces se superposent au pixel près, puis offre plusieurs modes de visualisation pour repérer instantanément ce qui a changé (traces, corrosion, usure, matière apparue ou disparue).

C'est un fichier HTML unique fonctionnant **100 % hors-ligne**, sans installation ni dépendance externe : OpenCV.js est embarqué directement dans le fichier. Il suffit d'ouvrir le `.html` dans un navigateur. Aucune image ne quitte le poste.

> Pour traiter plusieurs images d'un coup avec une référence commune, voir l'outil complémentaire **Batch Align**.

## Caractéristiques

- Fichier unique, sans dépendance, sans connexion réseau requise
- Alignement automatique par OpenCV.js (ORB), avec repli sur un pipeline maison (Harris) si OpenCV n'est pas encore chargé
- Plusieurs solutions d'alignement proposées + raffinement sub-pixel
- Mode manuel pour les cas difficiles
- Modes de visualisation : côte à côte, superposition, rideau, et **rouge/cyan**
- Interface française, esthétique sombre

## Utilisation

1. Ouvrir `index.html` dans un navigateur.
2. Charger l'image **Avant** et l'image **Après**.
3. Cliquer sur **Aligner automatiquement**.
   - Si la solution ne convient pas, recliquer pour obtenir une **autre solution** (la vue conserve alors votre zoom et votre position, elle ne se réinitialise pas).
4. Au besoin :
   - **Améliorer** — optimisation sub-pixel de l'alignement courant.
   - Mode **manuel** — placer les points de correspondance soi-même.
5. Choisir un mode de visualisation :
   - **Côte à côte** — les deux images l'une à côté de l'autre.
   - **Superposition / Rideau** — comparaison par transparence ou balayage.
   - **Rouge/Cyan** — gris = identique, **rouge = matière disparue**, **cyan = matière apparue**.

### Convention de nommage des photos

Les photos suivent la convention : `IDpièce-Face-NuméroTest-NomTest`
(par ex. `A1234-Cadran-07-AgentSoufré`).

## Pile technique

- HTML / CSS / JavaScript natif (aucun framework)
- [OpenCV.js](https://docs.opencv.org/4.x/d5/d10/tutorial_js_root.html) embarqué (build `@techstark/opencv-js` 4.12.0) — détection ORB, appariement BFMatcher, estimation de transformation affine via RANSAC
- Pipeline d'alignement maison de secours : coins de Harris, descripteurs orientés, appariement NCC + ratio de Lowe, RANSAC + Umeyama
- Optimisation locale : Nelder-Mead (simplexe descendant) sur le score NCC
- Polices : Inter (texte), JetBrains Mono (valeurs)

## Note sur le poids du fichier

Le `.html` pèse ~11 Mo car OpenCV.js y est inline pour garantir un fonctionnement hors-ligne. Pour le développement, il peut être pratique de travailler sur une version où OpenCV est un fichier `opencv.js` séparé placé à côté du HTML, puis de ré-inliner pour la distribution. L'outil détecte automatiquement OpenCV qu'il soit inline ou en fichier externe.

## Licence

À définir.
