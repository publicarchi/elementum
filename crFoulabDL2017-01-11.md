---
author: Emmanuel Château-Dutier
since: 2017-01-10
---

# Notes Foulab, Deep Learning, 11 janvier 2017

h activation du layer

W une métrique

Le plus souvent les mathématiques sont appliquées par des logiciels. Celles-ci déterminent l’apprentissage du système et l’amélioration de la performances.

Les algorithmes sont relativement résistants au bug, même si les gradients ne sont pas pertinents. Faire du checking.

Motivation deep learning modèle neurologique, traitement de la complexité par couches successives dans le cortex humain. Traitement par couches successives d’identification, détection des visages, identenfication des personnes, etc.

Des justification plus formelles. Dans un circuit booléen si restreint le nombre de couches alors besoin d’un nombre d’unité exponentiellement plus important si réduit les couches.

Réussites dans le domaine de la reconnaissance du langage, et vision computationnelle.

Pourquoi entraîner des réseaux neuronaux pas si simples. Certains gradiants peuvent diminuer quand va du haut au bas. Alors peut devenir difficile.

Parfois quand réseaux neuronaux plus importants correspondent trop (overfitting).

Si pas assez performants (underfitting), peut augmenter l’entrainement. Ou bien utiliser de meilleures méthodes d’optimisation.

Si overfitting, alors régularisation. Stochastic dropout. Criblage du réseau : on retire successivement les unités indépendamment.

Batch normalization. A montré que meilleure optimization et régularisation dans les cas de underfitting et overfitting respectivement.

Normaliser les entrée accélère l’entraînement. Elle est appliquée lors de la pre-activation. cf. dia.

