XQuery Update pour les impatients, Une rapide introduction à la fonctionnalité de mise à jour de XQuery
=========

essai de traduction française de

Xavier Franc, XQuery Update for the impatient, A quick introduction to the XQuery Update Facility, http://www.xmlmind.com/tutorials/XQueryUpdate/index.html

CC Attribution-ShareAlike

Table des matières
========

1. Bases
    1.1. Les primitives de mise à jour
    1.2. Comment les primitives de mise à jour se combinent avec le langage de base ?
    1.3. Le modèle de traitement
2. Pour allez plus loin
    2.1. Les opérations avec les primitives revisitées
    2.2. Le problème des mises à jour invisbles
    2.3. Mélanger des expressions de mise à jour avec d'autres expressions
    2.4. Ordre et conflits
3. Conclusion

La fonctionnalité de mise à jour XQuery Update est une relativement petite extenson du langage XQuery qui fournit des moyens pratiques pour modifier des documents ou des données XML. Depuis qu'elle est devenue une "recommandation candidate" le 14 mars 2008, la [XQuery Update Facility specification]() est maintenant plutôt stable.

Pourquoi une fonctionnalité de mise à jour en XML Query ? La réponse peut paraître évidente, mais après tout le langage XQuery lui-même – ou encore son cousin XSLT2 – est suffisamment puissant pour écrire n'importe quelle transformation d'un arbre XML. Ainsi, une simple fonction "store" ou "put" pourrait paraître suffisant pour réaliser n'importe quelle opération de mise à jour d'une base de données. Bon, peut-être. En pratique, cela ne serait ni très naturel ou pratique, ni non plus très efficient (une telle approche nécessite de stocker tout le document et rend l'optimisation très difficile). Ainsi, comme nous allons le voir, la petite complexité ajoutée par XQuery Update semble valoir la peine.

Ce tutoriel essaye de donner une introduction pratique mais aussi compréhensive de l'extension XQuery Update, tout en mettant en lumière certainnes de ses particularités.

__Pré-requis__ : le lecteur est présumé avoir qeulques accointances avec XML Query et son modèle de données (XDM, la représentation abstraite des données XML qui comporte six types de nœuds : document, element, attribute, text, comment, processing-instruction).


## 1. Bases

### Les primitives de mise à jour

La fonctionnalité de mise à jour de XQuery (_XQuery Update Facility_, abrégée en XQUF ci-après) fournit cinq opérations de base agissant sur des nœuds XML :
- __insérer (_insert_)__ un ou plusieurs nœuds à dans/après/avant un nœud spécifié
- __effacer (_delete_)__ un ou plusieurs nœuds
- __remplacer (_replace_)__ un nœud (et tous ses descendants si c'est un élément) par une séquence de nœuds.
- __remplacer le contenu (_replace the contents_)__ (c'est-à-dire les fils) d'un nœud par une séquence de nœuds, ou la __valeur (_value_)__ d'un nœud avec un valeur de chaîne.
- __renommer (_rename_)__ un nœud (applicable aux éléments, attributs et instructions de traitements) sans affecter leurs contenus ou attributs.

Ces primitives sont détaillées ci-après.

### 1.2. Comment les primitives de mise à jour se combinent-elles avec le langage ?

Typiquement, on utilise des requêtes pour sélectionner le(s) nœud(s) que l'on souhaite mettre à jour, puis on applique à ce(s) nœud(s) l'opération de mise à jour. Cela est très similaire à l'instruction SQL `UPDATE ... WHERE ...`.

#### Exemple 1 :

Dans un document `doc.xml`, renommer en tant que "SECTION_TITLE" tous les éléments fils "TITLE" d'une "SECTION" :

```xquery
    for $title in doc("doc.xml")//SECTION/TITLE (: sélection :)
    return renamenode $title as SECTION_TITLE   (: mise à jour :)
```

#### Exemple 2 :

Pour tous les éléments "ITEM" qui ont un attribut "Id", remplacer cet attribut par un enfant " NID" en première position :

```xquery
    for $idattr in doc("data.xml")//ITEM/@Id     (: sélection :)
    return (
        delete node $idattr,                     (: mise à jour 1 :)
        insert node <NID>{string($idattr)}</NID> (: mise à jour 2 :)
            as first into $idattr/..
    )
```

Avec ce dernier script, le fragment suivant

```xml
    <ITEM Id="id123">some content</ITEM>
```

serait transformé en :

```xml
    <ITEM><NID>id123</NID>some content</ITEM>
```

__Note__ : Dans ce dernier exemple, il est absolument indiférent que l'instruction  __delete__ soit inscrite avant ou après __insert node__. Cette propriété surprenante de XQUF est expliqué ci-dessous.

Il existe des restrictions dans la manière dont les cinq opérations de mise à jour peuvent être mélangées avec le langage XQuery de base. XQUF fait une distinction entre les Expressions de mise à jour (_Updating Expression_), lesquelles englobes les primitives de mise à jour, et les expressions de non mise à jour (_non-updating expressions_). Les expressions de mise à jour ne peuvent pas apparaître n'importe où. Cette question sera maintenant expliquée plus en détail.


### 1.3. Modèles de traitement

Il y a deux manières principales d'utiliser les primitives de mise à jour :

#### 1. en mise à jour directe d'une base de données XML :

Dans les exemples ci-dessus, les nœuds apparatenant à une base de données sont sélectionnés puis mis à jour.

__Note__ : La notion de base de données en XQUF est très générique : elle recouvre n'importe quelle collection de documents ou de fragments XML bien formés.

XQuery Update ne définit pas précisément le protocole au moyen duquel les opérations de mise à jour sont appliquées à une base de données. Celà est laissé aux implémentations. Par exmeple, les questions relatives aux transactions et à l'isolation ne sont pas considérées par les spécifications.

On suppose simplement que les mises à jour sont appliquées à la base de donnéesquand l'exécution d'un scripte est terminée. Le langage est conçu de telle manière que la sémantique des opérations de mise à jour (_"apply-updates"_) est précisément définie, aussi toute latitude est laissée pour l'optimisation pour les implémentations de base de données.

Points à noter :
- _Les mises à jour ne sont pas appliquées immédiatement lorsque l'expression s'exécute_. À l'inverse, elles sont accumulées dans une liste de mise à jour en attente ("_Pending Udate List_"). À un certain moment vers la vin de l'exécution, ces mises à jour en attente sont appliquées toutes en même temps, et la base de données est mise à jour atomiquement.
Une conséquence notable est que les _mises à jour ne sont pas visible pendant l'exécution du script_, mais seulement après. Cela peut être déconcertant pour un développeur. Cela a également une influence évidente sur le style de programmation. Nous verrons plus loin des exemples de cet effet et la manière de les prendre en compte.

- La même expression peut mettre à jour plusieurs document en même temps. Les examples ci-dessus pourraient être appliqués à n'importe quelle collection de documents au lien du simple document doc.xml.
Exemple :
```xquery
    for $title in collection("/allbooks")//SECTION/TITLE
    return rename node $title as SECTION_TITLE
```

#### 2. en transformation sans effet de bord :

XQUF dispose d'une opération supplémentaire appellée "tranform" qui met à jour une copie d'un nœud existant, sans modifier l'original et retourne l'abre transformé.

L'exemple suivant produit une version transformée de doc.xml sans toucher le document original :

```xquery
    copy $d := doc('doc.xml")
    modify (
        for $t in $d//SECTION/TITLE
        return rename node $t as SECTION_TITLE
    )
    return $d
```

Remarquez qu'_au sein de la clause modify_ XQUF interdit de modifier la _version originale_ des arbres copiés (ici le document doc.xml lui-même) : seuls les abres copiés peuvent être modifiés. L'expression suivante génèrerait une erreur :

```xquery
    copy $d := doc("doc.xml")
    modify (
        for $t in doc("doc.xml")//SECTION/TITLE (: **** FAUX **** :)
        return rename node $t as SECTION_TITLE
    )
    return $d
```

## 2. Pour aller plus loin

TODO :  à continuer
