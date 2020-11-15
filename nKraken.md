# Kraken

## Installation sur mac

𝛱

### Dépendances

Sur Debian

```bash
apt install libpangocairo-1.0 libxml2 libblas3 liblapack3 python3-dev python3-pi
```

Avec Brew

```bash
brew pango
```

```
brew cairo
```

```bash
brew install libxml2
```

```bash
brew install openblas # install libblas3
```

```bash
brew install lapack # install liblapack3
```

```python
pyenv install 3.4-dev # install python3-dev ?
```

Avec Conda

```
curl -O https://raw.githubusercontent.com/mittagessen/kraken/master/environment.yml
```

```
conda env create -f environment.yml
```



```
#
# To activate this environment, use
#
#     $ conda activate kraken
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```



PDF files have to be extracted beforehand using a tool such as `pdftocairo` or `pdfimages`

https://gallica.bnf.fr/ark:/12148/bpt6k1040563h

https://gallica.bnf.fr/iiif/ark:/12148/bpt6k1040561p/f43/full/full/0/native p. 17

Transformer pdf en images

```bash
pdftocairo -png xxxx.pdf
```

Nota, cela ne fonctionne pas avec conda pour un pb de version. cf. https://github.com/conda-forge/paraview-feedstock/issues/85

Sortie TXT

```bash
kraken -i sauvalT01f76.jpg sauvalT01f76.txt binarize segment ocr -m OCR17/Models/Kraken.mlmodel
```

Script de récupération

```sh
#!/bin/sh

if [ $# -lt 3 ]; then
        echo "Usage: $0 radical seq_start seq_end"
        exit
fi

radical=$1
seq_start=$2
seq_end=$3

for fichier in ($3 - $2)
do
        echo $fichier
done
```

```
./seq_wget http://someaddress.com/logs/dbsclog01s%03d.log 1 50
```

avec wget

```
$ wget http://someaddress.com/logs/dbsclog01s{001..050}.log
```

avec curl

Tome 1

https://gallica.bnf.fr/ark:/12148/bpt6k1040561p

```bash
curl https://gallica.bnf.fr/iiif/ark:/12148/bpt6k1040561p/f[120-140]/full/full/0/native -o sauvalT01f#1.jpg
```

Tome 2

https://gallica.bnf.fr/ark:/12148/bpt6k1040563h/

```bash
curl https://gallica.bnf.fr/iiif/ark:/12148/bpt6k1040563h/f[17-50]/full/full/0/native -o sauvalT02f#1.jpg
```

Tome 3

https://gallica.bnf.fr/ark:/12148/bpt6k1040565b

```bash
curl https://gallica.bnf.fr/iiif/ark:/12148/bpt6k1040565b/f[23-50]/full/full/0/native -o sauvalT03f#1.jpg
```



## sed

```bash
sed 's/ſ/s/g' fichier.txt > fichier2.txt
```

```bash
sed -f <fichier_script> [options] 'fonctions' <fichier-entrée>
```

Remplacement des sauts de ligne

```bash
perl -p -0n -e 's/\n/, /g' # Le switch '-0n' indique qu'il n'y a pas de separateur de ligne en  entrée, donc tout le fichier est une seule 'ligne'.  Ensuite, il suffit  de replacer tous les '\n' sur cette 'ligne' par la virgule (et espace  comme dans l'example initial). 
```

```bash
 cat fichier |tr $'\n' ,
```

Concaténer fichiers

```
cat *.txt > all.txt
```

Pour un gd nb de fichiers

```
for i in *.txt;do cat $i >> ../output.txt;done # output in an other dir
```

https://stackoverflow.com/questions/2150614/concatenating-multiple-text-files-into-a-single-file-in-bash

```bash
awk 'NR>1 && FNR==1{print ""};1' ./*.html > /path/to/Final.html # make shure to output in an other dir
```

```bash
awk '(NR>1 && FNR==1){printf ("\n\n")};1' ./*.txt > ../sauval158-200.txt
```



rès de chaussée

assès

assés

d’aujour d’hui

St.

Evêque 

neantmoins

Francois

Hotel

séjour

éme

prës

Li.

en 1..

apres

Ie

aprës

riviere

premiere

troisiéme

quatriéme

Cimetiere

Etaux

Etal

Cesar

Lutece

Ie Ia Iu

Préfets

Arrêts

Gentilhomme Chevalier Sénéchal Empereur

Reine Roi Roy

Capitale Royaume

Evêque Comte Duc Roy Roi Prince Orfevres Regent Chanoine Auteur Prieuré Hopitaux Communautés Chancelier Cardinal

Pont Tour Clocher Maison Palais Eglise Place Bibliotheque Couvent Abbayie Monastere Archevêché Boucherie Coulture Hôtel-Dieu Hôtel Prétoire Cimetiere Forêt Fontaine

Fils Filles

Trône

Conseiller

Religieux

Me 

St

Savant Curieu

## Finales ?

assés