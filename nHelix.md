---
since: 2023-09-02
tags: editor, outils
---

# Helix

L’éditeur [Helix](https://helix-editor.com/news/release-23-03-highlights/) est une variante de [Kakoune](https://kakoune.org) implémenté en Rust. Bien que relativement récent, le logiciel présente des fonctionnalités très complètes et comparables à Vim avec le bénéfice de l’utilisation de primitives logiques pour travailler sur le texte. La cohérence des séquences de commandes et les retours visuels offerts par l’interface facilitent beaucoup la prise en main de l’éditeur qui constitue une très bonne option de départ lorsqu’il s’agit d’adopter un éditeur en ligne de commande.

### Installation

Sur Mac, le logiciel est distribué sous la forme d’une image disque ou bien par le gestionnaire de paquets Brew :

```bash
brew install helix
```

### Déclarer Helix comme éditeur par défaut pour Git

Après avoir installé le logiciel, il est possible de le déclarer comme éditeur par défaut pour Git dans le fichier de configuration de Git en ajoutant la ligne la variable core suivante :

```bash
# ~/.gitconfig
[core]
    editor = hx
```

### Documentation et prise en main

Après installation, Helix s’exécute avec la commande `hx`

```bash
hx
```

Documentation : https://docs.helix-editor.com

Exécuter le tutoriel installé avec le logiciel 

```bash
hx --tutor
```

ou dans l’éditeur exécuter la commande `:tutor`

À tout moment, vous pouvez accéder à de l’aide, depuis le mode normal, en tappant : `<SPACE>?`.

Pour réviser, il existe un quiz [Helix Shortcut Quiz](https://tomgroenwoldt.github.io/helix-shortcut-quiz/)

### Configuration des fichiers runtime

Sur Maci et Linux, on fait pointer la variable d’environnement du terminal vers les fichiers runtime

```bash
# ~/.bashrc ou ~/.zprofile
HELIX_RUNTIME=/home/user-name/src/helix/runtime
```

ou alors on créée un lien symbolique dans `~/.config/helix` qui lie vers le répertoire source

```bash
ln -s $PWD/runtime ~/.config/helix/runtime
```

### Configuration des serveurs de langages

Helix propose de riches fonctionnalités pour utiliser des serveurs LSP. 

Installaton des langages https://github.com/helix-editor/helix/wiki/How-to-install-the-default-language-servers

Voir la liste par défaut des serveurs de langages

```bash
hx --health
```

## Commandes utiles

### Modes 

À l’instar d’autres éditeurs en ligne de commande (Vim notamment), Helix propose une interface de travail qui repose sur l’utilisation de modes. Ce fonctionnement peut être déroutant pour le nouvel utilisateur, mais s’avère très productif à l’usage.

Dans un éditeur multimodal, les touches on des effets différents selon le mode sélectionné : par exemple en mode insertion la pluspart des touches insèrent des caractères dans le buffer, mais en mode normal les touches auront un effet différent. Par exemple `w` pourra déplacer le curseur à la fin du mot, `y` (yank) permettra de copier la sélection, `p` (paste) de coller, `u` (undo) d’annuler une opération, ou encore la combinaison de touche `g` suivie de `f` permettra d’ouvrir le nom de fichier sous le curseur.

Les éditeurs qui ne proposent pas de modes privilégient l’insertion afin de faciliter la saisie du texte. Toutefois, ce choix est effectué au détriment de d’autres fonctionnalités qui deviennent sous-optimales parcequ’elles son rendues difficiles d’accès au clavier ou vous obligent à quitter les mains du clavier pour utiliser la souris ou le trackpad. Bien sûr l’insertion doit être optimisée mais l’édition de document nécessite également de nombreux aller-retour à travers le texte ou le code, de multiples opérations de copier-coller ou de reformatage. Un éditeur de texte modal rend alors ces différentes opérations plus accessibles et plus simples à exprimer.

Le fonctionnement d’Helix s’inspire directement du modèle proposé par Maxime Coste pour [Kakoune](https://kakoune.org). Il reprend l’idée de Vim d’envisager l’édition modale comme un véritable langage d’édition. Les commandes sont composables de manière à exprimer des opérations complexes dans un langage qui permet à l’éditeur d’exprimer ses intentions de manière précise. Cette propriété est souhaitble car la pluspart des opérations d’édition sont répétitives. Pouvoir exprimer structurellement ces opérations permet de définir non-seulement des commandes réutilisables mais aussi plus facilement mémorisables.

La grammaire d’Helix repose sur des sélections suivies de verbes en les combinant avec des retours contextuels dynamiques qui permettent de visualiser l’objet courant (la sélection) avant d’y appliquer des changements ce qui permet de corriger les erreurs éventuelles.


Dans Helix, le mode par défaut est le mode normal `NOR`. En mode normal, on peut accéder à de l’aide sur les fonctionnalités possibles en tappant la touche `Espace`.

Depuis le mode normal, on accède au mode de commande en tappant `:`. L’interface propose alors plusieurs options possibles. Un des atouts de l’éditeurs est d’intégrer une aide contextuelle qui facilite la mémorisation des commandes.

Pour quitter le document, tapper `:quit` ou `:q`.

Si des modifications ont été effectuées au document, il est possible de renoncer aux changements en tappant `:quit!` ou `:q!`.

On peut enregistrer un document avec les commandes `:write` ou `:w`. Il est possible de combiner les commandes `:write-quit` ou `:wq`

Pour quitter sans entrer de commande, tapper la touche `Escape` pour revenir au mode normal `NOR`.

L’édition d’un document se fait en mode insertion `INS`. On y accède depuis le mode normal en tappant `i`.

Liste des modes mineurs
- `:` *command mode* pour enter des commandes
- `v` *select (extend) mode* pour faire des sélections complèxes
- `m` *match mode* pour sélectionner et éditer du texte sémantiquement
- `z` *view mode* pour modifier la vue
- `Z` *sticky view mode* pour visualiser un document 
- `g` *goto mode* pour se déplacer rapidement
- `Ctrl-w` *window mode* pour modifier les fenêtres
- `Space` *space mode* pour réaliser diverses actions

### Déplacements dans l’éditeur

Les touches `h` `j` `k` `l` servent à se déplacer dans l’éditeur. Il est toutefois également possible d’utiliser les flêches sur le clavier.

Helix propose une série de commandes inspirées de [Kakoune](https://kakoune.org) qui sont destinées à faciliter le déplacement ou la manipulation de texte dans un document. Ces sélections multiples sont le moyen d’interagir avec l’éditeur grâce à des primitives de manipulation puissantes.

Celles-ci peuvent être combinées entre elles dans des expressions complexes avec des expressions régulières.

- `w` déplace le curseur avant le début du prochain mot (*word*)
- `e` déplace le curseur à la fin du mot (*end*)
- `b` déplace le curseur en arrière au début du mot (*before*)
- `W`, `E`, et `B` déplace le curseur de la même manière mais ne considère que les chaînes de caractères séparées par des espaces en ignorant les tirets et les guillemets.

Le mode mineur *goto mode* permet de naviguer rapidement dans un document
- `ge` aller à la fin du document
- `gh` aller au début de la ligne
- `gl` aller à la fin de la ligne
- `gs` se rendre au premier caractère non-blanc d’une ligne
- `g.` aller aux dernières modifications

### Édition d’un document

L’édition d’un document s’opère habituellement dans le mode insertion `INS`. Depuis le mode normal, tapper `i` pour entrer en mode insertion. La ligne d’information en bas de l’écran affiche désormais `INS`.

D’autres commandes d’insertion permettent de passer en mode insertion :

- `i` insérer un caractère avant la sélection (*insert*)
- `a` insérer un caractère après la sélection (*append*)
- `I` insérer au début de la ligne
- `A` insérer à la fin de la ligne
- `o` ouvrir une nouvelle ligne à la fin de la ligne sélectionnée (*open*)
- `Ò` ouvrir une nouvelle ligne avant la ligne sélectionnée

Suppressions et remplacements

- `d` supprime le caractère au niveau du curseur ou la sélection (*delete*)
- `c` remplace le caractère au niveau du curseur ou la sélection (*change*)
- `wd` efface un mot (*word*, *delete*)
- `wc` change un mot ou la fin d’un mot (*word*, *change*)
- `ec` change la fin d’un mod (*end*, *change*)

Commenter
- `Ctrl-c` commenter ou décommenter la ligne

Autocompléter
- `Ctrl-x` autocompléter

### Déplacements et sélections multiples

Les commandes de déplacement peuvent être précédées par des quantificateurs.
- `2w` déplace le curseur de deux caractères en avant
- `3e` déplace vers la fin du troisième mot en avant.
- `2b` déplace le curseur deux mots en arrière.

Il existe un mode de sélection auquel on accès en tappant `v` (*view*). Pour revenir en mode normal tapper `v` une nouvelle fois.

En mode sélection, tous les déplacements étendent la sélection.

- `x` sélectionne la ligne du curseur
- `2x` sélectionne deux lignes
- `vgld` ou `t<ENTER>d` effacer la fin de la ligne. `v` est utilisé avec `gl` car cette dernière commande ne sélectionne par le texte. `t` (*til*) la nouvelle ligne est représentée par la touche `ENTER`.
- `;` permet d’abandonner la sélection.
- `;d` effacer après avoir réduit la sélection à un seul caractère

- `%` sélectionne l’ensemble du fichier
- `mm` se déplacer à l’élément correspondant (guillemets, crochets, etc.)
- `ms` entourer la sélection par... Par exemple pour entourer un mot par un caractère, `ebms`

### Annulations

- `u` permet d’annuler la dernière action (*undo*)
- `U` refait la dernière action (*redo*)

Les commandes peuvent être utilisées plusieurs fois de suite

### Copier/coller

- `y` copier la sélection (*yarn*)
- `p` colle la sélection après le curseur (*paste*)

- `xy` copier une ligne

Dès lors que du texte est supprimé (`d`) ou modifié (`c`), Helix copie le contenu altéré. On peut empêcher ce comportement avec `Alt-d` et `Alt-c`. Sur Mac, la touche Alt n’existe pas par défaut dans votre terminal. Il faut activer son replacement dans les préférences du terminal.

Helix ne partage pas son clipboard avec presse-papier avec le système. Néanmoins il est possible avec `Space + y` de copier dans le presse-papier du système pour réutiliser la sélection dans une autre application.

### Rechercher dans un fichier

- `/` recherche en avant dans un fichier, après avoir tappé la chaîne recherchée confirmer avec entrée
- `n` accède au résultat suivant (*next*)
- `N` accède au résultat précédent 
- `?` réalise une recherche en arrière

- `s` permet de faire une sélection au sein de la sélection (tapper la recherche dans le prompt)

- `sfoo<RETURN>cbar<ESC>,` remplace foo par bar en avant dan le fichier

La recherche permet aussi l’utilisation d’expressions régulières. 

Remplacements multiples
- `%s` sélectionne tout le buffer et ouvre une recherche dans la sélection, saisir la recherche ou la regex, valider avec la touche ENTER, puis `c` pour saisir la chaîne de remplacement. Quitter la sélection multiple avec `,`.

Chercher le mot sous le curseur
- `Alt-o*n` (s’il y un LSP) ou `be*n`. Lorsqu’il y a un LSP, `Alt-o` étend la sélection au nœud parent dans la syntaxe, puis `*` utlise la sélection comme motif de recherche, `n` va à la prochaine occurence. `b` sélectionne le début du mot, `e` sélectionne la fin du mot.

### Curseurs multiples

- `C` duplique le curseur à la ligne suivante pour éditer deux lignes simultanéemenet
- `Alt-C` fait la même chose au dessus du curseur
- `,` supprime le deuxième curseur 


Il n’y a pas de sélection de bloc avec Helix. Il est possible d’étendre la sélection au dessous avec les mouvements standards et les curseurs multiples `C`.

## Exécuter une commande shell
- `:sh`

Il n’y a pas de marque-page nommés dans Helix, mais il est possible de mémoriser une localisation dans la liste de rebond (*jumplist*) avec `Ctrl-s` puis de revenir à cette localisation en ouvrant la liste avec `<Espace>-j` ou de revenir en arrière dans la liste avec `Ctrl-o` et en avant avec `Ctrl-i`.



## Configuration

Voir la documentation https://docs.helix-editor.com/configuration.html

La lecture ou l’édition de textes longs, réclame souvent un mécanisme de coulée du texte pour éviter les longs lignes (soft-wrap). Depuis mars 2023, il est possible d’activer cette fonctionnalité dans la configuration.

```bash
# ~/.config/helix/config.toml
[editor.soft-wrap]
enable = true
```

Installation de modes d’autocomplétion, et de formatage.

```bash
hx -health # connaître la liste des langages disponibles
```

Il est possible d’ajouter des serveurs de langages.

Pour savoir quels LSP sont nécessaires pour un langage

```bash
hx -health markdown
```

Installer [Marksman](https://github.com/artempyanykh/marksman) pour la prise en charge de Markdown


```bash
# For Terraform (HCL), Bash, Generic YAML, 
# Docker, Docker compose and Ansible
brew install terraform-ls bash-language-server \
             yaml-language-server docker-ls \
             ansible-language-server

# For HTML, json, css, javascript and typescript
npm i -g vscode-langservers-extracted typescript typescript-language-server

# Go official language server
go install golang.org/x/tools/gopls@latest
```

### Personnalisations avancées

Par défaut le navigateur de fichiers ne permet pas de chercher le contenu des documents mais seulement leur nom. L’ajout de ce script dans le profil de votre shell offre une fonction hxs qui règle la question.

Après avoir installé [fzf](https://github.com/junegunn/fzf) et [ripgrep](https://github.com/BurntSushi/ripgrep) avec brew, ajouter les lignes suivantes à votre fichier de configuration de terminal.

```bash
# ~/.zprofile
# Helix Search
hxs() {
	RG_PREFIX="rg -i --files-with-matches"
	local files
	files="$(
		FZF_DEFAULT_COMMAND_DEFAULT_COMMAND="$RG_PREFIX '$1'" \
			fzf --multi 3 --print0 --sort --preview="[[ ! -z {} ]] && rg --pretty --ignore-case --context 5 {q} {}" \
				--phony -i -q "$1" \
				--bind "change:reload:$RG_PREFIX {q}" \
				--preview-window="70%:wrap" \
				--bind 'ctrl-a:select-all'
	)"
	[[ "$files" ]] && hx --vsplit $(echo $files | tr \\0 " ")
}
```

## Références

- [Maxime Coste. Why Kakoune, The quest for a better code editor.](https://kakoune.org/why-kakoune/why-kakoune.html)
- [Helix documentation](https://docs.helix-editor.com/title-page.html)
- [Lorenzo Setale, «Switching to Helix: My Experience and Tips», 2022](https://blog.setale.me/2022/12/27/Switching-to-Helix-My-Experience-and-Tips/)
- [Helix Shortcut Quiz](https://tomgroenwoldt.github.io/helix-shortcut-quiz/)

## Conseils pour la personnalisation

- [Ari Seyhun, Enhanced Helx config, 2023](https://theari.dev/blog/enhanced-helix-config/)
- [Hårek, Tim. « My thoughts on Helix after 6 months ». Tim Hårek (blog), 19 juin 2023.](https://timharek.no/blog/my-thoughts-on-helix-after-6-months)
- [Tim Hårek, Tim. « Helix as a notes tool ». Tim Hårek (blog), 25 août 2023.](https://timharek.no/blog/helix-as-a-notes-tool)
- [Balkan, Aral. « Installing Helix Editor Language Servers ». Aral Balkan (blog), 14 novembre 2022](https://ar.al/2022/11/14/installing-helix-editor-language-servers/)
