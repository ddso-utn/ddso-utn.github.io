---
layout: page
title: Clase 8
description: Jueves Mañana, 2025, Segundo Cuatrimestre
permalink: /bitacoras/2025-2c/jueves-manana/clase-08/
---

# Temario

* Logica de servicio (API). Transformaciones. CORS
* Manejo de estado global.
* Logica de dominio visual. Validaciones

# Resumen

* Hablamos de la cabecera `Origin`. Vimos un ejemplo en el que:
  1. accedimos a una página web, que se ubica en una cierta dirección, por ejemplo "www.google.com"
  2. el contenido que se descarga puede contener código javascript. Incluso podríamos podemos abrir la consola y ejecutar nuestro propio código JS. Este código JS podría hacer nuevos pedidos HTTP (incluso sin recargar la pagina).
      1. Este pedido se hace a una nueva dirección
      2. Con el pedido (es decir, la dirección, el cuerpo, parámetros, etc) se envía una cabecera de origen (`Origin`). Esta cabecera contiene la dirección de la página que inició la interacción.
* Hablamos sobre CORS e hicimos una mención al paquete node `cors`.
* Hicimos una mención al paquete `body-parser`
* Repasamos los hooks `useEffect` y `useState`
* Vimos un ejemplo de integración de Axios en nuestra aplicación React. Respondimos a preguntas como:
  * ¿Cómo hago par obtener los datos del servidor?
  * ¿Cuando hago todo esto?
  * ¿Cómo hago para con los datos que traje del servidor, llenar los componentes visuales?
* Trabajamos algunos ejercicios sobre el contador de clicks

# Material

* [Origin en la página de MDN](https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Headers/Origin)
* [CORS en la página de MDN](https://developer.mozilla.org/es/docs/Web/HTTP/Guides/CORS)
* [Contador de Clicks](https://github.com/ddso-utn/contador-clicks) (¡de nuevo!)
    * [Versión en clase](https://github.com/ddso-utn/contador-clicks/tree/en-clase-2)

# Tarea

La siguiente tarea consiste en dos extensiones al ejercicio de contador de clicks. La empezaremos en clase y dejaremos un formulario para que la envíen a medida que la terminen:

1. Hasta ahora venimos llevando registro de la cantidad de clicks. Nos gustaría ahora llevar registro de donde se hizo el click, es decir, guardar también la lista de donde se hizo click. Todo esto también se tiene que mandar al servidor.
2. Queremos que haya una ruta /stats que me de las estadísticas de quienes ganan a lo largo de todas las direcciones IP
