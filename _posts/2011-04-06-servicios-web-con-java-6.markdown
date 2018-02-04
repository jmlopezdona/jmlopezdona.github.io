---
layout: single
title: Servicios Web en Java
date: '2011-04-06T21:37:00.000+02:00'
author: José Manuel López
tags:
- Metro
- CFX
- Java 6
- JAX-WS
- Axis
- MTOM
- Servicios Web
- JAX-RPC
modified_time: '2011-09-25T13:26:00.751+02:00'
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-7253373200821609196
blogger_orig_url: http://josemlopez.blogspot.com/2010/11/servicios-web-con-java-6.html
---

Esta es una de las definiciones que se pueden encontrar sobre un [servicio web:](http://es.wikipedia.org/wiki/Servicio_web)

"_Un **servicio web** (en inglés, web service) es un conjunto de protocolos y estándares que sirven para intercambiar datos entre aplicaciones. Distintas aplicaciones de software desarrolladas en lenguajes de programación diferentes, y ejecutadas sobre cualquier plataforma, pueden utilizar los servicios web para intercambiar datos en redes de ordenadores como Internet. La interoperabilidad se consigue mediante la adopción de estándares abiertos. Las organizaciones [OASIS](http://www.oasis-open.org/) y [W3C](http://www.w3.org/) son los comités responsables de la arquitectura y reglamentación de los servicios Web. Para mejorar la interoperabilidad entre distintas implementaciones de servicios Web se ha creado el organismo [WS-I](http://www.ws-i.org/), encargado de desarrollar diversos perfiles para definir de manera más exhaustiva estos estándares._"

Al estar basado en la interoperabilidad el desarrollo de Servicios Web puede realizarse en diferentes entornos de desarrollo como Java o .NET.

Si nos centramos en el mundo Java, para el desarrollo de un servicio web se pueden emplear diferentes frameworks, por ejemplo, [Apache Axis](http://axis.apache.org/axis/), [Apache Axis2](http://axis.apache.org/axis2/java/core/), [Apache CFX](http://cxf.apache.org/) o [GlassFish Metro](http://metro.java.net/discover/). Estas implementaciones están basadas en alguna de las versiones del modelo de programación estandarizado dentro de la Comunidad Java.

Es interesante conocer la evolución de la especificación del modelo de programación de servicios web en Java, pues puede permitir identificar las características y compatibilidad, dentro de un mismo desarrollo, en el caso de utilizar diferentes frameworks.</div>

La primera especificación de servicios web (JAX-RPC 1.0), desarrollada dentro de la [Java Community Process](http://www.jcp.org/), fue [JSR-101](http://jcp.org/en/jsr/detail?id=101) liberada en junio de 2002 e incluida en J2EE 1.4\. Una versión actualizada (JAX-RCP 1.1) se publicó en octubre de 2003 para proveer mejor integración con [JAXB 1.0](http://jcp.org/en/jsr/detail?id=31) y un mejor soporte para el modo doc/literal.

La evolución de JAX-RPC en vez de ser JAX-RPC 2.0 pasó a denominarse JAX-WS 2.0 y se incluyó en Java EE 5 conviviendo con la versión JAX-RPC 1.1\. En el post "[JAX-RPC 2.0 renamed to JAX-WS 2.0"](http://weblogs.java.net/blog/kohlert/archive/2005/05/jaxrpc_20_renam.html) de Doug Kohlert se comentan las principales razones que motivaron el cambio de nombre en la especificación.

De las principales diferencias de la evolución de JAX-RPC 1.1 a JAX-WS 2.0 se pueden destacar:</div>

* Se basa en Java 5 y utiliza muchas de sus nuevas características como las anotaciones.
* Usa la especificación JAXB para el mapeo de los mensajes a estructuras Java lo que permite mejor soporte de XML Schema, así como mejorar el rendimiento. Más detalle en [este articulo](http://www.ibm.com/developerworks/webservices/library/ws-tip-jaxwsrpc2.html).
* Soporte para SOAP 1.2, aunque se mantiene el soporte para SOAP 1.1, HTTP 1.1 y WSDL 1.1 por lo que está asegurada la interoperabilidad con JAX-RPC.
* Soporte de WS-I's Basic Profile 1.1\. JAX-RPC soporta la versión 1.0 de las especificaciones de interoperabilidad.
* Permite desarrollar clientes dinámicos con un modelo de programación orientada a mensajes y también permite interacciones asíncronas.
* Soporte para MTOM, para optimizar el intercambio de datos adjuntos en los mensajes. Para una introducción sobre esta tecnología ver [este articulo](http://www.crosschecknet.com/intro_to_mtom.php).
* Permite usar XML/HTML como alternativa a SOAP para desarrollo de servicios RESTful.

Desde la versión 6 de Java se incluye en la JRE la implementación de referencia (RI) de JAX-WS lo que permite publicar o acceder a servicios web sin tener que utilizar otros frameworks que implemente la especificación ni incluir librerías adicionales en el proyecto para tener soporte para servicios web. También se incluye un contenedor web ligero para la publicación de los servicios sin necesitar un servidor de aplicaciones.

Este soporte nativo desde la versión 6 de Java, requiere tener la precaución de tener que sobrescribir adecuadamente las versiones de las librerías que se incluyen en la JRE si se quiere utilizar una versión JAX-WS superior, como puede suceder al usar alguna de las últimas versiones de frameworks como Axis, CFX, etc.

Enlaces interesantes para profundizar en el uso de servicios web en Java:<

1. Apache Axis 2: [descripción del modelo de programación de JAX-WS](http://ws.apache.org/axis2/1_5_1/jaxws-guide.html).
2. Oracle: [inclusión de la referencia de implementación de JAX-WS en Java 6](http://java.sun.com/developer/technicalArticles/J2SE/jax_ws_2/)
3. GlassFish: [comparativa de rendimiento de implementación de JAX-WS](http://weblogs.java.net/blog/kohsuke/archive/2007/02/jaxws_ri_21_ben.html)
4. Spring: [Spring Web Services](http://static.springsource.org/spring-ws/sites/2.0/)
