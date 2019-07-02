# Travailler des fichiers JSON avec XSLT

Les versions 3.0 de XSLT et de XQuery ainsi que la version 3.1 de XPath standardisées par le W3C en 2017 permettent toutes les deux de manipuler des données au format JSON.

Que les jeux données soient mises à disposition dans les formats XML, JSON ou JSON-LD, il est dès lors maintenant possible de travailler avec ces données mises à disposition par des services web dans ce format en utilisant ces langages.

L’utilisation des langages XQuery, XSLT et XPath présentent notamment l’avantage de permettre l’intégration aisée de données mises à disposition dans ces différents formats. De plus, les extensions de ExPATH permettent de requêter directement des webservices par l’intermédiaires de leur interface programmables (API).

## Quelques précisions sur les formats

JSON est un format principalement axé sur les données structurées. 

Si son utilisation permet souvent de remplacer XML de manière efficace dans certaines applications, ce format est moins adapté pour prendre en charge des documents structurés. La capacité du métalangage XML à prendre en charge des contenus mixte en fait un format plus appropriés pour le texte.

Les outils disponibles pour manipuler des fichiers structurés XML sont plus matures que ceux actuellement disponibles pour JSON. C’est notamment le cas des langages de schémas et de l’expressivité du langage XPath ou du caractère fonctionnel des langages XSLT et XQuery.

### JSON

json.org

Le format JavaScript Object Notation JSON, a été proposé en 2001 par Douglas Crockford.

Il est aujourd’hui spécifié par le standard ECMA-404, The JSON Data Interchange Syntax

Dans ce format, les données sont représentées avec les structurées de données bien connues du langage JavaScript, ce qui explique son grand succès : Object {...}, Array [...], chaînes de caractères ”...“, entier et décimal (number), ou encore booléen et valeur nulle.

Assignement : l’attribution des données a lieu sous la forme de paires clé-valeur qui peuvent être imbriquées.

JSON Schema permet la modélisation et la validation de fichier JSON. Mais cette spécification n’est pas encore standardisée. cf. json-schema.org

@todo fournir un exemple annoté signalant un objet, l’utilisation d’un array et d’une chaîne de caractères.

## Références

https://speakerdeck.com/xmlarbyter/verarbeitung-von-json-daten-mit-aktuellen-xslt-techniken

