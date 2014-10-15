---
filename: trRESTXQ
date: 2014-02-18
version: 0.1
---

Traduction article RESTXQ (documentation BaseX)
=============

[source](http://docs.basex.org/wiki/RESTXQ)

Cette page présente un des services d'application web. Elle décrit comment utiliser l'API RESTXQ de BaseX.

RESTXQ, introduit par [Adam Retter][1], est une nouvelle API qui facilite l'utilisation de XQuery comme un langage de traitement côté serveur pour le web. RESTXQ s'inspire de l'[API JAX-RS](http://en.wikipedia.org/wiki/Java_API_for_RESTful_Web_Services) pour Java : elle définit un ensemble prédéfini d'annotations XQuerry 3.0 qui alignent les requêtes HTTP à des fonctions XQuery, qui à leur tour génèrent et retournent des réponses HTTP.

Notez que certaines extensions présentées dans cette documentation sont spécifiques à BaseX ; il est possible qu'elles soient intégrées dans des versions futures du brouillon de RESTXQ.

Depuis la Version 7.7, les fonctionnalités suivantes ont été ajoutées :

- Les fonctions RESTQX peuvent aussi être spécifiées dans des modules principaux (extension : .xq)
- les types `multipart` sont maintenant supportés, y compris `multipart/form-data`
- une nouvelle annotation `%rest:error` peut être employée pour obtenir les erreurs XQuery
- les erreurs du servlet peuvent être redirigées vers d'autres pages RESTXQ
- un Module RESTXQ fournit des fonctions d'aide
- les paramètres son implicitement convertis dans le type de l'argument de la fonction
- le préfixe d'espace de nom RESTXQ a été modifié pour `rest`
- par défaut, RESTXQ est maintenant disponible au niveau supérieur via [http://localhost:8984/](http://localhost:8984/)

-------------

Utilisation
-------

Le service RESTXQ est accessible via [http://localhost:8984/](http://localhost:8984/), et le serveur HTTP est démarré avec les crédits d'administration ([voir ici](http://docs.basex.org/wiki/Web_Application#User_Management)).

Toutes les [annotations](http://docs.basex.org/wiki/XQuery_3.0#Annotations) RESTXQ sont assignées à l'espace de nom `http://exquery.org/ns/restxq`, qui est statiquement lié au préfixe `rest`. Une _fonction ressource_ est une fonction XQuery qui a été marquée par des annotations RESTXQ. Lorsqu'une requête HTTP arrive, une fonction ressource sera invoquée en correspondant aux contraintes indiquées par ses annotations.

Lorsqu'une URL RESTXQ est requétée, le répertoire du module [RESTXQPATH](http://docs.basex.org/wiki/Options#RESTXQPATH) et ses sous-répertoires seront parcourus pour des fonctions disposant d'annotations RESTXQ dans les modules de bibliothèque (détectés par l'extension `xqm`) et les modules principaux (détectés par `.xq`). Dans les expressions principales, le module principal ne sera jamais évalué. Tous les modules seront mis en cache et parcouru une nouvelle fois quand leur timestamp change.

Un module RESTXQ simple est présenté ci-dessous. Il fait partie d'une installation propre et est disponible à [http://localhost:8984/](http://localhost:8984/).

```xquery
    (: simplified version of the function found in webapp/restxq.xqm :)
    module namespace page = 'http://basex.org/examples/web-page';

    declare %rest:path("hello/{$world}")
        %rest:GET
        %rest:header-param("User-Agent", "{$agent}")
        function page:hello($world as xs:string, $agent as xs:string*) {
    <response>
        <title>Hello { $world }!</title>
        <info>You requested this page with { $agent }.</info>
    </response>
    };
```

Si l'URI [http://localhost:8984/hello/World](http://localhost:8984/hello/World) est accédée, le résultat sera similaire à :

```xml
    <response>
        <title>Hello World!</title>
        <time>The current time is: 18:42:02.306+02:00</time>
    </response>
```

Le module RESTXQ contient également une autre fonction :


```xquery
    declare
        %rest:path("/form")
        %rest:POST
        %rest:form-param("message","{$message}", "(no message)")
        %rest:header-param("User-Agent", "{$agent}")
        function page:hello-postman(
            $message as xs:string,
            $agent   as xs:string*)
            as element(response)
    {
    <response type='form'>
        <message>{ $message }</message>
        <user-agent>{ $agent }</user-agent>
    </response>
    };
```

Si vous postez quelque chose (par exemple en utilisant curl ou un formulaire embarqué dans [http://localhost:8984/](http://localhost:8984/)...

```bash
    curl -i -X POST --data "message='CONTENT'" http://localhost:8984/form

```

... le résultat suivant sera reçu :

```
    HTTP/1.1 200 OK
    Content-Type: application/xml; charset=UTF-8
    Content-Length: 107
    Server: Jetty(8.1.11.v20130520)
```
```xml
    <response type="form">
        <message>'CONTENT'</message>
        <user-agent>curl/7.31.0</user-agent>
    </response>
```

Requêtes
---------

Cette section montre comment les annotations peuvent être employés pour manipuler et traiter des requêtes HTTP.

### Contraintes (_constraints_)

Les contraintes restreignent les requêtes HTTP qu'une fonction ressource peut traiter.

#### Chemins (_paths_)

Une fonction ressource doit avoir une seule _annotation de chemin_ qui prend une seule chaîne comme argument. La fonction sera appelée si une URL correspond aux segments de chemin et au motif de l'argument. Les _motifs de chemin_ (path templates) contiennent des variables entre accolades, et alignent les segments correspondants du chemin de la requête aux arcguments de la fonction ressource.

L'exemple suivant contient une annotation de chemin avec trois segments et deux motifs. Un des arguments de la fonction est plus loin spécifié avec un type de données qui signifie que la valeur pour `$variable` sera convertie en `xs:integer` avant d'être liée :

```xquery
    declare %rest:path("/a/path/{$with}/some/{$variable}")
  function page:test($with, $variable as xs:integer) { ... };
```

#### Négociation de contenu (_content negociation_)

Les deux annotations suivantes peuvent être employées pour restriendre des fonctions à des types de contenus particuliers :

- **HTTP Content Types** : une fonction sera seulement invoquée si l'en-tête HTTP `Content-Type` de la requête correspond à l'un des types mime renseigné. Par exemple :

```xquery
    %rest:consumes("application/xml", "text/xml")
```

- ** HTTP Accept** : une fonctin sera seulement invoquée si l'en-tête HTTP `Accept` de la requête correspond à l'un des types mime définis. Par exemple :

```xquery
    %rest:produces("application/atom+xml")
```

Par défaut, les deux types mime sont `*/*`. Notez que cette annotation n'affectera pas le type de contenu (_content-type_) de la réponse HTTP. Pour cela, vous devrez ajouter une annotation [`%output:media-type`](http://docs.basex.org/wiki/RESTXQ#Output).

#### Méthodes HTTP (_HTTP Methods_)

Les annotations de méthodes HTTP équivalent à toutes les [méthodes de requête HTTP](http://en.wikipedia.org/wiki/HTTP#Request_methods) hormis TRACE et CONNECT. Zéro ou plusieurs méthodes peuvent être employées pour une fonction ; si aucune n'est sépcifiée, la fonction sera invoquée pour chaque méthode.

La fonction suivante sera ppellée si les méthodes de requêtes GET ou POST sont employées :

```xquery
    declare %rest:GET %rest:POST %rest:path("/post")
  function page:post() { "This was a GET or POST request" };
```

Les annotations POST et PUT peuvent optionnellement prendre un litéral chaîne de caractères pour faire correspondre le corps de la requête HTTP à un [argument de la fonction](http://docs.basex.org/wiki/RESTXQ#Parameters). Encore une fois, la variable cible doit être comprise entre accolades :

```xquery
    declare %rest:PUT("{$body}") %rest:path("/put")
  function page:put($body) { "Request body: " || $body };
```

Si un type de contenu (_content-type_) est spécifié dans la requête, le contenu est converti dans le type XQuery suivant :

Content-Type | XQuery type
`application/json`, `application/jsonml+json` | `document-node()` (conversion décrite dans le [module JSON](http://docs.basex.org/wiki/JSON_Module))
`text/html`| `document-node()` (conversion décrite dans le [module HTMl](http://docs.basex.org/wiki/HTML_Module))
`text/comma-separated-values` | `document-node()``
`text/xml`, `application/xml` | `document-node()``
`text/*` | `xs:string``
_autres_ | `xs:base64Binary
`multipart/*` | sequence (voir le paragraphe suivant)

#### Types Multipart

Un début de support pour les types de contenu (_content-type_) `multipart` a été ajouté. Les parties d'un message multipart sont représentées comme une séquence, et chaque partie est convertie en un item XQuery comme décrit dans le dernier paragraphe.

Une fonction qui est capable de manipuler des types multipart est identique à d'autres fonctions RESTXQ :

```xquery
    declare
        %rest:path("/multipart")
        %rest:POST("{$data}")
        %rest:consumes("multipart/mixed") (: optional :)
        function page:multipart($data as item()*)
        {
            "Number of items: " || count($data)
        };
```

Veuillez noter que le support des types multipart est encore expérimental, il pourrait changer dans une version future de BaseX. Vos retours sont bienvenus.


### Paramètres (_parameters_)

Les annotations suivantes peuvent être employées pour lier des valeurs de requête à des arguments de fonction. Les valeurs seront implicitement converties vers le type de l'argument.

#### Paramètres de requête (_query parameters_)

La valeur du _premier paramètre_, si elle est trouvée dans le [composant de requête](http://docs.basex.org/wiki/Request_Module#Conventions), sera assignée à la variable spécifiée comme _second paramètre_. Si aucune valeur n'est spécifiée dans la requête HTTP, tous les paramètres additionnels seront liés à la variable (si aucun paramètre additionnel n'est donné, une séquence vide sera liée) :

```xquery
    declare
        %rest:path("/params")
        %rest:query-param("id", "{$id}")
        %rest:query-param("add", "{$add}", 42, 43, 44)
        function page:params($value as xs:string?, $answer as xs:integer+)
        {
        <result id="{ $id }" sum="{ sum($add) }"/>
        };
 ```

#### Champs de formulaire HTML (_HTML form fields)

Les paramètres de formulaire sont spécifiés de la même manière que les [paramètres de requête](http://docs.basex.org/wiki/RESTXQ#Query_Parameters). Leurs valeurs sont extraites depuis les requêtes GET ou POST.

```xquery
    %rest:form-param("parameter", "{$value}", "default")
```

#### Chargement de fichiers (_file uploads_)

Des fichiers peuvent être chargés sur le serveur en utilisant le type de contenu `multipart/form-data` (l'attribut `multiple` de HTML5 permet le chargement de plusieurs fichiers).

```xml
    <form action="/upload" method="POST" enctype="multipart/form-data">
        <input type="file" name="files"  multiple="multiple"/>
        <input type="submit"/>
    </form>
```

Le contenu des fichiers est placé dans un [map](http://docs.basex.org/wiki/Map_Module), le nom du fichier servant de key. L'exemple suivant montre comment les fichiers chargés peuvent être stockés dans un répertoire temporaire :

```xml
    declare
    %rest:POST
    %rest:path("/upload")
    %rest:form-param("files", "{$files}")
    function page:upload($files)
 {
    for $name    in map:keys($files)
    let $content := $files($name)
    let $path    := file:temp-dir() || $name
    return (
        file:write-binary($path, $content),
        <file name="{ $name }" size="{ file:size($path) }"/>
    )
 };
```

#### En-têtes HTTP (_HTTP headers_)

Les paramètres d'en-tête sont spécifiés de la même manière que les [paramètres de requête](http://docs.basex.org/wiki/RESTXQ#Query_Parameters) :

```xquery
    %rest:form-param("parameter", "{$value}", "default")
```

#### Cookies

Les paramètres de cookies sont spécifiés de la même manière que les [paramètres de requête](http://docs.basex.org/wiki/RESTXQ#Query_Parameters) :

```xquery
    %rest:form-param("parameter", "{$value}", "default")
```

### Réponses (_responses_)

Par défaut, une requête réussie reçoit le code de statut HTTP `200` (OK) et est suivie du contenu correspondant. Une requête éronnée mène à un code d'erreur et un message d'erreur optionnel (par exemple `404` pour "resource not found").

#### Réponses personnalisées (_custom responses_)

Les réponses personnalisées peuvent être construites au sein de XQUery en retournant un élément `rest:response`, un nœeud fils `http:response` qui correspond à la syntaxe du [module Client HTTP de la spécification EXPath](http://expath.org/spec/http-client), et plusieurs nœuds fils optionnels qui seront serialisés comme habituellement. Une fonction qui réagit sur une ressource inconnue peut ressembler à ce qui suit :

```xquery
    declare %rest:path("") function page:error404() {
        <rest:response>
            <http:response status="404" message="I was not found.">
                <http:header name="Content-Language" value="en"/>
                <http:header name="Content-Type" value="text/html; charset=utf-8"/>
            </http:response>
        </rest:response>
    };
```

#### Redirections et Retours en arrière (_forwards and redirects_)

// Reprendre la traduction //


------------
[1][http://www.adamretter.org.uk]

