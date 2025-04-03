---
layout: page
title: Clase 2
description: Jueves Mañana, 2025, Primer Cuatrimestre
permalink: /bitacoras/2025-1c/jueves-manana/clase-02/
---

# Resumen

En esta clase hablamos de lo siguiente:

1. Repaso de JavaScript (ya deberían haber tenido un primer acercamiento el sábado). Se trata de un lenguaje común, que se ejecuta en dos entornos diferentes (en el servidor, mediante `node`, y el cliente, mediante cualquiera de los motores provistos por tu navegador preferido) y ofrece varias herramientas que hacen de puente entre estos. Repasamos algunas de sus características de sintaxis y tipado, mencionamos algunas de sus herramientas (`node`, `npm` / `yarn`) y hacemos una brevísima demo de `node`.
2. ¿Por qué son relevantes ambos entornos? Porque vamos a trabajar en ambos mundos: cliente y servidor.
  1. Esto nos da pié a hacer un repaso de la arquitectura distribuida, cliente servidor, web.
  2. También nos sirve para contar una verdad sobre algo que no profundizamos en el encuentro anterior: el cliente también es un dispositivo.
  3. En la arquitectura Web, el servidor es obligatorio, el cliente no. De hecho, hay diferentes estilos de clientes: livianos (se trabajan en DDSi) y pesados (los trabajamos acá). Los clientes pesados darán origen a una división (técnica, tecnológica, de equipos de trabajo) frecuente en el mundo Web: Front-end y Back-end (no es el mismo sentido que en otras materias).
3. La comunicación entre cliente y servidor se hace a través del protocolo HTTP y (¿el protocolo?) REST. REST como un protocolo sobre otro, REST como un conjunto de buenas prácticas y convenciones. Paréntesis: Redes e Internet.
4. Para gestionar la interacción http necesitamos (o mejor dicho, resultan convenientes) herramientas: comunicarnos "a mano" (a bajo nivel), abriendo sockets y escribiendo texto plano es engorroso. Por eso tenemos Frameworks HTTP como Express. Paréntesis: biblioteca vs framework.
5. Mencionamos el problema del asincronismo (profundizaremos luego)


# Material

 * Tutorial HTTP
 * Herramientas de diagramación: Mermaid y PlantUML

# Tarea

_Sección en progreso_
