# eScriptorium

## Segmentation

https://escriptorium.inria.fr

L’outil de segmentation de Kraken ne traite pas les éléments hiérarchiques. Il n’est donc pas possible de traiter par exemple une zone principale et des sous-zones pour les paragraphes.

Afin de traiter la segmentation de manière plus riche, il est possible d’explorer d’autres outils. Pour la segmentation en utilisant SegmentOnto https://pypi.org/project/YALTAi/

Pour les points d’insertion de notes, important de vérifier qu’ils figurent dans la zone détectée pour pouvoir être traités comme des caractères. Il est alors possible d’utiliser un charactère spécial pour la détection (https://www.compart.com/fr/unicode/U+2380).

Problème du nombre d’exemples pour pouvoir découper la ligne.

Quel est l’ordre de traitement des blocs ? Sont-ils gérés de manière aléatoire ou dans l’ordre de lecture de la page ? Pas forcément utile de numéroter les zones, car pas sûr que fonctionne comme cela.

On peut entraîner un modèle de segmentation dans Kraken, il prendra en compte tous les types utilisés pour annoter les zones.

Il n’est pas possible de faire des sélections d’images pour l’entrainement. Celui-ci se fait au niveau du document, mais pas au niveau du projet. Cela impose d’avoir un document qui contient les données de terrains bien délimité.

Possible de définir un modèle de segmentation pour définir des zones sur un document où les lignes déjà transcrites. Lors de l’entraînement, plusieurs modes possibles : un pour redéfinir les masques (pour récupérer choses segmentées avec Transkribus), un mode ligne et région (supprime les transcriptions), line baselines et masks (détruit lignes si existent déjà), régions ne fait pas sauter la transcription car définit seulement les zones, mais pas certain que réassocie les lignes transcrites à la région. Si on veut entraîner un modèle pour définir des lignes. Efface la transcription.

Des outils de segmentation externe sont aussi envisageables. Par exemple YALTAi fonctionne en utilisant YOLO. La réintégration des annotations nécessite l’utilisation d’un outil de conversion.



Il y a une API pour importation en lots. Il est possible de créer des documents avec une ontologie prédéfinie en passant par l’API. 

Addon Mozilla pour valider Segmonto https://addons.mozilla.org/en-US/firefox/addon/escriptorium-segmonto-checker/

https://www.youtube.com/watch?v=FX8H9LJ_LfA

## Traitement de la transcription

L’annotation du texte

Alix ne s’en sert pas car pour le moment pas exportable. La fonctionnalité est rendue inutile. Pour les parties que n’arrive pas à transcrire ou manquantes, mieux vaut laisser toute la ligne vide [plutôt que de mettre un pseudo balisage]. Mais pénible.

Pour certains dataset, Alix coupe seulement la partie que n’arrive pas à lire.

Kraken ignore pour l’entraînement si la ligne est libre.

Pré-annoté avec un modèle de transcription et laisser modèle bizarre.

utilisation ^ pour les exposants ?

Mots barrés [[eee]]

Si biffé difficile à transcrire. Peut les ignorer mais seulement espérer que le modèle ne les interprète pas comme du texte à transcrire.

Type interlinéaire line pour les contenus insérés entre les lignes. Créée une ligne numérotée que devra potentiellement réinsérer plus tard. Si symbole insertion tant mieux.

## Guides

- À propos de l'interface, il y a le tutoriel de prise https://lectaurep.hypotheses.org/documentation/prendre-en-main-escriptorium
- Tutoriel vidéo de l'équipe SCRIPTA https://escripta.hypotheses.org/escriptorium-video-gallery

## Références

https://escriptorium.readthedocs.io/en/latest/shortcuts/

[Choco muffin : CHaracter OCR COordination for MUFI iN texts](https://github.com/PonteIneptique/choco-mufin) Mais à bien documenter pour la compatibilité

## Outils de segmentation

- [SegmOnto](https://segmonto.github.io) ontologie pour la segmentation
- [YALTAi](https://pypi.org/project/YALTAi/) segmentation fondée sur YOLO
- [RTK: Release the Krakens](https://github.com/PonteIneptique/rtk), conversion ALTAI vers Kraken.