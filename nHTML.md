# HTML notes diverses

### Utilisation d’une division container

Très souvent la mise en page des pages HTML introduit une division fille de `body`avec une classe `.container`. Cela n’est pas obligatoire et il est toujours possible de styler l’élément `body` avec un sélecteur direct comme cet élément est unique dans une page HTML. L’avantage d’utiliser une division avec une classe conteneur est de faciliter l’utilisation de largeurs négatives, de changement de position ou d’autres styles qui permettent à des éléments d’étendre elur parent.

```css
.container {
  padding: 0 10vw;
}
```

```html
<body class="container">
  <div style="background-color: red">
    This div can't fill the body here without more styles
  </div>
  <div style="background-color: lime; margin: 0 -10vw">
    This div can, using negative margin
  </div>
</body>
```

versus

```css
.container {
  padding: 0 10vw;
}
```

```html
<body>
  <div class="container" style="background-color: red">
      By moving the class to a div inside the body, we can have elements stretch the page without resorting to negative margin.
  </div>
</body>
```

cf. https://stackoverflow.com/questions/77362203/why-use-div-class-container-just-below-the-body-element-in-html-instead-of-p