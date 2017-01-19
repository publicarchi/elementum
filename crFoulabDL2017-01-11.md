---
author: Emmanuel Château-Dutier
since: 2017-01-10
tags: deep learning, computer vision
---

# Notes Foulab, Deep Learning, 11 janvier 2017

h activation du layer

W une métrique

Le plus souvent les mathématiques sont appliquées par des logiciels. Celles-ci déterminent l’apprentissage du système et l’amélioration de la performances.

Les algorithmes sont relativement résistants au bug, même si les gradients ne sont pas pertinents. Faire du checking.

Motivation deep learning modèle neurologique, traitement de la complexité par couches successives dans le cortex humain. Traitement par couches successives d’identification, détection des visages, identenfication des personnes, etc.

Des justification plus formelles. Dans un circuit booléen si restreint le nombre de couches alors besoin d’un nombre d’unité exponentiellement plus important si réduit les couches.

Réussites dans le domaine de la reconnaissance du langage, et vision computationnelle.

Pourquoi entraîner des réseaux neuronaux pas si simples. Certains gradiants peuvent diminuer quand va du haut au bas. Alors peut devenir difficile.

Parfois quand réseaux neuronaux plus importants correspondent trop (overfitting).

Si pas assez performants (underfitting), peut augmenter l’entrainement. Ou bien utiliser de meilleures méthodes d’optimisation.

Si overfitting, alors régularisation. Stochastic dropout. Criblage du réseau : on retire successivement les unités indépendamment.

Batch normalization. A montré que meilleure optimization et régularisation dans les cas de underfitting et overfitting respectivement.

Normaliser les entrée accélère l’entraînement. Elle est appliquée lors de la pre-activation. cf. dia.

## Computer vision (lecture)

Andrej Karpathy

Considérer les images, la vidéo, etc. en nDimension

Hubel et Wiesel, 1959, 1962, 1968 expérimentations pour déterminer ce que pouvait voir un chat.

Neucognitron, Fukushima 1980. Pas de backpropagation même si assez proche des réseaux neuronaux.

LeCun 90s. Gradient-based learning applied to document recognition, 1998. Alors back propagation en plus de la supervision. Circonvolution modèle. LeNet-5

2011, beaucoup de gens au courants de ces modèles mais pas traités à l’échelle. Ne fonctionnaient pas encore bien. Détection de voitures dans les arbres à 99% !!!

Souvent rechercher extraction de features, implémenter chacun de manière différente. De l’espace pour amélioration.

Krizhevsky et Sutskever, Hinton, 2012. ImageNet Classification with Deep Convolutional Neural Networks, 2012. première fois passe à l’échelle avec les idées de LeCun.

Revolution of Depth, passe de 3.57 courts ResNet, 22 couches Google net, etc.

http://karpathy.github.io ConvNet et ImageNet. TLDR Human accuracy is somewhere 2-5% en fonction du temps dont dispose ! 

Réduction de complexité et très bonne qualité des résultats. Transfère Learning fonctionne très bien. Reconnaissance train, transférables.

https://keras.io pour utiliser ces résultats.

ConvNets partout, Google Photo Search, Goddfellow et al 2014. Face versification Taignman et al. Whale récognition Kaggle Challenge. WeveNet and den Oord et al, 2016. Galawy Challenge Dielman.

Atari Game playing, AlphaGo, etc. Convents pour agri.

Usage en art, DeepDream, reddit.com/r/deepdream/

NeuralStyle Gatys et al 2015

Deep Neurol Networks Rival the Representation of Primate IT Cortex for Cor Visual Objet Recognition. Adieu et al, 2014.

Création d’autant de plan d’activation que de couches d’analyse.

Pooling layer fonctionne sur plusieurs taille d’image.

ConvNetJS CIFAR-10

http://cs.stanford.edu/people/karpathy/convnetjs/demo/cifar10.html￼

Yosinski #deepvis

https://github.com/yosinski/deep-visualization-toolbox

http://yosinski.com/deepvis

ImageNet Challenge

AlexNet 2012

ZFNet 2013, basé sur AlexNet. https://www.clarifai.com

VGGNet 2014, meilleur modèle aujourd’hui. Très consommateur de mémoire. Pas le gagnant mais une architecture simple.

2014 GoogLeNet Szegedy et al. plus efficace. Moins de paramètres, car beaucoup moins de couches connectées. Optimiser pour la performance, même si moins élégant que VGGNet.

ResNet, 2015 He et al, introduction de ? Ajout de couches, n’apporte pas forcément de meilleures performances. Un problème d’optimisation dans ce genre d’architecture.

Torch publié par FaceBook. Une des raisons pour laquelle champs évolue très rapidement, très lié au fait que les gens partagent leur code. 

arxiv-sanity.com

apprentissage pour recommandations de papiers !

Précisions sur l’acquisition. NVIDIA DIGITS DevBox Titan X GPUs

https://developer.nvidia.com/devbox

Construire sa machine mais 

Cloud GPUs

Plupart des choses adressables avec Keras. Sinon TensorFlow en second lieu.

Nombreux conseils sur la mise en œuvre et le matériel nécessaire.

aller voir http://karpathy.github.io/neuralnets/

https://openai.com/about/

https://www.quora.com/What-are-the-best-ways-to-pick-up-Deep-Learning-skills-as-an-engineer

https://openai.com/requests-for-research/

https://ycr.org