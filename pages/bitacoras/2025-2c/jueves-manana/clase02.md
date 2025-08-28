---
layout: page
title: Clase 2
description: Jueves Mañana, 2025, Segundo Cuatrimestre
permalink: /bitacoras/2025-2c/jueves-manana/clase-02/
---

# Temario

 * Repaso JS.
 * Introducción a herramientas
 * Proceso de desarrollo. Etapas
 * Intro a backend con API REST. Concepto de framework y biblioteca
 * HTTP. REST
 * Modelo de Capas: Capa de Dominio Capa de Services, Capa de Controladores, Capa de Repositorios. Manejo de errores.  Alternativas, ventajas y desventajas. Intepretación del modelo.


# Resumen

En esta clase hablamos de lo siguiente:

## Repaso de JS

Hacemos un repaso de JavaScript (ya deberían haber tenido un primer acercamiento el sábado). Se trata de un lenguaje común, que se ejecuta en dos entornos diferentes (en el servidor, mediante `node`, y el cliente, mediante cualquiera de los motores provistos por tu navegador preferido) y ofrece varias herramientas que hacen de puente entre estos.

Repasamos algunas de sus características de sintaxis y tipado:

  - Lenguaje orientado a objetos (prototipos, clases)
  - Lenguaje con tipado "dinámico"
  - Lenguaje interpretado:
      - tenemos un intérprete que _parsea_ y ejecuta las instrucciones "al vuelo"


Mencionamos algunas de sus herramientas (`node`, `npm` / `yarn`) y hacemos una brevísima demo de `node` vs el navegador. Es que JavaScript soporta múltiples entornos de ejecución (_runtime environment_):

   - servidor: `node` (intérprete) + `npm` (gestor de paquetes / dependencias) + otras cosas
   - cliente: navegadores (_browsers_)
      - opera
      - brave
      - chrome: v8
      - firefox: spidermonkey


Por ejemplo, así se ve un programa `index.js` para `node`:

```javascript
// esto es un script / programa en lotes
function sumar(x, y) {
  return x + y
}

console.log("hola, soy un programa JS")
console.log(`y sé sumar: ${sumar(4, 5)}`)
```

Para ejecutarlo, hacemos `node index.js`.

## Mención a Markdown

- Lenguaje para formatear documentación, notas, etc
- Omnipresente en Github y otras herramientas
  - Sirve para hacer READMEs, Wikis, etc


## Arquitectura Web

Pero, ¿por qué son relevantes ambos entornos? Porque vamos a trabajar en ambos mundos: cliente y servidor. Esto nos da pié a hacer un repaso de la arquitectura distribuida, cliente servidor, web.

También nos sirve para contar una verdad sobre algo que no profundizamos en el encuentro anterior: el cliente no es un ser humano, sino un dispositivo, que corre otro software:

  - puede ser, por ejemplo, un cliente de línea de comandos (como `curl`)
  - o puede, más comúnmente, un navegador (Firefox, etc)

En la arquitectura Web, programar en el servidor es obligatorio, hacerlo en el cliente no. De hecho, hay diferentes estilos de clientes:
  - cliente liviano: solo tienen programación (significativa) en el servidor. En DDSi se trabajará esta arquitectura.
  - cliente pesado: tienen (y ejecutan) cantidades de código significativas tanto en el cliente (tipicamente navegador) como en el servidor. En DDSo utilizaremos esta arquitectura.
     - Tecnologías típicas: Angular, React, Vue

Además, los clientes pesados darán origen a una división (técnica, tecnológica, de equipos de trabajo) frecuente en el mundo Web: Front-end y Back-end (no es el mismo sentido que en otras materias): la primera es el nombre que se le da a la programación del lado del cliente, mientras que el segundo se le da a la programación del lado del servidor.

>
> Paréntesis para pensar: ¿Toda aplicación Web requiere JavaScript?
>
>  - El servidor se puede programar en CUALQUIER lenguaje.
>  - El cliente sí requiere JS, porque es el único lenguaje soportado en la práctica en los navegadores.
>      - Peeeeero, no toda aplicación requiere programar en el cliente (puede ser cliente liviano!)
>      - Igual, aún en aplicaciones cliente liviano podría haber alguna porción pequeña de JS
>

![Diagrama de arquitectura Web](https://www.plantuml.com/plantuml/png/IqmkoIzI22qkJIpAJEJYuihBJqbLSCx9JCqhIOLmWbEBoZ9JyekukA2g57Jju2gWD508hWu0)


>
> Para pensar: Frontend y Backend:
>
> ¿Qué diferencias habrá en el estilo de programación / las tecnologías / lo que se programa?
>   - Lenguaje: en el Front sí o sí tenemos que usar JS. En el servidor, no es necesario
>   - Versiones: puede haber diferencias en las versiones y tabla de compatibilidad del entorno de JS entre navegadores. Por lo tanto en el Front, tenemos que considerar que nuestro código podría no funcionar igual en todos los navegadores.
>   - Capacidad de cómputo/memoria: la programación del lado del cliente podría ejecutarse en entornos con menor capacidad de cómputo que el servidor (ejemplo, un celular)
>   - Seguridad: lo que se ejecuta en el servidor ocurre dentro de un entorno controlado, bajo nuestra supervisión, pero lo que se ejecuta en el cliente no: el cliente podría estar ejecutando un código modificado que NO sea el que diseñamos
>   - Conexión: el cliente podría tener un nivel de conectividad limitado (por ejemplo 3g)
>   - El servidor está bajo presión de cómputo: tiene que ser capaz de escalar su capacidad de cómputo a medida que tiene mas clientes.
>   - El código del servidor suele girar en torno al dominio, mientras que el código del cliente gira en torno a los elementos visuales y sus eventos e interacciones con quien usa la aplicación.


![](https://www.plantuml.com/plantuml/png/oyjFILK8JYqgoqp9B-82yvnpCbFpIbAvk1Iu4fDByeiKGejB4uioKnMuk60iNJkuAWWD4a8O0m00)

### HTTP

Acá hacemos una breve demo de un API JSON (utilizando [`json-server`, una herramienta excelente de prototipado](https://github.com/typicode/json-server)), de un servidor HTTP y de un cliente HTTP. Mencionamos que:

1. La comunicación entre cliente y servidor se hace a través del protocolo HTTP
2. Para gestionar la interacción http necesitamos (o mejor dicho, resultan convenientes) herramientas: comunicarnos "a mano" (a bajo nivel), abriendo sockets y escribiendo texto plano es engorroso. Por eso tenemos Frameworks HTTP como Express. (Paréntesis: biblioteca vs framework, ver apunte)

Además, hablamos de dos tipos de interfaces de sistemas...
   1. interfaces gráficas (_UI_)
   2. APIs (interfaz de programación de aplicaciones)

...y de dónde las encontramos en la arquitectura web cliente pesado
   1. servidor: expone APIs
   2. cliente: consume APIs y expone UIs

Mencionamos dos tecnologías para interactuar con APIs desde JavaScript:
   1. `axios`: biblioteca para consumir APIs HTTP
   2. `express`: framework para exponer APIs HTTP

Y por último, mencionamos el problema del asincronismo (profundizaremos luego en las [promesas](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Promise) y las palabras clave `async` y `await`)

## Modelo de capas

Ya hablamos bastante sobre aspectos físicos de las arquitecturas, es decir, sobre cuestiones de infraestructura tecnológica y sobre cómo distribuimos (o no) nuestros programas a lo largo de los nodos de una red. Sin embargo, poco hablamos sobre como organizar nuestros componentes lógicos (es decir, aquellos que podemos pensar y trabajar con cierta independencia de la tecnología de cómputo subyacente) tales como objetos, clases, módulos y paquetes. ¿Cómo organizar entonces nuestro código? ¿Cómo repartir nuestras responsabilidades?

En particular, en el contexto de la programación del _lado del servidor_ (ya sea porque estamos en una arquitectura web de cliente liviano o porque estamos trabajando en backend de una arquitectura web cliente pesado), hay varias formas de responder a esto:

  * Modelo de capas
  * Modelo MVC Web
  * Modelo VIP (_Interactor_)
  * Modelos orientados a objetos sin una arquitectura particular
  * Modelos orientados a objetos organizados únicamente en torno a _incumbencias_ de presentación, dominio y persistencia. Muchas veces esta idea y el modelo de capas convergen, pero acá la organización entre componentes no es tan rígida.

En esta materia estudiaremos el primero, que organiza a los componentes lógicos en 4 grupos principales (llamados capas o _layers_), clara y rígidamente estratificados. En este modelo se sigue una metáfora que recuerda a las capas geológicas: contamos capas _superiores_, cercanas al mundo HTTP, que van descendiendo hasta llegar a capas _inferiores_, vinculadas a la persistencia de datos. Además, cada capa sólo presenta interacciones con su capaz directamente superior o inferior:

  1. Capa de enrutamiento (nivel superior), en la que encontraremos _rutas_
  2. Capa de controladores, en la que encontraremos _controladores_
  3. Capa de servicios, en la que encontraremos _servicios_
  4. Capa de persistencia (nivel inferior), en la que encontraremos _modelos_ y _repositorios_ (también llamados _managers_ o _DAOs_)

> ⚠️ Es importante tener en cuenta que esta explicación es intencionalmente esquemática: la estructura de capas
> presenta muchas variantes (por ejemplo en algunas arquitecturas lógicas se trazan diferencias entre _repositorios_ y _managers_, o la capa de enrutamiento se omite) y diferentes interpretaciones (más rígidas o más laxas)
>


# Material

 * La [presentación de sábado sobre JS](https://docs.google.com/presentation/d/1DSlTheHfB-q5oMV98c9DQGYWgjIG6RV38k3JpKeDv7E/edit?slide=id.p1#slide=id.p1)
 * Herramientas de diagramación: [Mermaid](https://mermaid.js.org/) y [PlantUML](https://www.plantuml.com/)
 * La página de [Can I Use](https://caniuse.com/)
 * [Servidor HTTP de ejemplo](https://github.com/flbulgarelli/http-tutorial/tree/node-client) (con `express`)
 * [Cliente HTTP de ejemplo](https://github.com/flbulgarelli/http-tutorial/tree/node-server) (con `axios`)

# Tarea

 * [Tutorial HTTP](https://github.com/flbulgarelli/http-tutorial)
 * [Biblioteca vs Framework](https://docs.google.com/document/d/1D_MCoh4J8kL1MAKNlbDgAMu2nYxri-81nZBYOPFWnO0/edit?tab=t.0#heading=h.6ab0fffv8tld)
 * [Leer el tutorial de express](https://docs.google.com/document/d/1Nn6GMzm7bD9tvVi_wGjLbt8X4KEk5IChzXdPpEFK4vY/edit?tab=t.0#heading=h.halhyllz00mo)
 * Leer el enunciado del TP
