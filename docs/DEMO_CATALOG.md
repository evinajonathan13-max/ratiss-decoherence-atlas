# Catalogue des démonstrations WebGL — Studio Personnel

Le Studio Personnel est distribué avec deux pages WebGL autonomes, conçues pour ouvrir directement par `file://`. Elles reçoivent des snapshots JavaScript générés depuis les artefacts JSON versionnés du dépôt. Leur rôle est de rendre visible le fonctionnement sans serveur, pas de recalculer ou modifier les données.

| Démonstration | Fichier | Source de données | Interaction |
|---|---|---|---|
| Replay de trajectoire topologique | [`demos/trajectory-replay.html`](../demos/trajectory-replay.html) | `data/full_timeline.json` | Timeline, rotation, zoom, route TSP exportée |
| Comparaison d’ablation TTF | [`demos/ttf-ablation.html`](../demos/ttf-ablation.html) | `data/ttf/timeline_baseline.json` et `timeline_regularized.json` | Basculer référence/régularisation, timeline, rotation et zoom |

Les deux pages ont été ouvertes directement depuis le système de fichiers. Le replay de trajectoire a rendu l’artefact `internal_studio_import`, sa route `0 → 1 → 0` et ses métriques exportées. La comparaison TTF a rendu les deux snapshots séparés, la frontière de variation et les contrôles de bascule.

> Les snapshots sont générés par `node scripts/build_demo_snapshots.mjs`. Ils sont versionnés pour l’ouverture hors ligne et doivent être régénérés après tout changement des artefacts source.

Ces pages ne soumettent aucun circuit, ne simulent pas une matrice densité dans le navigateur et ne déclarent aucune validation de matériel.
