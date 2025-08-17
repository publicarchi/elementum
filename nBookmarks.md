---
since: 2025-08-11
tags: signets
---

# Format pour les signets

Les listes de signets ou de favoris (*bookmarks*) ont longtemps été un moyen d’échanger des sources d’information pertinentes sur le web. La plupart des navigateurs proposent des fonctionnalités destinées à organiser des listes de signets. Au milieu des années 2000 plusieurs applications du web social ont été développées autour du partage de liens hypertextes.

## Les annuaires web

Avant l’avènement des moteurs de recherche, les annuaires de liens (*web directory* ou *link directory*) jouaient un rôle fondamental dans la consultation du web. Dmoz et Yahoo! ont longtemps constitué le passage obligé pour débuter toute navigation. 

- [World Wide Web Virtual Library](https://vlib.org) (VLIB) – fut le premier répertoire pour le web, il fonctionna de 1991 à 2005.
- [The Open Directory](https://web.archive.org/web/20100107102839/http://websearch.about.com/od/enginesanddirectories/a/dmoz.htm), aussi connu sous le nom DMOZ (Directory Mozilla), fut fondé en 1999 et était manuellement édité.

cf. https://en.wikipedia.org/wiki/Web_directory

## Netscape bookmarks.html format

```html
<!DOCTYPE NETSCAPE-Bookmark-file-1>
<META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=UTF-8">
<!-- This is an automatically generated file.
It will be read and overwritten.
Do Not Edit! -->
<TITLE>Bookmarks</TITLE>
<H1>Bookmarks</H1>
<DL><p>
...
... lots and lots of boookmark entries
...
</DL><p>
```

https://github.com/go-shiori/shiori/issues/125

« Netscape Bookmark File Format (Internet Explorer) ». s. d. Consulté le 11 août 2025. https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753582(v=vs.85).

« Netscape Bookmarks File Format - FlyingWolFox/Netscape-Bookmarks-File-Parser GitHub Wiki ». s. d. Consulté le 11 août 2025. https://github-wiki-see.page/m/FlyingWolFox/Netscape-Bookmarks-File-Parser/wiki/Netscape-Bookmarks-File-Format.

## Live Bookmarks

Live bookmarks sont des liens internet supportés par RSS. Ils permettent de tracer de manière dynamique des changements apporté à des sources. 

Solution abandonnée par Firefox en 2018

## XML Bookmark Exchange Language (**XBEL**)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE xbel>
<xbel version="1.0">
    <folder folded="no">
        <title>Wikimedia resources</title>
        <folder folded="yes">
            <title>Wikimedia websites</title>
            <bookmark href="https://en.wikipedia.org/">
                <title>Wikipedia</title>
            </bookmark>
            <bookmark href="https://en.wikibooks.org/">
                <title>Wikibooks</title>
            </bookmark>
        </folder>
    </folder>
</xbel>
```

Spécifié en 1998 par une DTD.

Courremment remplacé aujourd’hui par OPML.

## **OPML** (Outline Processor Markup Language)

Type MIME : `application/xml`, `text/xml`, `text/x-opml`

Spécification : http://opml.org/spec2.opml (2006)

Outline Processor Markup Language (OPML) est un format pour la création de listes hiérarchiques (*outline*). Il s’agit d’un standard ouvert qui est souvent utiliser dans le contexte de partage de listes pour la gestion de flux de syndication RSS.

>The purpose of this format is to provide a way to exchange information between outliners and Internet services that can be browsed or controlled through an outliner.

https://en.wikipedia.org/wiki/OPML

https://web.archive.org/web/20070901000000*/http://www.dlese.org/Metadata/opml/2.0/index.htm

https://github.com/imdj/opml-editor

https://www.minifier.org/opml-to-json

## **XOXO** (**eXtensible Open XHTML Outlines**)

https://en.wikipedia.org/wiki/XOXO_(microformat)

Peu pertinent, proche de OPML

## Open Archives Initiative Object Reuse and Exchange (OAI-ORE)

L’Open Archives Initiative Object Reuse and Exchange (OAI-ORE) définit un standard pour la description, l’échange d’aggrégations de ressources web.



## Liens d’intérêt

https://en.wikipedia.org/wiki/Bookmark_(World_Wide_Web)

[shaarli](https://mastodon.xyz/tags/shaarli)