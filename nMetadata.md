---
author: emchateau
tags: métadonnées, Mac
---

Comment afficher et supprimer des attributs étendus d'un fichier sur Mac OS



https://fre.applersg.com/how-view-remove-extended-attributes-from-file-mac-os

```
xattr ~/Desktop/samplefile.jpg 
```

```
xattr -d com.apple.metadata:kMDItemIsScreenCapture ~/Desktop/samplefile.jpg
```

```
xattr -dr com.apple.metadata:kMDItemIsScreenCapture ~/Desktop/
```

http://hints.macworld.com/article.php?story=20101206161739274

**xttra -c**
With **-c** option is possible to clear all attributes including their associated values. In case of a downloaded file:



https://hackernoon.com/how-to-change-a-file-s-last-modified-and-creation-dates-on-mac-os-x-494f8f76cdf4