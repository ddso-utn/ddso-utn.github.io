---
layout: page
title: Clase 2
description: Martes Noche, 2026, Primer Cuatrimestre
permalink: /bitacoras/2026-1c/martes-noche/clase-02/
---

# Clase N°2: Arquitectura y HTTP
*Desarrollo de Software K3552 (Martes Noche)*

# Resumen
Esta clase hablamos de Arquitectura de Software, cuáles son los esquemas más comunes y qué restricciones nos impone la tecnología. Aparte, respondimos consultas sobre Git y enviamos un video sobre Cualidades de Diseño 

## 📑 Arquitectura y DDS: Índice

- [Introducción](#introduccion)
- [Centralización](#centralizacion)
	- [Estilos de arquitectura](#estilos-de-arquitectura)
- 🌐 [La Web e Internet](#web-internet)
	- [DNS](#dns)
- 📨 [HTTP: El idioma de la Web](#http)
	-  [Elementos y conceptos](#elementos-conceptos)
		- [Métodos](#metodos)
		- [Códigos de estado](#codigos-estado)
		- [JSON](#json)
	- [Cómo es un pedido](#pedido)
	- [Cómo es una respuesta](#respuesta)
- [Clasificación del cliente](#clasificacion-cliente)
	- [Cliente liviano](#cliente-liviano)
	- [Cliente pesado](#cliente-pesado)
- [REST](#rest)
	- [Recursos y URIs](#recursos-uris)
- [APIs y backend REST](#api-backend-rest)
	- [Qué hace el servidor](#rol-servidor)
	- [Qué hace el cliente](#rol-cliente)
- [Conclusión](#conclusion)

<a id="introduccion"></a>
## Introducción

Cuando hablamos de **arquitectura de software**, nos referimos a la manera en que se organizan las diferentes partes de una aplicación y cómo interactúan entre sí.

En la clase anterior vimos que la **arquitectura en capas** es un esquema que divide una aplicación para separar responsabilidades.

Por ejemplo, una capa se encarga de la interfaz de usuario, otra de la lógica de negocio y otra de la persistencia de datos. Bajo este enfoque, estamos definiendo *qué hace* nuestro sistema. 

Sin embargo, en esta clase vamos a dar un paso más y trataremos de responder esta pregunta:

*¿Dónde se ejecuta **físicamente** cada componente para que la aplicación funcione?*

Si miramos las aplicaciones que usamos todos los días —como **Gmail**, **Instagram** o la **cámara** del celular— vemos que no todas funcionan igual:

- Algunas se instalan en nuestros **dispositivos** (como celulares o computadoras)

> Además, algunas corren de forma **local**, mientras que otras necesitan estar conectadas a internet.

- Otras se ejecutan directamente en el **navegador** (también llamadas *aplicaciones web*).

Dado que existe una gran variedad de aplicaciones, resulta útil clasificarlas según dónde se ejecutan sus componentes y cómo se comunican entre sí. Para ello, hablemos de la **centralización**.

<a id="centralizacion"></a>
## Centralización

La **centralización** en arquitectura de software no se refiere a equipos físicos, sino a **cómo se distribuyen** las responsabilidades y los recursos de una aplicación.

En líneas generales, existen dos enfoques:

1. **Estilo centralizado**: gran parte de la lógica y los datos se concentran en un único punto —por ejemplo, un servidor que responde a múltiples clientes.

2. **Estilo distribuido**: las responsabilidades se reparten entre distintos nodos o servicios que cooperan entre sí.

Es importante remarcar que estas son **cualidades relativas, no absolutas**; una aplicación puede estar mas o menos centralizada dependiendo de cómo esté diseñada.

<a id="estilos-de-arquitectura"></a>
### Estilos de arquitectura

De los enfoques mencionados surgen algunos estilos de arquitectura que son muy utilizados:

- **Monolítico (o Desktop)**: toda la aplicación corre en un mismo entorno, como un programa instalado en la computadora. Por ejemplo, **Visual Studio Code**.

- **Cliente-Servidor**: este es el modelo más extendido. Se basa en la interacción entre dos componentes bien diferenciados:

	1. **Servidor**: actúa como un punto centralizado que almacena la información y ejecuta la lógica principal del sistema.
	
	2. **Cliente**: se limita a enviar solicitudes y esperar respuestas del servidor.

	Es importante remarcar que el flujo de comunicación está **restringido**: el cliente únicamente puede realizar peticiones, mientras que el servidor solo puede responderlas.

Además, existen otras alternativas como el **P2P (peer-to-peer)** o los **microservicios**, que no veremos en profundidad pero también son muy utilizados.

---

En definitiva, la **arquitectura actual es el resultado de una mezcla de decisiones**:

- Algunas responden directamente a necesidades concretas del presente.

- Otras se mantienen por razones históricas: reemplazarlas sería más costoso o riesgoso que continuar apoyándonos en ellas.
 
Al final del día, lo que buscamos es **adoptar la arquitectura que mejor se adapte a nuestro contexto**, aquella que resulte más sencilla de implementar y que nos permita materializar la aplicación.

<a id="web-internet"></a>
## 🌐 La Web e Internet

Para entender dónde “viven” las aplicaciones que usamos todos los días, conviene separar dos conceptos fundamentales:

La **Internet** es la **infraestructura física**. Una red mundial de cables, satélites, routers y servidores que conecta computadoras en todo el planeta.

- Sus orígenes se remontan a **ARPANET** (en los 60'), un proyecto militar que sentó las bases de la conectividad descentralizada.

- En la práctica, Internet es el “soporte” sobre el cual se montan distintos servicios (correo electrónico, mensajería, Web, etc.).

Luego, la **Web** es uno de esos servicios que **corre sobre Internet**:

- Nació a principios de los 90 como un sistema de documentos de solo lectura, conectados mediante **enlaces** (o *hypertext*).

*Aunque hoy nos parezca trivial, fue algo revolucionario para su época (imaginen navegar solo usando el click🤯)*.

Finalmente, tenemos el **navegador** (o browser) que fue la pieza clave para masificar la red. En su versión más básica, cumple tres funciones:

1. **Enviar consultas** a un servidor.

2. **Recibir respuestas** (texto, imágenes, código).

3. **Renderizar** ese contenido para que sea comprensible e interactivo.

> **Nota:** el funcionamiento del navegador —cómo procesa, interpreta y renderiza los recursos— será abordado más adelante, en la parte de *frontend* de la materia.

<a id="dns"></a>
## DNS

Detrás de cada dirección web hay una **IP** (un número que identifica a un servidor).

El sistema **DNS** (Domain Name System) nos permite usar nombres fáciles de recordar —como `www.google.com`— en lugar de memorizar esas direcciones numéricas.

> **Aclaración**: Queda por fuera del alcance de esta materia profundizar sobre estos temas.

---

Podemos observar que la Web, entendida como el **conjunto de aplicaciones que corren sobre Internet**, funciona mayormente con el modelo **cliente-servidor.**

Es ahora que toca preguntarnos: *¿Cómo se comunican el cliente y el servidor?*

<a id="http"></a>
## 📨 HTTP: El idioma de la Web

El protocolo **HTTP (HyperText Transfer Protocol)** define cómo un cliente y un servidor intercambian información. Se basa en tres ideas simples:

1. **Pedido–Respuesta**: el cliente **inicia** cada interacción con un pedido, y el servidor responde.
 
2. **Stateless** (*sin estado*): cada pedido es independiente; el servidor no guarda memoria de interacciones anteriores, salvo que se utilicen mecanismos adicionales (cookies, sesiones, tokens).

3. **Textual**: los mensajes son texto plano, legibles por humanos y fáciles de inspeccionar.

<a id="elementos-conceptos"></a>
### Elementos y conceptos

<a id="metodos"></a>
#### Métodos 

Los **métodos** expresan la operación que un cliente quiere que el servidor realice sobre un recurso. Ellos son:

- **`GET`**: Se **lee** un recurso (no cambia su estado).
	Por ejemplo: `GET /usuarios/204` → devuelve el usuario solicitado.

- **`POST`**: Se **crea** un recurso en una **colección**.
	Por ejemplo: `POST /usuarios` (+body) → crea un usuario en la colección `usuarios`.

> **Observación**: También puede usarse para operaciones que no encajan en otros métodos, como el *login*.

- **`PUT`**: Se **reemplaza** un recurso completo.
	Por ejemplo: `PUT /usuarios/204` (+body) → reemplaza todos los campos del usuario solicitado.

- **`PATCH`**: Se **modifica parcialmente** un recurso.
	Por ejemplo: `PATCH /usuarios/204` (+body) → cambia sólo los campos solicitados.

- **`DELETE`**: Se **elimina** un recurso.
	Por ejemplo: `DELETE /usuarios/204` → elimina el usuario solicitado.

> **Nota**: Existen otros métodos (como `HEAD`, `OPTIONS` o `TRACE`), pero no los utilizaremos en esta materia.

<a id="codigos-estado"></a>
#### Códigos de estado

Los **códigos de estado** son números de tres dígitos que acompañan cada respuesta HTTP e indican el **resultado** de la petición.

Se agrupan en familias según el primer dígito:

| **Familia** | **Significado**               | **Ejemplos**                                                                 |
|-------------|-------------------------------|-------------------------------------------------------------------------------|
| **1xx**     | Informativos                  | `100 Continue` →El cliente puede continuar con la petición.                   |
| **2xx**     | Éxito                         | `200 OK` → Respuesta exitosa genérica. <br> `201 Created` → Recurso creado. <br> `204 No Content` → Éxito sin contenido (ej. tras un `DELETE`). |
| **3xx**     | Redirecciones                 | `301 Moved Permanently` → Recurso movido a otro lugar.                        |
| **4xx**     | Errores del cliente           | `400 Bad Request` → El pedido está mal formado. <br> `401 Unauthorized` → Falta autenticación.  <br> `404 Not Found` → recurso inexistente. |
| **5xx**     | Errores del servidor          | `500 Internal Server Error` → Error interno genérico. <br> `503 Service Unavailable` → Servidor no disponible. |

> 💡 **Tip**: pueden explorar todos los códigos en [http.cat](https://http.cat/) 🐱 o [http.dog](https://http.dog/) 🐶.

#### JSON

**JSON** (*JavaScript Object Notation*) es un **formato de texto** utilizado para representar e intercambiar datos de manera estructurada.

Se basa en la sintaxis de **objetos de JavaScript**, pero es un estándar independiente del lenguaje (se puede usar en cualquier tecnología).

Representa la información en forma de **pares key–value**, usando estructuras como:

- **Objetos**: agrupaciones delimitadas por `{ }`.

- **Arreglos**: listas ordenadas delimitadas por `[ ]`.

Por ejemplo:

```json
{
  "id": 204,
  "nombre": "Sofía",
  "rol": "estudiante",
  "materias": ["Arquitectura", "Redes", "Bases de Datos"]
}
```

<a id="pedido"></a>
### Cómo es un pedido

Un **pedido** (o *request*) contiene:

- **Método**: el verbo que indica la acción (`GET`,`POST`,etc).

- **URI**: la ubicación exacta del recurso sobre el que se quiere ejecutar la acción.

- **Headers**: *metadatos* sobre la petición (tipo de contenido, idioma, credenciales).  

- **Body (o cuerpo)**: opcional, se usa cuando se envían datos adicionales (ej. un objeto JSON).

Ejemplo en crudo:

```http
GET /usuarios/204 HTTP/1.1
Host: ddso-utn.com
Accept-Language: es
Accept: application/json
Authorization: Bearer token-super-seguro-123
```

> **Aclaración**: No escribiremos estos pedidos a mano: usaremos herramientas especializadas como [**Postman**](https://www.postman.com/web).

<a id="respuesta"></a>
### Cómo es una respuesta

Una **respuesta** (o *response*) contiene:

- **Código de estado**: informa el resultado de la operación (`200 OK`, `404 Not Found`).

- **Headers**: metadatos de la respuesta (tipo de contenido, codificación, políticas de acceso).

- **Body**: el contenido devuelto (HTML, archivo, JSON, etc.).

Ejemplo en crudo:

```http
HTTP/1.1 200 OK
Date: Tue, 26 Aug 2025 22:30:00 GMT
Content-Type: application/json
Content-Length: 58

{
  "id": 204,
  "nombre": "Sofía",
  "rol": "estudiante"
}
```

<a id="clasificacion-cliente"></a>
## Clasificación del cliente

Si pensamos en **quién construye la interfaz de usuario** en aplicaciones **cliente–servidor**, podemos distinguir dos modelos clásicos:

<a id="cliente-liviano"></a>
### Cliente liviano

En este modelo el servidor hace casi todo: procesa la lógica de negocio, arma las páginas y se las envía al cliente para que las muestre sin mayor procesamiento.

El cliente (por ej. el navegador) recibe principalmente **HTML** —es decir, "vistas" que están listas para mostrar.

<a id="cliente-pesado"></a>
### Cliente pesado

En este modelo el servidor **no envía páginas listas**, sino **datos crudos** (ej. en formato **JSON**). 

El cliente es quien se encarga de **interpretar esos datos y construir la interfaz de usuario**.

> Este es el enfoque más común en aplicaciones modernas, y el que usaremos en este curso.

<a id="rest"></a>
## REST

**REST** (*Representational State Transfer*) es un **estilo de arquitectura** muy popular para diseñar **APIs sobre HTTP**.

> Una **API** (*Application Programming Interface*) es el mecanismo mediante el cual un sistema expone sus funciones y datos para que otros puedan utilizarlos.

En REST, el foco está en **exponer recursos** (usuarios, productos, etc.) mediante **URIs claras y consistentes**, devolviendo **representaciones** de esos recursos (en nuestro caso, **JSON**).  

> Una **URI** (*Uniform Resource Identifier*) indica la ubicación exacta de un recurso.

<a id="recursos-uris"></a>
### Recursos y URIs

Un **recurso** es “algo” del dominio que queremos exponer y las rutas (*URIs*) los ubican:

| Tipo de recurso         | Ejemplo URI             | Significado                                  |
|--------------------------|-------------------------|----------------------------------------------|
| **Colección**           | `/usuarios`            | Conjunto completo de usuarios.               |
| **Recurso puntual**     | `/usuarios/204`        | Usuario con ID 204.                          |
| **Sub-recurso**         | `/usuarios/204/fotos`  | Las fotos pertenecientes al usuario con ID 204.     |

> **🔔 Importante**: Las URIs deben usar **sustantivos** para identificar recursos.
>   
> Las acciones (crear, leer, actualizar, eliminar) se expresan con **los métodos HTTP**, no en la URI:
> * `/crearUsuario` → Incorrecto  
> * `POST /usuarios` → Correcto

---

<a id="api-backend-rest"></a>
## APIs y backend REST

Una **API REST** es un **servidor** que expone información y operaciones mediante **endpoints**.

Cada **endpoint** es la combinación de una **URI** (recurso) y un **método** (acción). Por ejemplo:  

- `GET /usuarios` → devuelve la lista de usuarios.  
- `POST /usuarios` → crea un nuevo usuario.  
- `DELETE /usuarios/204` → elimina al usuario con ID 204.  

<a id="rol-servidor"></a>
### Qué hace el servidor

El **servidor** REST cumple dos funciones clave:  

1. **Lógica de negocio**: define y aplica las reglas de la aplicación.  
2. **Persistencia de datos**: guarda y recupera información (generalmente en una base de datos). 

Cuando recibe un pedido HTTP, el servidor lo interpreta, ejecuta la lógica correspondiente y responde con datos en **JSON**, siguiendo las convenciones de REST.  

<a id="rol-cliente"></a>
### Qué hace el cliente

En nuestro caso usamos un **cliente pesado**.  Esto significa que:  

- No recibe páginas completas, sino **datos crudos en JSON**.  
- Se encarga de **interpretar esos datos**, construir las pantallas y manejar la interacción con el usuario.  

Cada vez que necesita algo, hace un **pedido HTTP** a un endpoint específico, obtiene un JSON como respuesta y lo utiliza para **renderizar la interfaz** que ve el usuario.

<a id="conclusion"></a>
## Conclusión

Para cerrar, es importante remarcar cómo todos estos conceptos se conectan con el trabajo práctico que van a realizar:

Desarrollaremos una aplicación web basada en la arquitectura **cliente–servidor** y organizada en **capas** (multicapa).

Adoptaremos el modelo de **cliente pesado**, en el cual la lógica de presentación recae en el **frontend**.

El primer paso será diseñar y construir una **API REST**, encargada de exponer los recursos y la lógica de negocio en formato **JSON**.

Posteriormente, esa API será consumida desde el frontend, que procesará los datos y generará la interfaz de usuario con la que interactuarán directamente.

# Material
 - [Video de Cualidades de Diseño](https://drive.google.com/file/d/1enIq0az1Fx9dtB70GWRayN1i917yf5M6/view)

# Para la próxima clase
Estaremos trabajando sobre el enunciado de [Kommanda](https://docs.google.com/document/d/1QHOLDwn7LaETVxSIkOWK5nGT9xrBjatjZoiKafDebsw/edit?tab=t.0#heading=h.btqp28xuwru4). 

La idea es que lo traigan leido y tengan pensado cómo implementarían el modelo de objetos. Si se animan a empezar a pensar algunas rutas, mejor aun! Comenzaremos poniendo en común una solución para el modelo de dominio (no discutirermos sobre el mismo) y luego avanzaremos en la definición de Rutas HTTP que más tarde comenzaremos a implementar 
