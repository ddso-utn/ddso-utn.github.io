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

  1. Qué es UX y en qué se diferencia del concepto de diseño de UI y Usabilidad. Mencionamos conceptos tales como espaciado, tipografías, colores, tamaños, proximidad, orden de lectura, diseño mobile first, _analytics_, _calls to action_, tiempos de espera y cuestiones de contraste. Todos estos contenidos serán desarrollados en profundidad en el video de UX.
  2. En qué se diferencia del concepto de accesibilidad y por qué es tan importante (ser accesible no es una opción, **es una obligación***). En particular:
    * Presentamos los atributos ARIA, los atributos `alt` y las etiquetas semánticas.
    * Hablamos de lectores de pantalla
    * Hablamos sobre validadores de accesibilidad

### Situación del sistema científico universitario

Luego conversamos sobre la [situación universitaria](https://www.cin.edu.ar/en-el-problema-universitario-esta-en-juego-el-futuro-de-la-nacion/) y [científica actual](https://www.cin.edu.ar/sin-respuesta-ni-plan-para-la-ciencia-del-pais/), [la movilización convocada para esta semana](https://www.infobae.com/educacion/2025/06/23/las-universidades-publicas-se-movilizan-el-jueves-en-todo-el-pais-para-reclamar-por-la-ley-de-financiamiento-y-habra-paro-docente/) y [la ley de financiamiento universitario](https://www.cin.edu.ar/hacia-un-nuevo-proyecto-de-ley-de-financiamiento-universitario/) y [la convocatoria para apoyar a la misma](https://www.cin.edu.ar/yo-apoyo-la-ley-de-financiamiento-universitario/)


### Pruebas E2E

Realizamos una breve mención a técnicas y tecnologías de pruebas punta a punta (end to end, E2E). Algunas de ellas (para el ecosistema de JavaScript) son:

  * [Cypress](https://www.cypress.io/)
  * [Playwright](https://playwright.dev/)

Mencionamos sus ventajas y desventajas: por un lado son herramientas que permiten la prueba a lo largo y ancho de un sistema, asegurando que casos de uso completos puedan ser validados, aún cuando involucran interacciones con sistemas externos. Por otro lado, por su naturaleza las pruebas son frágiles y altamente dependientes de pequeñas modificaciones a las interfaces. Aún así, esto puede ser mitigado mediante un uso cuidadoso de selectores semánticos.


### Dudas

Respondemos dudas. En particular, focalizamos en cuestiones vinculadas a login y manejo de sesión. Nos resulta útil repasar o presentar algunas cuestiones:

  1. Manejo de sesión: demostrar que un pedido HTTP fue realizado por la misma entidad que un pedido anterior. Esto puede sonar trivial, pero dado que el protocolo HTTP es stateless, no lo es. Por eso necesitamos de cabeceras que nos permitan el manejo de sesión: `Cookie` y `Set-Cookie`. La primera es una cabecera que se envía en pedidos HTTP, en la que el cliente envía un código (asociado a un cierto dominio) como prueba de que está continuando un pedido anterior y que permite dar continuidad a la sesión. La segunda es enviada por el servidor cada vez que necesite asignar o reemplazar la cookie existen para ese dominio. Luego, el cliente se encargará de enviar esta cookie como parte del siguiente pedido HTTP.
  2. Registración (_sign up_) e Inicio de sesión (_log in_): dos procesos típicos de sistemas destinados a usuaries finales en los que se alguna forma se asocia información a una persona (física o jurídica).
  3. Autenticación y Autorización: dos procesos de cualquier sistema en que haya operaciones o recursos protegidos. El primero trata de demostrar que un actor (una persona o incluso otro sistema) es quien dice ser, utilizando algún mecanismo de validación de identidad (como por ejemplo, una contraseña). El segundo trata de evaluar si ese actor cuenta con los permisos necesarios para hacer lo que intenta. Esto puede ser hecho mediante un control de acceso basado en roles (RBAC), que puede o no ser jerarquíco.
  4. Autenticación básica HTTP (_Basic-Auth_).
  5. Token _al portador_ (_Bearer_). Un mecanismo alternativo tanto de manejo de sesión como de autenticación y autorización. Pueden ser enviados dentro de la cabecera `Cookie` y `Set-Cookie` (con lo que se vuelven a muchos fines prácticos y a ojos del cliente indistinguibles de una cookie normal) o mediante la cabecera `Authorization`. Es importante tener en cuenta que de esta última forma la gestión del envío de estos tokens pasa a ser manual (a diferencia de lo que ocurre con las cookies, que por defecto son enviadas por el navegador en cada pedido HTTP al dominio correspondiente).


# Material

* [Video sobre UX](https://www.youtube.com/watch?v=78l4oTU6AfA)
* [JWT](https://jwt.io/)

# Tarea

## Accesibilidad

1. Instalar un lector de pantalla (o utilizar uno ya provisto por el sistema operativo). Ejemplos:
   1. Orca https://orca.gnome.org/
   2. JAWS
   3. NVDA
2. Elegir al menos un sitio
3. Navegar el sitio utilizando el lector de pantalla. ¿Qué partes no se pueden acceder? ¿Qué partes son leídas de forma incorrecta? ¿Qué elementos visuales como fotos e imágenes no se pueden leer? ¿Qué partes se leen en un orden incorrecto? Elaborar un breve informe.
4. Probar el sitio utilizando un validador de accesibilidad como por ejemplo https://wave.webaim.org/. ¿Qué otros errores se detectan?