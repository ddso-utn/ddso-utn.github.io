---
layout: page
title: Clase 3
description: Jueves Mañana, 2025, Primer Cuatrimestre
permalink: /bitacoras/2025-1c/jueves-manana/clase-03/
---

# Resumen

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

 * MVC Web del lado del servidor: inspirado en MVC de los 80, pero buscando resolver las limitaciones del modelo cliente servidor. Separación de modelo y vista.
 * MVC (y sus derivados MVP, MVVM) Web del lado del cliente.
 * Modelo de backend en basado en _concerns_ (incumbencias):
    * Presentación, Dominio, Persistencia.
 * Model de backend basado en capas:
    * Servicios. Controladores. Repositorios. "Modelos" y DTOs (objetos anémicos)
 * Modelo OO: se lleva bien con el modelo de _concerns_ y/o MVC y derivados.

### Errores

Como manejarlos y dónde.
  * Excepciones
  * "Capas" superiores / Presentación

# Material

 * [Cualidades de diseño](https://docs.google.com/document/d/14HdvHvS33WqYb6Ak0BGa0IeCTbzeCRSDKs-1Ot-qLDw/edit?tab=t.0). Apunte tomado prestado de DDSi, donde se profundiza el concepto, pero que nos provee un vocabulario útil para la materia.
 * [Presentación cortesía de los Martes noche](https://www.canva.com/design/DAGjWQ_nX6E/_vwL62qHc2FsEnwtYD7j-g/view?utm_content=DAGjWQ_nX6E&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=hf3334dcf89#5), con una breve mención a los principios SOLID, que en general podemos pensar como una reversión de las cualidades de diseño en el contexto de OOP.
 * [Formalización de Convenciones REST básicas](https://github.com/flbulgarelli/http-tutorial/tree/master/tutorial/es#14-recursos)

# Tarea

Si no lo hiciste ya:

 * Leer el [Tutorial HTTP](https://github.com/flbulgarelli/http-tutorial)
 * Leer [Biblioteca vs Framework](https://docs.google.com/document/d/1D_MCoh4J8kL1MAKNlbDgAMu2nYxri-81nZBYOPFWnO0/edit?tab=t.0#heading=h.6ab0fffv8tld)
 * Leer el enunciado del TP
 * Repasá el video de manejo de Dependencias (`npm`) y flujos de trabajo con `git` del sábado pasado

Además:

 * [Leer la nueva versión del tutorial de express](https://docs.google.com/document/d/1Nn6GMzm7bD9tvVi_wGjLbt8X4KEk5IChzXdPpEFK4vY/edit?tab=t.0#heading=h.halhyllz00mo) (la publicaremos pronto)
 * ¡No te olvides de asistir a la próxima clase de los sábados!