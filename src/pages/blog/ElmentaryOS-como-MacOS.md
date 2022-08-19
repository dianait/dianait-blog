---
layout: "../../layouts/BlogPost.astro"
title:  "🎯 El mail que lo cambió todo"
pubDate: "Jul 13 2019"
heroImage: "./img/elementary.svg"
text: "Hoy vengo de nuevo con algo un poco más personal.
Once upon a time..."
---


No se me ocurre mejor manera de inaugurar este rincón. Si una cosa tenía clara, después de más de 8 años con MacOS, era evitar volver a sufrir windows.

Mi nuevo ordenador tenía que tener linux, porque, seamos sinceras, los precios de un MacBook Pro con alguna configuración interesante se va de madre por mucho.

Elementary OS, basada en Ubuntu, fue la elegida. La versión “MAC” por excelencia para linux. Pero aún faltaban algunas cositas. Puede parecer una tornería, pero era muy importante para mi buscar la experiencia de usuario más próxima a los ordenadores de Cupertino.

#### 🎨 Iconos y temas

[Aquí](https://github.com/codemelinux/Elementary5.0-JunoTheme-ver1.0) podeis descargaros el tema y los iconos. 🙏 Gracias, [Codemelinux](https://github.com/codemelinux).

#### 👷🏾 Instalar Elementary tweaks

- `sudo add-apt-repository ppa:philip.scott/elementary-tweaks`
- `sudo apt-get update`
- `sudo apt-get elementary-tweaks`
- `sudo apt install software-properties-common`

#### 🎶 Cambiar los iconos y los temas

- Abrir como administardor _usr/share/icons_ y pegar la carpeta **Dark-Mode** y **Light-Mode**.
  Ahora lo mismo en _usr/share/themes_ pegando **Sierra-dark**, **Sierra-dark-solid** y **Sierra-light-solid**.

- Abrir preferencias del sistema, y tendremos un icono nuevo llamada **Tweaks** desde el que podremos cambiar el layout a OSX, para que los botones de las ventanas estén a la izquierda.

También podreis cambiar el tema entre el claro y el oscuro, los iconos... Un montón de personalización en unos pocos pasos.

Aquí podéis ver el resultado, la verdad es que no puedo estar más satisfecha, el parecido está muy conseguido.

![escritorio de ElementaryOS](../img/elementarytweaks.png)

Y hasta aquí la primera entrada de muchas, espero. Sed buenos.

📚 _Sources:_

- [How to Install Mac OS X theme on Elementary os 5.0 Juno](https://visionofgeek.com/how-to-install-mac-os-x-theme-on-elementary-os-5-0-juno/)
- [Tweaks](https://github.com/elementary-tweaks/elementary-tweaks)
