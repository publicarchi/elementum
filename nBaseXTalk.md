
BaseX Talk, discussion intéressantes
==========

Ce fichier liste quelques discussions intéressantes sur BaseX Talk pour y avoir
recours au besoin.

## RESTXQ

[RESTXQ declare base-uri "."](http://www.mail-archive.com/basex-talk@mailman.uni-konstanz.de/msg04298.html)


## HTTP Request

[request:http()](http://www.mail-archive.com/basex-talk%40mailman.uni-konstanz.de/msg04639.html)

[How to get the data of a http post request?](https://www.mail-archive.com/basex-talk%40mailman.uni-konstanz.de/msg03171.html)

[Request Module](http://docs.basex.org/wiki/Request_Module)

[Fetch Module](http://docs.basex.org/wiki/Fetch_Module)

[Content-negociation with BaseX](https://www.mail-archive.com/basex-talk@mailman.uni-konstanz.de/msg08712.html)


## XML-TEI and XSLT

[xsl:transform, spaces and mixed content](http://www.mail-archive.com/basex-talk%40mailman.uni-konstanz.de/msg01149.html)

[Serialisation before xslt](http://www.mail-archive.com/basex-talk%40mailman.uni-konstanz.de/msg04462.html)


## Templating

[What to use for page layout/view templating](http://www.mail-archive.com/basex-talk%40mailman.uni-konstanz.de/msg01705.html)


## XForms


## Rmqs diverses


## Sécurisation des accès

[Rest Access from javascript using AngularJS](http://www.mail-archive.com/basex-talk%40mailman.uni-konstanz.de/msg04146.html)


## Upload et download de fichier

[Dowloading files](http://www.mail-archive.com/basex-talk%40mailman.uni-konstanz.de/msg04615.html)


## BaseX for dummies


## Notes en Français concernant RESTXQ

### Extension des modules XQuery

L'utilisation de l'extension .xqm est obligatoire pour le module principal.
Les méthodes RESTXQ ne sont détectées que dans ces modules. En revanche les annotations dans les modules importées ne sont pas importées car cela ne permettait pas des dépendances circulaires entre les modules [pas compris].

Le choix de .xqm a été effectué car les modules de bibliothèque recquièrent une déclaration de module, et (par conséquent) parce que les modules principaux ne peuvent être importés comme modules.

BaseX utilise .xq pour les modules principaux et .xqm pour les modules de bibliothèque (library modules).

### parsing des annotations RESTXQ

Il est possible d'attribuer directement à toutes les fonctions exécutables des annotations spécifiques de chemin. Une fonction spécifique de dispatch n'est pas nécessaire car tous les modules .xqm sont automatiquement parsés pour rechercher des annotations restxq avant chaque exécution de requête. Par la suite, l'implémentation est conçue de manière à ce que seulement le code qui a été modifié soit parsé. De telle sorte qu'il devrait être possible de gérer plusieurs centaines de modules restxq sans encombre.

### Static

Par défaut, la configuration des applications web requiert que tous les fichiers statiques (css, images, html, etc.) soient stockés dans le répertoire `static`. Ces fichiers peuvent ensuite être référencés par le chemin `/static/...` dans les fichiers HTML générés.

### Requêtes successives de la base en RESTXQ

Les requêtes succesives sur la base de données ne sont pas possible avec RESTXQ. La méthode conseillée consiste à employer les fonctionnalités de redirection (`forward` et `redirect`).
L'utilisation de scripts restent possible pour des opérations séquentielles. Par ailleurs, lors de la création de la base de données, on peut directement spécifier dans la fonction les sources à insérer.
[1] http://docs.basex.org/wiki/RESTXQ#Forwards_and_Redirects
[2] http://docs.basex.org/wiki/Commands#Command_Scripts
[3] http://docs.basex.org/wiki/Database_Module#db:create

### Upload et download de fichiers



#### Dowload de fichiers

```xquery
(:~ form for downloader :)
<form method="get" action="/download/{$file}">
              <button type="submit">Download</button>
              </form>
```

```xquery
declare
  %rest:path("/download/{$file}")
  function page:download-file($file)
  {
   (download-response("raw",$file), file:read-binary(..))
  };

(:~ headers for download  :)
declare function download-response($method,$filename){
<restxq:response>
    <output:serialization-parameters>
        <output:method value="{$method}"/>
    </output:serialization-parameters>
   <http:response>
       <http:header name="Content-Disposition"
value='attachment;filename="{$filename}"'/>
    </http:response>
</restxq:response>
};
```

## Citation

Thanks for your question. Here are the texts that I can recommend as references:

• General information on BaseX (storage, query processor): Storing and
Querying Large XML Instances, Christian Grün (my thesis)
• XQuery Update: Efficient Structural Bulk Updates on the
Pre/Dist/Size XML Encoding, Lukas Kircher et al.
• XQuery, Function Inlining: Function Inlining in XQuery 3.0
Optimization, Leonard Wörteler et al.
• Always possible as well: The web site ([http://basex.org](http://basex.org/)).

http://basex.org/about-us/publications/
