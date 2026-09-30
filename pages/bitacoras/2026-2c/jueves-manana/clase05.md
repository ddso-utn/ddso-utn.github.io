---
layout: page
title: Clase 5
description: Jueves Mañana, 2026, Primer Cuatrimestre
permalink: /bitacoras/2026-2c/jueves-manana/clase-05/
---

# Temario

 * Intro a testing. Tipos de tests.
 * Intro a Frontend. Concepto de UI. Tipos. Ejemplos
 * Vistas estáticas. Concepto de HTML. Concepto de CSS
 * Interactividad. Eventos. Callbacks
 * DOM


# Resumen

## Primera parte

En esta primera repasamos los conceptos de testing ya que fuimos adelantando en clases anteriores. Si bien en otras materias trabajamos los conceptos de pruebas unitarias (en el contexto de aplicaciones Web cliente pesado), acá trabajaremos más sobre pruebas de mayor nivel de abstracción. Refrescamos los distintos tipos:

  1. Pruebas unitarias: pruebas una minima unidad lógica. Si bien esto cierra en la teoría, en la práctica tenemos algunas variantes
      1. Pruebas que validan componentes muy simples y que no tienen mayores dependencias
      2. Pruebas que validan componentes que tienen dependencias, pero que a su vez son simples y resulta más sencillo usar esas dependencias reales.
      3. Pruebas que validan componentes que tienen dependencias, pero en las que por su complejidad, su dificultad de instanciación o configuración, porque aún no existen, porque dependden de sistemas externos, porque no son determinísticas o porque tienen un alto costo computacional, decidimos reemplazarlas por un _impostor_, frecuentemente conocidos como _mock_ o _stubs_ ([aunque no son exactamente lo mismo](https://martinfowler.com/articles/mocksArentStubs.html))
  2. Pruebas de integración: pruebas en las que probamos componentes de alto nivel, con características similares a los del punto anterior `1.3`, pero en las que decidimos utilizar los componentes reales para tener una idea más realista de como se comportan las partes del sistema en conjunto. Suelen probar (de forma aislada o en combinación) la integración con:
      1. Las interfaces HTTP
      2. La base de datos
      3. Algunos servicios externos
  3. Pruebas de punta a punta (`e2e`), que pruebas la integración con (casi) todas las partes del sistema, usualmente desde la interfaz gráfica. Lo veremos más adelante.


Como regla general, de cuanto más alto nivel de abstracción, más difícil de escribir y mantener el test es, más lento es, pero más realista es. A la vez, cuanto menor abstracción, más grano fino podremos tener en lo que se valida. Todo esto lleva a que una base de código "sana" tendrá de los tres tipos de tests, siendo usualmente los unitarios los más comunes.


## Segunda parte

En esta parte conversamos sobre las siguientes cuestiones:

### Introducción a la Arquitectura de la UI

1. Analizamos distintas arquitecturas físicas para la construcción del frontend. Estudiamos algunos de los tipos más comunes de UIs en el contexto de las arquitecturas Web cliente pesado:
    * Desktop (de escritorio) vs Web vs Móvil. Diferenciamos UIs de escritorio y móviles nativas vs basadas en navegadores embebidos y tecnologías web.
    * Comparamos los conceptos de aplicación web vs arquitectura Web
2. Profundizamos sobre las aplicaciones (UIs) Web, que son aquellas que desarrollaremos en la materia.
    * Estudiamos el significado de las interfaces adaptativas (responsive) y como a veces esto se utiliza (de forma mas o menos imprecisa) para diferenciarlas de las aplicaciones nativas.
    * Repasamos las tecnologías de la Web: el protocolo HTTP, los lenguajes HTML, CSS, JS, las tecnologías de [_local storage_](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/storage/local) y _session storage_ del navegador, [historial](https://developer.mozilla.org/en-US/docs/Web/API/History_API),  [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CORS), [DOM](https://developer.mozilla.org/en-US/docs/Glossary/DOM), [AJAX](https://developer.mozilla.org/en-US/docs/Glossary/AJAX) /[`fetch`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API), etc
    * Mencionamos las arquitecturas lógicas más comunes para estructurar al frontend:
        * MVC: Modelo, Vista y Controlador
        * MVVM: Modelo, Vista y Modelo de la Vista. Binding bidireccional
        * Arquitecturas reactivas, en que cada componente se encarga de resolver las aproximadamente 3 cuestiones que MVC ataca en componentes independientes: la reacción ante eventos, la ejecución de lógica de dominio y la generación de una nueva (porción de) vista.
    * Mencionamos algunos framework populares (o que supieron serlo):
        * React y Vue, que aplican arquitecturas reactivas
        * Angular 1.x, uno de los grandes frameworks que se utilizaron para construir clientes pasados, hoy ya obsoleto. Aplicaba ideas MVVM.
        * Backbone, un framework que fue muy popular durante los primeros años del 2010, que se basa en MVC.

### Presentación de HTML y el DOM

Estudiamos qué es HTML y CSS y para qué sirve cada uno: estructura vs formato.

En particular HTML (_HyperText Markup Language_) es el lenguaje estándar que los navegadores ofrecen para representar información en la Web. Ofrece una cantidad enorme de elementos diferentes, llamados etiquetadas (_tags_), con una estructura similar a la de XML pero más relajada: no todas las etiquetas se abren y cierran, por ejemplo. Algunas de las etiquetas mas frecuentes de ver son:


- `<html>`: representa el elemento raíz de la página.
- `<head>`: contiene metadatos y configuraciones, como el `<title>` o etiquetas para *open graph*.
- `<body>`: define el cuerpo de la página, donde se colocan los elementos visibles: encabezados, párrafos, imágenes, enlaces, etc.
- `<h1>` a `<h6>`: Títulos
- `<p>`: Párrafos
- `<strong>`, `<em>`, `<code>`: Modificadores semánticos del texto
- `<div>`, `<span>`: Contenedores estructurales (sin semántica)
- `<header>`, `<footer>`, `<nav>`, `<section>`, `<aside>`, `<article>`, `<quote>`: Contenedores semánticos
- `<a>`: Vínculos
- `<table>`: Tablas
- `<form>`, `<input>`, `<button>`: Formularios
- `<img>`, `<video>`: Elementos multimedia


Además, mencionamos algunos de los problemas típicos que el frontend debe resolver:
    * UI: _layout_ (disposición de componentes), colores, tipografias, tamaños, márgenes, bordes y rellenos (padding)
    * Integración con el servidor
    * Validaciones. Hicimos hincapié en que mientras las validaciones en el servidor son obligatorias y fundamentales para garantizar la seguridad y consistencia de los datos, en el cliente son opcionales y orientadas a mejorar la experiencia de les usuaries.

Por último, mencionamos que el DOM es una estructura arbórea, programática y orientada a objetos que nos permite manipular al código HTML que está cargado en el navegador.


### Presentación del navegador

Mostramos sus herramientas (_dev tools_):
    * Redes (_Network_)
    * Inspector
    * Almacenamiento (_storage_)
    * Intérprete de JS (_console_)



# Material

 * [Guía de maquetado Web](https://docs.google.com/document/d/1UoEb9bzut-nMmB6wxDUVND3V8EymNFgOsw7Hka6EEkc/edit?tab=t.0#)
 * [Tutorial de Grid](https://cssgridgarden.com/#es)
 * [Tutorial de Flex](https://flexboxfroggy.com/#es)
