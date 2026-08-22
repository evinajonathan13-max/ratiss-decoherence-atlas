# RATISS Quantum Topology Studio Personal

Ce studio personnel est la version **locale et hors ligne** de la famille RATISS. Il réunit un espace de conception Quantum Circuit Studio compact et l’Atlas WebGL de cartographie topologique. Il ne contient ni API, ni jeton, ni appel réseau au runtime.

## Lancement local

Ouvrir directement `index.html` dans Chrome, Firefox ou Safari. Le panneau **Studio Personnel** contient immédiatement un design local `transmon-microcell`, son schéma, ses couches conceptuelles, ses fréquences nominales et son overlay de diaphonie. Cliquer sur **« Exporter le design »** pour produire un fichier `quantum-circuit-studio/v0.1`.

Cliquer ensuite sur **« Ouvrir un artefact JSON »** et sélectionner `data/full_timeline.json`. Ce choix volontaire évite les limites de sécurité des navigateurs sur `fetch()` depuis une URL `file://` et rend le projet réellement navigable sans serveur local.

| Ressource | Rôle |
|---|---|
| `index.html` | Interface sans framework et sans étape de build |
| `app.js` | Lecteur de contrat, scène Three.js locale, interaction et graphique Canvas |
| `studio-model.js` + `personal-studio.js` | Modèle et contrôleur Quantum Circuit Studio compatibles avec `file://` |
| `studio-model.mjs` | Copie traçable du modèle source Quantum Circuit Studio pour tests et comparaison |
| `styles.css` | Mise en page responsive et accessible |
| `vendor/three.min.js` | Dépendance Three.js empaquetée localement, jamais chargée depuis un CDN |
| `data/full_timeline.json` | Exemple calculé par le moteur complet, à importer via le sélecteur |

## Contrat de données

Le format principal est `ratiss.topological-decoherence.timeline.v1` produit par le Studio Cloud. Le modèle de conception local utilise `quantum-circuit-studio/v0.1`. L’atlas accepte également, en lecture de compatibilité, le premier format RATISS contenant `timeline`, `states`, `graphs` et `n_qubits`. Le format ancien est affiché comme un import legacy et ne reçoit pas de métrique inventée.

La ligne bleu clair trace le `P_sig` du graphe de corrélations. La ligne verte trace, lorsqu’elle est fournie, la signature du **qubit topologique logique simulé RATISS**. Elles sont affichées séparément parce qu’elles ne décrivent pas le même objet. La route TSP rose est un parcours d’inspection de nœuds critiques ; elle ne sert jamais à calculer `P_sig`.

## Frontière de portée

Le navigateur ne lance pas une simulation matrice densité, ne soumet pas de circuit, ne réalise pas d’extraction EM et ne constitue pas une validation de matériel. Il prépare/exporte un design local et visualise strictement les résultats calculés ou importés par le moteur.

## Relation avec le Studio Cloud

Ce dépôt est clonable seul. Pour une simulation matrice densité, une trajectoire issue de Quantum Circuit Studio ou l’adaptateur Qiskit Statevector, exporter le design et le traiter dans le **RATISS Quantum Topology Studio Cloud**. Celui-ci produit la même timeline `timeline.v1`, que ce Studio Personnel peut ensuite charger et analyser hors ligne.

## Vérification

```bash
pnpm test
```

Les tests vérifient l’artefact fourni et le contrat de modèle du Studio Personnel. [`docs/VERIFICATION_NOTES.md`](docs/VERIFICATION_NOTES.md) consigne l’ouverture en `file://`, les panneaux du Studio et l’import d’une timeline générée par le Studio Cloud.

Le dossier `data/external/` contient trois timelines de fixtures importables et étiquetées : comptages Qiskit (`external_qiskit_counts`), distributions de modes photoniques (`external_photonic_modes`) et matrices de corrélation bio déclarées (`external_bio_correlation`). Elles testent les contrats d’import ; elles ne représentent ni des résultats QPU, ni un dispositif photonique, ni des données biologiques réelles.
