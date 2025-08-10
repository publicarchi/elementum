# Techniques de plongement lexical (word embedding)

> Les *plongements lexicaux* représentent les mots sous forme de vecteurs dans un espace multidimensionnel, où la distance et la direction entre les vecteurs reflètent la similarité et les relations entre les mots correspondants.
>
> (Barnard 2024)

La représentation vectorielle d’un mot est généralement obtenue par l’analyse de sa distribution et du contexte lexical de chacune de ses occurences au sein du corpus. Les plus récentes approches reposent sur des modèles probabilistes.

L’utilisation des plongements pour representer du texte a joué un rôle déterminant dans le développement des applications de traitement automatique du langage naturel (NLP). Leur utilisation est aujourd’hui fondamentale pour les tâches de classification de texte, d’analyse de sentiments ou de traduction de textes.

cf. https://vitrinelinguistique.oqlf.gouv.qc.ca/fiche-gdt/fiche/26560496/plongement-de-mots

Word2Vec et TF-IDF.

Les One Hot Encoding, TF-IDF, Word2Vec, FastText sont des méthodes souvent utilisées pour le plongement lexical.

### Encodage 1 parmi n (*One Hot Encoding*)

Dans l’*encodage 1 parmi n* (*One hot encoding*), chaque mot est représenté sous la forme d’un vecteur creux dont la dimension est égale à la taille du vocabulaire.

Les données catégorielles doivent être converties en données numériques pour pouvoir être traitées avec des modèles de machine learning. On peut alors assigner une valeur numérique à ces étiquettes puis utiliser la technique du One Hot Encoding.

La dimension augmente plus le lexique augmente (*curse of*
*dimensionality*). Par ailleurs, cette représentation manque d’informations sémantiques et ne capture pas les relations entre les mots.

### Plongements lexicaux

> Les *plongements lexicaux*, quant à eux, sont des vecteurs denses avec des valeurs continues qui sont entraînés à l’aide de techniques de machine learning, souvent basées sur des réseaux neuronaux. L’idée est d’apprendre des représentations qui encodent la signification et les relations sémantiques entre les mots. Les plongements lexicaux sont entraînés en exposant un modèle à une grande quantité de données textuelles et en ajustant les représentations vectorielles en fonction du contexte dans lequel les mots apparaissent.
>
> (Barnard 2024)

>Les plongements de mots sont des représentations numériques de mots de faible dimension, générées par des méthodes d’intelligence artificielle (IA) qui prennent en compte les statistiques de cooccurrence des mots. L’hypothèse sur laquelle reposent ces modèles est que les mots situés à proximité les uns des autres dans l’espace vectoriel sont sémantiquement similaires. La similarité entre deux sens de mots, tels que “assiette” et “bol”, peut être quantifiée par la similarité cosinus entre les vecteurs correspondants dans le modèle. 
>
>(Calistan & Lewis, 2020, p. 3).

La *représentation distributionnelle* compte le nombre de fois où un mot apparait dans un texte et lui attribue un vecteur correspondant.

> Word2Vec est une méthode populaire d’entraînement des plongements lexicaux. Elle utilise un réseau neuronal pour prédire les mots voisins d’un mot cible dans un contexte donné. Une autre approche largement utilisée est GloVe (Global Vectors for Word Representation), qui tire parti de statistiques globales pour créer des plongements.
>
> (Barnard 2024)

Les plongements lexicaux s’avèrent très efficaces dans diverses tâches car ils permettent de tenir compte des relations sémantiques entre les mots de manière plus nuancée que d’autres approches traditionnelles.

Ils sont notamment utilisées pour :

- la classification de texte (analyse de sentiments, détection des spams, catégorisation des sujets)
- la reconnaissance d’entité nommées (Names Entity Recognition NER) en permettant une meilleure prise en compte du contexte et des relations entre les mots
- la traduction automatique
- la recherche d’information
- la réponse aux questions
- la similarité sémantique et le regroupement de documents
- la génération de textes
- la recherche de similarité et d’analogies
- servir de modèles de pré-entraînements

## Sources

- https://vitrinelinguistique.oqlf.gouv.qc.ca/fiche-gdt/fiche/26560496/plongement-de-mots
- https://fr.wikipedia.org/wiki/Plongement_lexical
- Barnard, Joël. 2024. « Que sont les plongements lexicaux ? » 16 mai 2024. https://www.ibm.com/fr-fr/topics/word-embeddings.