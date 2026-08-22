# Notes de vérification

## Ouverture locale

Le 22 août 2026, `index.html` a été ouvert directement via une URL locale `file://`. La structure HTML, la scène WebGL, l’inspecteur, le lecteur de timeline et le graphique Canvas se sont tous chargés sans CDN ni serveur.

L’état initial est volontairement vide : l’utilisateur choisit explicitement un artefact JSON au moyen du sélecteur de fichier. Cette approche est requise pour rester compatible avec l’ouverture directe d’un fichier HTML, car un navigateur restreint habituellement la lecture automatique d’un fichier JSON voisin depuis `file://`.

La vérification suivante doit charger `data/full_timeline.json`, généré par le moteur complet, puis confirmer le rendu des nœuds, des tubes et des valeurs exportées.

## Chargement de l’artefact calculé

Le même jour, `data/full_timeline.json` a été sélectionné localement dans l’interface. L’atlas a chargé **11 étapes** et affiché la scène de cinq nœuds, les tubes provenant des arêtes exportées, la timeline, ainsi que les métriques suivantes à l’étape initiale : `P_sig` de graphe `0.000`, signature logique RATISS `1.214`, décohérence moyenne `0.000` et Betti `[1, 0, 0]`.

La différence entre la persistance de graphe nulle à cette étape et la signature du noyau logique non nulle est intentionnelle et visible : les deux pipelines sont exportés séparément. Aucun tube, score ou chemin n’a été inventé par l’atlas.

Le curseur a ensuite été positionné sur l’étape terminale de l’artefact régénéré. Cette étape comporte une route TSP exportée calculée sur les nœuds critiques `3` et `4` : `3 → 4 → 3`, avec la méthode exacte `held_karp_exact` et un coût de `6.670742751` dans les coordonnées de visualisation déterministes.

Le visualiseur a ensuite été corrigé pour lire le seuil de criticité directement dans `config.criticality_threshold` de l’artefact, plutôt que de conserver un seuil d’interface fixe. Cette correction garantit que les couleurs, le compteur de nœuds critiques et la route TSP restent synchronisés avec le calcul du moteur.

L’artefact régénéré a été rechargé avec succès après cette correction ; l’atlas confirme de nouveau le schéma `timeline.v1` et ses onze étapes. La vérification terminale est ensuite menée par positionnement du curseur sur l’étape `10`.

## Vérification terminale alignée

À l’étape `10` (`cx(2,4)`), l’interface affiche désormais exactement les éléments fournis par l’artefact : décohérence moyenne `0.018`, deux nœuds critiques en rouge, `P_sig` logique `0.766`, Betti `[1, 0, 0]` et la route rose `3 → 4 → 3`. Le panneau indique `held_karp_exact` et le coût arrondi `6.671`.

Cette vérification confirme que la couleur, le compteur de criticité, la route et le panneau ne sont pas décoratifs : ils sont synchronisés avec `config.criticality_threshold`, les scores de nœuds et `tsp_inspection` du JSON réel.
