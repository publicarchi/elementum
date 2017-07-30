---
since: 2017-07
tags: vim
---

# Aide-mémoire Vim

### Circulations

- `h`, `j`, `k`, `l` déplacements
- `w` mot suivant (`W` en ignorant la ponctuation)
- `b` mot précédent (`B` en ignorant la ponctuation)
- `e` fin du mot (`E` en ignorant la ponctuation)
- `$` fin de ligne
- `0` début de ligne
- `^` premier caractère non-blanc
- `H` aller en haut de l’écran
- `M` aller au milieu de l’écran
- `L` aller en bas de l’écran
- `%` aller au caractère correspondant (pour supporter les pairs par défaut utiliser :h matchpairs)
- `gg` aller à la première ligne du document
- `G` aller à la dernière ligne du document
- `5G` aller à la ligne 5
- `fx` aller à la prochaine occurence du caractère x
- `tx` aller à la précédente occurence du caractère x
- `}` aller au prochain paragraphe
- `{` aller au paragraphe précédent
- `Ctrl`+`b` reculer d’un écran
- `Ctrl`+`f` avancer d’un écran
- `Ctrl`+`d` avancer d’un ½ écran
- `Ctrl`+`u` reculer d’un ½ écran

### Suppressions

- `x` effacer le caractère courant
- `X` effacer un caractère à gauche du curseur
- `D` ou `d`+`w` effacer le mot depuis la position du curseur
- `C` ou `c`+`w` idem et mode [insert]
- `d`+`$` effacer le reste de la ligne depuis la position du curseur
- `D` ou `d`+`d` efface la ligne courante
- `r` remplacer un seul caractère

### Changements de modes

- `Esc` passer en mode [commande]
- `i` entrer dans le mode [insert]
- `A` aller en mode [insert] à la fin de la ligne
- `R` entrer en mode [insert] et remplacer le caractère courant
- `u` undo
- `o` ajoute et ouvre une nouvelle ligne sous la ligne courante
- `o` ajoute et ouvre une nouvelle ligne au-dessus de la ligne courante
- `ea` insert après la fin du mot

## Globaux

- `:q` quitter
- `:q!` quitter sans sauver
- `:w` enregistrer
- `:o` ouvrir un fichier
- `:help keyword` obtenir de l’aide sur un mot-clef
- `:close` fermer le panneau courant

## Références

- http://www.nathael.org/Data/vi-vim-cheat-sheet.svg
- [Graphical vi-vim Cheat Sheet and Tutorial](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html)
- https://vim.rtorr.com/lang/fr_fr/