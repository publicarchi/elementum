---
tags: machine learning, computer vision
---

# Annotation pour l’apprentissage automatique

## Common Objects in Context COCO

Le format Common Objects in Context COCO est un format souvent utilisé pour partager des annotations sur les images et les vidéos. Il a été développé dans le cadre du *COCO image and video recognition challenge* pour le [MS COCO dataset](https://cocodataset.org).

Les annotations sont stockées dans un fichier JSON qui contient les informations sur l’image ou la vidéo, le chemin du fichier, ses dimensions et une liste d’objets annotés. 

Le format COCO est très largement utilisé au sein de la communauté de reconnaissance de formes pour l’entraînement et l’évaluation de la détection d’objets et les modèles de classification. Il est également employé dans le développeemnt de nouveau algorithmes d’apprentissage machine.

Chaque objet est représenté sous la forme d’un 

- `info` ce champs contient des métadonnées concernant le jeu de données, sa version, sa description et ses contributeurs
- `licence` contient des informations sur les licences associées avec les images et les vidéos du jeu de données
- `images` contient une liste de dictionnaires qui représente chacun une image dans le jeu de données

Chaque dictionnaire comprend les champs suivants :

- `id` un identifiant unique pour l’image
- `width` la largeur de l’image en pixels
- `height` la hauteur de l’image en pixels
- `file_name` le nom de fichier de l’image
- `licence` la licence associée avec l’iamge
- `date_captured` la date et l’heure où l’image a été capturée (optionnel)
- `coco_url` une URL de l’image sur le site COCO (optionnel)
- `flickr_url` une URL vers l’image sur Flickr (optionnel)
- `annotations` un champ qui contient une liste de dictionnaires représentant chacun un objet annoté dans le dataset.

Chaque dictionnaire contient les champs suivants : 

- `id` un identifiant unique pour l’annotation
- `image_id` l’identifiant de l’image contenant l’objet annoté
- `category_id` l’identifiant de la catégorie (par exemple la classe) de l’objet annoté
- `bbox` une liste de 4 nombres rerpésentant la *bounding box* de l’objet annoté dans le forma [x, y, width, height], où (x, y) décrivent le coin gauche de la zone
- `area` la zone de la *bounding box* en pixels
- `iscrowd` une valeur booléenne indiquant si l’objet annoté fait partie d’un ensemble (optionnel)
- `segmentation` une liste de liste de points représentant le contour de l’objet (optionnel)
- `keypoints` une liste de points clefs sur l’objet, avec leur visibilité et leur position (optionnel)
- `num_keypoints` le nombre de points clefs dans le champs `keypoints` (optionnel)
- `attributes` un dictionnaire d’attributs pour l’objet annoté (optionnel)



“info”: This field contains metadata about the dataset, such as the version, description, and contributor information.

“licenses”: This field contains information about the licenses associated with the images and videos in the dataset.

“images”: This field contains a list of dictionaries, each representing an image in the dataset. Each dictionary includes the following fields:

- “id”: A unique identifier for the image.
- “width”: The width of the image in pixels.
- “height”: The height of the image in pixels.
- “file_name”: The file name of the image.
- “license”: The license associated with the image.
- “date_captured”: The date and time the image was captured (optional).
- “coco_url”: A URL to the image on the COCO website (optional).
- “flickr_url”: A URL to the image on Flickr (optional).

“annotations”: This field contains a list of dictionaries, each representing an annotated object in the dataset. Each dictionary includes the following fields:

https://cocodataset.org

## Utilisation en Python

Le code suivant lit le fichier JSON et extrait la liste des iamegs et des annotations en créant un dictionnaire qui mappe les ID d’images avec leurs label puis itère sur la liste d’mage et charge chacune d’entre elles.

```python
import json
import numpy as np
import cv2

# Load the COCO JSON file
with open("coco.json", "r") as f:
    coco_data = json.load(f)

# Extract the list of images and annotations
images = coco_data["images"]
annotations = coco_data["annotations"]

# Create a dictionary mapping image IDs to labels
label_dict = {}
for annotation in annotations:
    label_dict[annotation["image_id"]] = annotation["category_id"]

# Load the images and labels into memory
X = []
y = []
for image in images:
    # Load the image
    img = cv2.imread(image["file_name"])
    
    # Extract the label for the image
    label = label_dict[image["id"]]
    
    # Add the image and label to the dataset
    X.append(img)
    y.append(label)

# Convert the lists to numpy arrays
X = np.array(X)
y = np.array(y)

# Preprocess the data (e.g., resize, normalize, etc.)
# ...

# Split the data into a training set and a validation set
# ...
```





Document layout analysis (DLA)

PDF > JPG > Feature extraction (IA) > Image feature > Region proposal (IA) + Classifier > Segmented document

Prise en charge 

- mise en page en colonnes
- mise en page complexe
- mise en page tabulaire

## Outils orientés OCR/HTR

[dhSegment](https://github.com/dhlab-epfl/dhSegment)

[PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)

[Kraken](https://github.com/mittagessen/kraken)

[ocropy](https://github.com/tmbdev/ocropy)

## Outils d’annotation

Il existe différents outils d’annotation d’images capables de créer des annotation COCO.

- [VGG Image Annotator (VIA)](https://www.robots.ox.ac.uk/~vgg/software/via/)
- [LabelStudio](https://github.com/HumanSignal/label-studio)
- [LabelImg](https://github.com/HumanSignal/labelImg#) (plus maintenu, voir Label Studio)
- [Coco-annotator](https://github.com/jsbroks/coco-annotator)

Outils propriétaires

- [Labelbox](https://labelbox.com)
- [RectLabel](https://rectlabel.com) outils standalone, utilisation de annotate anything
- [CVAT](https://www.cvat.ai)

## Références

- Manu. « COCO Format , What and How ». *Medium*, 24 décembre 2022. https://medium.com/@manuktiwary/coco-format-what-and-how-5c7d22cf5301.
- Lee, Wei-Meng. « Understanding the COCO Annotation Format for Object Detection ». *Medium*, 5 mai 2023. https://levelup.gitconnected.com/understanding-the-coco-annotation-format-for-object-detection-770081fefa87.