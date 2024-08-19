---
title: Configuration des droits pour wordpress
since: 2016
tags: wordpress, cms
---

# Configuration des droits pour Wordpress

Les permissions pour les fichiers et les répertoires sont les suivantes :

```bash
  chown www-data:www-data -R *          # Let apache be owner
  find . -type d -exec chmod 755 {} \;  # Change directory permissions rwxr-xr-x
  find . -type f -exec chmod 644 {} \;  # Change file permissions rw-r--r--
```

Selon les configurations, la permission 775 pour `wp-content`permet au groupe d'écrire dans le répertoire.

## Sources

- <http://codex.wordpress.org/Hardening_WordPress>
