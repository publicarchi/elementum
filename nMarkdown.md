# Markdown

Markdown est une syntaxe de balisage légère destinée à l’édition de textes en HTML. Elle permet de gérer des documents textuels au format texte.

## Historique

L’avènement du web est lié à la possibilité offerte à tout à chacun de créer ses propres pages web. La présentation du contenu sur le web utilise un langage de balisage, l’Hypertext Markup Language (HTML).

```html
<!DOCTYPE html>
<html>
		<head>...</head>
    <body>
        <h1>Titre de premier niveau</h1>
        <p>Paragraphe</p>
    </body>
</html>
```

La syntaxe de HTML peut s’avérer lourde pour les auteurs, en particulier lorsque l’on n’utilise pas d’éditeur de code qui permet l’autocomplétion et la fermeture automatique des balises.

En 2004, John Gruber crée (avec Aaron Swartz) le langage **[Markdown](http://daringfireball.net/projects/markdown/)** destiné faciliter la création de contenu en HTML.

> Markdown is a text-to-HTML conversion tool for web writers. Markdown allows you to write using an easy-to-read, easy-to-write plain text format, then convert it to structurally valid HTML.

En proposant des équivalents simples aux balises HTML, markodwn propose un balisage léger des textes facile à lire et à écrire.

```markdown
# Titre de premier niveau

Texte balisé avec un *italique*, du **gras**. Un [hyperlien](https://www.xxx)

## Titre de deuxième niveau

Liste
- item 1
- item 2
```

D’après Gruber

> A Markdown-formatted document should be publishable as-is, as plain text, without looking like it’s been marked up with tags or formatting instructions.

Si la syntaxe n’a jamais évolué, elle n’a jamais fait l’objet s’une standardisation par son auteur. Avec l’apparition de besoins divers, plusieurs formalismes sont apparus.

- [GitHub Flavored Markdown (GFM)](https://guides.github.com/features/mastering-markdown/)
- [Kramdown](http://kramdown.gettalong.org/) pour Ruby
- [Markdown Extra](https://michelf.ca/projects/php-markdown/extra/) pour PHP
- [MultiMarkdown](https://github.com/fletcher/MultiMarkdown/wiki/MultiMarkdown-Syntax-Guide)
- [Pandoc’s Markdown](https://pandoc.org/MANUAL.html#pandocs-markdown) contient des extensions implémentées en R
- cf. [Markdown Variants](https://www.iana.org/assignments/markdown-variants/markdown-variants.xhtml)

Face à cette diversité, [CommonMark](https://commonmark.org) est une tentative de standardisation.

## Utilisation de MarkDown

Un simple éditeur plein-texte suffit pour écrire du MarkDown. Vous pouvez utiliser l’éditeur de texte brut fourni par défaut sur votre système d’exploitation TextPad sur Windows ou TextEdit sur Mac, ou n’importe quel éditeur de texte sur Linux. N’importe quel éditeur de code fera également l’affaire ([Codium](https://vscodium.com) [logiciel libre], [VSCode](https://code.visualstudio.com), ou [Zed](https://zed.dev) ou encore [Helix](https://helix-editor.com), [Vim](https://www.vim.org), ou [emacs](https://www.gnu.org/software/emacs/), etc.). Toutefois, pour un plus grand confort d’écriture, il est préférable d’utiliser un des nombreux éditeurs spécialisés existants comme [Zettlr](https://www.zettlr.com) [logiciel libre], [Obsidian](https://obsidian.md) ou [Typora](https://typora.io).

### Syntaxe de base

@todo

Titres

Bloc de citation

Microtypographie

Hyperliens

Images

Blocs de code

Notes

### Gestion des métadonnées

Avec certaines syntaxes MarkDown, il est possible de fournir des métadonnées en reseignant une entête dans un bloc avec la syntaxte YAML Ain't Markup Language  (YAML).

Le bloc YAML commence et se termine toujours par trois tirets courts, il doit nécessairement apparaître dans la première ligne du document.



## Convertir les documents

De nombreux outils de conversion existent pour travailler à partir de ses documents MarkDown.

[Pandoc](https://pandoc.org) est une des solutions les plus employées dans le contexte du travail académique.

Vous pourriez également être intéressés par [Quarto](https://quarto.org).

## Gestion des références bibliographiques



## Liens utiles

- Pochet, Bernard. 2023. *Markdown & vous. L’écriture académique au format texte avec Markdown et Pandoc*. ULiège Library. https://doi.org/10.25518/978-2-87019-318-1.
- Tenen, Dennis, et Grant Wythoff. 2014. « Rédaction durable avec Pandoc et Markdown ». *Programming Historian*, mars 19. https://programminghistorian.org/fr/lecons/redaction-durable-avec-pandoc-et-markdown.
- « Markdown Guide ». s. d. Consulté le 5 août 2025. https://www.markdownguide.org/.
- Gruber, John. 2004. « Markdown ». Daringfireball, décembre 17. https://daringfireball.net/projects/markdown/.

https://nicolascasajus.fr/mastering-markdown/#82