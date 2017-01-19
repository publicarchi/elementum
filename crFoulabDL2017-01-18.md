---
author: Emmanuel Château-Dutier
since: 2017-01-18
tags: deep learning, tal

---

# Foulab, 18 janvier 2017 (part-1)

What is Natural Language Processing ?

Traiter du texte pour effectuer des tâches utiles pour les personnes. La compréhension et la représentation complète de la signification du langage ou même le définir presque impossible.

## NPL Levels

discours (speech) vs text

phonetic/phonologic analysis vs OCR/Tokenization

morphological analysis

Syntactif analysis

Semantic Interpretation

Discource processing

DL beaucoup évolué dans la reconnaissance du langage et de la sémantique. Notamment en sautant l’analyse morphologique. Possible d’aller directement à des tâches utiles du point de vue sémantique.

## Pourquoi le NLP est difficile

Complexité dans la représentation et l’apprentissage en utilisant des savoirs linguistiques, situations, le monde ou connaissance visuelle.

- synonymie, complexité
- ambiguité

Nombreuses applications, comme la correction orthographique, extraction information de sites web, classification de documents, analyse de sentiments, etc.

Mais encore traduction par la machin, réponse à des questions ou réponses automatiques par courriel, ou les systèmes de dialogues vocaux. Beaucoup de progrès dans ces trois domaines, mais encore loin de la précision humaine.

## Représentation des tâches

Vauquois triangle

Nombreux niveaux de traduction ont été essayés dans le passé. Système de traduction par la machine (MT Machine translation) souvent très larges et complexes. Nombreux problèmes dans ces représentation.

Ici le Deep Learning employé à la manière dont ils sont utilisés pour la vision computationnelle. Ensemble de vecteurs qui vont servir de représentation pour les caractères, les mots, les phrases, leur sémantique et parfois les documents proprement dits.

## Outiline

Words vectors

Sequences models

Multiple sentences mais plus rarement

# Words

Souvent utilise des taxonomies comme wordnet qui permettent de déterminer comment un terme est en rapport avec d’autres termes. Construits de bags complexes. Une manière de définir des termes.

Mais peut aussi définir ensemble de synonymes.

Cette représentation discrete posent des difficultés. Parfois utiles mais pas suffisantes pour capter la signification. Notamment car les termes ne sont pas toujours utilisés dans le même contexte. Par ailleurs manque toujours de nouveaux mots. Jamais personne en mesure de capter l’ensemble de la signification.

Enfin très subjectif, et demande travail humain dès que change de domaine. Par ailleurs difficile de computer des similarités.

Plutôt, nous allons employer, et c’est un premier pas vers le DL, en utilisant une similarité distributionnelle. On peut obtenir beaucoup de valeur en regardant les voisins, c’est à dire en ayant recours au contexte.

ex. Window based concurrence matrix, en fait des vecteurs, très sparce. Alors peut plutôt exécuter SVD sur cette matrix donne une approximation raisonnable des vecteurs.

par ex. avec word2vec (Mikolov et al 2013) au lieu de capturer les coorcurences, capter les contextes. Peut ainsi produire de l’apprentissage en ligne.

Pour une version améliorée aller voir : cs224d.stanford.edu

pLSA methods, etc.

GloVe (Pennington et al 2014) réunit tous les avantages de ces méthodes.

- rapide à entraîner
- passage à l’échelle sur des grands corpus
- bonnes performances même avec des petits corpus, et petits vectors

chaque mot regardé comme un vector, alors possible de regarder ses voisins.

Word Vector Analogies, peut-il y avoir une relation directe et linéaire entre des termes. Quelle est l’analogie appropriée lorsque essaye de relier deux termes. Soustrait les vecteurs de mots de l’homme à celui de la femme.

visualision avec projection deux dimension, alors possible extraire relations sémantiques hommes/femmes. également relations syntactiques.

Analyse sur efficacité, s’aperçoit que plus a de données meilleurs sont les résultats.

CBOW plus efficace pour syntactique, etc. voir le schema.

## Recurrent neural network

termes qui interviennent dans un contexte donc RNN 

similaire au réseaux neuronaux normaux.

Given list of work vectors, at each time step, predicts the next word.

Un modèle très utilise pour de nombreuses tâches.

Même ensemble de poids W à toutes les étapes. Sinon le reste idem que les réseaux neuronaux.

MOdélisation du langage peut alors être considérée comme presque complète. Souvent peut prédire le mots suivant.

GRUs **Gated Recurrent Unit**, RNN mais gate mis à jour...

Deuxième modèle important à bien comprendre.

cf. https://arxiv.org/pdf/1412.3555v1.pdf

Avec ces deux, les deux concepts pour NLP

@smerity

mais problèmes qu’a souvent avec cela, souvent un softmax qui détermine les classes que l’on peut prédire. Mais peut rencontrer de nouveaux noms. Dès lors que l’introduit doit pouvoir l’intégrer dans un nouveau contexte. Steppe Merity et al, 2016.

Va beaucoup aidé notamment dans les performances

Premier obstacle pas d’architecture modèle pour le NLP

Apprentissage multitâche difficile. Souvent évaluation sur deux tâches, mais ne considère pas effets sur les autres tâches. Aide seulement si tâches relatives. Souvent brise performance.

Dynamic memory network, dernier grand modèle. S’oriente de plus en plus dans l’utilisation de principes du développement logiciel. Construction de blocs modulisables et réutilisables.

Influence prétendue des neurosciences (mémoires épisodique). Nombreux travaux sur ces modèles depuis 2014.

Souvent comparé à MemNets, mais DMN si entrée et sorties similaires de même que mécanismes de réponses. Différence input MemNets...

Sentiment analysis, c. 75% pertinence avec des modèles très simples.

POS Tagging (part of the speech tagging) que peut encore améliorer.

**Intérêt du secteur, que pas besoin d’être du domaine pour créer un modèle tout à fait approprié pour un domaine donné.**

Deux blocs qui sont essentiels pour travailler en NLP. Peuvent aujourd’hui être combinés de manière plus efficace dans des systèmes additionnels.

## Discussion

Pour travailler dans un domaine d’abord créer des données. Si pas possible de créer des données, alors peut-être que pas besoin d’automatiser.

## Différences

<http://alpage.inria.fr/~sagot/wolf.html>

