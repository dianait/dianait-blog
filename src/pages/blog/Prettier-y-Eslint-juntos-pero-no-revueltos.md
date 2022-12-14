---
layout: "../../layouts/BlogPost.astro"
title: "馃摑 Prettier y Eslint juntos, pero no revueltos"
author: "DianaIT"
pubDate: "Nov 08 2020"
heroImage: "./img/eslint.svg"
description: "Utliza los mejor de los dos en tus proyectos."
---

**Prettier** y **ESLint** se pelean entre ellos porque los dos se preocupan por **formatear tu c贸digo**, pero con la configuraci贸n adecuada puedes tener lo mejor de cada uno en todos tus proyectos.

#### 馃摂 RESUMEN

1锔忊儯 PRETTIER

```javascript
1. npm install prettier -D
2. Crear .prettierrc.json en ./
3. Actualizar _settings.json_ con
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode",
        "editor.formatOnSave": true
      }
4. Instalar extensi贸n Prettier
```

2锔忊儯 ESLINT

```bash
1. npm install eslint -D
2. npx eslint --init
3. Instalar exptensi贸n ESLint

```

3锔忊儯 EVITAR CONFLICTOS

```javascript
1. npm install eslint-config-prettier -D
2. Actualizar .eslintrc.js con "Prettier" en 煤tlimo lugar

  extends: [
            "plugin:react/recommended",
            "standard",
            "prettier"
            ],
```

---

### 馃摝 Prettier

Prettier **formatea tu c贸digo**. La idea original de Prettier es no tener configuraci贸n. Pretende **evitar debates de sobre el formateo** de c贸digo. Aqu铆 podeis ver lo que dicen en su p谩gina oficial.

![Prettier has a few options but we dont want more of them](../img/prettier.PNG)

#### 馃敤 Instalaci贸n

```bash
npm install prettier -D
```

- Crear archivo de configuraci贸n de Prettier _prettierrc.json_ aunque sea vac铆o.

#### 馃幆 Comandos

```bash
npx prettier . --check
# Nos muestra por consola los errores de formateo

npx prettier . --write
# Nos arregla los errores de formateo
```

馃憣 Estos comandos hacen un checkeo general de todo tu proyecto. Podemos ignorar carpetas creando un archivo **.prettierignore**

- Instalar extensi贸n de Prettier

  ![Plugin de Prettier para VSC](../img/prettierextension.PNG)

Hay que mirar que en _settings.json_ est谩 **esbenp.prettier-vscode** como formateador por defecto.

```javascript
   "editor.defaultFormatter":
    "esbenp.prettier-vscode"
```

### 馃摝 Eslint

**Encuentra problemas en tu c贸digo**. No s贸lo de formateo, si no tambi茅n errores como dejar una variable sin usar y cosas as铆. Autom谩ticamente **puede solucionarte estos problemas**. Evidentemente no lo soluciona todo, pero es una muy buena aproximaci贸n.

#### 馃敤 Instalaci贸n

```bash
npm install eslint -D
# Instala el apquete EsLint

npx eslint --init
# Inicializar ESLint
```

Nos va a hacer una serie de preguntas para configurar ESLint. Si usamos TypeScript, que tipo de errores queremos que contemple... 馃憣 Puedes ver una configuraci贸n explicada por Midudev [aqui](https://youtu.be/EEDRcolSHms?t=499).

Nos pedir谩 instalar algunas dependencias necesarias y ahora tendremos un archivo _.eslintrc.js_ en la ra铆z desde nuestro proyecto parecido a este:

![.eslintrc.js](../img/eslint.PNG)

- instalar la extensi贸n eslint

  ![extension ESLint para VSC](../img/eslintextension.PNG)

#### 馃幆 Comandos

```bash
npx eslint .
# Nos muestras los errores que encuentra
npx eslint --fix
# Arregla todos los errores que puede solucionar
```

馃憣 **Formatear al guardar**. Esto no lo hace por defecto. Pero podemos configuarlo en el archivo settings.json.

```javascript
    "editor.formatOnSave": true
```

### 馃檶 Evitar conflictos entre ESLint y Prettier

```bash
npm install eslint-config-prettier -D
```

- A帽adimos esta nueva configuraci贸n **Prettier** en el archivo .eslintrc.js. **A帽adirla la 煤ltima**
  Con poner **Prettier** autom谩ticamente ya detecta que estamos hablando del paquete que acabamos de instalar.

```javascript
// eslintrc.js
  extends: [
            "plugin:react/recommended",
            "standard",
            "prettier"
            ],
```

Estas configuraci贸n desactivar todas la reglas de **ESLint** que entren en conflicto con las de Prettier. 脡ste ser谩 ahora el encargado de formatear tu c贸digo.

### 馃専 EXTRA: Pasar ESLint & Pritter antes de commitear

```bash
npx mrm lint-staged
```

mrm es un paquete para **cambiar de forma r谩pida los archivos de configuraci贸n** de un proyecto, como el package.json, por ejemplo.

A este mrm se le pasa el preset de lint-staged que actualiza nuestro package.json con los scripts necesarios para que pase el ESLint y el Prettier antes de ejecutar un commit y nos impida commitear si encuentra alg煤n error.

馃憣 S贸lo lo pasa a los archivos que hemos modificado.

Esto es lo que se a帽ade a nuestro **package.json**

```javascript
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "*.js": "eslint --cache --fix",
    "*.{js,css,md}": "prettier --write"
  }
```

### 馃摎 Sources

- [ESLint](https://eslint.org/docs/user-guide/getting-started)
- [Pretiter](https://prettier.io/)
- [Javascript Standar Style](https://youtu.be/EEDRcolSHms?t=1321)
- [Prettier's Option Philosoply](https://prettier.io/docs/en/option-philosophy.html)
- [Lint-staged](https://github.com/okonet/lint-staged)
