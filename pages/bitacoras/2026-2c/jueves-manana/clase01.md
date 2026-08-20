---
layout: page
title: Clase 1
description: Jueves Mañana, 2026, Primer Cuatrimestre
permalink: /bitacoras/2026-2c/jueves-manana/clase-01/
---

# Bienvenida

¡Hola!

Ésta página corresponde a la primera clase, y habrá una por cada encuentro. Acá encontrarás apuntes y ejercicios que desarrollamos en clase, además de contenido recomendado para que profundices (o amplíes) lo visto después. Si bien está pensado para que puedas seguir lo visto estés donde estés, es importante aclarar que éstos contenidos no reemplazan a la cursada, aunque son una buena guía, en especial en el caso de las clases dadas en modalidad virtual.

¡Buen comienzo!

# Quiénes Somos

 * Franco Bulgarelli
 * Gastón Prieto

# Temario

 - Quienes Somos
 - Contexto de la materia (académico, político, económico, histórico)
 - Modalidad de la materia
 - Tecnologias, Arquitecturas Lógica y Física

## Palabras clave

  * Distribución: existen arquitecturas centralizadas en las que todo está en una única computadora, y arquitecturas en descentralizadas en las que los componentes software están distribuidos en una red a lo largo de múltiples computadoras (_nodos_)
  * Arquitecturas de a pares (P2P) y Arquitecturas Cliente-Servidor (estas últimas son las que trabajaremos en la materia)
  * La arquitectura Web: un tipo particular de Cliente-Servidor en que utilizamos el protocolo de comunicación HTTP (nuevamente, la materia versará sobre ésta)
  * Persistencia: su motivación y la existencia de diferentes paradigmas de persistencia. En otras materias se trabajará el modelo relacional, mientras que aquí trabajaremos con el modelo documental (un tipo de paradigma de persistencia no-relacional)
  * Procesos de vida corta (scripts, comandos, etc) vs de Vida larga (aplicaciones de escritorio, servidores, `REPLs`/intérpretes, etc)
  * Arquitecturas Centralizadas (también llamadas monolíticas) vs Distribuídas
  * Arquitecturas Lógicas vs Físicas
  * Arquiteturas Web de cliente liviano vs cliente pesado
    * Dentro de cliente pesado: Frontend vs Backend
    * En general: arquitecturas web "monolíticas" vs "distribuidas"


# Resumen

## ¿Desarrollo de software?

La "trampa" de llamar a esta materia de esta forma. ¿Qué aprenderemos a desarrollar? ¿Qué no?

 * Aprenderemos a desarrollar solo un tipo de sistema muy particular: Cliente Servidor, Web, Para Internet. Monolítico, Cliente Pesado, Para navegadores, Comercial, OLTP, Software de Larga Vida.
 * Web vs internet. Repaso: La diferencia entre Internet (una red global y pública de computadoras) y la Web (un servicio que permite consular páginas hipervinculadas)
 * Web vs móvil.
 * Web vs desktop.
      * escritorio como tecnología de presentación (pero aún con una arquitectura web, híbrida o simplemente otro tipo de arquitectura distribuida no-web)
        * vscode
        * discord
        * whatsapp
        * el navegador web en sí (browser)
        * ofimática
        * juegos
      * escritorio como arquitectura (concepto clásico)
        * presentación de escritorio
        * no se conecta a internet
        * no utiliza los protocolos de la web
        * no almacena información remota (lo hace por ejemplo en archivos)
        * no computa información en la nube (lo hace todo local)
 * Web vs software de terminal (repls, scripts, programas, etc).
    * aplicaciones de línea de comandos (CLI): sudo, find, grep, cd, git, apt,
    * interactivas (REPL, TUIs): htop, nano, vim, node, python, irb, etc...
 * Procesos de vida corta (scripts, comandos, etc) vs de Vida larga (aplicaciones de escritorio, servidores, `REPLs`/intérpretes, etc)
 * Software de control vs de análisis (OLAP) vs transaccional (OLTP) vs .....
 * Software comercial vs software para servicios públicos vs científico.
  * paréntesis: no estudiaremos cuestiones vinculadas a escala ni de mantenimiento
 * Web vs sistemas distribuidos no principalmente web ni cliente servidor.

Y ahora sí, que entendimos que software NO vamos a desarrollar, empecemos con desarrollo de "software":

Cliente Servidor, Web, Para Internet. Monolítico, Cliente Pesado, Para navegadores, Comercial, OLTP, Software de Larga Vida.

## Arquitectura física

* Repaso arquitectura física: cómo distribuimos los componentes lógicos a través de agentes de cómputo que tienen memoria, procesamiento, almacenamiento y acceso a la red.
* Cliente servidor: hay un nodo que hace peticiones (cliente) y un nodo que responde (servidor). Si esta regla no se cumple, no es cliente servidor. Ejemplo: arquitectura Web, JDBC y ODBC.
  ¿Y web?: son arquitecturas cliente-servidor, donde utilizamos los protocolos de la web (o algún subconjunto de ellos):
    * HTTP/HTTPS para comunicarse (lateralmente, WebSocket, que no es cliente servidor pero está vinculado a la Web)
    * HTML: lenguaje de representación de información
    * CSS: lenguaje de formateo de información
    * JS: lenguaje de programación (ahora vemos como)
    * Tecnologías del navegador: local storage, DOM, CORS, etc......
    * Y otras tecnologías, protocolos y estilos de comunicación de facto asociadas a la web:
        * JWT (tecnología)
        * REST (lo podemos pensar como un protocolo o simplemente un conjunto de buenas práctica de uso de HTTP)

    * nota: el cliente típico en la arquitectura web es el navegador web (browser). Pero hay otros posibles:
      * cliente CLI: `curl` / `wget`
      * aplicaciones de escritorio que por detrás utilicen los protocolos de la web
      * aplicaciones móviles
      * "código" que consuma servicios de la web de forma programática (usando curl, usando bibliotecas específicas para cada lenguaje de programación, etc --->> axios en nuestro caso particular)
* No es el único tipo de arquitectura: también existen, por ejemplo, las arquitecturas de pares (p2p, peer to peer, par a par en inglés). Ejemplos de arquitecturas p2p: ares, torrent, bitcoin
* Cliente liviano y pesado: en que grado tenemos lógica del lado del cliente o no.
* El diagrama de despliegue UML, que en su versión más sencilla se compone de:
    * Nodos: agentes de cómputo, interconectados a través de una red, como pueden ser computadoras de escritorio, celulares, dispositivos embebidos, supercomputadoras, servidores instalados en un rack de un centro de cómputos, etc.
    * Componentes: piezas de software que nuestro sistema ejecuta, como pueden ser scripts y programas de procesamiento en  lote, programas interactivos, procesos de larga duración, [demonios](https://es.wikipedia.org/wiki/Daemon_(inform%C3%A1tica)), procesos servidores, etc
    * Actores: agentes que se comunican y disparan interacciones con los nodos del sistema, que pueden ser personas físicas o jurídicas, otros sistemas informáticos o hasta incluso otros seres vivos.
    * Bases de datos
    * Redes
    * Procesos

![](https://www.plantuml.com/plantuml/png/IqmkoIzISCx9JCqhIULIuChBJqbL24ujAijC0OfpfIIM92Ob5gSgE049brINn9ByOYukg785NJkuKYuO0oY8eXW0)


## Arquitectura lógica

¿Como organizar el código servidor? En esta materia trabajaremos sobre la arquitectura de capas. En clase hicimos una breve presentación de sus cuatro elementos fundamentales (capas): 1. enrutamiento, 2.control, 3. servicios, 4. repositorios y modelos. Mencionamos que (en su forma más básica) una de sus características salientes es la "facilidad" de diseño, al simplificar las decisiones que se pueden tomar comparadas contra una arquitectura de objetos, guiada por el dominio u orientada a incumbencias, lo que permite un desarrollo rápido y por equipos menos formados (con sus evidentes y no tan evidentes consecuencias negativas). En la materia diseño profundizaremos más sobre arquitecturas guiadas por el dominio y orientadas a incumbencias; acá buscaremos presentar la arquitectura de capas a modo de contrapunto.

¿Y como organizar el codigo cliente? Lo veremos más adelante, pero adelantamos que trabajaremos sobre patrones de UI reactivos (como los que proponen React y Vue), en contraposición a arquitecturas MVC clásicas y sus derivados como MVVM.

## Tecnologías: JavaScript y Node

 * Hablamos sobre los entornos de ejecución de JS: navegador (ejemplo, webkit), vs servidor (node)
 * Mencionamos brevemente la existencia de tecnologías para exponer y consumir APIs HTTP: express y axios/fetch.

## Contextos organizacionales

También conversamos contextos organizacionales en los que construimos software:

 * Software comercial
 * Software para el estado / público
 * Software "activista" / para fundaciones / ONGs
 * Software científico

Y sobre sus posibilidades y restricciones en cada uno.

También hicimos un brevísimo racconto histórico hablamos de como el horizonte del desarrollo de software ha ido mutando a lo largo de las últimas tres décadas, pero sobre todo nos concentramos en las tecnologías y modos que surgieron a partir de 2008 y se cimentaron en la década de 2010-2020. Mencionamos su relación con la cultura "startup", sus fuentes de financiamiento tras los rescates a los bancos de 2008, la momentánea expansión frenética durante la pandemia de estos modelos y su caída final hacia 2022-2023 con el fin de la pandemia, la guerra de Ucrania y el advenimiento de las tecnologías generativas de consumo masivo (las mal llamadas "IA"s). Todo esto no sólo ha cambiado la forma de construir empresas, sino la reorientación de mercado: de orientado a productos comerciales de consumo masivo a industrias más "pesadas": farmacéuticas y alimentos y, en mucha mayor medida, energía, hardware, vigilancia, militar y de "IA".

Finalmente planteamos las incertezas ante nuevas realidades económicos y modos de producción que ya no se adaptan perfectamente con las tecnologías gestadas en la década pasada, pero también señalamos que, en última instancia, las tecnologías basales de la Web también derivan de momentos históricos muy diferentes (mediados y fines de la guerra fría).

# Material

 * Sobre las tecnologías y arquitecturas:
   * [Introducción a Arquitectura](https://docs.google.com/document/d/1XaKMrWPA0jntDK29gtEDRw-CoQgWXfHOmdbmihg4MpE/edit?tab=t.0#heading=h.z9jwy1eurzt9)
   * [Introducción al Desarrollo de Software](https://docs.google.com/document/d/10X8VbMkvJ99JOzH2LuIF2DfGQ55IZpO3ba7eT28Ot4o/edit?tab=t.0)
 * Sobre el contexto
   * [_Is AI Profitable Yet?_](https://isaiprofitable.com/) (sitio que mencionamos brevemente al discutir sobre quien gana y quien pierde con la "IA")
   * [Sobre los costos de infraestructura de Starlink vs ARSAT](https://www.letrap.com.ar/letrae/economia-digital/javier-milei-elon-musk-y-starlink-conectar-escuelas-rurales-costara-casi-el-triple-lo-que-cobra-arsat-n5425583) (lo mencionamos brevemente a modo de ejemplo)
   * [Código de guerra](https://www.naranjacyt.org/articulos/codigo_de_guerra_ed_1_2026.html) (nota de opinión para discutir que toca algunos de los temas que fuimos conversando)
   * Dos libros breves: Tecnofeudalismo de Yanis Varoufakis y Teoría de la dependencia Digital, de Cecila Rikap

# Tarea

* [¡Repasá Objetos!](https://www.pdep.com.ar/material/apuntes)
* Si aún no usaste Git, es importante que [leas ésta introducción](https://docs.google.com/document/d/1nadC6-rwR2eRC0FYFWuq22pCRyZWXmCiPBuQ0cD-vMI/edit#heading=h.r9wuhoi4rpgq)
* Obligatorio:
  * Instalar [Visual Code](https://code.visualstudio.com/) y git
  * Instalar [node 22](https://nodejs.org/es/download)
* Opcional:
  * Instalar [Docker](https://docs.docker.com/get-started/get-docker/)
  * Instalar [Mongo 8](https://www.mongodb.com/try/download/community) nativamente o bien utilizando Docker
