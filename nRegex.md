---
tags: regex
---

# Regex



 `\w*(?= )`

`Morand\W?(.*?)(?:\p{Z}?;|$)`

Un chat chien ; deux moutons brebis ;

`un\W?([[:<:]]\w.*)(?:\s?;|$)`

`un\s(.*)(\s?;|$)`

`un\s?(.*)(\s?;|$)`



## Capturer du texte entre parenthèses

``````regex
/\(([^)]+)\)/
``````

Breakdown:

- `\(` : match an opening parentheses
- `(` : begin capturing group
- `[^)]+`: match one or more non `)` characters
- `)` : end capturing group
- `\)` : match closing parentheses

## Sites utiles

- http://www.regexplained.co.uk
- https://regex101.com

## Références

