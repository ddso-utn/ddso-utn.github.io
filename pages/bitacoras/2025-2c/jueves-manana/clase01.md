---
layout: page
title: Clase 1
description: Jueves Mañana, 2025, Segundo Cuatrimestre
permalink: /bitacoras/2025-2c/jueves-manana/clase-01/
---

# Bienvenida

¡Hola!

Ésta página corresponde a la primera clase, y habrá una por cada encuentro. Acá encontrarás apuntes y ejercicios que desarrollamos en clase, además de contenido recomendado para que profundices (o amplíes) lo visto después.
Si bien está pensado para que puedas seguir lo visto estés donde estés, es importante aclarar que éstos contenidos no reemplazan a la cursada, aunque son una buena guía, en especial en el caso de las clases dadas en modalidad virtual.

¡Buen comienzo!

# Quiénes Somos

 * Franco Bulgarelli
 * Débora Fortini
 * Gastón Prieto

# Temario

# Resumen

En este encuentro hablamos de:

 1. Cuestiones administrativas: sobre los [parciales](../../../pautas/sobre-los-parciales.md) y [trabajos prácticos](../../../pautas/sobre-los-trabajos-practicos.md).
 2. Algunos conceptos fundamentales sobre arquitectura:
    * Distribución: existen arquitecturas centralizadas en las que todo está en una única computadora, y arquitecturas en descentralizadas en las que los componentes software están distribuidos en una red a lo largo de múltiples computadoras (_nodos_)
    * Arquitecturas de a pares (P2P) y Arquitecturas Cliente-Servidor (estas últimas son las que trabajaremos en la materia)
    * La arquitectura Web: un tipo particular de Cliente-Servidor en que utilizamos el protocolo de comunicación HTTP (nuevamente, la materia versará sobre ésta)
    * Persistencia: su motivación y la existencia de diferentes paradigmas de persistencia. En otras materias se trabajará el modelo relacional, mientras que aquí trabajaremos con el modelo documental (un tipo de paradigma de persistencia no-relacional)
  3. Contextos organizacionales en los que construimos software
  4. El diagrama de despliegue UML, que en su versión más sencilla se compone de:
     * Nodos: agentes de cómputo, interconectados a través de una red, como pueden ser computadoras de escritorio, celulares, dispositivos embebidos, supercomputadoras, servidores instalados en un rack de un centro de cómputos, etc.
     * Componentes: piezas de software que nuestro sistema ejecuta, como pueden ser scripts y programas de procesamiento en  lote, programas interactivos, procesos de larga duración, [demonios](https://es.wikipedia.org/wiki/Daemon_(inform%C3%A1tica)), procesos servidores, etc
     * Actores: agentes que se comunican y disparan interacciones con los nodos del sistema, que pueden ser personas físicas o jurídicas, otros sistemas informáticos o hasta incluso otros seres vivos.
     * Bases de datos
     * Redes

![](https://www.plantuml.com/plantuml/png/IqmkoIzISCx9JCqhIULIuChBJqbL24ujAijC0OfpfIIM92Ob5gSgE049brINn9ByOYukg785NJkuKYuO0oY8eXW0)

  5. La diferencia entre Internet (una red global y pública de computadoras) y la Web (un servicio que permite consular páginas hipervinculadas)
  6. Las principales tecnologías y protocolos de la Web: HTTP, HTTPS, HTML, CSS, JS.
  7. Algunas clasificaciones de las arquitecturas:
     * Procesos de vida corta (scripts, comandos, etc) vs de Vida larga (aplicaciones de escritorio, servidores, `REPLs`/intérpretes, etc)
     * Centralizadas (también llamadas monolíticas) vs Distribuídas
     * Lógicas vs Físicas
     * Arquiteturas Web de cliente liviano vs cliente pesado
        * Dentro de cliente pesado: Frontend vs Backend
        * En general: arquitecturas web "monolíticas" vs "distribuidas"
  8. Una introducción a HTTP, como protocolo cliente servidor basado en texto plano, el cual define operaciones en términos de verbos, cabeceras, rutas, recursos, etc.
  9. Una mención a tecnologías misceláneas que veremos a lo largo del cuatrimestre como DOM, Mongo y Docker.
  10. Una brevísima mención a las arquitecturas lógicas comunes en el mundo de la programación backend.

# Material

 * [Introducción a Arquitectura](https://docs.google.com/document/d/1XaKMrWPA0jntDK29gtEDRw-CoQgWXfHOmdbmihg4MpE/edit?tab=t.0#heading=h.z9jwy1eurzt9)
 * [Introducción al Desarrollo de Software](https://docs.google.com/document/d/10X8VbMkvJ99JOzH2LuIF2DfGQ55IZpO3ba7eT28Ot4o/edit?tab=t.0)


# Tarea

* [¡Repasá Objetos!](https://www.pdep.com.ar/material/apuntes)
* Si aún no usaste Git, es importante que [leas ésta introducción](https://docs.google.com/document/d/1nadC6-rwR2eRC0FYFWuq22pCRyZWXmCiPBuQ0cD-vMI/edit#heading=h.r9wuhoi4rpgq)
* Obligatorio:Instalar [Visual Code](https://code.visualstudio.com/) y git
* Opcional:
  * Instalar [node 22](https://nodejs.org/es/download)
  * Instalar [Mongo 8](https://www.mongodb.com/try/download/community) nativamente o bien utilizando [Docker](https://docs.docker.com/get-started/get-docker/)