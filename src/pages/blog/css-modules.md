---
layout: "../../layouts/BlogPost.astro"
title: " 📝 CSS Modules"
description: "Vamos a ver como funciona esto de CSS Modules, y porque mola tanto el CSS scoped."
pubDate: "Aug 07 2020"
heroImage: "./img/cssmodules.png"
---

## ❓ ¿Por qué?

La última versión de Next.js, la [v9.5.0](https://github.com/vercel/next.js/releases/tag/v9.5.0), ha cambiado el CSS que incorporá en su plantilla por defecto pasando de jsx a CSS Modules. Así que vamos a echarle un ojo a ver que va esto.
![ Use CSS and CSS modules in default application template](../img/cssmodulesnext.png)
Como siempre, esto no deja de ser una introducción que me ayuda a interiorizar conceptos más rápidamente.

## 🤷 ¿Qué es?

> _"A CSS Module is a CSS file in which all class names and animation names are scoped locally by default"_

Ficheros CSS con clases de ámbito local por defecto.

## 🌐 ¿Qué significa esto?

No se trata de una especeficacion oficial, es más bien un proceso que se realiza en el paso de **build**. Css modules cambia el nombre de las clases, añandiendole numéritos y letras - [un hash de toda la vida 😄](https://es.wikipedia.org/wiki/Funci%C3%B3n_hash) - para evitar sobrescritura de clases y conflictos de estilos.

Sin CSS Modules cada documento .css tiene un ámbito global, si repetimos una clase en 2 archivos diferentes, 2 clases o 2 elementos html, y tenemos importados los dos archivos no tenemos ningún control sobre los estilos que estamos aplicando a nuestra aplicación.

Bueno, para ser exactos, realmente si lo tenemos, ya que por algo esta lo de **\*Cascading** style sheets.\* Existe una jerarquía que nos dice que el último archivo importando será el ganador, siempre y cuando el selector sea más especifico, pero nos puede dar más de un problema si no controlamos CSS correctamente.

## 🔨 ¿Cómo funciona?

Crea una clase globalmente única compuesta por el nombre del archivo css, el nombre de la clase y un identificador único. Sería algo así.

```javascript
/* styles.module.css */
.foo { color: red; }

/* importación */
import styles from "./styles.css" // CSS MODULES
import "./main.css" // IMPORTACIÓN NORMAL DE CSS
<h1 class={sytles.foo}> CSS </h1>

/* output */
class = "ARCHIVO_CLASE_ID_UNICO"
<h1 class="styles_foo_4xfe1">CSS</h1>
```

## 🤚 A tener en cuenta

- Se recomienda el uso de **camelCase** para el nombrado de las clases, porque la alternativa, **kebab-case** puede causar un comportamiento inesperado al intentar acceder mediante **style.class-name**

```javascript
style.class - name // Puede crear problemas
style["class-name"] // Así se evitarían estos problemas
style.className // camelCase
```

## 🍉 Resumiendo...

> Whenever I start a new component, I know that there are no global styles that will interfere with my work.

[**@ahfarmer**](https://twitter.com/ahfarmer)

**CSS Modules** coge nuestras clases y las hace únicas. Esto nos permite repetir nombres de clases sin miedo a que se produzcan resultados no deseados en el layout de nuestra aplicación.

## 📚 Sources

- [css-modules/css-modules](https://github.com/css-modules/css-modules)

- [What are CSS Modules? A visual introduction](http://javascriptstuff.com/what-are-css-modules/)

- [Create React App · Set up a modern web app by running one command.](https://create-react-app.dev/docs/adding-a-css-modules-stylesheet/)

- [What are CSS Modules and why do we need them? | CSS-Tricks](https://css-tricks.com/css-modules-part-1-need/)
