---
layout: "../../layouts/BlogPost.astro"
title: "📝  Ir al final de un ScrollView en SwiftUI"
pubDate: "Aug 14 2022"
heroImage: "/img/swiftUI.png"
description: "ScrollViewReader: de retos, listas y chats"
---

agosto ya y todavía no he terminado ningún reto mensual de [Mouredev](https://github.com/mouredev/Monthly-App-Challenge-2022) & [Rviewer](https://go.rviewer.io/dev-firebase-chat-es/?utm_source=mouredev&utm_medium=github_repo&utm_campaign=firebase_chat_mouredev), lo cierto es que empecé el del trivial y el del pomodoro pero la vida se interpuso y no los pude terminar. También tenía un TFG que entregar. Por suerte, ahora ya no. Graduada hace un mes al aparato. 🎓

El reto de este mes es crear un chat en tiempo real con Firebase. Allá vamos... Voy a ir compartiendo las cositas que aprendo para la realización de esta aplicación. Y la primera es el componente ScrollViewReader de SwiftUI.

### 💬 Situación

Tengo un scrollView con todos los mensajes del chat, pero cuando arranco la aplicación el scroll se queda en la parte de arriba, donde están los mensajes más antiguos. Quiero que el scrollView esté siempre ubicado en la parte de abajo dónde están los mensajes más recientes, al arrancar la aplicación pero también cuando reciba un nuevo mensaje.

### 🛠️ ¿Cómo lo hacemos?

Desde iOS 14 podemos movernos a un elemento en concreto dentro de un ScrollView gracias a ScrollViewReader. Este componente debe envolver a un ScrollView. Y hay varias fromas de hacerlo:

❌ La primera que he encontré no me acaba de gustar porque añadía elementos a la vista inecesarios. Se trata de crear un texto vacío con un identificador concreto al final del ScrollView y scrolleaba hasta ese texto vacío. Funcionar funciona pero... Meh!

✅ La segunda manera que encontré en la maravillosa [Hacking with swift](https://www.hackingwithswift.com/), página que si no conoceis os recomiendo muchísimo. Con esta aproximación podeis hacer scroll a cualquier elemento de la lista sabiendo su identificador.

- 1️⃣ Añadir la propiedad id a cada elemento de la lista
- 2️⃣ Desplazar el scroll hasta el elemento deseado, en nuestro caso el último del array de chats. Para esto hemos hecho una función que comprueba el ultimo id de la lista de chats. Recibe como parametro un ScrollViewProxy que es el que nos permitirá movernos por el scrollView.

![scrollTo with animation code](../code/scrollDown.png)

Pero... ¿Dónde ejecutamos está función?

- 3️⃣ Gracias a la función _onChange_ vamos a estar observando el número de chats, para que cuando cambie al añadir un nuevo chat se desplace hasta éste último.

Pero también necesitamos que haga esto mismo cuando se renderice la vista, así que en el hilo principal, para asegurarnos de tener ya los chats cargados, vamos a ejecutar la función scrollDown.

- 4️⃣ En la función _onAppear_ vamos a ejecutar la función scrollDown de nuevo.

![scrollTo with animation code](../code/scrollViewReader.png)

📰 EXTRA! Se puede añadir también animación al efecto del scroll de la siguiente manera, con la propiedad anchor se especifica donde se quedará el elemento después de la animación:

![scrollTo with animation code](../code/withAnimation.png)

📚 Sources

- [How to make a scroll view move to a location using ScrollViewReader](https://www.hackingwithswift.com/quick-start/swiftui/how-to-make-a-scroll-view-move-to-a-location-using-scrollviewreader)
- [ScrollViewReader en Swift on tap](https://swiftontap.com/scrollviewproxy)
