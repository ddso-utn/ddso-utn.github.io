---
layout: page
title: Clase 2
description: Jueves Mañana, 2025, Primer Cuatrimestre
permalink: /bitacoras/2025-1c/jueves-manana/clase-02/
---

# Resumen

En esta clase hablamos de lo siguiente:

1. Repaso de JavaScript (ya deberían haber tenido un primer acercamiento el sábado). Se trata de un lenguaje común, que se ejecuta en dos entornos diferentes (en el servidor, mediante `node`, y el cliente, mediante cualquiera de los motores provistos por tu navegador preferido) y ofrece varias herramientas que hacen de puente entre estos. Repasamos algunas de sus características de sintaxis y tipado, mencionamos algunas de sus herramientas (`node`, `npm` / `yarn`) y hacemos una brevísima demo de `node` vs el navegador.
2. ¿Por qué son relevantes ambos entornos? Porque vamos a trabajar en ambos mundos: cliente y servidor.
   1. Esto nos da pié a hacer un repaso de la arquitectura distribuida, cliente servidor, web.
   2. También nos sirve para contar una verdad sobre algo que no profundizamos en el encuentro anterior: el cliente también es un dispositivo.
   3. En la arquitectura Web, el servidor es obligatorio, el cliente no. De hecho, hay diferentes estilos de clientes: livianos (se trabajan en DDSi) y pesados (los trabajamos acá). Los clientes pesados darán origen a una división (técnica, tecnológica, de equipos de trabajo) frecuente en el mundo Web: Front-end y Back-end (no es el mismo sentido que en otras materias).


![](https://www.plantuml.com/plantuml/png/oyjFILK8JYqgoqp9B-82yvnpCbFpIbAvk1Iu4fDByeiKGejB4uioKnMuk60iNJkuAWWD4a8O0m00)

3. La comunicación entre cliente y servidor se hace a través del protocolo HTTP
4. Para gestionar la interacción http necesitamos (o mejor dicho, resultan convenientes) herramientas: comunicarnos "a mano" (a bajo nivel), abriendo sockets y escribiendo texto plano es engorroso. Por eso tenemos Frameworks HTTP como Express. Paréntesis: biblioteca vs framework.
5. Hablamos de dos tipos de interfaces de sistemas...
   1. interfaces gráficas (_UI_)
   2. APIs (interfaz de programación de aplicaciones)
6. ...y de dónde las encontramos en la arquitectura web cliente pesado
   1. servidor: expone APIs
   2. cliente: consume APIs y expone UIs
7. Mencionamos dos tecnologías para interactuar con APIs desde JavaScript:
   1. `axios`: biblioteca para consumir APIs HTTP
   2. `express`: framework para exponer APIs HTTP
8. Mencionamos el problema del asincronismo (profundizaremos luego en las [promesas](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Promise) y las palabras clave `async` y `await`)


# Material

 * La [presentación de sábado sobre JS](https://docs.google.com/presentation/d/1DSlTheHfB-q5oMV98c9DQGYWgjIG6RV38k3JpKeDv7E/edit?slide=id.p1#slide=id.p1)
 * Herramientas de diagramación: [Mermaid](https://mermaid.js.org/) y [PlantUML](https://www.plantuml.com/)
 * La página de https://caniuse.com/

# Tarea

 * [Tutorial HTTP](https://github.com/flbulgarelli/http-tutorial)
 * [Biblioteca vs Framework](https://docs.google.com/document/d/1D_MCoh4J8kL1MAKNlbDgAMu2nYxri-81nZBYOPFWnO0/edit?tab=t.0#heading=h.6ab0fffv8tld)
 * [Leer el tutorial de express](https://docs.google.com/document/d/1Nn6GMzm7bD9tvVi_wGjLbt8X4KEk5IChzXdPpEFK4vY/edit?tab=t.0#heading=h.halhyllz00mo)
 * Leer el enunciado del TP
