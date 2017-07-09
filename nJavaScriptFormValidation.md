---
since: 2017-07-07
author: emchateau
tags: javascript, formulaires

---

# Validation de formulaire en JavaScript

Plusieurs stratégies sont envisageables pour la validation directe de formulaire. Au lieu d’utiliser un framework, il est également possible d’écrire cette validation directement en JavaScript.

## Contraindre le choix d’une valeur par défaut

On peut facilement contraindre le choix d’une valeur par défaut de manière minimale, lisible et maintenance. Le JQuery utilisé ici peut facilement être réécrit en JavaScript. 

```html
<input data-default-val='my default val'>

<script>
function resetOnEmpty(event) {  
  var elem = event.target;
  if (!elem.value) { 
    elem.value = elem.dataset['defaultVal'];
  }
}

// rewrote in vanilla JavaScript @EC
// $('[data-default-val]').on('blur', resetOnEmpty)
document.querySelectorAll('data-default-val]').addEventListener('blur', resetOnEmpty);
</script>

```

## Ajouter une logique de validation

Considérons maintenant l’ajout d’une logique de validation supplémentaire, par exemple tester la longueur de l’entré, ou bien l’ajout d’un comportement supplémentaire comme alerter l’utilisateur sur le fait que le champ du formulaire ne peut être vide.

Avec JQuery

```html
<input class='warnOnEmpty'>

<style>
  .error-border { 
    border:1px solid red;
  }
</style>

<script>

function warnOnEmptyInput(selectorStr) {
  var elems = $(selectorStr);
  elems.focus(function(){ $(this).removeClass('error-border') });
  elems.blur(function(){ 
    if (!this.value.length) { 
      $(this).addClass('error-border') 
    }
  });
}

warnOnEmptyInput('.warnOnEmpty')
</script>
```

Sans JQuery (@EC)

```html
<input class='warnOnEmpty'></input>

<style>
  .error-border { 
    border:1px solid red;
  }
</style>

<script>
// bug
function warnOnEmptyInput(selectorStr) {
  var elems = document.getElementsByClassName(selectorStr);
  elems.focus(function(){
    this.classList.remove('error-border')
  });
  elems.blur(function(){ 
    if (!this.value.length) {this.classList.add('error-border')}
  });
}

warnOnEmptyInput('warnOnEmpty')
</script>
```



## Références

https://www.sellarafaeli.com/blog/vanillajs_and_jquery_kiss.html