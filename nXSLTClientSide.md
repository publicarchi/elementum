# Exécution de XSLT côté client

Lorsque l’on sert des contenus en ligne, il reste possible d’exécuter des transformations XSLT côté client pour rendre des fichiers XML. Le support de transformation XSLT est à peu près pris en charge par l’ensemble des navigateurs à l’exclusion de certaines plate-formes mobiles, mais cette fonctionnalité se limite à la version 1.0 du langage XSLT.

En 2013, Mickael Kay a présenté en 2012  [Saxon-CE](http://www.saxonica.com/ce/user-doc/1.1/index.html) un processeur permettant l’exécution de XSLT 2.0 côté client.


## Association d’un document XML à une XSLT

Il est possible de lier un document XML à une XSLT avec l’instruction de traitement `xml-stylesheet`.

En insérant la ligne suivante après le prologue de votre document XML, la transformation s’exécutera automatiquement dans un navigateur qui supporte XSLT.

```xml
  <?xml-stylesheet type="text/xsl" href="filename.xsl"?>
```

## Utiliser la spécification XSLTProcessor de l’API HTML5

Il est dorénavant possible d’exécuter une tranformation XSLT en utilisant XSLTProcessor de l’API HTML5.

Le contenu scripté doit alors être marqué avec "parser-inserted".

Cette fonctionnalité est supportée à partir de iOS 2.0
Android 2.2.x(Level 8) ajoute les APIs Java pour XSLT, qui sont accessibles côté client via l’API XSLTProcessor de JavaScript.
Android 4.0 supporte le traitement des instructions XSLT processing.


```
  //Create an XSLT processor instance
  var processor = new XSLTProcessor();
  //Create an empty XML document for the XSLT transform
  var transform = document.implementation.createDocument("", "", null);
  //Load the XSLT
  transform.onload = loadTransform;
  transform.load("display.xslt");

  //Triggered once the XSLT document is loaded
  function loadTransform(){
    //Attach the transform to the processor
    processor.importStylesheet(transform);
    source = document.implementation.createDocument("", "", null);
    source.load("source.xml");
    source.onload = runTransform;
  }

  //Triggered once the source document is loaded
  function runTransform(){
  //Run the transform, creating a fragment output subtree that can be inserted back into the main page document object (given in the second argument)
  var frag = processor.transformToFragment(source, document);
  //insert the result subtree into the document, using the target element ID
  document.getElementById('updateTarget').appendChild(frag);
}

```

Source : http://www.ibm.com/developerworks/library/x-ffox3/#N10148



## Exécuter une transformation XSLT côté client avec Javascript

Même si l’association d’un document XML à une feuille de style fonctionne parfaitement, il n’est pas toujours souhaitable d’inclure une référence à une feuille de style dans un document XML. Une solution plus versatile consiste à employer JavaScript pour exécuter la transformation.

Avec JavaScript on peut :
- tester la nature du navigateur
- employer des transformations spécifiques selon le navigateur ou les besoins de l’utilisateur

```html
<html>
  <head>
    <script>
      function loadXMLDoc(filename)
        {
          if (window.ActiveXObject)
            {
              xhttp = new ActiveXObject("Msxml2.XMLHTTP");
            }
          else
            {
              xhttp = new XMLHttpRequest();
            }
          xhttp.open("GET", filename, false);
          try {xhttp.responseType = "msxml-document"} catch(err) {} // Helping IE11
            xhttp.send("");
          return xhttp.responseXML;
        }

      function displayResult()
        {
          xml = loadXMLDoc("cdcatalog.xml");
          xsl = loadXMLDoc("cdcatalog.xsl");
          // code for IE
          if (window.ActiveXObject || xhttp.responseType == "msxml-document")
            {
              ex = xml.transformNode(xsl);
              document.getElementById("example").innerHTML = ex;
            }
          // code for Chrome, Firefox, Opera, etc.
          else if (document.implementation && document.implementation.createDocument)
          {
            xsltProcessor = new XSLTProcessor();
            xsltProcessor.importStylesheet(xsl);
            resultDocument = xsltProcessor.transformToFragment(xml, document);
            document.getElementById("example").appendChild(resultDocument);
          }
        }
      </script>
    </head>
    <body onload="displayResult()">
      <div id="example" />
    </body>
  </html>
```

source : http://www.w3schools.com/xsl/xsl_client.asp

La fonction loadXMLDoc() exécute les opérations suivantes :
- création d’un objet XMLHttpRequest
- utilisation des méthodes open() et send() de l’objet XMLHttpRequest pour envoyer une requête au serveur
- Récupération des données de réponse en XML

La fonction displayResult() est employée pour rendre le XML stylé par la transformation XSL
- Chargement des fichiers XML et XSLT
- Test du navigateur
  - Si Internet Explorer :
    - Utilisation de la méthdoe transformNode() pour appliquer la XSLT au document XML
    - réglage du body du document courant (id="example") pour contenir le contenu XML mis en forme
  - Pour les autres navigateurs :
    - création d’un objet XSLTProcessor et importation du fichier XSLT
    - Utilisation de la méthode transformToFragment() pour appliquer la transformation XSL au document XML
    - Réglage du body du document courant (id="example") pour contenir le XML stylé.

## Liens d’intérêt

Test Cases for XSLT support in browser http://greenbytes.de/tech/tc/xslt/

http://stackoverflow.com/questions/28041557/client-side-xslt-internet-explorer-does-not-cache-xslt

http://dh.obdurodon.org/transformation-scenario.xhtml
