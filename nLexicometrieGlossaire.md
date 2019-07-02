# Glossaire de lexicométrie

Tiré de Glossaire pour la statistique textuelle

http://lexi-co.com/ressources/manuel-3.41.pdf

La définition de quelques notions de base en statistique textuelle est reprise dans l’aide en ligne.

NB : Les astérisques renvoient à une entrée de ce même glossaire. Les abréviations qui suivent entre parenthèses précisent le domaine auquel s'applique plus particulièrement la définition. 

## Abréviations : 

- ac Analyse factorielle des correspondances 
- acm Analyse des correspondances multiples 
- cla Classification
- sp Méthode des Spécificités 
- sr Analyse des segments répétés 
- ling Linguistique
- stat Statistique
- sa Segmentation automatique 

## Définitions

### accroissement spécifique

**accroissement spécifique** – (sp) spécificité* calculée pour une partie d'un corpus par rapport à une partie antérieure

### analyse factorielle

**analyse factorielle** – (stat) famille de méthodes statistiques d'analyse multidimensionnelle, s'appliquant à des tableaux de nombres, qui visent à extraire des "facteurs" résumant approximativement par quelques séries de nombres l'ensemble des informations contenues dans le tableau de départ. 

### analyse des correspondances

**analyse des correspondances** – (stat) méthode d'analyse factorielle s'appliquant à l'étude de tableaux à double entrée composés de nombres positifs. L'AC est caractérisée par l'emploi d'une distance (ou métrique) particulière dite distance du chi-2 (ou c2). 

### caractère

**caractère** – (sa) signe typographique utilisé pour l'encodage du texte sur un support lisible par l'ordinateur. 

### caractères délimiteurs / non-délimiteurs

**caractères délimiteurs / non-délimiteurs** – (sa) distinction opérée sur l'ensemble des caractères qui entrent dans la composition du texte, permettant aux procédures informatisées de segmenter le texte en occurrences* (suite de caractères non-délimiteurs bornée à ses extrémités par des caractères délimiteurs). 

On distingue parmi les caractères délimiteurs : 

-  les caractères délimiteurs d'occurrence (encore appelés "délimiteurs de forme") qui sont en général : le blanc, les signes de ponctuation usuels, les signes de préanalyse éventuellement contenus dans le texte. 
- les caractères délimiteurs de séquences : sous-ensemble des délimiteurs d'occurrence correspondant, en général, aux ponctuations faibles et fortes contenues dans la police des caractères. 
- les caractères séparateurs de phrase : (sous-ensemble des délimiteurs de séquence) qui correspondent, en général, aux seules ponctuations fortes.

### classification

**classification** – (stat) technique statistique permettant de regrouper des observations ou des individus entre lesquels a été définie une distance. 

### classification hiérarchique

**classification hiérarchique** – (cla) technique particulière de classification produisant par agglomération progressive des classes ayant la propriété d'être, pour deux quelconques d'entre-elles, soit disjointes, soit incluses. 

### concordance

**concordance** – (sa) l'ensemble de lignes de contexte se rapportant à une même forme-pôle. 

### contribution absolue (ou contribution)

**contribution absolue (ou contribution)** – (ac) contribution apportée par un élément au facteur. Pour un facteur donné, la somme des contributions sur les éléments de chacun des ensembles mis en correspondance est égale à 100. 

### contribution relative (ou cosinus carré)

**contribution relative (ou cosinus carré)** – (ac) contribution apportée par le facteur à un élément. Pour un élément donné, la somme des contributions relatives sur l'ensemble des facteurs est égale à 1. 

### cooccurrence

**cooccurrence** – (sa) (une c. ) présence simultanée, mais non forcément contiguë, dans un fragment de texte (séquence, phrase, paragraphe, voisinage d'une occurrence, partie du corpus etc.) des occurrences de deux formes données. 

### corpus

**corpus** – (ling) ensemble limité des éléments (énoncés) sur lesquels se base l'étude d'un phénomène linguistique. 

– (lexicométrie) ensemble de textes réunis à des fins de comparaison; servant de base à une étude quantitative. 

### délimiteurs de séquence

**délimiteurs de séquence** – (sa) sous-ensemble des caractères délimiteurs* de forme* correspondant aux ponctuations faibles et fortes (en général - le point, le point d'interrogation, le point d'exclamation, la virgule, le point-virgule, les deux points, les guillemets, les tirets et les parenthèses). 

### dendrogramme

**dendrogramme** – (cla) représentation graphique d'un arbre de classification hiérarchique, mettant en évidence l'inclusion progressive des classes. 

### discours/langue

**discours/langue** – La langue est un ensemble virtuel qui ne peut être appréhendé que dans son actualisation orale ou écrite; "discours" est un terme commode qui recouvre les deux domaines de cette actualisation. 

### distance du chi-2

**distance du chi-2** – distance entre profils* de fréquence utilisée en analyse des correspondances* et dans certains algorithmes* de classification*. 

### éditions de contextes

**éditions de contextes** – (sa) éditions de type concordanciel dans lesquelles les occurrences d'une forme sont accompagnées d'un fragment de contexte pouvant contenir plusieurs lignes de texte autour de la forme-pôle. La longueur de ce contexte est définie en nombre d'occurrences avant et après chaque occurrence de la forme-pôle. 

### éléments d'un segment

**éléments d'un segment** – (sr) chacune des formes correspondant aux occurrences qui entrent dans sa composition. ex : A, B, C sont respectivement les premier, deuxième et troisième éléments du segment ABC. 

### éléments actifs

**éléments actifs** – (ac ou acm) ensemble des éléments servant de base au calcul des axes factoriels, des valeurs propres relatives à ces axes et des coordonnées factorielles. 

### éléments supplémentaires (ou illustratifs)

**éléments supplémentaires (ou illustratifs)** – (ac ou acm) ensemble des éléments ne participant pas aux calculs des axes factoriels, pour lesquels on calcule des coordonnées factorielles qui auraient été affectées à une forme ayant la même répartition dans le corpus mais participant à l'analyse avec un poids négligeable. 

### énoncé/énonciation

**énoncé/énonciation** – (ling) à l'intérieur du texte un ensemble de traces qui manifestent l'acte par lequel un auteur a produit ce texte.

### facteur

**facteur** – (ac ou acm) variables artificielles construites par les techniques d'analyse factorielle permettant de résumer (de décrire brièvement) les variables actives initiales. 

### forme

**forme** – (sa) ou "forme graphique" archétype correspondant aux occurrences* identiques dans un corpus de textes, c'est-à-dire aux occurrences composées strictement des mêmes caractères non-délimiteurs d'occurrence. 

### forme banale

**forme banale** – (sp) pour une partie du corpus donnée, forme ne présentant aucune spécificité (ni positive ni négative) dans cette partie . 

### forme caractéristique

**forme caractéristique** – (d'une partie) synonyme de spécificité positive*. forme commune - forme attestée dans chacune des parties du corpus. 

### forme originale

forme originale – (pour une partie du corpus) forme trouvant toutes ses occurrences dans cette seule partie. 

### fréquence

**fréquence** – (sa) (d'une unité textuelle) le nombre de ses occurrences dans le corpus. fréquence d'un segment (sr) - (ou d'une polyforme) le nombre des occurrences de ce segment, dans l'ensemble du corpus. 

### fréquence maximale

**fréquence maximale** – (sa) fréquence de la forme la plus fréquente du corpus (en français, le plus souvent, la préposition "de"). 

### fréquence relative

**fréquence relative** – (sa) la fréquence d'une unité textuelle dans le corpus ou dans l'une de ses parties, rapportée à la taille du corpus (resp. de cette partie). 

### gamme des fréquences

**gamme des fréquences** – (sa) suite notée Vk, des effectifs correspondant aux formes de fréquence k, lorsque k varie de 1 à la fréquence maximale. 

### hapax

**hapax** – gr. hapax (legomenon), "chose dite une seule fois". 
– (sa) forme dont la fréquence est égale à un dans le corpus (hapax du corpus) ou dans une de ses parties (hapax de la partie). 

### identification

**identification** – (stat, ling, sa) reconnaissance d'un seul et même élément à travers ses multiples emplois dans des contextes et dans des situations différentes. 

### index

**index** – (sa) liste imprimée constituée à partir d'une réorganisation des formes et des occurrences d'un texte, ayant pour base la forme graphique et permettant de regrouper les références* relatives à l'ensemble des occurrences d'une même forme. 

### index alphabétique

**index alphabétique** – (sa) index* dans lequel les formes-pôles* sont classées selon l'ordre lexicographique* (celui des dictionnaires). 

### index hiérarchique

**index hiérarchique** – (sa) index* dans lequel les formes-pôles* sont classées selon l'ordre lexicométrique*. 

### index par parties

index par parties – ensemble d'index (hiérarchiques ou alphabétiques) réalisés séparément pour chaque partie d'un corpus. 

### lemmatisation

**lemmatisation** – regroupement sous une forme canonique (en général à partir d'un dictionnaire) des occurrences du texte. En français, ce regroupement se pratique en général de la manière suivante : 

- les formes verbales à l'infinitif,
- les substantifs au singulier,
- les adjectifs au masculin singulier,
- les formes élidées à la forme sans élision.

### lexical

**lexical** – (ling) qui concerne le lexique* ou le vocabulaire*. 

– lexicométrie ensemble de méthodes permettant d'opérer des réorganisations formelles de la séquence textuelle et des analyses statistiques portant sur le vocabulaire* d'un corpus de textes. 

### lexique

**lexique** – (ling) ensemble virtuel des mots d'une langue. 

### longueur

**longueur** – (sa) (d'un corpus, d'une partie de ce corpus, d'un fragment de texte, d'une tranche, d'un segment, etc.) le nombre des occurrences contenues dans ce corpus (resp. : partie, fragment, etc.). Synonyme : taille. 

On note : T la longueur du corpus ; t j celle de la partie (ou tranche) numéro j du corpus. 

### longueur d'un segment

**longueur d'un segment** – (sr) le nombre des occurrences entrant dans la composition de ce segment. 

### occurrence

**occurrence** – (sa) suite de caractères non-délimiteurs bornée à ses extrémités par deux caractères délimiteurs* de forme. 

### ordre lexicographique

**ordre lexicographique** – 

- pour les formes graphiques : l'ordre selon lequel les formes sont classées dans un dictionnaire. 
  NB : Les lettres comportant des signes diacrisés sont classées au même niveau que les mêmes caractères non diacrisés, le signe diacritique n'intervenant que dans les cas d'homographie complète. Dans les dictionnaires, on trouve par exemple rangées dans cet ordre les formes : mais, maïs, maison, maître . 

- pour les polyformes : ordre résultant d'un tri des polyformes par ordre lexicographique sur la première composante. Les polyformes commençant par une même forme graphique sont départagées par un tri lexicographique sur la seconde, etc. 

### ordre lexicométrique

**ordre lexicométrique** – (sa)

- pour les formes graphiques : ordre résultant d'un tri des formes du corpus par ordre de fréquences décroissantes ; les formes de même fréquence sont classées par ordre lexicographique. 
- pour les polyformes : ordre résultant d'un tri par ordre de longueur décroissante des segments, les segments de même longueur sont départagés par leur fréquence, les segments ayant même longueur et même fréquence par l'ordre lexicographique. 

### paradigme

**paradigme** – (ling) ensemble des termes qui peuvent figurer en un point de la chaîne parlée. paradigmatique 

- (sa) qui concerne le regroupement en série des unités textuelles, indépendamment de leur ordre de succession dans la chaîne écrite. 

### partie

**partie** – (d'un corpus de textes) fragment de texte correspondant aux divisions naturelles de ce corpus ou à un regroupement de ces dernières. 

### partition

**partition** – (d'un corpus de textes) division d'un corpus en parties constituées par des fragments de texte consécutifs, n'ayant pas d'intersection commune et dont la réunion est égale au corpus. 

(d'un ensemble, d'un échantillon) division d'un ensemble d'individus ou d'observations en classes disjointes dont la réunion est égale à l'ensemble tout entier. 

### partition longitudinale

**partition longitudinale** – (sa) partition d'un corpus en fonction d'une variable qui définit un ordre sur l'ensemble des parties.

### périodisation

**périodisation** – (sa) regroupement des parties naturelles du corpus respectant l'ordre chronologique d'écriture, d'édition ou de parution des textes réunis dans le corpus. 

### phrase

phrase** – (sa) fragment de texte compris entre deux séparateurs* de phrase. 

### polyforme

**polyforme** – (sr) archétype des occurrences d'un segment; suite de formes non séparées par un séparateur de séquence, qui n'est pas obligatoirement attestée dans le corpus. 

### ponctuation

**ponctuation** – Système de signes servant à indiquer les divisions d'un texte et à noter certains rapports syntaxiques et/ou conditions d'énonciation. 

– (sa) caractère (ou suite de caractères) correspondant à un signe de ponctuation.
 pourcentages d'inertie 
– (ac ou acm) quantités proportionnelles aux valeurs propres* dont la somme est égale à 100. Notées ta. 

### profil

**profil** – (stat et ac) (d'une ligne ou d'une colonne d'un tableau à double entrée) vecteur constitué par le rapport des effectifs contenus sur cette ligne (resp. colonne) à la somme des effectifs que contient la ligne (resp. la colonne). 

### répartition

**répartition** – (sa) (des occurrences d'une forme dans les parties du corpus) nombre des parties du corpus dans lesquelles cette forme est attestée. 

### section

**section** – (sr) portion de texte comprise entre deux délimiteurs de section (exemple : le paragraphe, etc.). 

### segment

**segment** – (sr) toute suite d'occurrences consécutives dans le corpus et non séparées par un séparateur* de séquence est un segment du texte. 

### segment répété

**segment répété** – (sr) (ou polyforme répétée) suite de forme dont la fréquence est supérieure ou égale à 2 dans le corpus. 

### segmentaire

**segmentaire** – (sr) ensemble des termes* attestés dans le corpus. 

### segmentation

segmentation – opération qui consiste à délimiter des unités minimales* dans un texte. 

### segmentation automatique

**segmentation automatique** – ensemble d'opérations réalisées au moyen de procédures informatisées qui aboutissent à découper, selon des règles prédéfinies, un texte stocké sur un support lisible par un ordinateur en unités distinctes que l'on appelle des unités minimales*. 

### séparateurs de phrases

**séparateurs de phrases** – (sa) sous-ensemble des caractères délimiteurs* de séquence* correspondant aux seules ponctuations fortes (en général : le point, le point d'interrogation, le point d'exclamation). 

### séquence

**séquence** – (sa) suite d'occurrences du texte non séparées par un délimiteur* de séquence. 

### seuil

**seuil** – (stat) quantité arbitrairement fixée au début d'une expérience visant à sélectionner parmi un grand nombre de résultats, ceux pour lesquels les valeurs d'un indice numérique dépassent ce seuil (de fréquence, en probabilité, etc.). 

### sous-fréquence

**sous-fréquence** – (sa) (d'une unité textuelle dans une partie, tranche, etc.) nombre des occurrences de cette unité dans la seule partie (resp. tranche, etc.) du corpus. 

### sous-segments

**sous-segments** – (sr) pour un segment donné, tous les segments de longueur inférieure et compris dans ce segment sont des sous-segments. ex : AB et BC sont deux sous-segments du segment ABC. 

### spécificité chronologique

**spécificité chronologique** – (sp) spécificité* portant sur un groupe connexe de parties d'un corpus muni d'une partition longitudinale*. 

### spécificité positive

**spécificité positive** – (sp) pour un seuil de spécificité fixé, une forme i et une partie j données, la forme i est dite spécifique positive de la partie j (ou forme caractéristique* de cette partie) si sa sous-fréquence est "anormalement élevée" dans cette partie. De façon plus précise, si la somme des probabilités calculées à partir du modèle hypergéométrique pour les valeurs égales ou supérieures à la sous-fréquence constatée est inférieure au seuil fixé au départ. 

### spécificité négative

**spécificité négative** – (sp) pour un seuil de spécificité fixé, une forme i et une partie j données, la forme i est dite spécifique négative de la partie j si sa sous-fréquence est anormalement faible dans cette partie. De façon plus précise, si la somme des probabilités calculées à partir du modèle hypergéométrique pour les valeurs égales ou inférieures à la sous-fréquence constatée est inférieure au seuil fixé au départ. 

### stock distributionnel du vocabulaire

**stock distributionnel du vocabulaire** – (d'un fragment de texte) le vocabulaire* de ce fragment assorti de comptages de fréquence pour chacune des formes entrant dans sa composition. 

### syntagmatique

**syntagmatique** – (sa) qui concerne le regroupement des unités textuelles, selon leur ordre de succession dans la chaîne écrite. 
– (ling) groupe de mots en séquence formant une unité à l'intérieur de la phrase. 

### tableau de contingence (stat)

**tableau de contingence (stat)** – synonyme de tableau de fréquences ou de tableau croisé: tableau dont les lignes et les colonnes représentent respectivement les modalités de deux questions (ou deux variables nominales) , et dont le terme général représente le nombre d'individus correspondant à chaque couple de modalités. 

### tableau lexical entier (TLE)

**tableau lexical entier (TLE)** – tableau à double entrée dont les lignes sont constituées par les ventilations* des différentes formes dans les parties du corpus. Le terme générique k(i,j) du TLE est égal au nombre de fois que la forme i est attestée dans la partie j du corpus. Les lignes du TLE sont triées selon l'ordre lexicométrique* des formes correspondantes. 

### tableau des segments répétés (TSR)

**tableau des segments répétés (TSR)** – tableau à double entrée dont les lignes sont constituées par les ventilations* des segments répétés dans les parties du corpus. Les lignes du TSR sont triées selon l'ordre lexicométrique* des segments. (i.e. longueur décroissante, fréquence décroissante, ordre lexicographique). 

### tableau lexical

**tableau lexical** – tableau à double entrée résultant du TLE par suppression de certaines lignes (par exemple celles qui correspondent à des formes dont la fréquence est inférieure à un seuil donné). 

### taille

**taille** – (sa) (d'un corpus) sa longueur* mesurée en occurrences (de formes simples). 

### terme

**terme** – (sr) nom générique s'appliquant à la fois aux formes* et aux polyformes*. Dans le premier cas on parlera de termes de longueur 1. Les polyformes sont des termes de longueur 2,3, etc. 

### termes contraints / termes libres

**termes contraints / termes libres** – Un terme S1 est contraint dans un autre terme S2 de longueur supérieure si toutes ses occurrences* sont des sous-segments* de segments correspondant à des occurrences du segment S2. Si au contraire un terme possède plusieurs expansions distinctes, qui ne sont pas forcément récurrentes, c'est un terme libre. 

### types généralisés (Tgens)

**types généralisés (Tgens)** – unités de dépouillement définies par l'utilisateur à l'aide d'outils permettant d'effectuer automatiquement des regroupements d'occurrences du texte (ex : les occurrences des formes qui commencent par la séquence de caractère patr : patrie, patriotes, patriotisme, etc.). 

### unités minimales (pour un type de segmentation)

**unités minimales (pour un type de segmentation)** – unités que l’on ne décompose pas en unités plus petites pouvant entrer dans leur composition (ex : dans la segmentation en formes graphiques les formes ne sont pas décomposées en fonction des caractères qui les composent) 

### valeur modale

**valeur modale** – (stat) valeur pour laquelle une distribution atteint son maximum. 

### valeurs propres

**valeurs propres** – (ac ou acm) quantités permettant de juger de l'importance des facteurs successifs de la décomposition factorielle. La valeur propre notée la. mesure la dispersion des éléments sur l' axe.a.

### valeurs-tests

**valeurs-tests** – (ac ou acm) quantités permettant d'apprécier la signification de la position d'un élément supplémentaire* (ou illustratif) sur une axe factoriel. Brièvement, si une valeur test dépasse 2 en valeur absolue, il y a 95 chances sur 100 que la position de l'élément correspondant ne puisse être due au hasard. 

### variables actives

**variables actives** – variables utilisées pour dresser une typologie, soit par analyse factorielle, soit par classification. Les typologies dépendent du choix et des poids des variables actives, qui doivent de ce fait constituer un ensemble homogène. 

### variables supplémentaires (ou illustratives)

**variables supplémentaires (ou illustratives)** – variables utilisées a posteriori pour illustrer des plans factoriels ou des classes. Une variable supplémentaire peut-être considérée comme une variable active munie d'un poids nul. 

### variables de type T

**variables de type T** – variable dont la fréquence est à peu près proportionnelle à l'allongement du texte. (ex : la fréquence maximale)
 variables de type V- variable dont l'accroissement a tendance à diminuer avec l'allongement du texte (ex : le nombre des formes, le nombre des hapax). 

### ventilation

**ventilation** – (sa) (des occurrences d'une unité dans les parties du corpus) La suite des n nombres (n = nombre de parties du corpus) constituée par la succession des sous-fréquences* de cette unité dans chacune des parties, prises dans l'ordre des parties.
 vocabulaire (sa) - ensemble des formes* attestées dans un corpus de textes. 

### vocabulaire commun

**vocabulaire commun** – (sa) l'ensemble des formes attestées dans chacune des parties du corpus. 

### vocabulaire de base

**vocabulaire de base** – (sp) ensemble des formes du corpus ne présentant, pour un seuil fixé, aucune spécificité (négative ou positive) dans aucune des parties , (i.e. l'ensemble des formes qui sont "banales" pour chacune des parties du corpus).
 vocabulaire original- (sa) (pour une partie du corpus) l'ensemble des formes* originales* pour cette partie. 

### voisinage d'une occurrence

**voisinage d'une occurrence** – (sa) pour une occurrence donnée du texte, tout segment (suite d'occurrences consécutives, non séparées par un délimiteur de séquence) contenant cette occurrence. 