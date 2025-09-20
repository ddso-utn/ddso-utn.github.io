---
layout: page
title: Clase 5
description: Jueves Mañana, 2025, Segundo Cuatrimestre
permalink: /bitacoras/2025-2c/jueves-manana/clase-05/
---

# Temario

 * Intro a testing. Tipos de tests.
 * Intro a Frontend. Concepto de UI. Tipos. Ejemplos
 * Vistas estáticas. Concepto de HTML. Concepto de CSS
 * Interactividad. Eventos. Callbacks
 * DOM
 * Patrones de UI. Componentes. Conceptos
 * Client side vs Server Side.
 * MVC. MVVM.

# Resumen

En esta clase conversamos sobre las siguientes cuestiones:

1. Cliente pesado vs cliente liviano. Repasamos qué lugar ocupan el Frontend y Backend en el contexto de cliente pesado.
2. Analizamos distintas arquitecturas físicas para la construcción del frontend. Estudiamos algunos de los tipos más comunes de UIs en el contexto de las arquitecturas Web cliente pesado:
    * Desktop (de escritorio) vs Web vs Móvil. Diferenciamos UIs de escritorio y móviles nativas vs basadas en navegadores embebidos y tecnologías web.
    * Comparamos los conceptos de aplicación web vs arquitectura Web
3. Profundizamos sobre las aplicaciones (UIs) Web, que son aquellas que desarrollaremos en la materia.
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
4. El navegador: mostramos sus herramientas (_dev tools_):
    * Redes (_Network_)
    * Inspector
    * Almacenamiento (_storage_)
    * Intérprete de JS (_console_)
4. Estudiamos qué es HTML y CSS y para qué sirve cada uno: estructura vs formato. Presentamos algunos ejemplos
5. Dentro del inspector, profundizamos en el uso del editor de CSS y HTML.
6. Mencionamos algunos de los problemas típicos que el frontend debe resolver:
    * UI: _layout_ (disposición de componentes), colores, tipografias, tamaños, márgenes, bordes y rellenos (padding)
    * Integración con el servidor
    * Validaciones. Hicimos hincapié en que mientras las validaciones en el servidor son obligatorias y fundamentales para garantizar la seguridad y consistencia de los datos, en el cliente son opcionales y orientadas a mejorar la experiencia de les usuaries.

# Material

 * [Guía de maquetado Web](https://docs.google.com/document/d/1UoEb9bzut-nMmB6wxDUVND3V8EymNFgOsw7Hka6EEkc/edit?tab=t.0#)
 * [Tutorial de Grid](https://cssgridgarden.com/#es)
 * [Tutorial de Flex](https://flexboxfroggy.com/#es)
