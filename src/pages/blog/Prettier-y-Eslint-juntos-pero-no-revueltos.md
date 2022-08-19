---
layout: "../../layouts/BlogPost.astro"
title: "📝 Prettier y Eslint juntos, pero no revueltos"
author: "DianaIT"
pubDate: "Nov 08 2020"
heroImage: "./img/eslint.svg"
description: "Utliza los mejor de los dos en tus proyectos."
---

**Prettier** y **ESLint** se pelean entre ellos porque los dos se preocupan por **formatear tu código**, pero con la configuración adecuada puedes tener lo mejor de cada uno en todos tus proyectos.

#### 📔 RESUMEN

1️⃣ PRETTIER

```javascript
1. npm install prettier -D
2. Crear .prettierrc.json en ./
3. Actualizar _settings.json_ con
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode",
        "editor.formatOnSave": true
      }
4. Instalar extensión Prettier
```

2️⃣ ESLINT

```bash
1. npm install eslint -D
2. npx eslint --init
3. Instalar exptensión ESLint

```

3️⃣ EVITAR CONFLICTOS

```javascript
1. npm install eslint-config-prettier -D
2. Actualizar .eslintrc.js con "Prettier" en útlimo lugar

  extends: [
            "plugin:react/recommended",
            "standard",
            "prettier"
            ],
```

---

### 📦 Prettier

Prettier **formatea tu código**. La idea original de Prettier es no tener configuración. Pretende **evitar debates de sobre el formateo** de código. Aquí podeis ver lo que dicen en su página oficial.

![Prettier has a few options but we dont want more of them](../img/prettier.PNG)

#### 🔨 Instalación

```bash
npm install prettier -D
```

- Crear archivo de configuración de Prettier _prettierrc.json_ aunque sea vacío.

#### 🎯 Comandos

```bash
npx prettier . --check
# Nos muestra por consola los errores de formateo

npx prettier . --write
# Nos arregla los errores de formateo
```

👌 Estos comandos hacen un checkeo general de todo tu proyecto. Podemos ignorar carpetas creando un archivo **.prettierignore**

- Instalar extensión de Prettier

  ![Plugin de Prettier para VSC](../img/prettierextension.PNG)

Hay que mirar que en _settings.json_ está **esbenp.prettier-vscode** como formateador por defecto.

```javascript
   "editor.defaultFormatter":
    "esbenp.prettier-vscode"
```

### 📦 Eslint

**Encuentra problemas en tu código**. No sólo de formateo, si no también errores como dejar una variable sin usar y cosas así. Automáticamente **puede solucionarte estos problemas**. Evidentemente no lo soluciona todo, pero es una muy buena aproximación.

#### 🔨 Instalación

```bash
npm install eslint -D
# Instala el apquete EsLint

npx eslint --init
# Inicializar ESLint
```

Nos va a hacer una serie de preguntas para configurar ESLint. Si usamos TypeScript, que tipo de errores queremos que contemple... 👌 Puedes ver una configuración explicada por Midudev [aqui](https://youtu.be/EEDRcolSHms?t=499).

Nos pedirá instalar algunas dependencias necesarias y ahora tendremos un archivo _.eslintrc.js_ en la raíz desde nuestro proyecto parecido a este:

![.eslintrc.js](../img/eslint.PNG)

- instalar la extensión eslint

  ![extension ESLint para VSC](../img/eslintextension.PNG)

#### 🎯 Comandos

```bash
npx eslint .
# Nos muestras los errores que encuentra
npx eslint --fix
# Arregla todos los errores que puede solucionar
```

👌 **Formatear al guardar**. Esto no lo hace por defecto. Pero podemos configuarlo en el archivo settings.json.

```javascript
    "editor.formatOnSave": true
```

### 🙌 Evitar conflictos entre ESLint y Prettier

```bash
npm install eslint-config-prettier -D
```

- Añadimos esta nueva configuración **Prettier** en el archivo .eslintrc.js. **Añadirla la última**
  Con poner **Prettier** automáticamente ya detecta que estamos hablando del paquete que acabamos de instalar.

```javascript
// eslintrc.js
  extends: [
            "plugin:react/recommended",
            "standard",
            "prettier"
            ],
```

Estas configuración desactivar todas la reglas de **ESLint** que entren en conflicto con las de Prettier. Éste será ahora el encargado de formatear tu código.

### 🌟 EXTRA: Pasar ESLint & Pritter antes de commitear

```bash
npx mrm lint-staged
```

mrm es un paquete para **cambiar de forma rápida los archivos de configuración** de un proyecto, como el package.json, por ejemplo.

A este mrm se le pasa el preset de lint-staged que actualiza nuestro package.json con los scripts necesarios para que pase el ESLint y el Prettier antes de ejecutar un commit y nos impida commitear si encuentra algún error.

👌 Sólo lo pasa a los archivos que hemos modificado.

Esto es lo que se añade a nuestro **package.json**

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

### 📚 Sources

- [ESLint](https://eslint.org/docs/user-guide/getting-started)
- [Pretiter](https://prettier.io/)
- [Javascript Standar Style](https://youtu.be/EEDRcolSHms?t=1321)
- [Prettier's Option Philosoply](https://prettier.io/docs/en/option-philosophy.html)
- [Lint-staged](https://github.com/okonet/lint-staged)
