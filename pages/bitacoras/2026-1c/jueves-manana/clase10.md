---
layout: page
title: Clase 10
description: Jueves Mañana, 2026, Primer Cuatrimestre
permalink: /bitacoras/2026-1c/jueves-manana/clase-10/
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
  * Para qué sirve: no es sólo para despliegue, aunque es uno de sus principales casos de usos hoy en día.
  * Comparación con otras herramientas de virtualización: Docker vs VirtualBox y VMWare vs QEMU
  * Vínculo entre 🐋 Docker y el mundo 🐧 Linux:
    - en Linux corre directamente en el sistema operativo, mientras que en otros sistemas operativos necesitamos una capa de virtualización adicional (igual esto es algo transparante en las distribuciones de hoy en día, pero es importante tenerlo presente al momento de resolver errores).
    - la instalación es diferente en cada sistema operativo. Les dejamos el enlace oficial https://www.docker.com/get-started/.
  * Mostrarmos como ejecutar descargar y ejecutar una primera imagen. Inicialmente, ejecutaremos un intérprete de nodejs _dockerizado_

```bash
# -it  sirve para para que lo que escribamos en STDIN sea redirigido al STDIN del contenedor
# --rm sirve para que el contenedor sea eliminado (y no ocupe lugar en nuestro disco innecesariamente)
#      luego de terminar de ejecutar el contenedor
$ docker run -it --rm node:alpine
Unable to find image 'node:alpine' locally
alpine: Pulling from library/node
4abcf2066143: Already exists
2997c4155347: Pull complete
803074618b54: Pull complete
249f9271d1d1: Pull complete
Digest: sha256:d3271e4bd89eec4d97087060fd4db0c238d9d22fcfad090a73fa9b5128699888
Status: Downloaded newer image for node:alpine
Welcome to Node.js v21.6.2.
Type ".help" for more information.
> console.log("¡Hola Mundo Docker!")
¡Hola Mundo Docker!
undefined
^CTRL + C
```

También mostramos que una vez que termina el contenedor ya no hay procesos docker corriendo:

```bash
$ docker ps
```

Sin embargo, si repetimos los pasos anteriores y no terminamos al intérprete, al ejecutar `docker ps` en otra terminal veremos al proceso corriendo.

### Proceso de despliegue

> Nota todo esto refiere al proceso de despliegue del servidor. El proceso de despliegue del cliente puede ser resuelto como
> un recurso estático integrado servidor por el servidor o como un recurso estático servidor desde otro servidor o servicio.

 * Hablamos sobre los pasos del proceso de despliegue utilizando contenedores:
    1. Creación de una imagen con el código de la aplicación (`docker build`)
    2. Distribución de la imagen a través de un registro (_registry_) público o privada (`docker push`)
    3. Descarga de la imagen en los nodos correspondientes (`docker pull`) y creación de contenedores a partir de la imagen (`docker run`)
 * Mencionamos que para poder crear nuestras propias imágenes necesitamos escribir un archivo `Dockerfile`, el cual especifica , de mínima:
    1. una imagen base (que describe, por ejemplo, la distribución Linux de base y el stack tecnológico),
    2. el software que dicha imagen incluirá y que el proceso de construcción instalará,
    3. los archivos que se copiarán en dicha imagen,
    4. (opcional, pero muy común) los puertos que la imagen expondrá, en caso que el sistema sea un software de red
    5. (opcional, pero muy común) el comando inicial que se ejecutará al crear un contenedor mediante `docker run`.
 * Mostramos cómo crear escribir nuestro primer `Dockerfile` y crear nuestra primera imagen Docker (más sobre esto lo estudiaremos en el taller de los sábados):

```Dockefile
FROM node:21-alpine
WORKDIR /hola-mundo

COPY package.json package.json
COPY index.js index.js

RUN npm install

ENTRYPOINT [ "node", "index.js" ]

EXPOSE 8080
```

 * Mencionamos que es usual que para garantizar la calidad del software, validemos que el software puede ser construido (y que sus pruebas automatizadas pueden ser ejecutadas) utilizando un sistema de integración continua (_CI_). Ocasionalmente podemos configurar a estos sistemas para que asistan en el proceso de despliegue ya sea poniendo en producción automáticamente toda versión nueva (_CD_), versiones específicas que sigan un cierto patrón (por ejemplo, _tags_) o que construyan las imágenes Docker y las suban a un registro para que puedan ser desplegadas de forma manual mas adelante.

# Material

* [Presentación Docker](https://docs.google.com/presentation/d/12N1BJhtlOYgTFzp3DP6Rl9xJQEZ2aN0qzf4O2H0KHKc/edit?slide=id.p7#slide=id.p7)
* [Apunte Docker](https://docs.google.com/document/d/16-ZVmZQrCbFDDnEyI8eABSp2rwsw3bz1WYyJ7DM9Rxw/edit?tab=t.0)
* [Otro apunte de Docker](https://docs.google.com/document/d/1xYF69TcGLIcQ3_fJnO7zUet6c5ud1zlFuinaRfNC3rU/edit?tab=t.0)
