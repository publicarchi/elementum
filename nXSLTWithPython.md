---
author: emchateau
tags: python, xslt
---

# XSLT with Python

Plusieurs librairies permettent de travailler des données XML avec Saxon. Toutefois, pendant longtemps ces librairies sont restées très limité car elles ne permettaient pas d’utiliser les versions 2 et 3 des langages XSLT, XPath et XQuery. Ces limitations étaient liées au fait que les processeurs supportant ces versions étaient développés en Java. Le développement de [Saxon/C](https://www.saxonica.com/saxon-c/doc1.1/html/index.html) au début des années 2020 a permis de faciliter le portage de ces versions dans d’autre langage.

## The ElementTree XML API

https://docs.python.org/3/library/xml.etree.elementtree.html

> The [`xml.etree.ElementTree`](https://docs.python.org/3/library/xml.etree.elementtree.html#module-xml.etree.ElementTree) module implements a simple and efficient API for parsing and creating XML data.

## XSLTools (2007)

https://pypi.org/project/XSLTools/

> XSLTools is a distribution providing modules and packages for the development of XML/XSL-based applications in Python, including Web-based applications, utilising the open source libxml2 and libxslt libraries through the libxml2dom wrapper.

## LXML (2007-2024, v. 5.2.1)

https://lxml.de

> The lxml XML toolkit is a Pythonic binding for the C libraries [libxml2](http://xmlsoft.org/) and [libxslt](http://xmlsoft.org/XSLT/). It is unique in that it combines the speed and XML feature completeness of these libraries with the simplicity of a native Python API, mostly compatible but superior to the well-known [ElementTree](http://effbot.org/zone/element-index.htm) API.

Malheureusement les processeurs utilisés ne permettent pas l’utilisation des versions 2 et 3 des langages XSLT et XPath.

## Saxonpy

https://pypi.org/project/saxonpy/

> This’s a python wheel package for [Saxon](https://www.saxonica.com/saxon-c/documentation/index.html), an XML processor from the Saxonica company. Saxon includes a range of tools for XML transformations, XML queries, and schema validations. For this release, we only include the support for the home edition or the open-source version.

Saxonpy offre une interface pour Saxon/C (2021).

## Saxonche

https://pypi.org/project/saxonche/

> Official Saxonica Python wheel package for Saxon, an XML document processor. SaxonC provides APIs to run XSLT 3.0 transformations, XQuery 3.1 queries, XPath 3.1, and XML Schema validation.
>
> The SaxonC release comes in separate wheels for the three product editions:
>
> - **saxonche** (SaxonC-HE: open-source Home Edition)
> - **saxoncpe** (SaxonC-PE: Professional Edition)
> - **saxoncee** (SaxonC-EE: Enterprise Edition)

13 janvier 2023, Saxonche est un wheel package officiel de Saxon. En 2024, c’est certainement la meilleure manière d’utiliser XSLT avec Python.