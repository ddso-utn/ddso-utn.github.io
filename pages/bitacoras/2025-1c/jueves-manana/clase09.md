---
layout: page
title: Clase 9
description: Jueves Mañana, 2025, Primer Cuatrimestre
permalink: /bitacoras/2025-1c/jueves-manana/clase-09/
---

# Temario

 * Frontend Testing. E2E. Herramientas
 * User experience. Concepto.
 * Reglas prácticas de UX. Accesibilidad

# Resumen

### UI, UX, Usabilidad y Accesibilidad

En esta clase conversamos sobre cobre conceptos de UX y accesibilidad. En particular:

  1. Qué es UX o experiencia de usuarie. Hablamos de la idea de aportar valor a le usuarie, o mas bien, a la empresa u organización dueña del sistema / producto y de cómo la UX busca llevar a la persona a realizar las acciones más importantes / de más valor.
  2. Cómo se diferencia del diseño de UI y Usabilidad (poder utilizar / descubrir la funciones del sistema con mínima ayuda, tanto en un primer uso como en usos subsecuentes). Mencionamos que la usabilidad está vinculada con saber donde están las cosas y en que el sistema presente reacciones esperables,es decir que presente un bajo nivel de sorpresa. Además, la vinculamos con conceptos tales como espaciado, tipografías, colores, tamaños, proximidad, orden de lectura, diseño mobile first, _analytics_, _calls to action_, tiempos de espera y cuestiones de contraste. Todos estos contenidos serán desarrollados en profundidad en el video de UX.
  3. En qué se diferencia del concepto de accesibilidad y por qué es tan importante (ser accesible no es una opción, **es una obligación***). En particular:
    * Presentamos los atributos ARIA, los atributos `alt` y las etiquetas semánticas.
    * Hablamos de lectores de pantalla
    * Hablamos sobre validadores de accesibilidad

#### Paréntesis: tipos de componentes

Hay componentes con los que podemos interactuar y desencadenar una acción puntual: enlaces y botones. Suelen verse como:
  - círculos o cuadrados redondeados. Formato típico de los _call to action_
  - "tres puntitos" y "hamburguesas". Formato típico para abrir menús y desencadenar acciones contextuales (generalmente de menor _valor_ que los _call to action_)


### Situación del sistema científico universitario

Luego conversamos sobre la [situación universitaria](https://www.cin.edu.ar/en-el-problema-universitario-esta-en-juego-el-futuro-de-la-nacion/) y [científica actual](https://www.cin.edu.ar/sin-respuesta-ni-plan-para-la-ciencia-del-pais/), [la movilización convocada para esta semana](https://www.infobae.com/educacion/2025/06/23/las-universidades-publicas-se-movilizan-el-jueves-en-todo-el-pais-para-reclamar-por-la-ley-de-financiamiento-y-habra-paro-docente/) y [la ley de financiamiento universitario](https://www.cin.edu.ar/hacia-un-nuevo-proyecto-de-ley-de-financiamiento-universitario/) y [la convocatoria para apoyar a la misma](https://www.cin.edu.ar/yo-apoyo-la-ley-de-financiamiento-universitario/)


### Pruebas E2E

Realizamos una breve mención a técnicas y tecnologías de pruebas punta a punta (end to end, E2E). Algunas de ellas (para el ecosistema de JavaScript) son:

  * [Cypress](https://www.cypress.io/)
  * [Playwright](https://playwright.dev/)

Otras (más historicas, pero igual vigentes):

  * Selenium
  * Capybara

Mencionamos sus ventajas y desventajas: por un lado son herramientas que permiten la prueba a lo largo y ancho de un sistema, asegurando que casos de uso completos puedan ser validados, aún cuando involucran interacciones con sistemas externos. Por otro lado, por su naturaleza las pruebas son frágiles y altamente dependientes de pequeñas modificaciones a las interfaces. Aún así, esto puede ser mitigado mediante un uso cuidadoso de selectores semánticos.


### Dudas

> Nota: Todos estos temas se profundizarán en DDSI.

Respondemos dudas. En particular, focalizamos en cuestiones vinculadas a login y manejo de sesión. Nos resulta útil repasar o presentar algunas cuestiones:

  1. Manejo de sesión: demostrar que un pedido HTTP fue realizado por la misma entidad que un pedido anterior. Esto puede sonar trivial, pero dado que el protocolo HTTP es stateless, no lo es. Por eso necesitamos de cabeceras que nos permitan el manejo de sesión: `Cookie` y `Set-Cookie`. La primera es una cabecera que se envía en pedidos HTTP, en la que el cliente envía un código (asociado a un cierto dominio) como prueba de que está continuando un pedido anterior y que permite dar continuidad a la sesión. La segunda es enviada por el servidor cada vez que necesite asignar o reemplazar la cookie existen para ese dominio. Luego, el cliente se encargará de enviar esta cookie como parte del siguiente pedido HTTP.
  2. Registración (_sign up_) e Inicio de sesión (_log in_): dos procesos típicos de sistemas destinados a usuaries finales en los que se alguna forma se asocia información a una persona (física o jurídica).
  3. Autenticación y Autorización: dos procesos de cualquier sistema en que haya operaciones o recursos protegidos. El primero trata de demostrar que un actor (una persona o incluso otro sistema) es quien dice ser, utilizando algún mecanismo de validación de identidad (como por ejemplo, una contraseña). El segundo trata de evaluar si ese actor cuenta con los permisos necesarios para hacer lo que intenta. Esto puede ser hecho mediante un control de acceso basado en roles (RBAC), que puede o no ser jerárquico.
  4. Autenticación básica HTTP (_Basic-Auth_).
  5. Token _al portador_ (_Bearer_). Un mecanismo alternativo tanto de manejo de sesión como de autenticación y autorización. Pueden ser enviados dentro de la cabecera `Cookie` y `Set-Cookie` (con lo que se vuelven a muchos fines prácticos y a ojos del cliente indistinguibles de una cookie normal) o mediante la cabecera `Authorization`. Es importante tener en cuenta que de esta última forma la gestión del envío de estos tokens pasa a ser manual (a diferencia de lo que ocurre con las cookies, que por defecto son enviadas por el navegador en cada pedido HTTP al dominio correspondiente). Hay dos casos ampliamente difundidos de uso de token al portador:

      * como una forma de manejo de sesión en aplicaciones para usuaries como finales. En este caso, la autenticación se realiza mediante los mecanismos usuales, pero en este caso la cookie contiene al token.
      * como una forma de manejo de autenticación y autorización en el contexto de APIs HTTP.

Y dejamos también unas notas finales sobre implementaciones "a mano" y la conveniencia de utilizar soluciones de gestión de usuaries como Keycloack.

Estas son algunas de las notas de clase que tomamos:

> - Autorización
>   - Poder evaluar permisos de acceso a ciertos recursos u operaciones
>   - Porque queremos restringir el acceso sólo a quien tenga tal autorización
>
> - Autenticación
>   - Validar que un actor sea quien dice ser
>     - ¿Cómo se lo valida?
>       - En el mundo físico hay muchas opciones
>       - En el mundo virtual:
>           - usuario y contraseña (forma más básica)
>           - dos factores (two factor authentication)
>           - métodos tradicionales: fotos de DNI, pasaporte etc
>           - datos biométricos
>           - tokens (código) al portador (_bearer_) (sobre todo con actores no humanos)
>   - Una vez que estamos autenticados:
>     - podemos evaluar permisos
>     - podemos acceder a información personalizada
>
> Si soy una persona física, jurídica o de alguna forma mapeable a un ser humano y necesitamos
> autenticarme, tendré que hacer _login_ para autenticarme.
>
> Pero si HTTP es stateless, en cada pedido debería volver a enviar mis credenciales.
> Como esto es impráctico, en su lugar vamos a autenticarnos una sóla vez y crear un estado
> que perdure la duración del caso de uso. Ese estado conversacional se llama sesión.
>
>   Corolario: login = autenticación + creación de una sesión => "iniciar sesión".
>     En la sesión típicamente ejecutaremos más de un caso de uso (y típicamente ejecutaremos al menos uno).
>
> Como hacemos para gestionar la sesión un protocolo stateless como HTTP? Usando cabeceras (headers):
>
>   - Cookie:  `=>`
>   - Set-Cookie:  `<=`
>

# Material

* [Video sobre UX](https://www.youtube.com/watch?v=78l4oTU6AfA)
* [JWT](https://jwt.io/). Uno de los tipos de tokens al portador más extendidos, que definen partes tanto opacas como transparantes para clientes y/o servidores, además de un mecanismo automático de expiración de tokens.
* [OAuth](https://oauth.net/2/): un protocolo ampliamente difundido de autorización, que permite la autorización delegada. En este, mientras que un nodo (o servicio) es el responsable de validar la identidad del actor (autenticación), otros nodos o servicios del sistema (o incluso sistemas externos) pueden consumir datos como información de le usuarie y ser empleado para validar permisos (autorización).
* [Keycloack](https://www.keycloak.org/) una solución de código abierto de autenticación

# Tarea

## Accesibilidad

1. Instalar un lector de pantalla (o utilizar uno ya provisto por el sistema operativo). Ejemplos:
   1. Orca https://orca.gnome.org/
   2. JAWS
   3. NVDA
2. Elegir al menos un sitio
3. Navegar el sitio utilizando el lector de pantalla. ¿Qué partes no se pueden acceder? ¿Qué partes son leídas de forma incorrecta? ¿Qué elementos visuales como fotos e imágenes no se pueden leer? ¿Qué partes se leen en un orden incorrecto? Elaborar un breve informe.
4. Probar el sitio utilizando un validador de accesibilidad como por ejemplo https://wave.webaim.org/. ¿Qué otros errores se detectan?