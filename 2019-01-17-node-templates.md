---
title: Sistema simple de plantillas con lodash
slug: node-templates
date: 2019-01-17
tags: node, javascript
---

Mientras creaba este sistema de publicación pensaba en cómo mostrar la información en el navegador. Hay decenas de sistemas de plantillas pero todos me parecen demasiado complicados para lo que andaba buscando.

Encontré un post de alguien con el mismo problema (lamentablemente no guardé la URL) y lo solucionó con [\_.template](https://lodash.com/docs/4.17.11#template). El funcionamiento es súper simple.

La parte buena es que se puede descargar [únicamente el método template](https://www.npmjs.com/package/lodash.template) y no toda la librería.

La única pega que se le puede encontrar es que se han de abrir ficheros en cada llamada. Supongo que será inapreciable a nivel de rendimiento.

Un ejemplo de uso usando _express_.

```javascript
const fs = require("fs");
const lodashTemplate = require("lodash.template");

app.get("/", (req, res) => {
  const post = {
    title: "Hola mundo",
    body: "..."
  };

  const template = fs.readFileSync("./views/post.html", "utf8");
  const html = lodashTemplate(template)({ post });

  res.send(html);
});
```

Para pintar los datos, `post.html` debe incluir las variables con la siguiente sintaxis (se puede configurar leyendo la documentación de _lodash_):

```html
<h1><%= post.title %></h1>
<span><%= post.date %></span> <%= post.body %>
```
