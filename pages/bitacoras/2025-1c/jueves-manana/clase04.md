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

# Tarea

_Sección en progreso_

Además:

 * ¡No te olvides de asistir a la próxima clase de los sábados! Se profundizará sobre el concepto y herramientas ODM.