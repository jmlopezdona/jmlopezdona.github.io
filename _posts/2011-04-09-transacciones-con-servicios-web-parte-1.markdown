---
layout: single
title: Transacciones con Servicios Web
date: '2011-04-09T20:34:00.000+02:00'
author: José Manuel López
tags:
- Trasacciones
- GlassFish Metro
- JPA
- WS-AtomicTransaction
- Weblogic Server
- Oracle SOA Suite
modified_time: '2011-09-25T13:30:21.976+02:00'
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-3480750750031486795
blogger_orig_url: http://josemlopez.blogspot.com/2011/04/transacciones-con-servicios-web-parte-1.html
---

En el diseño de una una aplicación con procesos que modifican información en una base de datos es fundamental implementar el uso de transacciones, de forma que siempre se garantice que las operaciones se realizan de forma atómica, consistente, aislada y durable (principios [ACID](http://es.wikipedia.org/wiki/ACID)).

Para el desarrollo de una aplicación en Java se tienen diversas alternativas para la creación y propagación de la transacción entre diferentes procesos, tanto de forma declarativa como programática. Por ejemplo usando [Java Persistence API](http://jcp.org/aboutJava/communityprocess/final/jsr220/index.html) (JPA), el estándar definido dentro de Java EE, o empleando otras alternativas como el framework [Spring](http://static.springsource.org/spring/docs/3.0.x/spring-framework-reference/html/transaction.html) para la gestión de transacciones.

Si la aplicación necesita integrar información de otros sistemas podemos necesitar que las operaciones de base de datos que se realicen en ambos sistemas estén dentro de una misma transacción. Para esto se puede optar en sistemas Java por una integración con EJB mediante [RMI](http://en.wikipedia.org/wiki/Java_remote_method_invocation) o, por ejemplo, usar CORBA si se necesita interoperabilidad con otros sistemas que no estén implementados en Java.

Aunque, para la comunicación entre procesos internos de una misma aplicación Java, en el caso de estar distribuidos, se puede optar por una integración RMI con EJB, pudiendo realizar la propagación de la transacción, cada vez es más habitual el uso de servicios Web, máxime cuando la integración es entre sistemas diferentes, por su facilidad de interoperabilidad, al estar basado en estándares abiertos, para el intercambio de información.

Estos servicios Web suelen ser implementados utilizando SOAP sobre HTTP o directamente HTTP si se usa un estilo [REST](http://es.wikipedia.org/wiki/Representational_State_Transfer), protocolos que no permiten la gestión de transacciones.

Podemos definir un servicio transaccional como aquel que guarda información usando una transacción de base de datos. Si hablamos de servicios Web, habitualmente la transacción comienza cuando se inicia el servicio y finaliza tras completarse la operación al no soportar unirse a una transacción ya existente en el sistema que los invoca.

Ahora bien, como comentábamos antes, en una integración basada en servicios, su principal utilidad es proporcionar interoperabilidad para el intercambio de información entre diferentes sistemas. Por tanto, no es fundamental que las operaciones se realicen en una misma transacción. De hecho, en una orquestación de servicios donde se realiza un flujo de llamadas a varios servicios, es habitual incluir mecanismos de compensación para poder realizar el roll back de las operaciones si, tras haber realizado de forma satisfactoria la llamada a N servicios, la llamada al servicio N+1 no se realiza de forma correcta.

En general siempre se puede enfocar el diseño de los servicios de forma que las diferentes operaciones que tengan que agruparse dentro de una misma transacción se puedan implementar en un mismo servicio, y en caso de no poder ser así, siempre se puede incorporar los mecanismo de compensación que permitan deshacer las operaciones en el orden adecuado.

Pero, en el caso de necesitar implementar transacciones distribuidas entre varios servicios Web, ¿es posible?¿qué opciones hay disponibles? Si revisamos los estándares especificados en [OASIS](http://www.oasis-open.org/home/index.php), organismo encargado de desarrollar estándares abiertos para el intercambio de información con servicios Web, encontramos:

* [WS-AtomicTransaction v1.2](http://www.oasis-open.org/specs/#wstx-wsatv1.2)
* [WS-BusinessActivity v1.2](http://www.oasis-open.org/specs/#wstx-wsbav1.2)
* [WS-Coordination v1.2](http://www.oasis-open.org/specs/#wstx-wscoorv1.2)

Se tratan de especificaciones de reciente aprobación (febrero 2009), en los que han participado la mayor parte de los líderes de la industria, Oracle, Microsoft, IBM, SAP, RedHat, etc, que han incorporado, en algunos casos sólo de forma parcial, implementaciones en las versiones más recientes de sus principales productos.

Dicho esto es conveniente destacar de nuevo que siempre que sea posible es preferible evitar el uso de transacciones distribuidas entre diferentes bases de datos, con independencia de que la gestión se realice mediante interfaces de servicios Web, componentes EJB o directamente mediante el API JDBC de Java.

Una transacción distribuida implica usar el [protocolo commit en dos fase](http://es.wikipedia.org/wiki/Commit_de_dos_fases), lo que supone una solución más compleja, mayor uso de recursos, posibles bloqueos de objetos en la base de datos, etc. Por lo que siempre que sea posible es preferible evitar y optar por soluciones más sencillas tanto a nivel de diseño como de implementación.

Ahora bien, como puede haber casos en lo que sea necesario y compensen los inconvenientes que se introducen, es interesante explorar algunas de las implementaciones que hay disponibles en estos momentos:

* [GlassFish, framework Metro](http://metro.java.net/guide/Using_Web_Services_Atomic_Transactions.html)
* [Oracle Weblogic Server 11g](http://download.oracle.com/docs/cd/E17904_01/web.1111/e13734/transaction.htm#BABEJACE)
* [Oracle SOA Suite 11g](http://download.oracle.com/docs/cd/E14571_01/integration.1111/e10224/sca_bindingcomps.htm#SOASE86071)