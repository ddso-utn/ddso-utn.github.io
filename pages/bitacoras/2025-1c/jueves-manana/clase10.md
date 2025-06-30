---
layout: page
title: Clase 10
description: Jueves Mañana, 2025, Primer Cuatrimestre
permalink: /bitacoras/2025-1c/jueves-manana/clase-10/
---

# Temario

 * Despliegue. Conceptos de infraestructura
 * CI/CD. Contenedores. Dockerización
 * Proceso de Release

# Resumen de clase

### Despliegue y virtualización

En esta clase hablamos sobre la necesidad de desplegar nuestras aplicaciones fuera del contexto de nuestras propias computadoras de desarrollo: si queremos que nuestro sistema quede disponible para cualquier persona en internet, comúnmente vamos a necesitar colocarlo en un nodo servidor accesible desde cualquier lugar en internet.

Este nodo (o nodos) deberá poder estar disponible las 24 horas del día, todos día del año. Si bien es posible hacer esto desde infraestructura completamente propia (ya sea utilizando nuestra computadora de escritorio, una computadora dedicada en nuestro hogar u oficina o un centro de cómputos (_data center_) propio o alquilado en el que tengamos un cierto grado de control de los procesos físicos que allí ocurren), existen múltiples motivos para hacerlo en infraestructura virtualizada y arrendada en la nube, en la modalidad IaaS (todo esto se desarrolla más en DDSI).

Tanto si contamos una infraestructura propia como sobre todo si utilizamos una infraestructura alquilada en la nube, nos interesará hacer al proceso de despliegue lo más repetible posible. De ahí que es común utilizar técnicas de virtualización en el proceso de despliegue, para buscar el entorno en que ejecuta el software sea lo mas homogéneo posible. Docker es una de ellas, y se basa en la idea de contenedores.

### Contenedores y Docker

* Qué es Docker.
* Para qué sirve.
* Comparación con otras herramientas de virtualización: Docker vs VirtualBox y VMWare vs QEMU
* Vínculo entre Docker y el mundo Linux:
  - en Linux corre directamente en el sistema operativo, mientras que en otros sistemas operativos necesitamos una capa de virtualización adicional (igual esto es algo transparante en las distribuciones de hoy en día, pero es importante tenerlo presente al momento de resolver errores).
  - la instalación es diferente en cada sistema operativo. Les dejamos el enlace oficial https://www.docker.com/get-started/.
* Mostrarmos como ejecutar descargar y ejecutar una primera imagen. Inicialmente, ejecutarmos un intérprete de nodejs _dockerizado_


# Material

* [Presentación Docker](....)
* [Apunte Docker](...)
* Instalación Docker

# Tarea

_Sección en progreso_