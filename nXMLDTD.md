# XML Document type definition

Les définitions de type de document.

Exemple

```
  <?xml version="1.0" encoding="UTF-8"?>
  <!ELEMENT chapter (title, paragraph)>
  <!ELEMENT title (#PCDATA)>
  <!ELEMENT paragraph (strong)>
```

/usr/bin/xmllint


## Validation

N’importe quel parseur XML peut être utilisé pour vérifier qu’une DTD conforme aux règles de la spécification XML. Les DTDs ne peuvent pas être validées au sens de la spécification XML car il ne s’agit pas d’instances de document XML.

Il existe plusieurs validateurs XML open-source parmi lesquels XMLLint (qui utilise libxml), rxp et Xerces.

