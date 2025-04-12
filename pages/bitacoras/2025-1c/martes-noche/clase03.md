---
layout: page
title: Clase 3
description: Martes Noche, 2025, Primer Cuatrimestre
permalink: /bitacoras/2025-1c/martes-noche/clase-03/
---

# Resumen

En esta clase hablamos de:

* Arquitectura:  
  * Centralización:   
    * Estilos arquitectonicos  
      * Estilo Centralizado  
      * Estilo Distribuido  
      * Relativo a ambientes, no equipos físicos  
      * Son cualidades relativas, no absolutas  
    * Opciones  
      * Monolitico / Desktop  
      * Cliente Servidor   
        * Web  
        * Mobile  
      * Otros (No los profundizaremos):  
        * P2P  
        * Microservicios  
        * Etc.  
* Internet y la Web  
  * Internet, orígenes  
    * Internet: Red fisica (darpanet, blah blah)  
    * Web: Servicio que corre sobre internet  
    * Orígenes 
      * Bólo lectura
      * Basado en texto  
      * Impacto en la arquitectura
    * Hypertext  
    * El browser básico  
      * Hace consultas  
      * Lee texto  
      * Renderiza HTML 
  * Modelo cliente servidor:  
    * Hay un servidor con información centralizada que responde pedidos de los clientes.  
    * El flujo es restringido: El cliente solo hace pedidos y el servidor solo puede hablar con el cliente para responder sus pedidos  
  * Arquitectura Web  
    * La Web  
      * Es el conjunto de apps que corren sobre internet  
    * Es Cliente servidor  
    * Corre sobre internet  
    * Cómo funciona?  
      * HTTP    
        * Características:  
          * Pedido / respuesta  
          * Stateless (no hay noción de pedidos anteriores)  
          * Textual  
        * Pedido  
          * Métodos (GET / POST / PUT / DELETE)  
            * Semántica  
          * URI  
            * Ubicación \+ Recurso  
          * Headers (metadata)  
          * Body:  
            * Es texto  
            * Hay varios formatos  
        * Respuesta  
          * Código de respuesta   
          * Headers 
          * Body (como en el pedido) 
      * DNS  
        * Concepto de IP  
        * Concepto de dominio	  
  * Cómo uso esto para hacer una app?  
    * Divido mi app en partes  
      * Un servidor  
      * Un cliente  
        * Liviano  
          * El cliente recibe “vistas”, elementos visuales ya procesados listos para renderizar
          * Solo la lógica de la capas de Presentación relacionada a dibujar elementos en pantalla vive en el cliente 
        * Pesado  
          * El cliente recibe información más estructurada o “cruda” y luego genera las vistas. 
          * Parte de la lógica de las capas de Aplicación y Presentación viven en el cliente 
          * Nosotros haremos esto  
    * Cómo estructurar la comunicación entre cliente y servidor 
      * Se comunican usando HTTP  
      * Cliente liviano  
        * Necesito un formato que me permita “dibujar cosas”  
        * Uso HTML   
          * Lenguaje de "estructurado" de elementos visuales y texto.
      * Cliente pesado  
        * Necesito formatos más “estructurados”  
          * Generalmente del tipo Clave \-\> valor  
            * XML  
            * JSON  
            * Existen otros que no se usan para esto pero podrían (como YAML)  
      * Aprovecho convenciones de HTTP  
        * REST  
          * Orientada a recursos   
          * Aprovecha semántica de verbos  
          * Semántica de codigos  
        * Uso headers para transmitir el formato  
          * Content-Type/Accept  
        * Uso headers para otra metadata  
          * Location  
          * Authorization  
      * Concepto de API/Backend REST  
        * Servidor  
        * HTTP  
        * Usualmente JSON  
        * Varias rutas para formar las URLs   
          * Tmb llamados “endpoints”  
        * El cliente pesado me va pidiendo la información y la muestra (cómo? ya lo veremos\!)  

--- 

# Material

* [Presentación](https://docs.google.com/presentation/d/1SmpUEv0SpWgwclgbfPRaFdweCt46cDkWHzevVWGiPik/edit?usp=sharing)
* [Intoduccion a arquitectura web](https://docs.google.com/document/d/1LBqAhXPzn-aeN5BIRZBmIrU5RKiYvySyWH-2Jkn-kJw/edit?tab=t.0#heading=h.jii8bn1f6qx1)
* [Tutorial HTTP (para practicar)](https://github.com/flbulgarelli/http-tutorial/tree/master/tutorial/es)
