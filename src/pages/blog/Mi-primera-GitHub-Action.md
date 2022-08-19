---
layout: "../../layouts/BlogPost.astro"
title: "📝 Mi primera GitHub Action"
pubDate: "Feb 03 2020"
heroImage: "./img/ga_logo.png"
description: "👀 Las posibilidades parecen infinitas, así que ¿Por dónde empezar? Pues por algo facilito, Diana. Así que esta es la historia de como cree mi primera GitHub Action."
---

![GitHub Actions](../img/ga_logo_xl.png)

👋 Una de las cosas que me he propuesto para este 2021 es ser más activa en la comunidad, escribir más por aquí, compartir, comentar, debatir... Y otra de las cosas que me había propuesto era aprender a usar los ya famosísimas y en boca de todos **GitHub Actions**. ¡2️⃣ ❌ 1️⃣ , amigues!

☕ Todo empezó cuando mi hermana me pidió consejo para hacerse una página web sin complicarse la vida... Y, a poder ser, gratis. Pensé en Notion y en exportar el HTML y así poder subirlo a Netlify o similar. Más que nada por evitar esa url tan larga que te da Notion al compartir. Pero claro, cada vez que hiciera un cambio tenía que volver a exportar la página, actualizarla en Netifly... 🧵 Demasiado mandanga para una muggle del desarrollo.

💡 Entonces se me ocurrió una **GitHub Action** para scrapear la página de Notion y actualizarla en GitHub para usar GitHub Pages. Y eso he hecho. Un script en **node.js** que coge el html de la página pública de Notion y actuliza el **index.html** del repositorio. He hecho una prueba con el tutorial que le hice en su momento para subir su página de Notion a Netlify.

## 💻 Desarrollo

Hay que crear un archivo .yml en la siguiente ruta _.github/workflows/_ con el nombre que queramos.
El mio se llama **deploy.yml** y lo dodeis ver [aquí](https://github.com/DianaIT/Tu-pagina-con-Notion-y-Netlify/blob/main/.github/workflows/deploy.yml).

⏲️ Lo más relevante es que esta programada en **schedule** para que se ejecute todos los martes a las 10:00 UTC. Desde [esta página](https://crontab.guru/) podéis comprobar que el valor de _cron_ es el que queréis y no la estáis liando parda. Además al añadir la instrucción **workflow_dispatch** podemos ejecutar el script manualmente desde la sección **actions** del repositorio.

```
on:
  workflow_dispatch:
  schedule:
    - cron: 0 10 * * 2
```

Para ejecutar el script tenemos que definirlo primero en el **package.json**, instalar las dependencias y, por último, pushear para tener la última versión de nuestra página de Notion en el archivo index.html de nuestro repositorio.

✍️ Las comandos se pueden escribir línea a línea con **run:** delante, o mediante el símbolo **|** seguidos. Aquí podéis ver las dos maneras 👇

```
    - run: npm install
    - run: npm run deploy
    - run: |
        git config --global user.name "Dianait"
        git config --global user.email diahdezsoler@gmail.com
        git add .
        git commit -m "Tutorial updated"
        git push
```

Y eso sería todo, nos vemos en 🐦 twitter.

## 🔗 Enlaces

- 🐙 Podeis ver el repositorio [por aquí](https://github.com/DianaIT/Tu-pagina-con-Notion-y-Netlify)

- 📦 He utilizado este paquete de npm [notion-to-html](https://www.npmjs.com/package/notion-page-to-html), y además he aprovechado para hacer 🌟 **mi primera pull-request** 🌟 porque tenían un código hexadecimal mal asignado.

- ⏲️ [Crontab](https://crontab.guru/). The quick and simple editor for cron schedule expressions by Cronitor.
