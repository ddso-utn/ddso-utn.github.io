---
layout: page
title: Clase 8
description: Martes Noche, 2026, Primer Cuatrimestre
permalink: /bitacoras/2026-1c/martes-noche/clase-08/
---

# Clase N°8: Introducción a la UI Client-Side

*Desarrollo de Software (Martes Noche)*


# Resumen

En esta clase dimos los primeros pasos en el desarrollo de interfaces del lado del cliente (Client-Side).

Repasamos la evolución de las arquitecturas **monolíticas** y **distribuidas**, la diferencia entre **cliente pesado** y **cliente liviano**, y cómo de esa necesidad de desacoplar responsabilidades surgió el patrón **MVC**.

A partir de ahí exploramos su evolución hacia **MVVM** y **Flux**, y vimos cómo estos modelos sentaron las bases del enfoque **reactivo** que caracteriza a **React** y a la mayoría de los frameworks modernos.

---

## 📑 Índice

- [Introducción](#introduccion)
- [Patrón MVC](#patron-mvc)
- [MVC en entornos Web](#mvc-en-entornos-web)
  - [MVC Server-Side](#mvc-server-side)
  - [MVC Client-Side](#mvc-client-side)
    - [Ventajas](#ventajas)
- [Variantes de MVC](#variantes-mvc)
  - [MVVM](#mvvm)
    - [Ventajas](#ventajas-mvvm)
    - [Problemas](#problemas-mvvm)
  - [Flux](#flux)
- [React](#react)
  - [Características](#caracteristicas)
    - [Reactividad](#reactividad)
    - [Estado y flujo de datos](#estado-flujo-datos)
    - [Virtual DOM](#virtual-dom)

<a id="introduccion"></a>
## Introducción

Hasta ahora trabajamos sobre la arquitectura del sistema del lado del **servidor**, donde se ejecutan las reglas de negocio y se manejan los datos.

En esta clase empezamos a mirar hacia el **lado del cliente**, es decir, hacia la interfaz con la que el usuario interactúa directamente.

Antes que nada, repasemos los dos grandes tipos de arquitectura:

- **Monolítica:** toda la aplicación vive en un mismo entorno (por ejemplo, un programa de escritorio).
- **Distribuida:** diferentes partes del sistema viven en distintos lugares (por ejemplo, aplicaciones web que combinan cliente y servidor).

Este cambio hacia lo distribuido nos lleva a repasar también la diferencia entre **cliente liviano** y **cliente pesado**:

- En el **cliente liviano**, el servidor hace casi todo: genera las vistas y las envía listas para mostrar.
- En el **cliente pesado**, el servidor envía solo los datos y el cliente se encarga de construir la interfaz.

> 💡 *Nota:* Para repasar en detalle cómo funcionan las arquitecturas **monolíticas** y la diferencia entre **cliente pesado** y **cliente liviano**, podés leer el apunte de la [**Clase N°2: Arquitectura y HTTP**]({{site.baseurl}}/bitacoras/2025-2c/martes-noche/clases/clase-02).

Ahora que entendemos dónde se ejecutan las distintas partes de una aplicación, necesitamos pensar **cómo organizar la interfaz del usuario** para mantener un buen orden interno y una clara separación de responsabilidades.

Ahí es donde entra en juego un patrón de diseño fundamental: el **MVC (Model–View–Controller)**.

---

<a id="patron-mvc"></a>
## Patrón MVC

El patrón MVC surge como una respuesta a un problema clásico: el **acoplamiento** entre la parte visual (la vista) y la lógica del dominio (el modelo).

En los primeros intentos, se tenía un modelo "Model-View" donde la vista no solo mostraba datos, sino que también debía manejar conversión y validación de entradas, así como decidir qué operaciones ejecutar en el dominio.

Para resolver esto, MVC propone dividir responsabilidades en componentes claramente diferenciados:

* **Modelo** (Model): representa el modelo de negocio o la capa de dominio. Contiene los datos y las reglas que definen cómo se comporta la aplicación.

* **Vista** (View): representa los elementos visuales que muestran ese modelo y permiten al usuario interactuar con él.

* **Controlador** (Controller): actúa como un intermediario entre la vista y el modelo. Recibe las acciones del usuario desde la vista, actualiza el modelo y decide qué vista mostrar a continuación.

En el esquema clásico de MVC, podemos distinguir dos tipos de interacciones:

**1. La carga inicial de datos:**

1. La **vista** pide datos al controller.
2. El **controller** los solicita al modelo, los transforma y los devuelve.
3. La **vista** renderiza esa información en pantalla.

**2. Las interacciones del usuario:**

1. Cuando ocurre un evento (por ejemplo, un clic o el envío de un formulario), la vista le avisa al **controller**.
2. El controller interpreta el evento, ejecuta la lógica correspondiente al **caso de uso** y actualiza el modelo.
3. Luego, la vista se actualiza para reflejar los nuevos datos.

En los sistemas transaccionales, los casos de uso suelen estar **basados en eventos (event-based)**, es decir, disparados por una acción del usuario.

Ahora bien, ¿qué ocurre si el **modelo cambia por razones externas** —por ejemplo, porque otro usuario modifica un dato?

En un entorno ideal, la vista debería poder enterarse de ese cambio y actualizarse automáticamente, sin intervención manual, lo que da origen al **[patrón Observer (publicador–suscriptor)](https://refactoring.guru/design-patterns/observer)**.

En ese patrón, la vista se **suscribe** al modelo: cada vez que el modelo cambia, **notifica** a sus suscriptores, y la vista se refresca para mostrar el nuevo estado.

En las aplicaciones web tradicionales, sin embargo, esto resulta difícil de lograr. Como el navegador y el servidor están desconectados la mayor parte del tiempo, la única forma de “enterarse” de un cambio externo suele ser **recargar la página (F5)** para volver a pedir los datos actualizados.

---

<a id="mvc-en-entornos-web"></a>
## MVC en entornos Web

El patrón MVC puede aplicarse tanto **en el servidor** como **en el cliente**, y la diferencia principal está en **dónde se construye la vista**.

<a id="mvc-server-side"></a>
### MVC Server-Side

En el modelo **Server-Side**, el **servidor** se encarga de procesar la lógica, combinar los datos y generar la vista completa.

El **cliente** (el navegador) solo recibe el resultado final —un documento HTML con estilo— y se limita a mostrarlo.

El flujo típico es el siguiente:

1. El cliente realiza una petición al servidor para obtener una página.

2. El **controller** en el servidor busca los datos en el modelo y los inserta en una vista utilizando un **template** (una plantilla de HTML con espacios reservados para datos dinámicos).

3. El servidor devuelve al navegador un **HTML + CSS** completo y listo para renderizar.

4. El navegador muestra esa vista.

Cuando el usuario realiza una acción (por ejemplo, envía un formulario o hace clic en un botón), el cliente envía una **nueva petición HTTP** al servidor.

El controller del servidor procesa el evento, actualiza el modelo y genera nuevamente la vista, que se envía de vuelta al navegador.

Este enfoque fue el más común en la primera etapa de la Web, pero tiene una limitación clara: si el modelo cambia en el servidor por razones externas, el cliente **no lo sabe** hasta que **recarga la página (F5)**.

---

<a id="mvc-client-side"></a>
### MVC Client-Side

Con el crecimiento de **JavaScript** y la potencia de los navegadores modernos, parte de la lógica del MVC comenzó a trasladarse al **cliente**.

En este modelo, el **servidor** ya no genera las vistas completas: solo envía **datos crudos**, generalmente en formato **JSON**.

El **cliente** (el navegador) se encarga de construir y actualizar la interfaz a partir de esos datos.

El flujo típico es el siguiente:

1. Al iniciar, el cliente descarga el código necesario de la aplicación: archivos **HTML**, **CSS** y **JavaScript** que aún no se ejecutaron.  
   > **Observación:** Estos archivos pueden provenir de un **servidor distinto** al que ofrece los datos.

2. Una vez cargado el código, el navegador comienza a **ejecutar la lógica de la vista**: renderiza parte del HTML estático y encuentra los scripts de JavaScript que controlan su comportamiento.

3. Dentro de ese código JS, el cliente realiza una primera petición al **controller** y éste los devuelve **en crudo**, transformados según el contrato de la API (por ejemplo, en formato JSON).

4. Con esa información, el cliente **arma la vista final** y la muestra en pantalla.

A partir de ahí, el ciclo continúa del lado del navegador.

Cuando el usuario interactúa (por ejemplo, hace clic o escribe algo), el **controller del cliente** decide qué hacer:

- Si la acción no requiere pedir nuevos datos, simplemente actualiza la vista localmente.
- Si la acción involucra el dominio (por ejemplo, guardar un cambio), envía una solicitud al backend, espera la respuesta y actualiza la vista con los nuevos datos.

Al igual que en el enfoque Server-Side, si el modelo cambia en el servidor por razones externas, el cliente no lo sabrá automáticamente, a menos que use mecanismos como **WebSockets** o **suscripciones en tiempo real**.

---

<a id="ventajas"></a>
#### Ventajas

El enfoque **Client-Side** introdujo mejoras notables:

- Permite actualizar partes de la interfaz **sin recargar** toda la página (mejorando la performance).
- Las llamadas al servidor se hacen **en segundo plano**, mejorando la fluidez.
- La vista puede reaccionar **en tiempo real** a la interacción del usuario.

Este modelo es la base de las **aplicaciones de página única (SPA, Single Page Applications)**.

---

<a id="variantes-mvc"></a>
## Variantes de MVC

Como vimos, el MVC ayudó a separar responsabilidades, pero en la práctica sigue teniendo algunas limitaciones.

En un entorno cliente–servidor, hacer que la **vista observe directamente al modelo** no es sencillo.

Si la vista no puede observarlo, entonces el **controller** debe encargarse de **modificar la vista** cada vez que cambian los datos.

Esto genera **acoplamiento** entre ambos: el controller necesita saber *cómo* actualizarla, no solo *qué* cambió.

Además, este enfoque es **poco declarativo**: en lugar de definir “qué estado quiero mostrar”, hay que escribir paso a paso *cómo llegar a él*.

Cuando existen muchos estados posibles, las combinaciones de cambios se vuelven difíciles de manejar y de razonar.

Por eso, con el tiempo aparecieron nuevas variantes del MVC que intentan resolver estos problemas y ofrecer una forma más **simple y declarativa** de construir interfaces.

---

<a id="mvvm"></a>
### MVVM

El patrón **MVVM** (Model–View–ViewModel) busca simplificar la comunicación entre la vista y los datos, eliminando parte del trabajo del controller.

Cada **componente visual** tiene su propio **ViewModel (VM)**, que representa su **estado actual**.

Ese estado incluye todo lo que la vista necesita mostrar, pero sin depender directamente del modelo del dominio.

El punto clave del MVVM es el **two-way binding**, un mecanismo que mantiene sincronizados la vista y el ViewModel.

Si el usuario cambia algo en la interfaz, el ViewModel se actualiza automáticamente, y si el código modifica el ViewModel, la vista refleja ese cambio sin que sea necesario escribir lógica adicional.

Veamos un ejemplo simple.

En el backend podríamos tener un modelo de dominio así:

```java
class Estudiante {
  String nombre;
  double promedio;
  boolean regular;
}
```

Y en el frontend, un **ViewModel** que lo adapta para la interfaz:

```js
class EstudianteViewModel {
  nombre = "";
  promedioTexto = "";
  estado = "";

  setEstudiante(estudiante) {
    this.nombre = estudiante.nombre;
    this.promedioTexto = estudiante.promedio.toFixed(1);
    this.estado = estudiante.regular ? "Regular" : "Libre";
  }
}
```

La vista se “bindea” (conecta) a este ViewModel: si el usuario modifica un campo —por ejemplo, cambia el nombre en un formulario—, el **two-way binding** actualiza el valor en el `ViewModel`.

Y si el código cambia el `ViewModel` (por ejemplo, al recibir datos del servidor), la vista se actualiza automáticamente.

En síntesis, el **ViewModel** es una **representación lógica del estado de la vista**: adapta los datos del dominio para que la interfaz pueda mostrarlos y modificarlos con facilidad.

---

<a id="ventajas-mvvm"></a>
#### Ventajas

- Elimina mutaciones manuales y reduce errores.
- Desacopla la vista de la lógica del dominio.
- Permite escribir código más **declarativo**: se describe qué mostrar, no cómo hacerlo.

---

<a id="problemas-mvvm"></a>
#### Problemas

- El **estado del ViewModel** puede **desincronizarse** del modelo real.  
  > Ejemplo: si el perfil muestra la cantidad de seguidores y un botón de “Seguir”, ambos deberían actualizarse juntos. Si solo cambia uno, la vista queda inconsistente.
- Los **valores calculados** dentro del VM deben **mantenerse coherentes manualmente**.  
  > Ejemplo: si el perfil muestra una ⭐ al superar los 1000 seguidores, el VM debe actualizarla cada vez que cambia el contador.

En aplicaciones con muchos componentes interdependientes, esta sincronización se vuelve difícil de manejar. De ahí surge **Flux**, que propone un flujo de datos más simple y predecible.

---

<a id="flux"></a>
## Flux

**Flux** surge como respuesta a los problemas que aparecen en MVVM cuando hay muchos componentes que dependen unos de otros.

En lugar de permitir que los cambios fluyan en todas direcciones, propone un **flujo de datos unidireccional**: la información va siempre en un solo sentido, lo que hace que el sistema sea más simple y predecible.

Podemos pensarlo así:

1. El usuario realiza una **acción** (por ejemplo, presiona un botón o envía un formulario).
2. Esa acción **genera un evento** que modifica el **store**, una estructura que guarda el **estado global** de la aplicación.
3. Cuando el store cambia, **notifica a las vistas** que dependen de esos datos.
4. Finalmente, las vistas se vuelven a renderizar mostrando la nueva información.

Observamos que se trata de un ciclo continuo y ordenado: **acción → store → vista**.

Luego, en Flux, las vistas nunca modifican directamente el estado, sino que describen qué debe pasar (“marcar como leído”) y el store aplica el cambio.

Sin embargo, este enfoque también tiene un costo: cada vez que cambia algo en el estado, **todas las vistas relacionadas se vuelven a renderizar**, incluso si algunas no lo necesitaban.

Luego veremos cómo **React** resuelve este problema con su sistema de **Virtual DOM**.

---

<a id="react"></a>
## React

**React** es una biblioteca moderna pensada para construir interfaces a partir de **componentes anidables**.

Cada componente es una pequeña unidad independiente, con su propio estado y comportamiento, que puede combinarse con otros para formar estructuras más grandes.

Dentro de cada componente encontramos tres ideas centrales:

- **Props:** los datos que recibe del componente padre.
- **State:** la información interna que maneja localmente.
- **Renderizado:** la función que define qué HTML y CSS se generan a partir de ese estado.

React utiliza **JSX**, un *superconjunto de JavaScript* que permite escribir estructuras parecidas a HTML dentro del código.

Por debajo, JSX se transforma en funciones de JavaScript, lo que nos da **toda la potencia de un lenguaje completo** sin perder legibilidad ni expresividad.

> En otras palabras, escribimos “como si fuera HTML”, pero en realidad estamos definiendo funciones que devuelven elementos visuales.

---

<a id="caracteristicas"></a>

### Características

React se apoya en tres pilares fundamentales que explican su popularidad y su forma particular de construir interfaces: la **reactividad declarativa**, la **gestión del estado** y el **Virtual DOM**.

<a id="reactividad"></a>

#### Reactividad

Cada componente en React puede entenderse como una **función pura** que describe *cómo debería verse la interfaz* en función de su estado actual:

```js
(state + props) => JSX
```

Cuando cambia el **estado interno (state)** o los **datos externos (props)**, React **vuelve a ejecutar el renderizado del componente** para reflejar ese nuevo estado.

Lo importante es que **no necesitamos indicar manualmente qué parte de la interfaz debe cambiar**: simplemente declaramos *qué mostrar* en función del estado, y React se encarga del resto.

A esta capacidad de mantener la interfaz sincronizada con los datos la llamamos **reactividad**.
La interfaz “reacciona” ante los cambios de manera automática y consistente.

---

<a id="estado-flujo-datos"></a>

#### Estado y flujo de datos

React adopta un **flujo de datos unidireccional**, inspirado en el patrón **Flux**.
Esto significa que la información siempre fluye **desde los componentes padres hacia los hijos**, y nunca al revés.

Cada componente puede tener su propio **estado local**, que representa la información que maneja de forma independiente.
Cuando ese estado cambia, el componente se vuelve a renderizar con los nuevos datos.

En los casos donde varios componentes necesitan compartir información (por ejemplo, el usuario logueado o un tema de color), React ofrece mecanismos como **Context** o bibliotecas externas como **Redux** para administrar un **estado global** de forma controlada. (lo veremos en próximas clases)

Este modelo simplifica el razonamiento: sabemos siempre **de dónde vienen los datos** y **qué componentes dependen de ellos**.

---

<a id="virtual-dom"></a>

#### Virtual DOM

Cada vez que cambia algo en el estado o las props, React vuelve a calcular la interfaz.
Sin embargo, en lugar de modificar directamente el **DOM real** del navegador —una operación costosa—, React utiliza una copia virtual llamada **Virtual DOM**.

El Virtual DOM es una **representación en memoria** del árbol visual.
Ante un cambio, React:

1. Crea una nueva versión del árbol virtual.
2. La compara con la versión anterior (proceso conocido como *diffing*).
3. Aplica al DOM real **solo las diferencias necesarias**.

De esta manera logra combinar lo mejor de ambos mundos:

* Un modelo **declarativo y simple**, donde no necesitamos preocuparnos por los pasos intermedios.
* Una **ejecución eficiente**, que actualiza únicamente lo que realmente cambió.