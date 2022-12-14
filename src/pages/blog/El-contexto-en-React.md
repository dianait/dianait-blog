---
layout: "../../layouts/BlogPost.astro"
title:  " 馃摑 El Contexto en React"
description: "React.createContext. Como conseguir un 'estado global' en React sin Redux."
pubDate: "Aug 21 2020"
heroImage: "./img/react.svg"
---

Vamos a conseguir un **estado global** en React con la ayuda de **React.Context**.
React.Context puedes entenderlo como una objeto d贸nde guardar **informaci贸n que se puede compartir** con una serie de componentes a tu elecci贸n.

![El contexto en React](../img/contexto.jpg)

## 馃殌 Empezamos

Creamos un **Contexto** 馃憞

```
馃搧 ./contexts/context.js

import React from  "react"
const  Context  = React.createContext(
    {info : "No tienes acceso a este provider"}
    )
export  default Context
```

Una de las cosas que nos devuelve este Context es un provider. Este objeto _PROVIDER_ tiene que envolver a los componentes que queramos que compartan la informaci贸n. 馃憞

```
馃搧 ./App.js

<Context.Provider value={
    {"info": "Ahora tienes acceso a este provider"}
    }>
    <Component1/>
    <Component2/>
</Context.Provider>
<Component3 />

馃搧 ./components/Compoenente1.js

import Context from "context"
import { useContext } from "react"

const context = useContext(Context)
console.log(context.info)
馃憠 **Ahora tienes acceso a este provider**

```

De esta manera tanto el **Componente1** como el **Componente2** podr谩 acceder a la informaci贸n **sin necesidad de props**.

Si intentamos acceder al valor de info desde un componente que no est谩 dentro del Provider
nos devolver谩 el valor por defecto. El componente3 est谩 fuera del Provider 馃憞

```
馃搧 ./App.js

<Context.Provider value={
    {"info": "Ahora tienes acceso a este provider"}
    }>
    <Component1/>
    <Component2/>
</Context.Provider>
馃憠 <Component3 /> 馃憟


馃搧 ./components/Component3.js

import Context from "context"
import { useContext } from "react"

const context = useContext(Context)
console.log(context.info)
馃憠 **No tienes acceso a este provider**
```

Pero todav铆a podemos ir un poco m谩s lejos creando nuestros propio provider personalizado.

## 馃嵐 Custom Provider

Por ejemplo, para poder tener un **useState** dentro, y compartirlo con toda la aplicaci贸n 馃憞

```
馃搧 ./contexts/context.js
import React,  { useState }  from  "react"

const  Context  = React.createContext({})

export function UserContextProvider({ children })  {
	const  [user,  setUser]  =  useState()
	return (
        <Context.Provider value={{ user, setUser }}>
            {children}
	    </Context.Provider>
    )
}

export  default Context
```

Esta vez envolver铆amos los componenetes con nuestro **Provider personalizado** _UserContextProvider_ de este modo 馃憞

```
馃搧 ./App.js

import { UserContextProvider } from "context"

<userContextProvider>
    <Component1 />
    <Component2 />
</userContextProvider>
<Component3>

馃搧 ./components/Component2.js
const {user, setUser } = useContext(Context)

```

As铆 nos olvidamos de tener que pasarle un objeto value, como si ten铆amos que hacer antes.

Tambi茅n podr铆amos **acceder a la informaci贸n** del usuario y **actualizarla** desde el Componente1 o el Componente2 **sin necesidad de props.**

Y ya tendr铆amos nuestro **Context funcionando** 馃憦

## 猬嗭笍 Mejoras

La idea ser铆a que si el manejo del estado tiene cierta l贸gica se extraiga a un **Custom Hook** y 茅ste sea el que se encargue de comunicarse cn el contexto.

馃憢 Sed buenos, Diana
