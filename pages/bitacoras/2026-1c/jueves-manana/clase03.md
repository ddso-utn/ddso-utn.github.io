---
layout: page
title: Clase 3
description: Jueves Mañana, 2026, Primer Cuatrimestre
permalink: /bitacoras/2026-1c/jueves-manana/clase-03/
---

# Temario

 * REST
 * Paréntesis: Redes e Internet.
 * Cualidades de diseño: overview. SOLID (mención).
 * Backend: Capa de dominio/Aplicación.
 * Modelo OO. Services. Controllers. Repositories
 * Promises: Mención
 * Manejo de errores
 * Testing. Introducción. Conceptos generales. Estrategias. BDD. TDD.
 * Frameworks web mvc. Livianos y pesados. Ejemplos. Cómo se estructura el servidor (backend).

# Resumen

## Repaso de la clase pasada

Repasamos lo visto la clase pasada y dejamos materiales complementarios:

 * Internet y Redes: https://howdns.works/es/
 * Herramientas: https://developer.mozilla.org/es/docs/Learn_web_development/Extensions/Server-side/Express_Nodejs.
    * ⚠ Ojo, hoy en día otra herramienta común para construir interfaces Web y APIs es `next.js`, pero en la materia trabajaremos con `express` y con (sólo) `react`.
 * Docker: es una herramienta opcional. Si tenés curiosidad, acá dejamos [un tutorial](https://docs.google.com/document/d/16-ZVmZQrCbFDDnEyI8eABSp2rwsw3bz1WYyJ7DM9Rxw/edit?tab=t.0)
 * Concurrencia en node.js: el elemento central de planificación en las aplicaciones node es el _event loop_, que permite la programación concurrente aún con un sólo proceso y un sólo hilo (si utilizaste `poll`, `epoll` o `select` en Sistemas Operativos quizás no te resulte una idea tan novedosa). Podés encontrar más información sobre su funcionamiento en el sitio de la [electiva Arquitecturas Concurrentes](https://arquitecturas-concurrentes.github.io/iasc-book/event_loop) y [en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Execution_model)
  * Axios: aún es pronto para ponerse a trabajar con esta herramienta en profundidad (primero nos concentraremos en exponer APIs HTTP/REST antes que en consumirlas), pero acá dejamos [su documentación en español](https://axios-http.com/es/docs/intro)
  * Express vs node: node es un _entorno de ejecución_, que además de un intérprete y un gestor de paquete cuenta con bibliotecas de bajo nivel. Si bien node permite nativamente programar aplicaciones TCP/HTTP, para programar aplicaciones HTTP/REST es más conveniente utilizar un _framework_ de alto nivel que nos simplifique varias tareas y nos provea de un marco de trabajo para definir rutas.
  * JSON: es un formato basado en texto plano que sirve para representar datos estructurados. MDN nos da [una breve introducción](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Scripting/JSON). A diferencia de otros lenguajes de metadatos similares como XML y YAML, JSON se inspira en la sintaxis de objetos de JavaScript, que sigue la estructura `{ "clave": "valor" }`.
 * [CURL](https://curl.se/): es un cliente HTTP de línea de comandos, útil para usarlo como parte de scripts. Sin embargo para desarrollar y probar APIs te puede resultar útil [Postman](https://www.postman.com/downloads/).

## Proceso de desarrollo

 * Desarrollo iterativo-incremental: este concepto ya lo deberían tener de materias anteriores. Si no, [acá dejamos una breve introducción y comparación con otros enfoques](https://docs.google.com/document/d/11PQO8NPSOV4SW0ZwtFsh4RCtWubuEBV6E5qPicqJNKs/edit?tab=t.0#heading=h.bva2amx4ntdf). En esta materia, siempre asumiremos que trabajamos bajo ese enfoque.
 * Justamente, porque el software mutará todo el tiempo, es fundamental trabajar con herramientas de control de versiones, como `git`, y también con herramientas que permitan dar seguimiento a los problemas y propuestas de mejora que surgen: los _issue trackers_, como por ejemplo Github Issues y Github Projects (dos herramientas que nos acompañarán en el trabajo práctico). Hay muchísimas alternativas, como Jira o Trello (también un servicio en la nube) y [Bugzilla](https://www.bugzilla.org/) y [Mantis](https://mantisbt.org/) (herramientas de código abierto que se pueden instalar localmente)
  * Todas estas etapas son esenciales no sólo para dar soporte a la codificación del proyecto, sino también a la planificación, análisis y prueba.


## Desarrollo Backend

### Redes (de nuevo)

Ya mencionamos [HTTP](https://developer.mozilla.org/es/docs/Web/HTTP) (y su variante encriptada, [HTTPS](https://developer.mozilla.org/es/docs/Glossary/HTTPS)): se trata de un protocolo omnipresente en el mundo de internet (y en particular, la Web, su servicio de _páginas_). Está basado en texto plano, no tiene estado (es _stateless_), y sus elementos fundamentales son los pedidos HTTP, que tienen métodos, rutas, parámetros (opcionales), cuerpos (opcionales) y cabeceras de (pedido y respuesta, también opcionales).

Sobre HTTP se monta REST, que podemos pensarlo tanto como un protocolo de más alto nivel, como simplemente un conjunto de convenciones y buenas prácticas sobre el uso de HTTP, como por ejemplo que los pedidos de tipo `DELETE` serán utilizados para eliminar información, mientras que aquellos de tipo `GET` sólo se usarán para acceder información de forma [idempotente](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent).

Otro elemento importante de REST es la orientación a recursos, que plantea que las rutas HTTP no representan acciones sino contenidos organizados en una estructura arbórea que podemos consultar y operar. No será el foco de la materia aprender las convenciones de REST (tema que si se tratará en mayor profundidad en DDSi), pero sí comenzar a reconocer sus estructuras básicas. A quien quiera saber más le recomendamos consultar la sección sobre REST del Tutorial HTTP, o el libro _RESTful Web Services Cookbook_ de _Subbu Allamaraju_.


### Arquitectura lógica

Cuando hablamos de arquitectura nos encontraremos con múltiples definiciones e interpretaciones.  Una de ellas es la arquitectura física,  que ya trabajamos, que habla de la disposición (despliegue) de nuestros componentes software a lo largo de los distintos modos de una red.

Pero también podríamos hablar de la arquitectura lógica: el diseño de más alto nivel de nuestros componentes software. All´i estudiaremos como los módulos, paquetes, clases e interfaces se organizan en torno en agrupaciones de alto nivel, que comparten tecnológicas, estilos de comunicación,  equipos de trabajo, heurísticas o formas de trabajo.

Tal como existe una gran variedad de arquitecturas físicas, también existen muchos tipos de arquitecturas lógicas, también llamados estilos arquitectónicos o patrones arquitecturales (o cualquier combinación similar de estos términos 😛).

Cada una ya tiene sus propias ventajas y desventajas, detractores y defensores, y no son necesariamente antagónicas.

En el ámbito particular del desarrollo web podemos encontrar dos prominentes (que a su vez de han influenciado históricamente).

- MVC Web del lado del servidor: Inspirado en el patrón _Model-View-Controller_ de los años 80, adaptado a aplicaciones web. La lógica del servidor está dividida en controladores (que manejan la interacción del usuario), modelos (que representan los datos y lógica de negocio), y vistas (que generan las respuestas HTML o datos). Ejemplo clásico: aplicaciones con Ruby on Rails o Django.
- MVC (y derivados MVP, MVVM) Web del lado del cliente: cuando se utiliza un cliente pesado, el patrón MVC puede migrar al navegador. Frameworks como React (aunque no implementa MVC estrictamente), Angular o Vue ofrecen formas de organizar el código del cliente con separación entre lógica, datos y presentación.
- Modelo basado en _concerns_ (incumbencias): organiza el backend en grupos de componentes lógicos como Presentación, Dominio, y Persistencia. Esta separación permite un mayor desacoplamiento y extensibilidad, alineándose muchas veces con prácticas de diseño orientadas a dominio (como DDD).
- Modelo en capas: típicamente incluye capas como Controladores, Servicios, Repositorios y Modelos, y utiliza DTOs para la transferencia de información. Leer el  capítulo 4 del Libro Domain Driven Design de Eric Evans (ver materiales).
- Modelo orientado a objetos (OO): no es un patrón arquitectónico per se, pero se integra bien con los anteriores. Apunta a modelar el dominio a partir de un conjunto de objetos que colaboran sin una estructura a-priori, sino guiada por los requerimientos. En los mundos de MVC o la separación en base a _concerns_,  el modelo puede estar organizando en torno a un dominio de objetos sin otra estructura particular.

Ninguna arquitectura es “la mejor” en forma absoluta. Cada una tiene ventajas y limitaciones, y su elección dependerá del tipo de aplicación, el equipo, las tecnologías disponibles y los requerimientos del negocio.



### Cliente liviano y pesado

  * Pesado: genera (mayormente y en su forma más naíf) genera estructuras aptas para el consumo programático (ejemplo, API REST en JSON/XML) y el cliente lo transforma en HTML.
  * Liviano: el servidor produce HTML mas o menos definitivo, el cliente hace pocas transformaciones o ninguna.

En el mundo `node`, `express` nos sirve como framework para implementar servidores para ambos estilos arquitectónicos. Frameworks como React, Vue o Angular nos servirán para implementar la lógica de presentación en el cliente en el contexto de un cliente pesado.

### Errores

Como manejarlos y dónde.
  * Excepciones
  * "Capas" superiores / Presentación

# Material

 * [Cualidades de diseño](https://docs.google.com/document/d/14HdvHvS33WqYb6Ak0BGa0IeCTbzeCRSDKs-1Ot-qLDw/edit?tab=t.0). Apunte tomado prestado de DDSi, donde se profundiza el concepto, pero que nos provee un vocabulario útil para la materia.
 * [Presentación cortesía de los Martes noche](https://www.canva.com/design/DAGjWQ_nX6E/_vwL62qHc2FsEnwtYD7j-g/view?utm_content=DAGjWQ_nX6E&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=hf3334dcf89#5), con una breve mención a los principios SOLID, que en general podemos pensar como una reversión de las cualidades de diseño en el contexto de OOP.
 * [Formalización de Convenciones REST básicas](https://github.com/flbulgarelli/http-tutorial/tree/master/tutorial/es#14-recursos)
 * _Domain Driven Design (Eric Evans, 2003): Capítulo 4. Isolating the Domain_


# Tarea

Si no lo hiciste ya:

 * Leer el [Tutorial HTTP](https://github.com/flbulgarelli/http-tutorial)
 * Leer [Biblioteca vs Framework](https://docs.google.com/document/d/1D_MCoh4J8kL1MAKNlbDgAMu2nYxri-81nZBYOPFWnO0/edit?tab=t.0#heading=h.6ab0fffv8tld)
 * Leer el enunciado del TP
 * Repasá el video de manejo de Dependencias (`npm`) y flujos de trabajo con `git` del sábado pasado
 * [Introducción al Desarrollo de Software](https://docs.google.com/document/d/10X8VbMkvJ99JOzH2LuIF2DfGQ55IZpO3ba7eT28Ot4o/edit?tab=t.0)

Además:

 * ¡No te olvides de asistir a la próxima clase de los sábados!