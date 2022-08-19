---
layout: "../../layouts/BlogPost.astro"
title:  " 📝 El Contexto en React"
description: "React.createContext. Como conseguir un 'estado global' en React sin Redux."
pubDate: "Aug 21 2020"
heroImage: "./img/react.svg"
---

Vamos a conseguir un **estado global** en React con la ayuda de **React.Context**.
React.Context puedes entenderlo como una objeto dónde guardar **información que se puede compartir** con una serie de componentes a tu elección.

![El contexto en React](../img/contexto.jpg)

## 🚀 Empezamos

Creamos un **Contexto** 👇

```
📁 ./contexts/context.js

import React from  "react"
const  Context  = React.createContext(
    {info : "No tienes acceso a este provider"}
    )
export  default Context
```

Una de las cosas que nos devuelve este Context es un provider. Este objeto _PROVIDER_ tiene que envolver a los componentes que queramos que compartan la información. 👇

```
📁 ./App.js

<Context.Provider value={
    {"info": "Ahora tienes acceso a este provider"}
    }>
    <Component1/>
    <Component2/>
</Context.Provider>
<Component3 />

📁 ./components/Compoenente1.js

import Context from "context"
import { useContext } from "react"

const context = useContext(Context)
console.log(context.info)
👉 **Ahora tienes acceso a este provider**

```

De esta manera tanto el **Componente1** como el **Componente2** podrá acceder a la información **sin necesidad de props**.

Si intentamos acceder al valor de info desde un componente que no está dentro del Provider
nos devolverá el valor por defecto. El componente3 está fuera del Provider 👇

```
📁 ./App.js

<Context.Provider value={
    {"info": "Ahora tienes acceso a este provider"}
    }>
    <Component1/>
    <Component2/>
</Context.Provider>
👉 <Component3 /> 👈


📁 ./components/Component3.js

import Context from "context"
import { useContext } from "react"

const context = useContext(Context)
console.log(context.info)
👉 **No tienes acceso a este provider**
```

Pero todavía podemos ir un poco más lejos creando nuestros propio provider personalizado.

## 🍹 Custom Provider

Por ejemplo, para poder tener un **useState** dentro, y compartirlo con toda la aplicación 👇

```
📁 ./contexts/context.js
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

Esta vez envolveríamos los componenetes con nuestro **Provider personalizado** _UserContextProvider_ de este modo 👇

```
📁 ./App.js

import { UserContextProvider } from "context"

<userContextProvider>
    <Component1 />
    <Component2 />
</userContextProvider>
<Component3>

📁 ./components/Component2.js
const {user, setUser } = useContext(Context)

```

Así nos olvidamos de tener que pasarle un objeto value, como si teníamos que hacer antes.

También podríamos **acceder a la información** del usuario y **actualizarla** desde el Componente1 o el Componente2 **sin necesidad de props.**

Y ya tendríamos nuestro **Context funcionando** 👏

## ⬆️ Mejoras

La idea sería que si el manejo del estado tiene cierta lógica se extraiga a un **Custom Hook** y éste sea el que se encargue de comunicarse cn el contexto.

👋 Sed buenos, Diana
