---
author: emchateau
since: 2017-01-12
version: 0.1
tags: xml
---

# Awesome XML

## Organisations

- [X(Q)uery and XSL(T) Specifications (qtspecs)](https://qt4cg.org) [[git](https://github.com/qt4cg/qtspecs)]
- [Markup Declaration](https://markupdeclaration.org) [[git](https://github.com/markupdeclaration)]
- [EXPath](https://expath.org) [[git](https://github.com/expath)]
- [iXML](https://invisiblexml.org)

## Other awesomes XML

https://github.com/StanimirIglev/awesome-xml

https://github.com/jefim/JefimsIncredibleXsltTool

https://github.com/joewiz/learn-xquery

https://github.com/joewiz/xquery-power

## Outils XML

http://textalign.net

https://github.com/pgfearo/xmlspectrum

https://github.com/maxtoroq/rng.xsl (under dev)

https://github.com/sergeche/xmlview

https://github.com/AlainCouthures/xsltforms

https://github.com/greendrake/jsxml

https://github.com/t-davies/magicxml

https://github.com/moovweb/tritium, http://www.tritium.io

https://github.com/xspec/xspec

https://github.com/aerhard/xml-tools

https://atom.io/packages/atom-xsltransform

https://atom.io/packages/linter-autocomplete-jing

https://atom.io/packages/xml-common-schemata

https://xmlstar.sourceforge.net

## Transformations

https://github.com/BoyCook/XSLTJS

https://github.com/vicmortelmans/xslt-in-the-browser

https://github.com/sergeche/node-libxslt

https://github.com/albanm/node-libxslt

https://github.com/albanm/node-libxml-xsd

https://github.com/albanm/libxmljs

https://github.com/apache/xerces2-j

### Miscellaneous

- [XSLT Explorer](https://github.com/ndw/xsltexplorer) A simple analysis tool for complicated XSLT stylesheets

## Validation

http://www.thaiopensource.com/relaxng/jing.html

[RelaxNG validator in javascript](http://debeissat.nicolas.free.fr/relaxng.php)

cf. https://stackoverflow.com/questions/23906793/command-line-validator-supporting-relax-ng-schemas-with-embedded-iso-schematron

### Schematron

Cf. https://github.com/Schematron/awesome-schematron

#### Specifications

- [ISO Schematron 4th Edition ](https://www.iso.org/standard/85625.html) - ISO/IEC 19757-3:2025 - Information technology — Document Schema Definition Languages (DSDL)Part 3: Rule-based validation using Schematron

  > This document specifies Schematron, a schema language for XML. This document establishes requirements for Schematron schemas and specifies when an XML document matches the patterns specified by a Schematron schema. Schematron uses query languages such as XPath for writing assertions.

- [ISO Schematron 3rd Edition](https://www.iso.org/standard/74515.html) - ISO/IEC 19757-3:2020 - Information technology — Document Schema Definition Languages (DSDL)Part 3: Rule-based validation using Schematron

- [ISO Schematron 2nd Edition](https://www.iso.org/standard/55982.html) - ISO/IEC 19757-3:2016 - Information technology — Document Schema Definition Languages (DSDL) — Part 3: Rule-based validation — Schematron

- [ISO Schematron 1st Edition](https://www.iso.org/standard/40833.html) - ISO/IEC 19757-3:2006 - Information technology — Document Schema Definition Language (DSDL) — Part 3: Rule-based validation — Schematron.

- [Schematron Quick Fixes](http://schematron-quickfix.github.io/sqf) — Schematron Quick Fixes Specification

#### Implementations

- [SchXslt [ʃˈɛksl̩t] – An XSLT-based Schematron processor](https://codeberg.org/schxslt/schxslt) - An XSLT-based Schematron processor.
- [SchXslt2](https://codeberg.org/SchXslt/schxslt2) - A modern XSLT-based ISO Schematron to XSLT 3.0 transpiler
- [ml-schematron](https://github.com/ndw/ML-Schematron) - A `schematron.xqy` module that will allow you to perform Schematron validation with MarkLogic Server.
- [ph-schematron](https://github.com/phax/ph-schematron) - Java library to validate XML documents according to Schematron rules, using 2 different engines - additionally you can validate Schematron itself. Ships with Maven plugins and an Ant task (since 4.3.0).
- [schematron-basex](https://github.com/Schematron/schematron-basex) - XQuery module to use ISO Schematron in BaseX.
- [schematron-exist](https://github.com/Schematron/schematron-exist) - XQuery module to use ISO Schematron in eXist.
- [schematron](https://github.com/Schematron/schematron) - "skeleton" XSLT implementation of ISO Schematron. No longer maintained.
- [XQS](https://github.com/AndrewSales/XQS) - native XQuery implementation of ISO Schematron.
- [pyschematron](https://github.com/robbert-harms/pyschematron) - library package for Schematron validation in Python.
- [node-schematron](https://github.com/wvbe/node-schematron) - Javascript implementation of Schematron. Supports XPath 3.1 (via [fontoxpath](https://www.npmjs.com/package/fontoxpath)) but not XSLT functions.

[Schematron](https://github.com/Schematron/schematron) [archived]

#### Publications

##### Books

- Siegel, Erik. “[Schematron: A language for validating XML](https://xmlpress.net/publications/schematron/)” Denver, CO, USA: XML Press, 2022.
- Hedler, Marko, Manuel Montero Pineda, and Nico Kutscherauer. “[Schematron: Effiziente Business Rules für XML-Dokumente.](https://schematron.info/)” Heidelberg: dpunkt, 2011.
- Jelliffe, Rick. “[The Schematron Assertion Language 1.6](https://web.archive.org/web/20061230150144/http://xml.ascc.net:80/resource/schematron/Schematron2000.html)” Online, October 1, 2002.

##### Presentations

- Maus, David. "[ISO Schematron: A feather duster to reach the corners that other schema languages cannot reach](https://doi.org/10.5281/zenodo.16019038)" Poster presented at the Hub of Computing and Data Science's Research Software Engineering Day, Hamburg, Germany, 2025.
- Sales, Andrew. "[What's New in Schematron 4](https://andrewsales.com/schematron4/index.html)" In Schematron Users Meetup at Markup UK 2025. London, UK, 2025.
- Maus, David. "[SchXslt2 Schematron to XSLT 3.0 transpiler](https://dmaus.name/slides/schxslt2-2025.html)" Markup UK 2025. London, UK, 2025.
- Maus, David. "[ISO Schematron Conformance Tests](https://dmaus.name/slides/schematron-conformance-2025.html)" In Schematron Users Meetup at Markup UK 2025. London, UK, 2025.
- Sales, Andrew. "[XQS: A Native XQuery Schematron Implementation](https://markupuk.org/2023/webhelp/index.html#ar11.html)" In Markup UK 2023 Proceedings, 146-56. London, UK, 2023.
- Bormans, Geert. “[Customisation of Akoma Ntoso using Schematron.](https://www.balisage.net/Proceedings/vol27/html/Bormans01/BalisageVol27-Bormans01.html)” Presented at Balisage: The Markup Conference 2022, Washington, DC, August 1 - 5, 2022. In Proceedings of Balisage: The Markup Conference 2022. Balisage Series on Markup Technologies, vol. 27 (2022). https://doi.org/10.4242/BalisageVol27.Bormans01.
- Maus, David. “[Overview of Implementations](https://archive.xmlprague.cz/2022/files/presentations/Schematron.pdf)” In “[Schematron Users Meetup](https://www.xmlprague.cz/day3-2022/#sch)” at XML Prague 2022, Prague, Czech Republic, 2022.
- Siegel, Erik. “[Schematron Query Language Binding](https://archive.xmlprague.cz/2022/files/presentations/schematron-qlb.pdf)” In “[Schematron Users Meetup](https://www.xmlprague.cz/day3-2022/#sch)” at XML Prague 2022, Prague, Czech Republic, 2022.
- Holman, G. Ken. “[Non-programmers’ support for Schematron assertions](https://archive.xmlprague.cz/2022/files/presentations/Schematron Users Meetup 2022-06-11 20220521-1310z.pdf)” In “[Schematron Users Meetup](https://www.xmlprague.cz/day3-2022/#sch)” at XML Prague 2022, Prague, Czech Republic, 2022.
- Graham Tony, David Maus, Andrew Sales and Erik Siegel. “[Schematron State of the Union](https://www.xmlprague.cz/day2-2022/#sch)” XML Prague 2022, Prague, Czech Republic, 2022.
- Maus, David. “[Ex-Post Rule Match Selection: A Novel Approach to XSLT-Based Schematron Validation.](https://archive.xmlprague.cz/2019/files/xmlprague-2019-proceedings.pdf#page=79)” In XML Prague 2019 Conference Proceedings, 57–65. Prague, Czech Republic, 2019.
- Maus, David. “[An Introduction to Schematron and Schematron QuickFix.](https://doi.org/10.5281/zenodo.3429706)” Presented at the TEI Conference and Member’s Meeting 2019 (TEI 2019), Graz, Austria, 16–22 September 2019, Graz, September 16, 2019.
- Maus, David. “[Schematron Report Customization.](https://www.youtube.com/watch?v=V5M_mRLoy8s)” Webinar presented at the Markup UK Solidarity Edition, June 10, 2020.
- Maus, David. “[What’s in a Schematron?](https://markupuk.org/webhelp/index.html#ar02.html)” In Markup UK 2021 Proceedings. Online, 2021.
- Nadolu, Octavian, and Nico Kutscherauer. “[Schematron QuickFix](https://archive.xmlprague.cz/2016/files/xmlprague-2016-proceedings.pdf#page=93)” In XML Prague 2016 Conference Proceedings, 81–98. Prague, Czech Republic, 2016.
- Nadolu, Octavian. “[Taking Schematron QuickFix To The Next Level.](https://markupuk.org/2019/webhelp/index.html#ar09.html)” In Markup UK 2019 Proceedings, 125–34. London, UK, 2019.

#### Applications

- [focheck](https://github.com/AntennaHouse/focheck) - Validates XSL-FO property value expressions in attributes by parsing expressions using parser written in XSLT 2.0 then running `assert` and `report` on results.
- [org.doctales.terminology](https://github.com/doctales/org.doctales.terminology) - DITA-OT plugin and authoring framework for terminology management, that generates Schematron termchecker rule sets for DITA ([Demo](https://doctales.github.io/samples/termchecker-dita/terminology-DITA-en-GB.sch)) and XLIFF ([Demo](https://doctales.github.io/samples/termchecker-xliff/terminology-XLIFF-en-GB.sch)) files from DITA `<termentry>` topics.
- [XSLT Quality](https://github.com/mricaud/xslt-quality) - XSLT Quality checks your XSLT to see if it adheres to good or best practices.
- [oscal-xproc3](https://github.com/usnistgov/oscal-xproc3/blob/main/testing/xproc3-house-rules.sch) - Enforces house style for XProc 3.0 pipelines.
- [Schematron Schematron](https://codeberg.org/dmaus/schematron-schematron) - A Schematron schema that checks XPath expressions in your Schematron.
- *Add your Schematron application here*

## Correcteurs

http://jtidy.sourceforge.net

https://github.com/ndmitchell/tagsoup

## Pages

http://relaxng.org

## Collations

https://github.com/HuygensING/hyper-collate

## Editeurs

XPath 3.1 Notebook https://github.com/pgfearo/vscode-nodebook

http://xsltfiddle.liberty-development.net/

http://xqueryfiddle.liberty-development.net/

https://martin-honnen.github.io/xslt3fiddle/

## Tools

- [org-to-xml](https://codeberg.org/ndw/org-to-xml) Library to convert Emacs org-mode files to XML 
- [Word XML to HTML](https://github.com/crism/WordXML-to-HTML) XSL to convert MS Word-generated XML to HTML
- [Word XML to HTML](XSL to convert MS Word-generated XML to HTML)
- [XML Calabash TextDiff Extension Step](https://github.com/liamquin/xmlcalabash1-textdiff)
- [XSLT Excel engine](https://github.com/foglcz/xsl-excel-engine)

## TEI tools

- Annotation Studio http://www.annotationstudio.org
- Apache OpenNLP https://opennlp.apache.org The Apache OpenNLP library is a machine learning based toolkit for the processing of natural language text.
- CATview http://catview.uzi.uni-halle.de the Colored & Aligned Texts view
-  Classical Text Editor http://cte.oeaw.ac.at
-  CorrespSearch https://correspsearch.net Search scholarly editions of letters
- CWRC-Writer https://github.com/cwrc/CWRC-WriterBase
-  ecdosis https://ctan.org/pkg/ekdosis
- eLaborate http://elaborate.huygens.knaw.nl eLaborate is an online work environment in which scholars can upload  scans, transcribe and annotate text, and publish the results as on  online text edition which is freely available to all users. Short  information about and a link to already published editions is presented  on the page **Editions** under **Published**. Information about editions currently being prepared is posted on the page **Ongoing projects**.
-  EVT http://evt.labcd.unipi.it
- FreeLing 4.0 http://nlp.lsi.upc.edu/freeling/ open source language analysis tool suite
-  FromThePage https://fromthepage.com “Simply the finest crowdsourcing manuscript transcription software on the planet.”
-  FuD https://fud.uni-trier.de
- Image Markup Tool https://tapor.uvic.ca/~mholmes/image_markup/
- Isilex https://isilex.github.io/easy-xml/
-  Kiln http://kcl-ddh.github.io/kiln/ Kiln is a multi-platform framework for building and deploying complex websites whose source content is primarily in  XML. It brings together various independent software components into an  integrated whole that provides the infrastructure and base functionality for such sites.
-  LombardPress http://lombardpress.org   LombardPress is the publishing component of a digital ecosystem designed to help facilitate  a new kind of editing and publication of historical texts.
- ManuscriptDesk https://manuscriptdesk.uantwerpen.be/md/Main_Page The Manuscript Desk is an online environment in which manuscript  pages can be uploaded, manuscript pages can be transcribed, and  collations of transcriptions can be performed. The Manuscript Desk  builds on, and extends different software components used in the Digital Humanities. The project is open-source, licenced under the [GNU License](http://www.gnu.org/licenses/gpl-3.0.en.html). Full installation instructions, and additional information on the technical structure of the software can be found on [GitHub](https://github.com/akvankorlaar/manuscriptdesk). Do you have suggestions or questions, or have you found a bug? You can  always reach us at uamanuscriptdesk 'at' gmail 'dot' com.
- MOM-CA https://github.com/icaruseu/mom-ca/wiki
-  New Testament Virtual Manuscript Room (NTVMR)
  http://ntvmr.uni-muenster.de/de/manuscript-workspace
-  oXygen http://oxygenxml.com
- PhiloEditor http://site1705.web.cs.unibo.it/phed/
-  Scripto http://scripto.org Scripto brings the power of MediaWiki to your  Omeka sites. Designed to allow members of the public to transcribe a  range of different kinds of files, Scripto will increase your content’s  findability while building your user community through active  engagement.
- Stanford NLP https://nlp.stanford.edu/software/
- Stylo https://stylo.ecrituresnumeriques.ca/
-  T-Pen http://www.t-pen.org/TPEN/ T‑PEN is a web-based tool for working with images of manuscripts.  Users attach transcription data (new or uploaded) to the actual lines of the original manuscript in a simple, flexible interface. 
- TEI Critical Apparatus Toolbox http://teicat.huma-num.fr
-  TextGrid https://textgrid.de/en/
-  Pundit http://thepund.it
-  Transcribo http://transcribo.org/en/ 
- Transkribus https://transkribus.eu/Transkribus/
-  Versioning Machine http://v-machine.org
-  WMRCRE http://vmrcre.org
-  Zooniverse https://www.zooniverse.org

More Digital Tools and Environments can be found on dedicated lists and
in catalogs, for example:

-  TEI-Wiki Editing Tools
  (https://wiki.tei-c.org/index.php/Category:Editing_tools
  (https://wiki.tei-c.org/index.php/Category:Editing_tools)) ( last
  modified on 2015-02-20)
-  DIRT ([http://dirtdirectory.org](http://dirtdirectory.org/) (http://dirtdirectory.org/)) (last
  update 2015-04-24)
-  TAPOR 3.0 (http://tapor.ca/home (http://tapor.ca/home))

## XForms

- https://github.com/AlainCouthures/declarative4all XQuery and XForms implementations written in Javascript 
- https://github.com/AlainCouthures/xsltforms

> XForms to XHTML+Javascript (AJAX) conversion based on a unique XSL transformation. Suitable server-side (PHP) or client-side (Google Chrome, Edge, Internet Explorer, Mozilla FireFox, Opera, Safari) browser treatment where an XSLT 1.0 engine is available

## XProc

- [Innovimax XProc various inputs and samples](https://github.com/innovimax/xproc)

