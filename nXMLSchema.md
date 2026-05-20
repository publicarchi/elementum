# XML Schema

[XML Schema](https://www.w3.org/TR/xmlschema-0/) est une spécification de langage de schéma publiée par le W3C en 2001. La création de ce standard a tenu compte de l’existence d’autres langages de schéma préexistants que [XSchema, Document Definition Markup Language (DDML)](https://www.simonstl.com/xschema/), XML-Data, [XML-Data Reduced (XDR)](https://www.cogsci.ed.ac.uk/~ht/XMLData-Reduced.htm) et [Schema for Object-Oriented XML (SOX)](https://www.w3.org/TR/NOTE-SOX/), tout en s’appuyant sur les besoins de l’industrie et des producteurs de systèmes de gestion de bases de données.

Par rapport aux DTD, XML Schema apporte des types de données et la gestion des espaces de nom.

La spécification XML Schema propose un système complet de type de données (**XML Schema - part 2**) qui peuvent être utilisés pour les éléments et les attributs. Ces types étendent considérablement ceux qui étaient précédemment disponibles dans les DTD en introduisant des types habituellement utilisés dans le contexte des bases de données relationnelles.

XML Schema différentie les types de données simples (*simple datatypes*) et complexes (*complex datatypes*). Les types complexes qui concernent seulement les éléments associent plusieurs types simples. Les types simples sont soit pré-définis (*built-in*) ou dérivés. Ils sont caractérisés par un type de données primitif et un ensemble de facettes restrictives appliquées à l’espace de donnée (*value space*) ou l’espace lexical (*lexical space*).

Le système de type de XML Schema établit une distinction claire entre l’espace de valeur (*value space*) et l’espace lexical (*lexical space*). Alors que l’espace de valeurs consiste en une collection abstraite de valeurs valides pour un type de données, l’espace lexical contient les représentions lexicales de ces valeurs, c’est-à-dire les tokens qui peuvent apparaître dans le document XML. Par exemple la représentation lexicale canonique d’un type booléen est une chaîne `true` ou `false` mais elle peut recevoir d’autres représentations comme les chaînes de caractères `1` ou `0`.

## Structure d’un schéma XML

### Élément racine

D’après la syntaxe du W3C, un schéma XML débute par un élément racine `schema` de l’espace de nom `http://www.w3.org/2001/XMLSchema`.

```xml
<xs:schema 
  xmlns:xs="http://www.w3.org/2001/XMLSchema" 
  targetNamespace="http://namespace/for/your/schema" 
  xmlns="http://ouvroir.umontreal.ca/ns/museumscan" 
  elementFormDefault="qualified">
</xs:schema>
```

Les éléments sont les blocs qui servent à construire des éléments XML qui contiennent les données et ils déterminent la structure des instance des document.

### Déclaration d’un élément avec un modèle de contenu simple (*simple content model*)

On peut définir un élément et lui donner un type XML de la manière suivante :

```xml
<xs:element name="nom" type="xs:tring"/>
```

`@name` fournit le nom de l’élément, `@type` indique le type de données en utilisant les noms prédéfinis simples proposés par [XML Schema - Part 2 (voir la liste)](https://www.w3.org/TR/xmlschema-2/#built-in-datatypes). 

Le type de valeurs valide peut être encore plus contraint en utilisant des propriétés fixes ou par défaut.

- `@default` indique que si aucune valeur n’est spécifiée dans le document XML, alors l’application doit employé le default spécifié dans le schema.
- `@fixed` indique que la valeur dans le document XML peut seulement avoir la valeur spécifiée dans le schéma.

```xml
<xs:element name="pays" type="xs:sting" fixed="UK">
```

### Spécifier la cardinalité des éléments

Il est possible de contraindre le nombre d’instances d’un élément XML qui peuvent apparaître dans un document XML (*cardinality*) avec les attributs `@minOccurs` et `@maxOccurs`.

- `@minOccurs` peut prendre n’importe quelle valeur entière non négative (0, 1, 2, 3, ...)
- `@maxOccurs` peut prendre n’importe quelle valeur non négative ou la valeur spéciale `unbounded` lorsque l’élément peut apparaître un nombre de fois illimité.

```xml
<xs:element name="p" type="xs:string" minOccurs ="0" maxOccurs="unbounded" />
```

Lorsque les valeurs de `@minOccurs` et `@maxOccurs` ne sont pas spécifiées, l’élément est mandataire. Si `@minOccurs` est égal à 0, l’élément est optionnel.

### Définition de types simples

Il est possible de créer de nouveaux types simples en restreignant des types simples existants pour définir ses propres types de données. 

Ce mécanisme peut par exemple être utilisé pour contrôler la forme d’un code postal avec une expression régulière ou la longueur maximale d’un champ.

### Déclaration d’un élément avec un modèle de contenu complexe (*complexe content model*)

Les éléments qui peuvent contenir d’autres éléments sont dits complexes (*complex content model*). 

`xs:complexType` spécifie les éléments et les attributs permis dans le modèle de contenu d’un élément et les règles selon lesquelles ils peuvent apparaître ainsi que leur cardinalité.

Ces définitions peuvent être déclarées sur place ou faire référence à d’autres définitions.

Des compositeurs (*compositors*) permettent de définir la manière et l’ordre dans lequel les enfants peuvent apparaître dans le document.

- `xs:sequence` les éléments enfants DOIVENT apparaitre dans l’ordre de leur déclaration
- `xs:choice` seulement un des éléments fils peut apparaître dans le document
- `xs:all` les éléments fils peuvent apparaître dans le document dans n’importe quel ordre

Les compositeurs `xs:sequence` et `xs:choice` peuvent être imbriqués dans d’autres combinaisons avec leur propre cardinalités.

### Définition d’un attribut

```xml
<xs:attribute name="x" type="xs:string" />
```

L’attribut `@use` permet d’indiquer si l’attribut est optionnel (`optional`) ou obligatoire (`required`).

```xml
<xs:attribute name="x" type="xs:string" use="optional" />
```

Dans un type complexe, les attributs apparaissent après le compositeur.

```xml
<xs:element name="commande">
  <xs:complexType>
      <xs:attribute name="commandeID" type="xs:int" />
  </xs:complexType>
</xs:element>
```

### Définition de types complexes globaux

Il est possible de définir un type complexe de manière globale et de lui donner un nom afin de pouvoir le réutiliser ailleurs dans le schéma.

```xml
<xs:complexType name="adressLike">
    <xs:sequence>
        <xs:element name="street" type="xs:string" />
        <xs:element name="country" type="xs:string" />
    </xs:sequence>
</xs:complexType>
```

Ce type complexe peut ensuite être réemployé dans n’importe quel autre type complexe par une référence de la forme

```xml
<xs:element ref="adressLike"/>
```



### Contenu mixte

```xml
<xs:element name="p">
    <xs:complexType mixed="true">
        <xs:sequence>
            <xs:element name="em" type="xs:string" />
            <xs:element name="strong" type="xs:string" />
        </xs:sequence>
    </xs:complexType>
</xs:element>
```



## Les types de données (*dataTypes*)

XML Schema prédéfinit un grand nombre de types de données primaires (*primitive dataTypes*).

| Datatype     | Description                                                  | Lexical representation                                       | SQL equivalent                                        |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------------- |
| string       | Character string of unlimited length.                        | A short string                                               | VARCHAR                                               |
| boolean      | Boolean value.                                               | "true","false", "1", "0"                                     | BIT                                                   |
| decimal      | Decimal number. A minimum precision of 18 digits is supported by conforming processors. | "-1.23", "126.54", "0.0", "+100000.00", "210"                | DECIMAL                                               |
| float        | A single-precision 32-bit floating point type according to IEEE 754-1985. Special values are positive and negative zero, positive and negative infinity, and not-a-number. | "-1E4", "127.433E12", "12.78e-2", "12", "0", "-0", "INF", "-INF", "NaN" | REAL                                                  |
| double       | A double-precision 64-bit floating point type according to IEEE 754-1985. | "-1E4", "127.433E12", "12.78e-2", "12", "0", "-0", "INF", "-INF", "NaN" | DOUBLE                                                |
| duration     | Specifies a period of time. The value space is a six-dimensional space where the coordinates designate the Gregorian year, month, day, hour, minute, and second. | The lexical representation follows the format `PnYnMnDTnHnMnS`. An optional fractional part for seconds is allowed. Negative durations are allowed, too. *Examples:*"PT1H3M13.5S""P1Y5M""-PT3H" | INTERVAL                                              |
| time         | A specific time of day as defined in section 5.3 of ISO 8601 | The lexical representation follows the format `hh:mm:ss`An optional fractional part for seconds is allowed. Additionally, a time zone can be specified: "Z" for UTC, or a signed time difference in the format `hh:mm`.*Examples:*"05:20:23.2""13:20:00-05:00" | TIME                                                  |
| date         | A Gregorian calendar date according to section 5.2.1 of ISO 8601. | The lexical representation follows the format `CCYY-MM-DD`. To accommodate values outside the range 1-9999, additional digits and a negative sign can be added to the left. (The year 0000 is prohibited.)*Example:*"1999-05-31" | DATE                                                  |
| dateTime     | A specific instant of time (a combination of date and time) as defined in section 5.4 of ISO 8601. | The lexical representation follows the format `CCYY-MM-DDThh:mm:ssZ`, where the character "T" separates date from time and "Z" denotes an optional time zone.*Examples:*"1999-05-31T13:20:00-05:00" "2001-12-01T05:20:23.2" | TIMESTAMP (slightly different lexical representation) |
| gYearMonth   | Represents a specific Gregorian month in a specific Gregorian year. | The lexical representation follows the format CCYY-MMZ. "Z" denotes an optional time zone. *Examples:*"2001-05" | DATE                                                  |
| gYear        | Represents a Gregorian year.                                 | The lexical representation follows the format CCYYZ. "Z" denotes an optional time zone. *Examples:*"1984" | DATE                                                  |
| gMonthDay    | Specifies a recurring Gregorian date.                        | The lexical representation follows the format --MM-DDZ. "Z" denotes an optional time zone. *Examples:*"--04-01" | DATE                                                  |
| gMonth       | Denotes a Gregorian month that recurs every year.            | The lexical representation follows the format --MM--Z. "Z" denotes an optional time zone. *Examples:*"--07--" | DATE                                                  |
| gDay         | Denotes a Gregorian day that recurs every month.             | The lexical representation follows the format ---DDZ. "Z" denotes an optional time zone. *Examples:*"---13" | DATE                                                  |
| hexBinary    | Arbitrary hex-encoded binary data.                           | "9a7f", "FFFF3", "0100"                                      | BINARY/BLOB                                           |
| base64Binary | Base64-encoded arbitrary binary data. The entire binary stream is encoded using the Base64 Content-Transfer-Encoding defined in Section 6.8 of RFC 2045. |                                                              | BINARY/BLOB                                           |
| anyURI       | A Uniform Resource Identifier reference (URI).               |                                                              | VARCHAR                                               |
| QName        | An XML qualified name consisting of namespace name and local part. |                                                              | VARCHAR                                               |
| NOTATION     | Represents the NOTATION attribute type from XML attributes.  | This datatype is abstract; users must derive their own datatype from it. | VARCHAR                                               |

Outre ces types primaires, la spécification prédéfinit également des types dérivés en leur appliquant des facettes de contraintes. Par exemple, le type de données `nonNegativeInteger` est dérivé du type `integer` en contraignant son espace de valeur aux valeurs non négatives en lui applicant la facette de contrainte `minInclusive value"0"`.

XML Schema permet également à l’utilisateur de définir un système de données simple en appliquant des facettes de contraintes à des types existants. Les facettes de contraintes suivantes sont disponibles.

| Facet          | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| length         | Defines the length of a datatype value (number of characters for strings, number of octets for binary, etc.). |
| minLength      | Lower bound for the length of a datatype value.              |
| maxLength      | Upper bound for the length of a datatype value.              |
| pattern        | Restricts the values of a datatype by constraining the lexical space to a specific pattern. Patterns are defined via regular expressions. The syntax for the specification of patterns uses almost the same tokens and escape symbols as other languages that support patterns (such as Perl). |
| enumeration    | Constrains the value space of a datatype to the specified enumeration values. |
| whitespace     | This is not really a constraining facet but specifies a policy for handling whitespace in input values: `preserve` keeps all whitespace characters, `replace` replaces each whitespace character with the blank character, `collapse` reduces all sequences of whitespace characters to a single blank character. |
| maxInclusive   | Upper bound for the value space of a datatype, includes the specified value. |
| maxExclusive   | Upper bound for the value space of a datatype, excludes the specified value. |
| minInclusive   | Lower bound for the value space of a datatype, includes the specified value. |
| minExclusive   | Lower bound for the value space of a datatype, excludes the specified value. |
| totalDigits    | Maximum total number of decimal digits in the values of datatypes derived from datatype decimal. |
| fractionDigits | Maximum number of decimal digits in the fractional part of values of datatypes derived from decimal. |

Plusieurs types dérivés sont prédéfinis par le standard.

| Datatype                                             | Derived from       | Description                                                  | SQL equivalent                      |
| ---------------------------------------------------- | ------------------ | ------------------------------------------------------------ | ----------------------------------- |
| normalizedString                                     | string             | Cannot contain carriage return (#xD), line feed (#xA) or tab (#x9) characters. | VARCHAR VARWCHAR                    |
| token                                                | normalizedString   | Cannot contain line feed (#xA) or tab (#x9) characters, cannot have leading or trailing spaces (#x20) and cannot have internal sequences of two or more spaces. | VARCHAR VARWCHAR                    |
| language                                             | token              | Language identifiers as defined by ISO 639 and ISO 3166.     | VARCHAR VARWCHAR                    |
| NMTOKENNMTOKENSNameNCNameIDIDREFIDREFSENTITYENTITIES | token              | Represent the corresponding attribute type from XML 1.0 (DTD). | VARCHAR VARWCHAR                    |
| integer                                              | decimal            | The standard mathematical integer datatype of arbitrary size. Derived from datatype `decimal` by setting the facet fractionDigits to 0. | no equivalent (value range too big) |
| nonPositiveInteger                                   | integer            | Integer less than or equal to zero.                          | no equivalent                       |
| negativeInteger                                      | nonPositiveInteger | Integer less than zero.                                      | no equivalent                       |
| long                                                 | integer            | Integer in the range from -9223372036854775808 to 9223372036854775807. | BIGINT                              |
| int                                                  | long               | Integer in the range from -2147483648 to 2147483647.         | INTEGER                             |
| short                                                | int                | Integer in the range from -32768 to 32767.                   | SMALLINT                            |
| byte                                                 | short              | Integer in the range from -128 to 127.                       | TINYINT                             |
| nonNegativeInteger                                   | integer            | Integer greater than or equal to zero.                       | no equivalent                       |
| unsignedLong                                         | nonNegativeInteger | Integer in the range from 0 to 18446744073709551615.         | no equivalent                       |
| unsignedInt                                          | unsignedLong       | Integer in the range from 0 to 4294967295.                   | no equivalent                       |
| unsignedShort                                        | unsignedInt        | Integer in the range from 0 to 65535.                        | no equivalent                       |
| unsignedByte                                         | unsignedShort      | Integer in the range from 0 to 255.                          | TINYINT                             |
| positiveInteger                                      | nonNegativeInteger | Integer greater than zero.                                   | no equivalent                       |

Le langage de schéma permet de définir des types de données.

```xml
<xs:attribute name = "type">
  <xs:simpleType>
    <xs:restriction base = "xs:NMTOKEN">
      <xs:enumeration value = "instrumentalist"/>
      <xs:enumeration value = "jazzSinger"/>
      <xs:enumeration value = "jazzComposer"/>
    </xs:restriction>
  </xs:simpleType>
</xs:attribute>
```

```xml
<xs:element name = "grade">
  <xs:simpleType>
    <xs:restriction base = "xs:decimal">
      <xs:fractionDigits value = "1"/>
      <xs:totalDigits value = "2"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```



Cf. https://www.ibm.com/docs/en/tamino/10.7.0?topic=schema-introduction-xml

## Autres langages de modélisation

RelaxNG, deux syntaxes

### JSON Schema

JSON dispose depuis 2019 seulement d’un langage de schéma [JSON Schema](https://json-schema.org). Tout comme le format, l’expressivité de ce langage est particulièrement limitée en particulier du point de vue des types de données qui peuvent être utilisés dans le modèle de données même si la spécification ouvre la possibilité de définir des vocabulaires et d’étendre le système de types.

Les schémas XML sont plus rigoureux dans la définition de l’ordre des éléments, des types avancées ou l’expression de contraintes complexes. Ils permettent aussi de définir des modèles de contenus mixes très adaptés pour le contenu textuel.

La pile technologique JSON ne dispose par ailleurs pas d’équivalents pour plusieurs outils puissants disponibles en XML pour requêter ou transformer des documents. Le développement de JSON Schema a donné lieu à plusieurs hésitations qui ont conduit à la publication de plusieurs brouillons incompatibles. Les implémentations ont souvent été partielles ou avec des comportements divergents. Certains validateurs ne supportent pas toute la spécification de manière homogène.

La simplicité de la syntaxe est par ailleurs discutable. Par exemple : 

```json
{
  "type": "object",
  "properties": {
    "name": { "type": "string" }
  }
}
```

```xml
<xs:element name="name" type="xs:string"/>
```

Extension JSON Schema https://xschema.dev

## Références

Fallside, David C., et Priscilla Walmsley. 2004. *XML Schema Part 0: Primer (Second Edition)*. W3C Recommendation. W3C. https://www.w3.org/TR/2004/REC-xmlschema-0-20041028/primer.html.

Thompson, Henry S., David Beech, Murray Maloney, et Noah Mendelsohn. 2004. *XML Schema Part 1: Structures (Second Edition)*. W3C Recommendation. W3C. https://www.w3.org/TR/xmlschema-1/.

Biron, Paul V., et Ashok Malhotra. 2004. *XML Schema Part 2: Datatypes (Second Edition)*. W3C Recommendation. W3C. https://www.w3.org/TR/xmlschema-2/.

Malhotra, Ashok, et Murray Maloney. 1999. *XML Schema Requirements*. W3C Note. W3C. https://www.w3.org/TR/1999/NOTE-xml-schema-req-19990215.

Voir aussi

https://en.wikipedia.org/wiki/XML_schema#Languages

https://en.wikipedia.org/wiki/List_of_types_of_XML_schemas

Source https://www.liquid-technologies.com/xml-schema-tutorial/xsd-extending-types