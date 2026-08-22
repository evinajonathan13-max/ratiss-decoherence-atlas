# RATISS Decoherence Atlas

Cet atlas est la version **locale et hors ligne** du visualiseur RATISS. Il ne contient ni API, ni jeton, ni appel réseau au runtime. Il lit un fichier JSON choisi explicitement par la personne qui l’utilise, puis affiche strictement les nœuds, tubes, métriques, route TSP et chronologie présents dans cet artefact.

## Lancement local

Ouvrir directement `index.html` dans Chrome, Firefox ou Safari. Cliquer ensuite sur **« Ouvrir un artefact JSON »** et sélectionner `data/full_timeline.json`. Ce choix volontaire évite les limites de sécurité des navigateurs sur `fetch()` depuis une URL `file://` et rend le projet réellement navigable sans serveur local.

| Ressource | Rôle |
|---|---|
| `index.html` | Interface sans framework et sans étape de build |
| `app.js` | Lecteur de contrat, scène Three.js locale, interaction et graphique Canvas |
| `styles.css` | Mise en page responsive et accessible |
| `vendor/three.min.js` | Dépendance Three.js empaquetée localement, jamais chargée depuis un CDN |
| `data/full_timeline.json` | Exemple calculé par le moteur complet, à importer via le sélecteur |

## Contrat de données

Le format principal est `ratiss.topological-decoherence.timeline.v1` produit par le dépôt `ratiss-topological-decoherence-engine`. L’atlas accepte également, en lecture de compatibilité, le premier format RATISS contenant `timeline`, `states`, `graphs` et `n_qubits`. Le format ancien est affiché comme un import legacy et ne reçoit pas de métrique inventée.

La ligne bleu clair trace le `P_sig` du graphe de corrélations. La ligne verte trace, lorsqu’elle est fournie, la signature du **qubit topologique logique simulé RATISS**. Elles sont affichées séparément parce qu’elles ne décrivent pas le même objet. La route TSP rose est un parcours d’inspection de nœuds critiques ; elle ne sert jamais à calculer `P_sig`.

## Frontière de portée

L’atlas ne simule pas un QPU, ne réalise aucune soumission distante et ne constitue pas une validation de matériel. Il visualise les résultats calculés ou importés par le moteur.
