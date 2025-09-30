---
layout: page
title: Clase 6
description: Martes Noche, 2025, Segundo Cuatrimestre
permalink: /bitacoras/2025-2c/martes-noche/clases/clase-06/
---

# Clase N°6: ODM
*Desarrollo de Software K3552 (Martes Noche)*

**Fecha: 23 de Septiembre de 2025**

[Link a la grabación de la clase](https://www.youtube.com/watch?v=eDh96fuPorE)

# Resumen

Hoy introdujimos el **modelo documental**, comparándolo con el relacional. Presentamos **MongoDB** como la base de datos documental que utilizaremos, junto con **Mongoose** como **ODM** para mapear objetos a documentos.

Además, repasamos el **asincronismo en JavaScript**, incluyendo el event loop, las promises y el uso de `async/await`. 

Finalmente, revisamos de manera sencilla la **inyección de dependencias** y la importancia de mantener una clara separación entre **DTOs, entidades de dominio y entidades de persistencia**.

## Índice

- 📄[Introducción: Modelo documental](#introduccion)
	- [ODM](#odm)
- 🧩[Modelado de objetos](#modelado-objetos)
	- [Objetos embebidos](#objetos-embebidos)
	- [Objetos referenciados](#objetos-referenciados)
	- [Criterio de elección](#criterio-eleccion)
- [Asincronismo en JavaScript](#asincronismo-js)
	- [Callbacks](#callbacks)
	- 📦[Promises](#promises)
	- [Uso de `async/await`](#uso-async-await)
- [Inyección de dependencias](#inyeccion-dependencias)
- [DB vs REST: Separando responsabilidades](#db-vs-rest)

<a id="introduccion"></a>
## 📄 Introducción: Modelo documental

El **modelo documental** forma parte de la familia **NoSQL**. A diferencia de los sistemas relacionales, que se basan en tablas y filas, acá trabajamos con **documentos**, cuya estructura se asemeja a objetos **JSON**.  

En esta materia utilizaremos **MongoDB** como base de datos.  

> **Nota**: MongoDB no almacena exactamente JSON, sino **BSON** (*Binary JSON*), un formato binario optimizado para el procesamiento y almacenamiento eficiente de datos.

La principal característica de este modelo es su **flexibilidad**. No impone claves foráneas (**FKs**) ni estructuras rígidas. Esto permite **anidar documentos, incluir listas y modelar estructuras complejas dentro de un único registro**, siempre que resulte conveniente.  

Ahora bien, esta flexibilidad también implica **menores controles de consistencia** en comparación con un modelo relacional. Por eso, estas bases de datos se usan sobre todo en casos donde importa más la rapidez de acceso o manejar grandes volúmenes de datos que la consistencia estricta.

Cada documento se identifica mediante un **ObjectID**, generado automáticamente por MongoDB de forma única.

### ODM

Un **ODM** (*Object Document Mapper*) tiene como objetivo **mapear los objetos de la aplicación a documentos de la base de datos**, reduciendo el *impedance mismatch* entre ambos mundos.  

> En nuestro caso, podemos utilizar [**Mongoose**](https://mongoosejs.com/).

Este enfoque es análogo al de un **ORM** (*Object Relational Mapper*) en bases de datos relacionales: como por ejemplo, Hibernate o JPA que facilitan el trabajo con entidades en Java.

<a id="modelado-objetos"></a>
## 🧩 Modelado de objetos

Imaginemos una clase `Pedido` que contiene una lista de `Producto`. Ahora nos preguntamos: **¿cómo representamos esta relación en una base documental?**

Existen dos opciones, **embeber** o **referenciar** objetos. Veamos cómo sería:

---
<a id="objetos-embebidos"></a>
### Objetos embebidos

Supongamos que en nuestra aplicación los productos no tienen sentido fuera del contexto de un pedido. Como son básicos, podemos guardarlos directamente en `Pedido`:

```js
const pedido = {
  numero: 1234,
  cliente: "Juan Pérez",
  productos: [
    { nombre: "Lapicera", precio: 100 },
    { nombre: "Cuaderno", precio: 500 }
  ],
  total: 600
}
```

> Este objeto es representativo, Mongoose crea objetos un poco más complejos.

En este escenario, los productos viven **dentro** del pedido. Como no necesitamos gestionarlos de manera autónoma, es más que suficiente.

---
<a id="objetos-referenciados"></a>
### Objetos referenciados

Ahora supongamos que la aplicación crece, que los productos requieren de stock y de proveedor y además queremos consultarlos de forma independiente.

En ese caso, los productos sí tienen sentido como entidad propia, con vida fuera del `Pedido`. Por eso, tiene más sentido modelarlo de esta forma:

```js
const pedido = {
  numero: 1234,
  cliente: "Juan Pérez",
  productos: [
    ObjectId("6512f3..."),
    ObjectId("6512f4...")
  ],
  total: 600
}

const producto1 = {
  _id: ObjectId("6512f3..."),
  nombre: "Lapicera",
  precio: 100,
  stock: 200,
  proveedor: "Faber-Castell"
}

const producto2 = {
  _id: ObjectId("6512f4..."),
  nombre: "Cuaderno",
  precio: 500,
  stock: 50,
  proveedor: "Gloria"
}
```

> **Observación**: Otra opción sería que cada producto tenga el `ObjectID` de `pedido`.

En este escenario, cada producto se maneja de forma independiente, puede reutilizarse en muchos pedidos y tiene **información propia** que justifica el desacople.

---
<a id="criterio-eleccion"></a>
### Criterio de elección

La decisión entre **embeber** o **referenciar** depende de cómo se relacionen los datos y de las necesidades de la aplicación.

- Si los objetos **no viven de forma independiente**, embeberlos simplifica el modelo y mejora la performance al evitar consultas adicionales.

- Si, en cambio, requieren **identidad propia, trazabilidad o reutilización**, conviene guardarlos como documentos separados y referenciarlos, aunque esto implique más consultas para mantener la consistencia.

En definitiva, se trata de encontrar el **equilibrio entre performance y consistencia**, aplicando mayor complejidad solo cuando realmente aporta valor al modelo.

<a id="asincronismo-js"></a>
## Asincronismo en JavaScript

El acceso a una base de datos u otras operaciones de **I/O** lleva tiempo.

En **JavaScript**, durante ese tiempo no se bloquea el hilo principal: el lenguaje se ejecuta sobre un **event loop** de un único hilo (**single-threaded**) y delega las operaciones de I/O para que la ejecución continúe sin interrupciones.  

> **Analogía**: Esto se parece a los **ULT (User-Level Threads)** en Sistemas Operativos: parece que hay muchas tareas en paralelo, pero en realidad se planifican sobre un solo hilo.

---
<a id="callbacks"></a>
### Callbacks

Originalmente, el asincronismo se resolvía mediante **callbacks**, funciones que se ejecutan cuando el resultado estaba disponible.  

Ejemplo con callback:

```js
function obtenerDato(callback) {
  setTimeout(() => callback("dato listo"), 1000)
}

obtenerDato(dato => console.log(dato))
```

Si bien funcionan para operaciones simples, encadenar múltiples callbacks dificulta la lectura y el manejo de errores.

---
<a id="promises"></a>
### 📦 Promises

Las **promises** surgieron como una abstracción sobre los callbacks.

Podemos pensarlas como **una caja que en este momento está vacía, pero que en algún momento se llenará con un resultado o con un error**.

Lo importante no es cómo se llena, sino que sabemos que en el futuro la caja tendrá un contenido. Veamos un ejemplo:

```js
function obtenerDato() {
  return new Promise(resolve => {
    setTimeout(() => resolve("dato listo"), 1000)
  })
}

obtenerDato().then(dato => console.log(dato))
```

En este ejemplo, `.then()` se ejecuta cuando la caja ya está llena, es decir, cuando la promesa se resuelve.

---
<a id="uso-async-await"></a>
### Uso de `async/await`

El uso de `async/await` es un **syntax sugar** sobre las *promises*.

Permite escribir código con una apariencia secuencial, aunque internamente sigue siendo asincrónico.  

El operador `await` puede leerse como “ver el contenido de la caja cuando esté listo, sin bloquear el hilo principal”.

```js
async function main() {
  const dato = await obtenerDato()
  console.log(dato)
}
```

> **Regla**: cualquier función que use `await` debe declararse con `async`. 

> **Observación**: Si una función solo retorna una promesa sin usar `await`, no es necesario marcarla como `async`.

<a id="inyeccion-dependencias"></a>
## Inyección de dependencias

Nuestros **controllers**, **services** y **repositories** necesitan conocerse de manera controlada. Para eso usamos **inyección de dependencias**. 

La idea es simple: cada objeto recibe lo que necesita a través del **constructor** o de **setters**, en lugar de obtenerlo por su cuenta (creándolo, utilizando un *Singleton*, etc.).

En este curso vamos a hacerlo a mano con un **app context** sencillo: instanciamos cada clase y pasamos las dependencias por constructor. Es suficiente para nuestros proyectos y mantiene el acoplamiento bajo.

```js
// En Repository.js
class Repository { /* ... */ }

// En Service.js
class Service {
  constructor(repository) {
    this.repository = repository
  }
}

// En Controller.js
class Controller {
  constructor(service) {
    this.service = service
  }
}

// En context.js
const repo = new Repository()
const service = new Service(repo)
const controller = new Controller(service)
```

Este esquema facilita los tests y permite reemplazar dependencias por mocks cuando haga falta.

<a id="db-vs-rest"></a>
## DB vs REST: Separando responsabilidades

En una aplicación distinguimos tres tipos de objetos:

- **DTOs (Data Transfer Objects)**: representaciones planas de los datos usadas para la comunicación con el exterior (por ejemplo, en las peticiones y respuestas HTTP).
- **Entidades de dominio**: representan las reglas de negocio y sus validaciones.
- **Entidades de persistencia**: definen cómo se almacenan los datos en la base de datos.  

Aunque en algunos casos puedan parecer similares en estructura, **no cumplen el mismo rol**.

---

Ahora bien, cada capa trabaja con un tipo de objeto específico:

- La **capa de presentación** recibe representaciones externas (en nuestro caso, **DTOs**) y las transforma en objetos de dominio, y viceversa.
- La **capa de dominio** aplica las reglas de negocio sobre esas entidades.
- La **capa de persistencia** se encarga de almacenar y recuperar los datos, traduciendo entre entidades de dominio y representaciones de base de datos.

---

En **JavaScript**, este error de mezclar responsabilidades es particularmente común porque, al no ser tipado, resulta muy fácil “reciclar” objetos entre capas. 

Por ejemplo, si recibo un DTO muy parecido al objeto que persisto, *¿por qué no mandarlo directo al repository o usarlo tal cual en el service?*

Si bien a simple vista esto parece algo práctico, la realidad es que se va a generar una deuda técnica: tarde o temprano le faltarán métodos y nos hará ruido.

A modo de síntesis, aunque los objetos puedan parecerse, **no son intercambiables**. Respetar la separación de responsabilidades nos permite tener un diseño limpio y extensible.

