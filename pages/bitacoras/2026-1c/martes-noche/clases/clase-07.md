---
layout: page
title: Clase 7
description: Martes Noche, 2026, Primer Cuatrimestre
permalink: /bitacoras/2026-1c/martes-noche/clases/clase-07/
---

# Clase N°7: Introducción a Frontend
*Desarrollo de Software K3552 (Martes Noche)*

**Fecha: 30 de Septiembre de 2026**

[Link a la presentación de la clase](https://docs.google.com/presentation/d/1GyYSRf6pPjQoZIle0bts07WAV-ziDI0weVD2E4_uTBk/edit?usp=sharing)

# Resumen

En esta clase vimos una **introducción al frontend**, entendiendo cómo se construye la **UI** a partir de diferentes capas.

Primero abordamos el concepto de **vistas estáticas**, explicando el rol de **HTML** para la estructura y de **CSS** para el estilo. Luego, introdujimos la **interactividad** a través de **eventos** en JavaScript, que permiten reaccionar a acciones del usuario y transformar páginas estáticas en dinámicas.

> **Aclaración:** Este documento sirve como material de apoyo/repaso de la clase. Se recomienda ver la grabación y la presentación.

## 📑Índice

- [Introducción](#introduccion)
- 📝[HTML](#html)
- 🎨[CSS](#css)
	- [CSS 1](#css-1)
	- [CSS 2](#css-2)
	- [CSS 3](#css-3)
- [Eventos](#eventos)

<a id="introduccion"></a>
## Introducción

Hasta ahora trabajamos en la implementación de nuestro modelo y en la construcción de la API que lo expone.

Lo que todavía no vimos es cómo el usuario final puede acceder a una representación visual del sistema. Para eso necesitamos definir **vistas**, y esa definición no siempre coincide con la lógica de la API.

Esas vistas deben estar en un formato estándar que los navegadores entiendan y puedan mostrar en pantalla.

La pregunta entonces es: ¿Qué tecnología usamos para esto? La respuesta es **HTML**.

<a id="html"></a>
## 📝 HTML

HTML significa *HyperText Markup Language*. Es un estándar que define la estructura de una página web. Consiste en una serie de elementos que le indican al navegador cómo debe renderizar el contenido.

Cada elemento está compuesto por una etiqueta, que puede tener contenido y atributos. Las etiquetas suelen abrirse con `<nombre>` y cerrarse con `</nombre>`, aunque algunas no requieren cierre (se las conoce como *empty tags*). Además, los atributos permiten aportar información adicional, como por ejemplo `src` en una imagen o `lang` en la etiqueta `<html>`.

La estructura de un documento HTML se representa mediante el **DOM** (*Document Object Model*), que organiza los contenidos como un árbol de nodos. Entre los elementos principales se encuentran:

- `<!DOCTYPE html>`: define que el documento sigue el estándar HTML5.
- `<html>`: representa el elemento raíz de la página.
- `<head>`: contiene metadatos y configuraciones, como el `<title>` o etiquetas para *open graph*.
- `<body>`: define el cuerpo de la página, donde se colocan los elementos visibles: encabezados, párrafos, imágenes, enlaces, etc.

Algunos de los elementos más importantes son:

- Encabezados: `<h1>` a `<h6>`
- Párrafos: `<p>`
- Contenedores: `<div>`
- Estructurales: `<header>`, `<footer>`, `<nav>`, `<section>`, `<aside>`
- Vínculos: `<a>`
- Tablas: `<table>`
- Formularios: `<form>`, `<input>`, `<button>`

<a id="css"></a>
## 🎨 CSS

Por defecto, los navegadores aplicaban un estilo muy básico a cada elemento HTML. Sin embargo, los desarrolladores buscaban maneras de enriquecer el diseño.

Un libro muy popular de los 90s, *“La guía definitiva de HTML”*, enseñaba cómo maquetar páginas paso a paso. Se proponían soluciones rudimentarias, como:

- Usar `<center>` para centrar.
- Usar `<i>` para cursiva.
- Usar `<font>` con atributos como `color` o `size`.

Luego, el layout de las páginas se resolvía mayormente mediante **tablas**, alineando los contenidos dentro de las celdas.

> Un ejemplo clásico es la página de la película *Space Jam* (1996), que todavía se puede visitar en [este link](https://www.spacejam.com/1996/).

Todo esto hacía evidente la necesidad de un lenguaje que separara la estructura del contenido de su presentación: así surgió **CSS (Cascading Style Sheets)**.

---

<a id="css-1"></a>
### CSS 1

En diciembre de 1996 apareció la primera versión de **CSS**. Su finalidad era permitir aplicar estilos y definir la disposición de los elementos en una página web (*layouting*).

Se introdujeron conceptos fundamentales:

- **Selectores** para etiquetas HTML, clases e identificadores.
- La forma de declarar una **regla CSS**, compuesta por un selector y un bloque de declaración, que a su vez incluye propiedades y valores:

  ```css
  h1 {
    color: red;
    font-size: 24px;
  }
  ```

- **Pseudo-clases y pseudo-elementos**, como los estados de un enlace (`:active`, `:visited`).
- El **box model**, que describe los elementos como cajas formadas por contenido, padding, borde y margen.
- El concepto de **cascada**, con reglas de especificidad (y el uso de `!important`).
	- Si dos reglas tienen la misma especificidad, se aplica la última en el código.
	- Importa el orden de los *imports* de hojas de estilo.
- **Unidades de medida**: `px`, `vw`, `vh`, `rem`.

Con CSS 1 se establecieron las bases para estilar páginas de manera consistente, dejando atrás la dependencia de etiquetas HTML usadas con fines de presentación.

---

<a id="css-2"></a>
### CSS 2

En mayo de 1998 se publicó **CSS 2**, que amplió las capacidades introducidas en la primera versión.

Entre sus principales novedades se destacan:

- **Más pseudo-clases y pseudo-elementos**:
	- Pseudo-clases como `:hover`, `:focus` o `:first-child`.
	- Pseudo-elementos como `::before` y `::after`.

- **Posicionamiento**: se incorporó la propiedad `position` con valores `static`, `relative`, `absolute` y `fixed`, además de propiedades relacionadas como `top`, `left`, `bottom`, `right` y `z-index`.

- **Nuevos selectores**:
	- Selector a secas (ejemplo: `h1`).
	- Lista de selectores con comas (ejemplo: `h1, h2`).
	- Descendiente (`div p`) → cualquier `p` dentro de un `div`.
	- Hijo directo (`div > p`) → solo los `p` que son hijos inmediatos de un `div`.
	- Hermanos generales (`div ~ p`) → cualquier `p` que sea hermano de un `div`.
	- Hermanos adyacentes (`div + p`) → el `p` que aparece inmediatamente después de un `div`.
	- Selector universal (`*`).

---

<a id="css-3"></a>
### CSS 3

A diferencia de las versiones anteriores, **CSS 3** no fue un único documento publicado en un momento puntual, sino que se diseñó como un conjunto de **módulos independientes**.

Los primeros comenzaron a escribirse en 1999, y algunos se estandarizaron alrededor de 2011, mientras que otros siguen en revisión.

Entre sus principales aportes están:

- Nuevos **estilos visuales**: bordes redondeados (`border-radius`), fondos más avanzados, gradientes, transparencias (`opacity`, colores RGBA) y sombras en texto o cajas.

- **Transiciones y animaciones**, que agregan dinamismo a las páginas.

- **Herramientas de layout modernas**: **Flexbox** (2009) para organizar elementos en un eje, y **CSS Grid** (2016) para maquetados bidimensionales.

Con CSS3, el diseño web alcanzó un nivel mucho más expresivo y flexible, sentando las bases de las interfaces modernas.

---

<a id="eventos"></a>
## Eventos

Hasta este punto, con HTML y CSS podemos definir la estructura y el estilo de una página web. Sin embargo, el contenido sigue siendo estático.

Para agregar interactividad necesitamos **JavaScript (JS)**, el lenguaje que permite reaccionar a acciones del usuario o a cambios en la página.

Un caso típico es el manejo de **eventos**, como hacer clic en un botón, pasar el mouse sobre un elemento o escribir en un formulario. Por ejemplo:

```html
<button id="miBoton">Haz clic aquí</button>

<script>
  document.querySelector("#miBoton").onclick = () => {
    alert("¡Hiciste clic!");
  };
</script>
```

> Más adelante veremos cómo frameworks como **React** hacen esto todavía más sencillo.
