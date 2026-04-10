---
layout: page  
title: Clase 9  
description: Martes Noche, 2026, Primer Cuatrimestre  
permalink: /bitacoras/2026-1c/martes-noche/clase-09/
---

# Clase N°9: Componentes de UI  
*Desarrollo de Software K3552 (Martes Noche)*  

**Fecha: 21 de Octubre de 2025**

# Resumen

En esta clase vemos cómo se construyen las interfaces a partir de **componentes**. Estos pueden ser **estáticos** (cuando siempre muestran lo mismo) o **dinámicos** (cuando cambian según los datos o las acciones del usuario).

Luego se explica cómo React gestiona estos componentes, qué significa su **ciclo de vida** y qué son los **efectos secundarios**, es decir, las acciones que ocurren fuera (como responder a un click).

Por último, se aborda cómo **compartir y manejar el estado** entre varios componentes, y cómo usar `useEffect` para controlar cuándo y cómo se ejecutan esos efectos.

## 📑 Índice

- [Introducción](#introduccion)
- [Modelado orientado a componentes](#modelado-componentes)
- [Tipos de componentes](#tipos-componentes)
  - [Estáticos](#componentes-estaticos-react)
  - [Dinámicos](#componentes-dinamicos-react)
    - [Ciclo de vida](#ciclo-vida)
- [Componentes en React](#componentes-react)
  - [Estáticos](#componentes-estaticos-react)
  - [Dinámicos](#componentes-dinamicos-react)
- [Interacciones y efectos secundarios](#interacciones-efectos-secundarios)
  - [Tipos de efectos](#tipos-efectos)
    - [Disparados por eventos](#efectos-eventos)
    - [Del ciclo de vida](#efectos-ciclo-vida)
  - [Compartir y elevar estado](#compartir-elevar-estado)
  - [`useEffect` y manejo de dependencias](#useEffect-dependencias)

<a id="introduccion"></a>
## Introducción

Antes de arrancar, repasemos brevemente cómo los modelos **MVC**, **ViewModel** y **Flux** dieron origen al enfoque moderno de componentes reutilizables en la UI.

En el patrón **MVC**, el *controller* define tanto **qué** se muestra como **cómo** hacerlo, generando un fuerte acoplamiento con la vista. Este enfoque obliga a pensar las pantallas como una secuencia de pasos hasta alcanzar el estado visual deseado.

> **Ejemplo:** Un botón de "*following*". Antes se mostraba como texto, ahora como ícono. Aunque ambos representan lo mismo (`following = true`), el código debe cambiar por ser imperativo.

Luego, el **ViewModel** permite **declarar el estado a mostrar** sin preocuparse por la actualización de la interfaz.  Aunque este enfoque es más declarativo, los *double bindings* pueden generar bucles entre modelos dependientes.

Finalmente, **Flux** propone un **flujo de datos unidireccional**: el estado compartido se eleva en la jerarquía, y los componentes simplemente reaccionan a los cambios. 

Este principio —elevar el estado común y mantener un flujo predecible— sienta las bases de la arquitectura orientada a componentes.

<a id="modelado-componentes"></a>
## Modelado orientado a componentes

Al diseñar una interfaz, podemos abordarla desde dos enfoques: **orientado a páginas** u **orientado a componentes**.

El primero, característico del desarrollo *server-side*, asocia cada página con un caso de uso, lo que dificulta aislar responsabilidades internas.

El segundo, propio del desarrollo *client-side*, descompone la interfaz en **unidades más pequeñas, cohesionadas y reutilizables**.

Cada componente define una **interfaz clara** y **encapsula** tres aspectos: la lógica visual (cómo se muestra), la lógica de procesamiento (qué hace) y la estética (cómo se ve).

De este modo, una pantalla se construye a partir de **componentes que pueden integrarse y anidarse entre sí**, como plantillas que permiten incorporar nuevos elementos.

> Todo componente debería aspirar a ser **cohesivo, reutilizable y simple**: centrado en una única responsabilidad, adaptable a distintos contextos y fácil de razonar.

Finalmente, una analogía: así como en el *backend* modelamos objetos de dominio, en el *frontend* modelamos **componentes** con responsabilidades bien definidas.

<a id="tipos-componentes"></a>
## Tipos de componentes

Se pueden distinguir dos tipos de componentes: los **estáticos** y los **dinámicos**.

Antes de pensar en React, conviene entenderlos desde un punto de vista general.

<a id="componentes-estaticos"></a>
### Estáticos

Un **componente estático** recibe datos de entrada y los muestra sin modificarlos.

No posee estado interno ni lógica compleja: actúa como una **plantilla de presentación**, cuyo único objetivo es transformar datos en elementos visuales.

Si cambian los datos de entrada, el componente se vuelve a renderizar, pero él mismo **no toma decisiones**: no conserva estado ni ejecuta lógica adicional.

> **Ejemplo**: Un encabezado con un título o un ícono acompañado de texto.

<a id="componentes-dinamicos"></a>
### Dinámicos

Un **componente dinámico** no solo muestra datos: **también actúa**.

Recibe entradas, emite eventos y mantiene un **estado interno** que determina su comportamiento.

Podemos pensar en dos partes:

1. **Interfaz externa:** qué datos recibe y qué eventos emite.

2. **Lógica interna:** cómo usa su estado para procesar la información y generar la vista.

En conjunto, funciona como un **módulo independiente** dentro de la aplicación, que reúne estado, reglas y presentación en una sola unidad.

<a id="ciclo-vida"></a>
#### Ciclo de vida

Los componentes dinámicos tienen un ciclo de vida que se puede describir así:

1. Recibe datos de entrada desde su entorno.

2. Procesa esos datos junto con su estado interno.

3. Genera una representación visual mediante su lógica de renderizado.

4. Se muestra en pantalla y responde a interacciones del usuario.

5. Las interacciones disparan eventos que actualizan el estado o las entradas.

6. El componente se vuelve a renderizar de forma **reactiva**, reflejando los cambios

<a id="componentes-react"></a>
## Componentes en React

React adopta este mismo modelo, pero lo lleva a un **enfoque declarativo**.

La idea es que cada componente es una función que recibe datos (`props`), puede gestionar su propio estado (`state`) y devuelve una **representación visual** (`JSX`).

<a id="componentes-estaticos-react"></a>
### Estáticos

Un componente estático en React es una **función pura**: recibe `props` y devuelve JSX, sin manejar estado ni efectos secundarios.

Cada vez que cambian las `props`, React vuelve a ejecutar la función y actualiza el resultado en pantalla.

Por ejemplo, un botón:

```jsx
function BotonPrimario({ texto }) {
  return <button className="boton-primario">{texto}</button>;
}
```

<a id="componentes-dinamicos-react"></a>
### Dinámicos

Los **componentes dinámicos** combinan entradas, salidas y estado.

Las **entradas** se reciben mediante `props`, las **salidas**, como funciones *callback* (`onClick`, `onChange`) y el **estado interno** se gestiona con *hooks* como `useState`, que permiten conservar valores entre renders.

Dentro del componente conviven dos lógicas:

* La de **procesamiento**, donde se define el comportamiento ante eventos o acciones del usuario.
* La de **renderizado**, que determina la salida visual (`JSX`).

*¿Cómo funciona un componente en React?*

Podemos pensar un componente de React como una **función pura**:  `({ props, state }) => JSX`.

Por cada render, se ejecuta esta función completa y se traduce su resultado al DOM.

Luego, si las `props` cambian o se actualiza el estado del componente mediante `setState` o `useState`, se dispara un nuevo render.

> 💡**Ejemplo**: En [`esto-es-happy-new-year/komm-2`](https://github.com/ddso-utn/esto-es-happy-new-year/tree/komm-2), el usuario puede seleccionar un plato y marcarlo como “seleccionado” usando un estado local.

En React, los cambios en los datos **actualizan automáticamente la interfaz**: no se modifica la vista a mano, sino que este **recalcula** cómo debe mostrarse.

<a id="interacciones-efectos-secundarios"></a>
## Interacciones y efectos secundarios

Hasta ahora asumimos que los componentes eran funciones puras, sin efectos externos.

En la práctica, sin embargo, las aplicaciones necesitan interactuar con su entorno: leer o modificar el DOM, comunicarse con un servidor o usar APIs del navegador.

Estas acciones se conocen como **efectos secundarios** (*side-effects*) y rompen la transparencia referencial de una función, ya que su resultado deja de depender únicamente de sus entradas.

Es decir, cuando un componente interactúa con el exterior, deja de ser completamente puro. Lo importante es gestionar eso de forma controlada y predecible.

<a id="tipos-efectos"></a>
### Tipos de efectos

Podemos distinguir dos grandes tipos de efectos en una aplicación React: los **efectos disparados por eventos** y los **efectos del ciclo de vida**.

<a id="efectos-eventos"></a>
#### Disparados por eventos

Son aquellos que ocurren como respuesta directa a una acción del usuario.

Por ejemplo, manipular el DOM (`document`, `window`, `<video>`, `confirm`) o realizar solicitudes HTTP para crear o modificar datos.

> 💡 **Ejemplo:** En [`esto-es-happy-new-year/komm-2.5`](https://github.com/ddso-utn/esto-es-happy-new-year/tree/komm-2.5), un botón crea una comanda (por ahora vacía) cuando el usuario lo presiona.

En React, este tipo de efectos se manejan en los **controladores de eventos** (*event handlers*) definidos dentro del componente.

<a id="efectos-ciclo-vida"></a>
#### Del ciclo de vida

Otros efectos no dependen de eventos del usuario, sino del **propio ciclo de vida del componente**: se ejecutan cuando el componente se **monta**, se **actualiza** o se **desmonta**.

Estos momentos son útiles para inicializar datos, suscribirse a eventos externos o limpiar recursos.

En React, estos efectos se implementan mediante **funciones que se ejecutan después del renderizado**.

> Podemos verlos como una forma de **sincronizar** el estado interno del componente con el entorno.

<a id="compartir-elevar-estado"></a>
### Compartir y elevar estado

Además de interactuar con el entorno, los componentes también interactúan **entre sí**.

Cuando varios necesitan acceder al mismo conjunto de datos, se suele **elevar el estado** (*lift state up*) hacia un componente padre, que actúa como fuente de verdad y distribuye la información mediante `props`.

> 💡 **Ejemplo:** En [`esto-es-happy-new-year/komm-3`](https://github.com/ddso-utn/esto-es-happy-new-year/tree/komm-3), el botón que crea la comanda necesita acceder a la lista de platos seleccionados (estado elevado).

Este patrón sigue la filosofía de **Flux**: el estado común se centraliza y los cambios fluyen hacia abajo en un único sentido, lo que vuelve la interfaz más predecible y fácil de razonar.

<a id="useEffect-dependencias"></a>
### `useEffect` y manejo de dependencias

React ofrece el hook `useEffect` como mecanismo declarativo para gestionar estos efectos.

`useEffect` recibe una función que se ejecuta tras el renderizado y un **array de dependencias** que indica cuándo debe volver a hacerlo.

- Si el array está vacío (`[]`), el efecto se ejecuta solo una vez, al montar el componente.

- Si incluye variables, React lo ejecuta nuevamente cada vez que alguna de ellas cambia.

> 💡 **Ejemplo:** En [`esto-es-happy-new-year/komm-3.5`](https://github.com/ddso-utn/esto-es-happy-new-year/tree/komm-3.5), un efecto realiza una petición al servidor para obtener los platos disponibles del menú.

`useEffect` actúa como un **puente** entre la lógica pura del componente y el mundo exterior —ya sea el DOM, el servidor o cualquier otra fuente de datos.