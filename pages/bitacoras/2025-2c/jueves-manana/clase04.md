---
layout: page
title: Clase 4
description: Jueves Mañana, 2025, Segundo Cuatrimestre
permalink: /bitacoras/2025-2c/jueves-manana/clase-04/
---

# Temario

 * Persistencia. Concepto.
 * Conexión con la DB. ODM
 * Queries.

# Resumen

1. Introducción: ¿por qué necesitamos persistir a por qué persistir?
2. Modelos / paradigmas de persistencia y motores de bases de datos:
    * Modelo Relacional vs Modelos no Relacionales
    * Bases de datos SQL vs no-SQL
    * Ejemplo: Modelo Relacional vs Documental. PostgreSQL vs Mongo.
3. MongoDB: Profundización.
    * Explicamos con un ejemplo en vivo: creamos una base de datos en vivo.
    * Carga de un dataset, consulta, edición, exportación, borrado.
4. Paréntesis académico: ṕor qué damos Mongo y no (otra) base de datos relacional en la materia.
    * Conveniencia académica:
      * de código abierto, gratuita, multiplataforma, fácil de instalar.
      * Utiliza JavaScript como base de su lenguaje de consulta.
      * Utiliza [BSON](https://www.mongodb.com/resources/basics/json-and-bson) (derivado de JSON) como formato de persistencia
      * No requiere de una esquema definido a priori (DDL) y por tanto no necesitamos de tantos conceptos para empezar a manipular nuestros datos (DML)
   * Sin embargo, no que sea mejor ni peor: depende de cada contexto.
5. Infraestructura de bases de datos:
    * Se puede [instalar local](https://www.mongodb.com/try/download/community), instalar en la nube, o usar un SaaS.
    * Tiene ventajas y desventajas: facilidad de uso y escalamiento, costos, control, dependencia del proveedor, seguridad y soberanía de los datos.
6. Nota al pie: no todo se guarda, no todo se guarda de forma plana. Tener en cuenta:
  * Normalización
  * Encriptación y hasheo de datos sensibles
7. Mostramos cómo se puede consumir desde una aplicación con sólo el [_Driver_ de Mongo para NodeJS](https://www.mongodb.com/docs/drivers/node/current/).
8. Introducción al concepto de _impedance mismatch_ y a un mapeador ODM: [Mongoose](https://mongoosejs.com/).


## Notas de clase

### Persistencia

> ¿Persistencia? ¿Persistir? ¿Qué es eso?

  - Técnicas para resolver distintos problemas
    - Mantener los datos, sin perderlos => durabilidad
    - Manejar volúmenes de datos "grandes" de forma eficiente
      - CRUD / ABM / ABMC (alta, baja, modificación y consulta)
  - Un medio puede ser una base de datos
      - dónde se guarda la información: en disco, en memoria, etc
      - cómo se la representa físicamente: en qué formato (binario o textual)
  - Cómo se representa lógicamente la información: cómo razonamos sobre ella
      - Modelo (Persistencia) Relacional:  (~SQL~)
        - basado en tablas (entidades), Relaciones entre tablas (entidades)
        - se pueden representar mediante el diagrama entidad-relación (DER)
        - En el modelo relacional tenemos algunas operaciones básicas CRUD:
        - diseñado para mantener redundancia mínima y operaciones CRUD ricas
      - Modelos no relacionales: (~noSQL~)
          - Documental
            - Documentos (una estructura clave valor) que se organiza en colecciones (cúmulo de información de un tipo mas o menos similar)
            - Tiene objetivos que están a mitad de camino entre el relacional y el clave valor
          - Clave valor:
            - representa la información en forma de diccionarios (clave-valor)
            - diseñado para tener operaciones CRUD simples y rápidas
          - Tabular
              - no nos interesa ahora.

### Bases de datos

> ¿Bases de datos?  ¿Qué es eso?

- Una implementación concreta de un motor de persistencia
  - bajo un paradigma / modelo de persistencia
  - persistiendo en un medio particular (disco, memoria, híbridas)
  - con ciertos requerimientos no funcionales
  - utilizando un lenguaje de consulta particular
  - Ejemplos particulares:
    - Documentales:
      - MongoDB / Mongo
      - CouchDB
    - Clave Valor:
      - Redis
      - Riak
    - Tabulares
      - Casssandra
      - Clickhouse
    - Relacionales:
      - PostgreSQL / Postgres
      - Oracle
      - (Microsoft) SQL Server
      - MySQL
      - SQLite => es una de datos que se puede usar de forma embebida
      - HSQLDB => otra base de datos embebida, en memoria

### Lenguaje de consulta

> ¿Cómo consultamos los datos? ¿Cómo hacemos nuestras operaciones CRUD?

- SQL -> típicamente e históricamente está asociado al modelo relacional
  - crear: `insert`
  - eliminar: `delete`
  - modificar: `update`
  - consultar: `select`
- El lenguaje JavaScript de MongoDB -> sólo en MongoDB


### Paréntesis académico

> ¿Y por qué Mongo? ¿Por qué no MySQL? ¿Por qué no Redis? ¿Por qué no `<inserte su base favorita>`?

Elegimos Mongo y al modelo documental sólo porque nos calza bien en la cursada:

  - Para no solaparnos con otras materias
  - es fácil de instalar y multiplataforma y de código abierto, no esté atado / anclado a un proveedor (_vendor locking_)
  - porque utiliza el lenguaje JavaScript como lenguaje de consulta


### Conectarnos a una base de datos

1. Agregar el driver (de mongo, en este caso)  a nuestro `package.json` y hacer `npm install`
2. Vamos a tener que establecer una conexión con la base de datos, indicando la cadena de conexión: sin ella, la aplicación no funcionará
    1. Una forma sencilla (pero no siempre realista) es hacerlo al iniciar la aplicación
3. Pasar a los repositorios el cliente mongo
4. Usar el cliente en los repositorios en lugar de listas en memorias


### Repaso de la arquitectura de servicios

- Tenemos un componente ruteador, que redirige las rutas http a controladores
- Tenemos varios controladores, que procesan las peticiones HTTP e implementa la lógica de dominio
  delegando en servicios y siguiendo aproximadamente la forma de un caso de un uso
- Tenemos servicios que implementan la lógica de dominio asociada a una entidad o tarea particular,
  y si necesitan acceder a entidades (objetos del dominio persistentes), terminarán utilizando repositorios
- Tenemos repositorios que van a ser los responsables de consultar y almacenar las entidades en un medio persistente.
  - Podrían ser repositorios en memoria, que simplemente guardan la información en arrays/listas de JS
  - Podrían ser repositorios persistentes, que utilizan un cliente (ejemplo MongoClient) para realizar las operaciones CRUD

### Arquitecturas distribuidas

1. En la materia siempre vamos a tener una sóla base de datos y un sólo servidor
2. En el mundo real, sin embargo, podríamos conectar más de una aplicación al mismo servidor de base de datos

## Identificadores en Mongo: `ObjectID`

En relacional el tipo más fácil de indexar, y por tanto, el más común como clave primaria
es el entero autoincremental. Esto vale tanto si estamos hablando de claves naturales enteras
como claves subrrogadas (`id`).

En mongo también se puede, pero por defecto utiliza un tipo llamado `ObjectID`, que son UUIDs
que incluyen entre otras cosas la fecha de creación.

## ¿Mongo persiste en `JSON`?

En Mongo se persiste en `BSON`, que es una versión binaria de JSON que tiene soporte para alguns tipos de datos más.


## Paréntesis: el modelo _orden - item - producto_

pedido / orden: representa la compra
item: hay uno o más items por pedido, que representa cada tipo de cosa que se compró y sus repeticiones
producto: lo que se adquirió, cada item apunta a un producto

 * `pedido -> "*" items`
  * `item -> "1" producto`

En producto guardamos información de:
  - nombre
  - descripción
  - categoria,
  - otros atributos descriptivos
  - precio de referencia / precio actual
  - id / codigo

Corolario:
  - en sistema relacionales estas tres entidades se persisten de forma independiente,
    en parte por
      - limitaciones del modelo
      - y en parte para reutilizar almacenamiento
      - en parte porque así tenemos un modelo normalizado menos susceptible a inconsistencias de datos
  - en el mundo documental, no necesariamente vamos a persistir esta información en entidades (colecciones) separadas
    - porque no es necesaria
        - el modelo permite tener elementos multivaluados, en forma de arrays / listas
        - el modelo permite embeber otros modelos (podemos tener un producto embebido dentro de un item)
     - porque capaz no nos importa tanto optimizar el almacenamiento  (igual mongo optimiza esto comprimiendo valores duplicados, si puede)
       porque hoy en día contamos con más espacio en disco que cuando se pensaron las bases relacionales pero también porque
       almacenar la información repetida nos dará mayor velocidad de consulta (porque no tenemos que utilizar _joins_)
     - el tercer problema (las potenciales inconsistencias de datos) persiste
  - En el mundo relacional por defecto vamos a almacenar de forma normalizada, mientras que en el mundo documental (mongo) nuestra primera aproximación
    debería ser desnormalizada (luego normalizamos si es necesario)
      - dato al margen: para hacer "joins" en mongo, existe la operación `$lookup`


## Esquema sí / esquema no

Si bien es flexible no tener que definir un esquema _a priori_, a la larga, es difícil de mantener y vamos a tener que igualmente:
  - implementar migraciones de datos
  - y/o definir esquemas de datos para cada colección (esto se hace en el código de nuestra aplicación).
      - `mongoose` tiene soporte nativo para esto.
      - si utilizan lenguajes con tipado estático (typescript, java, etc) también se pueden incorporar estas validaciones de esquema


## Paquete `mongodb` vs `mongoose`

 * `mongodb` es un driver / conector de base de datos. Existe un paquete por cada lenguaje de programación común (ej: hay para python, para node, para java, etc)
    - `jdbc`: es la familia de drivers / la tecnología de conexión a bases de datos  (típicamente relacionales, tipicamente SQL) de Java
    - `odbc`: idem, pero para tecnologías del mundo de Microsoft / .net
 * `mongoose` es un ODM: sirve para resolver las diferencias entre el mundo documental de mongo y el mundo de objetos en tu lenguaje de programación OOP favorito (en este caso, para JS)


## Colecciones en REST vs Colecciones en Mongo

> ⚠️ Colección de REST ≠ Colección de Mongo

Repaso rápido: a los recursos plurales en REST también se los llama _colecciones_

```
/platos/
/platos/5
```

Pero también hablamos (hoy)  de colecciones en Mongo:  es la estructura donde se almacenan datos de tipos similares, análoga al concepto de tabla en relacional. Entonces...


* Si tenemos una ruta `/platos`, ¿tiene que haber un `db.platos`?
* Si tenemos una ruta `/pedidos`, ¿tiene que haber `db.pedidos`?

**¡No!** El modelado rest y el modelado de base de datos, si bien evidentemente tienen vinculación, van por caminos diferente. El modelado de colecciones rest y de colecciones de base de datos no tiene por qué coincidir. Podemos tener colecciones Mongo que no se mapeen directamente a una ruta rest, ni viceversa.


## Comandos de ejemplo

### Iniciar mediante docker

```bash
# esto no es necesario si lo instalaron nativamente
docker run --rm -it --name mongo-kommanda -p 27017:27017 mongo
```

### Conectarse al servidor de base de datos

```bash
# si lo ejecutaste con docker
docker exec -it mongo-kommanda mongosh kommanda

# si lo tenés instalado nativamente
mongosh kommanda

# equivalente a
mongosh kommanda mongodb://127.0.0.1:27017/kommanda

# también equivalente a
mongosh
use komanda # dentro de mongosh
```

### Acceso a bases de datos y colecciones

```mongosh
kommanda> show dbs
admin      40.00 KiB
config    108.00 KiB
kommanda   40.00 KiB
local      40.00 KiB
kommanda> show collections
platos
kommanda>
```

### Consulta de colecciones

```js
> db.platos.findOne()
{
  _id: ObjectId('681c1d4b464b8c003b796099'),
  nombre: 'Empanada de carne',
  categoria: 'ENTRADA',
  precio: 5000,
  estaDisponible: true
}
> db.platos.find()
[
  {
    _id: ObjectId('681c1d4b464b8c003b796099'),
    nombre: 'Empanada de carne',
    categoria: 'ENTRADA',
    precio: 5000,
    estaDisponible: true
  },
  {
    _id: ObjectId('681c1d4b464b8c003b79609a'),
    nombre: 'Provoleta',
    categoria: 'ENTRADA',
    precio: 7000,
    estaDisponible: true
  },
  ...
]
> db.platos.find({categoria: 'BEBIDA', precio: { $lt: 7000  }})
[
  {
    _id: ObjectId('681c1d4b464b8c003b7960aa'),
    nombre: 'Agua mineral',
    categoria: 'BEBIDA',
    precio: 3000,
    estaDisponible: true
  },
  {
    _id: ObjectId('681c1d4b464b8c003b7960ab'),
    nombre: 'Cerveza de lata',
    categoria: 'BEBIDA',
    precio: 6500,
    estaDisponible: true
  },
  {
    _id: ObjectId('681c1d4b464b8c003b7960ac'),
    nombre: 'Gaseosa',
    categoria: 'BEBIDA',
    precio: 4000,
    estaDisponible: true
  }
]
> db.platos.find({nombre: /dulce de leche/}, { nombre: 1, _id: 0 })
[
  { nombre: 'Flan con dulce de leche' },
  { nombre: 'Panqueque de dulce de leche' },
]
```

### Modificación de documentos

```js
> db.platos.find({nombre: /dulce/}, { nombre: 1, precio: 1, _id: 0 })
[
  { nombre: 'Flan con dulce de leche', precio: 4000 },
  { nombre: 'Panqueque de dulce de leche', precio: 4500 },
  { nombre: 'Queso y dulce', precio: 35 }
]
> db.platos.updateMany({ nombre: /dulce/ }, { $inc: { precio: 1000  }})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 3,
  modifiedCount: 3,
  upsertedCount: 0
}
> db.platos.find({nombre: /dulce/}, { nombre: 1, precio: 1, _id: 0 })
[
  { nombre: 'Flan con dulce de leche', precio: 5000 },
  { nombre: 'Panqueque de dulce de leche', precio: 5500 },
  { nombre: 'Queso y dulce', precio: 1035 }
]
> db.platos.deleteMany({ nombre: /dulce de leche/ })
{ acknowledged: true, deletedCount: 2 }
> db.platos.find({nombre: /dulce/})
[
  {
    _id: ObjectId('681c1d4b464b8c003b7960a6'),
    nombre: 'Queso y dulce',
    categoria: 'POSTRE',
    precio: 35,
    estaDisponible: true
  }
]
```

### Importación de datos

```bash
# nativo
mongoimport \
   --db kommanda \
   --collection='platos' \
   --file=/tmp/kommanda/platos.csv \
   --type=csv \
   --fields="nombre","categoria","precio","estaDisponible"

# con docker
docker exec -it mongo-kommanda mongoimport \
   --db kommanda \
   --collection='platos' \
   --file=/tmp/kommanda/platos.csv \
   --type=csv \
   --fields="nombre","categoria","precio","estaDisponible"

# Nota:  hay que montar el archivo primero
docker run --rm -it -v "$(pwd)/tmp":/tmp/kommanda --name mongo-kommanda -p 27017:27017 mongo
```


# Material

* [Enunciado Kommanda](https://docs.google.com/document/d/1QHOLDwn7LaETVxSIkOWK5nGT9xrBjatjZoiKafDebsw/edit?tab=t.0#heading=h.btqp28xuwru4)
  * [Código sin persistencia](https://github.com/ddso-utn/kommanda/tree/clase-odm-inicial)
  * [Código con persistencia](https://github.com/ddso-utn/kommanda/tree/clase-odm-repos)
  * [Datos de ejemplo](https://gist.github.com/flbulgarelli/0cfb4e0557f3d003c107f21f7345e2ee)
 

# Tarea

0. 🤹 Instalen Mongo y pónganse a "jugar" con mongo.
1. Lean el ejercicio de Kommanda e intenten hacerlo desde cero. Van a surgir al final los problemas de persistencia. Con lo que vieron hoy pueden encararlos todos. Si están en dudas pueden mirar la solución propuesta, pero sólo como último recurso.
2. **NO FALTEN** a la clase del sábado: se va a ver `ODM`. ¿Qué es ODM?: Mapeo Objeto-Documental, que es una forma un poco más fácil de hacer todo esto.
