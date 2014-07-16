Créer un disque bootable sur Mac
===

Les commandes sont légèrement différentes sur Mac.

Lister les volumes montés sur le système pour récupérer l'identifiant de la clef.
`diskutil list`

Repérer le chemin du disque du type /dev/disk1
Repérer l'identifiant de la Clef (en majuscule)

Démonter le volume
`diskutil unmount /Volume/NOM VOLUME`

En utilisateur root, formater la clef à partir de l'image disque téléchargée
`dd if=debian-7.5.0-i386-netinst.iso of=/dev/disk1`

!Attention, une erreur de nommage de disque peut avoir des conséquences catastrophiques.

Voir http://www.zen-tech.info/2012/09/creer-une-cle-usb-dinstallation-de-debian-sous-mac-os-x-methode-facile/
