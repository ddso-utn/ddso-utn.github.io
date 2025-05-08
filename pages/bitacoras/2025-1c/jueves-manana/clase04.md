---
layout: page
title: Clase 4
description: Jueves Mañana, 2025, Primer Cuatrimestre
permalink: /bitacoras/2025-1c/jueves-manana/clase-04/
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

# Material

* [Enunciado Kommanda](https://docs.google.com/document/d/1QHOLDwn7LaETVxSIkOWK5nGT9xrBjatjZoiKafDebsw/edit?tab=t.0#heading=h.btqp28xuwru4)
  * [Código sin persistencia](https://github.com/ddso-utn/kommanda/tree/clase-odm-inicial)
  * [Código con persistencia](https://github.com/ddso-utn/kommanda/tree/clase-odm-repos)

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

# Tarea

¡Hacer Kommanda!

Además:

 * ¡No te olvides de asistir a la próxima clase de los sábados! Se profundizará sobre el concepto y herramientas ODM.