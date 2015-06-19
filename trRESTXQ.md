---
filename: trRESTXQ
date: 2014-02-18
version: 0.1
---

# Traduction de l’article RESTXQ (documentation BaseX)

[source](http://docs.basex.org/wiki/RESTXQ)

Cette page présente un des services d’application web [de BaseX]. Elle décrit comment utiliser l’API RESTXQ de BaseX.

Introduit par [Adam Retter][1], RESTXQ est une nouvelle API qui facilite l’utilisation de XQuery comme un langage de traitement côté serveur pour le web. RESTXQ s’inspire de l’[API JAX-RS](http://en.wikipedia.org/wiki/Java_API_for_RESTful_Web_Services) pour Java : elle définit un ensemble prédéfini d’annotations XQuerry 3.0 qui font correspondre les requêtes HTTP à des fonctions XQuery, qui à leur tour génèrent et retournent des réponses HTTP.

Notez que BaseX fournit plusieurs extensions au brouillon officiel de la spécification :

- les types `multipart` sont supportés, y compris `multipart/form-data`
- une annotation `%rest:error` peut être employée pour obtenir les erreurs XQuery
- les erreurs du Servlet peuvent être redirigées vers d’autres pages RESTXQ
- un Module RESTXQ fournit des fonctions d’aide
- les paramètres sont implicitement convertis dans le type de l’argument de la fonction
- l’annotation de chemin peut contenir des expressions régulières
- les facteurs de qualité du Accept header sont évalués
- support de l’annotation `%input` pour les paramètres de type de contenu spécifiques aux input

-------------

## Préliminaires

Le service RESTXQ est accessible via [http://localhost:8984/](http://localhost:8984/).

Toutes les [annotations](http://docs.basex.org/wiki/XQuery_3.0#Annotations) RESTXQ sont assignées à l’espace de nom `http://exquery.org/ns/restxq` qui est statiquement lié au préfixe `rest`. Une _fonction ressource_ est une fonction XQuery qui a été marquée avec des annotations RESTXQ. Lorsqu’une requête HTTP arrive, une fonction ressource correspondant aux contraintes indiquées par ses annotations sera invoquée.

Lorsqu’une URL RESTXQ est requêtée, le répertoire du module [RESTXQPATH](http://docs.basex.org/wiki/Options#RESTXQPATH) et ses sous-répertoires seront parcourus à la recherche de fonctions disposant d’annotations RESTXQ dans les modules de bibliothèque (détectés par l’extension `xqm`) et les modules principaux (détectés par `.xq`). Dans les expressions principales, le module principal ne sera jamais évalué. Tous les modules seront mis en cache et parcouru une nouvelle fois quand leur timestamp change.

La version 8.3 rendra disponible les fonctionnalités suivantes :
- Cache des modules en réglant CACHERESTXQ à vrai. Cette option est particulièrement utile en environnement de production avec lourde charge.
- Le chemin static de la racine `/.init` peut être appelé pour invalider le cache du module RESTXQ.
- Un sous-répertoire sera ignoré s’il contient un fichier nommé `.ignore`.


## Exemples

Voici une première fonction RESXQ :

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

Si on accède à l’URI  [http://localhost:8984/hello/World](http://localhost:8984/hello/World) on obtient :

```xml
    <response>
        <title>Hello World!</title>
        <time>The current time is: 18:42:02.306+02:00</time>
    </response>
```

La fonction suivante est une démonstration d’une requête POST :

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

… vous recevrez le résultat suivant :

```txt
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


## Requêtes

Cette section montre comment les annotations peuvent être employées pour manipuler et traiter des requêtes HTTP.

### Contraintes (_constraints_)

Les contraintes restreignent les requêtes HTTP qu’une fonction ressource peut traiter.

#### Chemins (_paths_)

Une fonction ressource doit avoir une seule _annotation de chemin_ qui prend une seule chaîne comme argument. La fonction sera appelée si une URL correspond aux segments de chemin et au motif de l’argument. Les _motifs de chemin_ (path templates) contiennent des variables entre accolades, et alignent les segments correspondants du chemin de la requête aux arguments de la fonction ressource.

L’exemple suivant contient une annotation de chemin avec trois segments et deux motifs. Un des arguments de la fonction est plus loin spécifié avec un type de données qui signifie que la valeur pour `$variable` sera convertie en `xs:integer` avant d’être liée :

```xquery
    declare %rest:path("/a/path/{$with}/some/{$variable}")
  function page:test($with, $variable as xs:integer) { ... };
```

#### Négociation de contenu (_content negociation_)

Les deux annotations suivantes peuvent être employées pour restreindre des fonctions à des types de contenus particuliers :

- **HTTP Content Types** : une fonction sera seulement invoquée si l’en-tête HTTP `Content-Type` de la requête correspond à l’un des types Mime renseigné. Par exemple :

```xquery
    %rest:consumes("application/xml", "text/xml")
```

- ** HTTP Accept** : une fonction sera seulement invoquée si l’en-tête HTTP `Accept` de la requête correspond à l’un des types mime définis. Par exemple :

```xquery
    %rest:produces("application/atom+xml")
```

Par défaut, les deux types mime sont `*/*`. Notez que cette annotation n’affectera pas le type de contenu (_content-type_) de la réponse HTTP. Pour cela, vous devrez ajouter une annotation [`%output:media-type`](http://docs.basex.org/wiki/RESTXQ#Output).

#### Méthodes HTTP (_HTTP Methods_)

Les annotations de méthodes HTTP équivalent à toutes les [méthodes de requête HTTP](http://en.wikipedia.org/wiki/HTTP#Request_methods) hormis TRACE et CONNECT. Zéro ou plusieurs méthodes peuvent être employées pour une fonction ; si aucune n’est spécifiée, la fonction sera invoquée pour chaque méthode.

La fonction suivante sera appelée si les méthodes de requêtes GET ou POST sont employées :

```xquery
    declare %rest:GET %rest:POST %rest:path("/post")
  function page:post() { "This was a GET or POST request" };
```

Les annotations POST et PUT peuvent optionnellement prendre un littéral chaîne de caractères pour faire correspondre le corps de la requête HTTP à un [argument de la fonction](http://docs.basex.org/wiki/RESTXQ#Parameters). Encore une fois, la variable cible doit être comprise entre accolades :

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

Un début de support pour les types de contenu (_content-type_) `multipart` a été ajouté. Les parties d’un message multipart sont représentées comme une séquence, et chaque partie est convertie en un item XQuery comme décrit dans le dernier paragraphe.

Une fonction qui est capable de manipuler des types multipart est identique à d’autres fonctions RESTXQ :

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

Les annotations suivantes peuvent être employées pour lier des valeurs de requête à des arguments de fonction. Les valeurs seront implicitement converties vers le type de l’argument.

#### Paramètres de requête (_query parameters_)

La valeur du _premier paramètre_, si elle est trouvée dans le [composant de requête](http://docs.basex.org/wiki/Request_Module#Conventions), sera assignée à la variable spécifiée comme _second paramètre_. Si aucune valeur n’est spécifiée dans la requête HTTP, tous les paramètres additionnels seront liés à la variable (si aucun paramètre additionnel n’est donné, une séquence vide sera liée) :

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

Des fichiers peuvent être chargés sur le serveur en utilisant le type de contenu `multipart/form-data` (l’attribut `multiple` de HTML5 permet le chargement de plusieurs fichiers).

```xml
    <form action="/upload" method="POST" enctype="multipart/form-data">
        <input type="file" name="files"  multiple="multiple"/>
        <input type="submit"/>
    </form>
```

Le contenu des fichiers est placé dans un [map](http://docs.basex.org/wiki/Map_Module), le nom du fichier servant de key. L’exemple suivant montre comment les fichiers chargés peuvent être stockés dans un répertoire temporaire :

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

Les paramètres d’en-tête sont spécifiés de la même manière que les [paramètres de requête](http://docs.basex.org/wiki/RESTXQ#Query_Parameters) :

```xquery
    %rest:form-param("parameter", "{$value}", "default")
```

#### Cookies

Les paramètres de cookies sont spécifiés de la même manière que les [paramètres de requête](http://docs.basex.org/wiki/RESTXQ#Query_Parameters) :

```xquery
    %rest:form-param("parameter", "{$value}", "default")
```

### Réponses (_responses_)

Par défaut, une requête réussie reçoit le code de statut HTTP `200` (OK) et est suivie du contenu correspondant. Une requête erronée mène à un code d’erreur et un message d’erreur optionnel (par exemple `404` pour "resource not found").

#### Réponses personnalisées (_custom responses_)

Les réponses personnalisées peuvent être construites au sein de XQUery en retournant un élément `rest:response`, un nœeud fils `http:response` qui correspond à la syntaxe du [module Client HTTP de la spécification EXPath](http://expath.org/spec/http-client), et plusieurs nœuds fils optionnels qui seront sérialisés comme habituellement. Une fonction qui réagit sur une ressource inconnue peut ressembler à ce qui suit :

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

Les deux éléments XML `rest:forward` et `rest:redirect` peuvent être employés dans le contexte d’applications web, plus précisément dans le contexte de RESTXQ. Ces nœuds autorisent par exemple des multiples requêtes de mise à jour XQuery dans une rangée en redirigeant vers le chemin RESTXQ des fonctions RESTXQ. Les deux englobent une URL avec un chemin RESTXQ. L’URL englobée doit être correctement encodée via `fn:encode-for-uri()`.

Notez que, pour le moment, ces éléments n’apartiennent pas à la spécification RESXQ.

##### rest:forward

Utilisation : englober la localisation comme suit

```xquery
  <rest:forward>{ $location }</rest:forward>
```

Cela résulte en une redirection côté-serveur qui peut réduire le traffic entre le client et le serveur. Une redirection de ce type ne changera pas l’URL visible par le client.

Par exemple :

```xquery
  <rest:forward>/hello/universe</rest:forward>
```

redirigera de façon interne vers http://localhost:8984/hello/universe

##### rest:redirect

La fonction `web:redirect` peut être employée pour créer un élément de réponse de redirection. Alternativement, les éléments suivants peuvent être envoyés :

```xquery
  <rest:redirect>{ $location }</rest:redirect>
```

Qui est une abréviation pour :
```xquery
  <rest:response>
    <http:response status="302">
      <http:header name="location" value="{ $location }"/>
    </http:response>
  </rest:response>
```

Le client décide s’il faut choisir de suivre cette redirection. Les navigateurs le feront habituellement par défaut, tandis que des outils comme [curl](http://curl.haxx.se/) ne le feront pas à moins que l’option `-L` soit spécifiée.

#### Sortie (_Output_)

Le type de contenu (_content type_) d’une réponse peut être influencé par l’utlisateur via des paramètres de sérialisation (_Serialization Parameters_). Les étapes sont décrites dans le chapitre REST. Avec RESTXQ, les paramètres de sérialisation peuvent être spécifiés dans le prologue de la requête, via des annotations, ou au sein de l’élément de réponse REST :

##### Prologue de requête (_Query Prolog_)

Dans les modules principaux, les paramètres de sérialisation peuvent être spécifiés dans le prologue de la requête. Ces paramètres seront ensuite appliqués à toutes les fonctions au sein d’un module. Dans l’exemple suivant, le type de contenu de la réponse est surchargé par le paramètre `media-type` :

```xquery
  declare option output:media-type 'text/plain';

  declare %rest:path("version1") function page:version1() {
'Keep it simple, stupid'
  };
```

##### Annotations

Les paramètres globaux de sérialisation peuvent être surchargés au moyen d’annotation `%output`. Les exemples suivnats sérialisent en JSON des nœuds XML, en utilisant le format [JsonML](http://docs.basex.org/wiki/JSON_Module) :

```xquery
  declare
    %rest:path("cities")
    %output:method("json")
    %output:json("format=jsonml")
    function page:cities()
  {
    element cities {
      db:open('factbook')//city/name
    }
  };
```

La fonction suivante génère les headers XHTMl avec le type de contenu `text/html` lorsqu’elle est appelée :

```xquery
  declare
    %rest:path("")
    %output:method("xhtml")
    %output:omit-xml-declaration("no")
    %output:doctype-public("-//W3C//DTD XHTML 1.0 Transitional//EN")  
    %output:doctype-system("http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd")
    function page:html()
    {
      <html xmlns="http://www.w3.org/1999/xhtml">
        <body>done</body>
      </html>
    };
```

##### Élément réponse (_Response Element_)

Les paramètres de sérialisation dans un élément de réponse REST peuvent aussi être spécifiés dans une requête. Les paramètres de sérialisation seront surchargés.

```xquery
  declare %rest:path("version3") function page:version3() {
    <rest:response>
      <output:serialization-parameters>
        <output:media-type value='text/plain'/>
      </output:serialization-parameters>
    </rest:response>,
    'Not that simple anymore'
  };
```

#### Gestion des erreurs (_Error Handling_)

##### Erreurs XQuery (_XQuery Errors_)

Les erreurs XQuery peuvnet être traitées à la volée via des annotations d’erreur. Les annotations d’erreur ont un ou plusieurs arguments qui représentent les erreurs qui doivent être captées. Les codes sont égaux aux noms des constructions try/catch de XQuery 3.0.

Priority | Syntax | Example
1 | `prefix:name Q{uri}name` | `err:FORG0001` `Q{http://www.w3.org/2005/xqt-errors}FORG0001`
2 | `prefix:*` `Q{uri}*` | `err:* Q{http://www.w3.org/2005/xqt-errors}*`
3 | `*:name` | `*:FORG0001`
4 | `*` | `*`

Tous les codes d’erreur qui sont spécifiés pour une fonction doivent être de la même priorité. Les règles suivantes s’appliquent quand on attrape les erreurs :
Les codes avec une priorité plus importante peuvent être préférés.
Une erreur RESTX globale sera élevée si deux fonctions avec des codes conflictuels sont trouvées.
Des variables pré-définies similaires à try/catch (code, description, value, module, line-number, column-number, additional) peuvent être liées à des variables via des annotations de paramètres d’erreur qui sont spécifiés de la même manière que les paramètres de requête.
Les erreurs peuvent intervenir involontairment. Toutefois elles peuvent aussi être récupérées par une requêtes comme dans l’exemple suivant :

```xquery
  declare
    %rest:path("/check/{$user}")
    function page:check($user)
  {
    if($user = ('jack', 'lisa'))
    then 'User exists'
    else fn:error(xs:QName('err:user'), $user)
  };

  declare
    %rest:error("err:user")
    %rest:error-param("description", "{$user}")
    function page:user-error($user)
  {
    'User "' || $user || '" is unknown'
  };
```

##### Erreurs HTTP (_HTTP Errors_)

Les erreurs qui interviennent en dehors de RESTXQ peuvent être récupérées en ajoutant des éléments de page d’erreur avec un code d’erreur et une cible vers le fichier configuration web.xml (voir les détails dans la documentation de Jetty) :

```xml
  <error-page>
    <error-code>404</error-code>
    <location>/error404</location>
  </error-page>
```

La cible peut être une fonction RESTXQ. La fonction `request:attribute` peut être employée pour requêter les détails sur l’erreur ramenée :

```
  declare %rest:path("/error404") function page:error404() {
    "URL: " || request:attribute("javax.servlet.error.request_uri") || ", " ||
    "Error message: " || request:attribute("javax.servlet.error.message")
  };
```

##### Fonctions (_Functions_)

Le module de requête contient les fonctions pour accéder aux données relatives à la requête courante. Deux modules existent pour régler et retrouver les session de données côté-serveur de l’utilisateur courant (Session Module) et tous les utilisateurs connus du serveur HTTP (Sessions Module). Le Module RESTXQ fournit les fonctions pour requêter les URIs de base RESTXQ et générer des descriptions WADL de tous les services. Notez que l’espace de nom de tous ces modules doivent être expliciter spécifié via l’import de modules dans le prologue de la requête.
Les exemples suivants retourne le nom de l’hôte courrant :

```xquery
  import module namespace request = "http://exquery.org/ns/request";

  declare %rest:path("/host-name") function page:host() {
    'Remote host name: ' || request:remote-hostname()
  };
```

##### References

Les ressources externes suivantes sur RESXQ existent actuellement :
- [RESTXQ Specification](http://exquery.org/spec/restxq), premier brouillon
- [RESTful XQuery, Standardised XQuery 3.0 Annotations for REST](http://www.adamretter.org.uk/papers/restful-xquery_january-2012.pdf). papier présenté à XMLPrague, 2012
- [RESTXQ](http://www.adamretter.org.uk/presentations/restxq_mugl_20120308.pdf). Diapositives, MarkLogic User Group London, 2012
- [Web Application Development](http://files.basex.org/publications/xmlprague/2013/Develop-RESTXQ-WebApps-with-BaseX.pdf). Diapositives de XMLPrague 2013


------------
[1][http://www.adamretter.org.uk]
