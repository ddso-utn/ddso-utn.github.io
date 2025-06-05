---
layout: page
title: Clase 7
description: Jueves Mañana, 2025, Primer Cuatrimestre
permalink: /bitacoras/2025-1c/jueves-manana/clase-07/
---

# Temario

* Componentes de UI: estructura
* Anatomía de un componente (props, state, etc.)
* Ciclo de vida
* Técnicas de reutilización: introducción

# Resumen

Formalizamos los _hooks_ de react. En particular, estudiamos los dos más frecuentes:
  * `useState`
  * `useEffect`

Discutimos sobre cómo modelar el estado en react, y cómo aplicar la técnica de "subir" el estado a través de la jerarquía de componentes de react.

Estudiamos como cada componente puede verse como una función que va de (state+props) => JSX, Ante cualquier reasignación de props o state, re-renderiza todo el componente, recalculando cualquier valor que pueda haber cambiado. Este concepto de reaccionar de forma declarativa ante cualquier cambio y re-renderizar el componente se conoce como “Reactividad”, de ahí el nombre.

Por último, estudiamos un ejemplo con formularios.

# Material

 * [Guía sobre hooks](https://hooks-guide.netlify.app/)
 * [Presentación del taller de los sábados](https://docs.google.com/presentation/d/1Cq-ElvtfndlUxnMjJNhVjPr3uApaSCMmslSTlkGhEBI/edit?slide=id.p1#slide=id.p1)

# Tarea

_Sección en progreso_
