---
layout: single
title: 'Codemotion 2012: conociendo nuevos trucos de magia'
date: '2012-04-01T14:43:00.000+02:00'
author: José Manuel López
tags: 
modified_time: '2012-04-15T13:10:56.794+02:00'
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-2357871927052284766
blogger_orig_url: http://josemlopez.blogspot.com/2012/04/codemotion-2012-conociendo-nuevos.html
---

Hace unos días tuve la oportunidad de asistir a la codemotion que se celebró en Madrid. Sin duda, una excelente idea juntar en un mismo evento diferentes tipos de tecnologías: Javascript, Microsoft, Agile, Devops, Mobile, Ruby, Cloud, Java, PHP, HTML, .NET, Grooby, Phyton, etc. En estos casos, la diversión está asegurada si eres entusiasta de la tecnologías y te interesa conocer cual es el estado del arte en el desarrollo software, con independencia del lenguaje de programación utilizado.

Hubo siete track simultáneos durante el día que duró el evento. En general me gustaron todos a los que asistí, aunque ya se sabe que elegir siempre es difícil y me quedé con las ganas de haber podido ir a alguno mas. A modo de resumen os pongo las presentaciones a las que fui y las impresiones que me causaron:

# Creando Web Apps con express.js, zombie.js y knockout.js (Iván Loire)

Un buen ejemplo del "revival" que está viviendo Javascript: desde hace tiempo viene pegando muy fuerte en la parte cliente para la construcción de interfaces de usuario avanzadas con una buena productividad de desarrollo, y con la aparición del framework [node.js](http://nodejs.org/) también está proporcionando buenas soluciones para la parte servidor.

Ya conocía algo de node.js y esta charla me ha animado a encontrar un rato para realizar alguna que otra prueba de concepto y comprobar sus posibilidades. Es un framework que destaca sobretodo por su sencillez y rendimiento, permitiendo procesar muchas peticiones en paralelo gracias a una buena gestión de los hilos cuando hay bloqueos I/O en el procesamiento, lo habitual, por ejemplo, si se accede a una base de datos o un sistema de ficheros.

Para el desarrollo de aplicaciones Web se presentarón las librerías express.js para trabajar con un patrón MVC, [knockout.js](http://knockoutjs.com/) para renderizar el HTML y realizar el binding con los valores del modelo y [zombie.js](http://www.blogger.com/) para la realización de pruebas unitiarias simulando el entorno de ejecución de un navegador Web. 

La aplicación que se utilizó como ejemplo utilizaba [websocket](http://dev.w3.org/html5/websockets/) para una comunicación bidireccional y full-duplex entre los clientes Web y el servidor, poniendo de manifiesto los puntos fuertes de node.js: reducidos tiempos de respuesta y capacidad para procesar una gran cantidad de peticiones simultaneas. Se habló también de [socket.io](http://socket.io/) como alternativa a websocket para navegadores que no tienen soporte para HTML5.

Durante la presentación, viendo el pontencial de node.js, me vino a la memoria la plataforma [spire.io](http://www.spire.io/) donde, junto con el uso de [redis](http://redis.io/), ofrecen un PaaS de mensajería para aplicaciones. Este tipo de ejemplos son los que ponen de manifiesto que **NO** está todo inventado y que conocer las nuevas tecnologías que van surgiendo te permite poder emprender la construcción de productos novedosos. Por los requerimientos que parece tener node.js no descartó que hayan montando la plataforma con un servidor en la nube (Amazon EC2) para tener un modelo de negocio "elastico": coste de infraestructura proporcional al uso que realicen de su servicio. En este caso la clave está en apostar por tecnologías como node.js y redis que permite escalar bastante bien y permitir ofrecer un servicio novedoso a bajo coste.

# From Dev to DevOps (Carlos Sánchez)

No había escuchado antes de esta presentación hablar del movimiento [DevOps](http://dev2ops.org/blog/2010/2/22/what-is-devops.html), pero me parece muy interesante la idea de reducir la barrera que suele haber entre desarrolladores y operadores, con el objetivo de "agilizar" la puesta en producción de nuevas versiones de aplicaciones.

Habitualmente las prioridades de los grupos de desarrollos y operación de una organización son diferentes, lo que se pone más de manifiesto cuando los desarrolladores utilizan metodología ágiles y se generan con intervalos de tiempo mucho más cortos nuevas versiones de aplicaciones a instalar. Los operadores, cuyo principal objetivo es garantizar la estabilidad de los sistemas, se sienten más cómodos con un ritmo menos elevado de implantación, máxime cuando muchas veces las instrucciones facilitadas no son claras y los procesos se realizan mediante intervención manual.

Seria mucho más conveniente poder disponer de procesos de actualización automáticos de los entornos, lo que minimizaría los riesgos y reduciría los tiempos de implantación de nueva versiones de aplicaciones.

Para esto, de forma similar a como las herramientas de integración continua facilitan la adopción de metodologías ágiles en los procesos de desarrollo, el movimiento devops busca "agilizar" la implantación en producción. Las metodologías en las que se basa devops utilizan una aproximación similar a la utilizada en desarrollo para poder gestionar los entornos de operación: **infraestructura como código**. A mi modo de ver, no deja ser una forma de enfocar la gestión de configuración de los entornos desde un punto de vista de desarrollo. De hecho, al tratar la configuración como código los problemas de gestión se pueden resolver con los mismos conceptos utilizados en el control de versiones de cualquier desarrollo software: tags, release branchs, etc.

Detrás del movimiento devops hay disponibles varias herramientas para resolver la configuración de la infraestructura mediante código. Algunas de las más populares son: [puppet labs](http://puppetlabs.com/) y [chef](http://www.opscode.com/chef/).

Con puppet se puede realizar una configuración del entorno de forma declarativa, de forma similar a como para una aplicación definimos sus dependencias con Maven. Es decir, se indica el estado que se quiere conseguir pero no los pasos para conseguirlo. Para especificar un orden determinado se pueden usar dependencias. También se pueden emplear variables de entorno de sistema, condicionales, agrupar definiciones en clases, plantillas, módulos, realizar test, etc.

Otras herramientas interesantes y complementarias son:

* [Vagrant](http://vagrantup.com/): para construir y distribuir entornos virtuales usando Oracle VirtualBox.
* [VeeWee](https://github.com/jedi4ever/veewee): permite automatizar la creación de imagenes base con vagrant. Por ejemplo, se puede partir de una imagen inicial de ubuntu, instalar paquetes, configurar credenciales de acceso, etc. de forma que tengamos una imagen virtual personalizada a partir de la cual configurar nuestro entorno con puppet o chef.
* [Geppetto](http://cloudsmith.github.com/geppetto/): plugin de Eclipse para editar los manifiestos y módulos de puppet.

El movimiento DevOps pinta bastante bien y hay ya bastante módulos pre-construidos que automatizan tareas de instalación y configuración de muchos tipos servidores (Apache, Tomcat, etc.) ahorrando tiempo y evitanto cometer errores gracias a trabajar con procesos automáticos en vez de manuales.

Para el tema de pruebas también hay ventajas, ¿cuantas veces nos hemos encontrado con un error en producción que no logramos reproducir en desarrollo por temas de entorno? Con las metodologías y herramientas devops sería tan sencillo como partir de la imagen base de producción y ejecutar el código configuración para tener un entorno idéntico (al margen de los datos de aplicación, claro está) con el que realizar pruebas.

Os dejo el enlace del [blog](http://blog.carlossanchez.eu/) del ponente con bastante información sobre devpos.

# Desarrollo con Guice, Jersey y AppEngine (Nacho Coloma)

La presentación se centro en exponer en base a la experiencia del ponente como salvar las principales dificultades en el uso de la plataforma PaaS de Google y cómo sacar el mayor rendimiento. El enfoque fue interesante y agradecí que no fuera una mera exposición de las principales características del entorno de desarrollo. 

Me dejó bastante sorprendido los ajustes y limitaciones a realizar para poder implantar una aplicación en AppEngine por el hecho de que Google no permite que el arranque de la aplicación supere los 30 segundos. Para esto algunas de las recomendaciones que se realizaron fueron: 

* Evitar librerías pesadas: por ejemplo, olvidaros de Spring... :-(
* Evitar configuraciones con búsquedas en el classpath
* Inicialización lazy siempre que sea posible

ambién se presentó Jersey como un framework bastante simple y sin excesiva funcionalidad, pero adecuado para realizar interfaces tipo REST con JSON. En este sentido nada que no se pueda conseguir con otras herramientas, pero en caso de trabajar con AppEngine sería la opción a utilizar. Me gustó más Guice como framework de inyección de dependencias, aunque de nuevo también hay otras alternativas fuera del cloud de Google.

Otras recomendaciones que se realizaron para mejorar rendimiento y costes de ejecutar en la nube:

* No utilizar variables de sesión.
* Uso de base58 para acortar los identificadores en las URL
* Usar JSON en vez de XML
* Reducción del número de indices del modelo de datos. Restringido a un máximo de 200 por la plataforma.
* Nombre reducidos para tablas y columnas
* Cachear todo lo posible
* Utilizar SimpleDS en vez de JPA o JDO

En general el desarrollo una aplicación para AppEngine tiene bastante limitaciones por lo que hay que leerse con detenimiento la documentación. Pero la parte positiva es que se aprende muchas buenas prácticas asociadas a mejorar el rendimiento.

Os copio el [enlace](http://www.slideshare.net/icoloma/codemotion-appengine) a las slides de la presentación.

# Single Page Application con Backbone (Julien Castelain y Denis Ciccale)

Si se está pensando en desarrollar una aplicación tipo SPA con interfaces de usuario avanzadas y mucho JavaScript resulta imprescriptible utilizar alguna estrategia para organizar y estructurar bien el código, de lo contrario nos quedará una solución tipo "espagueti" difícil de comprender, mantener, probar y evolucionar. 

Afortunadamente, con el auge y resurgir de JavaScript, han ido apareciendo numerosos frameworks para ayudarnos a implementar patrones de diseño MVC o MVVM que facilitan tener un código bien estructurado. Las alternativas son varias y si realizáis una búsqueda encontrareis que cada uno tiene sus ventajas e inconvenientes. Os copio el [enlace](http://goo.gl/ODpkm) tras realizar un trending entre algunas de las alternativas más populares (BackBone, Knockout, JavaScriptMVC y Batman). 

La presentación trató sobre los fundamentos de backbone, una de la alternativas con más adeptos. Si bien 45 minutos no dan para mucho, se expusieron las bases: el modelo, las colecciones de modelos, el uso de plantillas con underscore.js o handlebar (éste último como recomendación), la interacción entre componentes mediante eventos, el uso de enrutadores para controlar la navegación, el patron Pub/Sub, la gestión de recursos/librerías con RequireJS, etc. 

Os dejo un [enlace](http://addyosmani.com/blog/building-spas-jquerys-best-friends/) interesante como introducción al desarrollo de aplicaciones tipo SPA con herramientas como backbone, jquery, etc.

# Integrando Sistemas reales con REST, JMS, Protobuf y MongoDB (Andrés Pérez y David Gómez) 

La presentación fue interesante: un problema complejo real y dos ponentes con mucha experiencia. Lo malo fue que se les hicieron escasos los 45 minutos de los que disponían y no pudieron exponer la parte de MongoDB. 

En general me gusto la exposición del dominio del problema (aunque quizás aquí se les fue parte del tiempo) y la estrategia seguida para abordar el problema de escalabilidad que se les planteó. La explicación sobre los servicios REST fue bastante didáctica y se resumen en tres conceptos: 

* HTTP como protocolo de comunicación y no sólo de transporte.
* No ha sesiones: el estado es responsabilidad del cliente y no del servidor.
* URI: identifica recursos y no una acción.

Sobre los servicios REST y colas JMS si bien es reconfortante ver que son utilizados como piezas clave en un proyecto de envergadura, conceptualmente no es nada novedoso.

En cambio me llamó mucho la atención el uso [Protobuf](http://code.google.com/p/protobuf/) (Protocol Buffers), herramienta de Google que no conocía, que permite la codificación de datos estructurados de una forma eficiente y extensible. Además, al generar clases para la codificación / descodificación en Java, C++ y Phyton proporcionan una solución de gran interoperabilidad. Por lo que indican en la página del proyecto se trata del formato de intercambio interno de datos de Google, utilizado para casi todas las comunicaciones RPC y formato de ficheros. Ahí es nada xD.

# APIs REST usables (Javier Ramírez) 

Esta presentación fue muy divertida. El punto álgido fue el [símil entre Darth Vader y Hello Kitty](http://goo.gl/9dq3l); coincido con Javier, hay cosas que pueden "molar" por separado, pero cuando las juntas... xD 

Cosas interesantes que anoté: 

* El API como elemento básico de comunicación entre componentes software pero que es utilizado por personas, por lo que es fundamental que sea usable, de lo contrario se corre el riesgo que nadie lo utilice :-( 
* Facilitar el uso todo lo posible, a modo de ejemplo, para la parte de autentificación está bien ofrecer [oauth](http://oauth.net/) por pero asumiendo que puede ser "incomodo" de utilizar, dar también otras posibilidades como acceso mediante token o autentificación básica.
* Tipica pregunta cuando explican la aproximación REST y que todo lo que recuperas son recursos. ¿Cómo hacemos para realizar acciones en un servicio? Las acciones se tiene que transformar en verbos. Por ejemplo, "Imprimir PDF" y realizar una petición POST (acción HTML de dar de alta un recurso).
* REST no es un estandar, es una recomendación sobre arquitectura. Como tal está en continua evolución y es posible encontrar diferencias sobre que mejores práctica aplicar.
* Para el descubrimiento del API hay diferentes estrategias, una de ellas es la de publicar una lista de enlaces donde se describa lo que hace cada operación y como utilizarlas. Otra opción es devolver una plantilla rellena a modo de ejemplo para que el cliente introduzca sus datos.

# ¿Por qué metodologías ágiles? (Jesús J. Ballano)

Fue básica en conceptos, como corresponde a un introducción sobre este tipo de metodologías, pero me gustó porque hicieron bastante hincapié en la exposición de las principales motivaciones, con ejemplos simples pero muy cotidianos. 

Siempre que asisto a una presentación sobre "agilismo" me vienen a la cabeza el mismo problema de siempre en el desarrollo software: suele ser un proceso de ingeniería con altas dosis de **artesanía** e **innovación** que dificulta en gran medida el poder tener una estimación predictiva de cada tarea a realizar. 

A diferencias de otros sectores (construcción, industria, etc.) se pide con bastante frecuencia la utilización de herramientas extremadamente vanguardistas, con frecuencia somos de los primeros que las utilizaremos y seguramente habrá errores que corregir y/o "sufrir", y una capacidad continua de adaptación a cambios en los requerimientos. 

Coincido con las metodologías ágiles que esto no debe de ser un problema, si no justamente lo contrario, un valor que podemos ofrecer. De hecho, me entusiasme como el que más trabajar con nuevas herramientas (siempre que aporte algo mejor a lo existente, claro está) y desarrollar cosas que realmente resuelvan problemas y ofrezcan un valor para el que las va a utilizar. 

En este sentido, la clave que aparece en cualquier presentación de metodologías ágiles es la **excelencia** en todos los aspectos del desarrollo (análisis, implementación, pruebas, implantación, etc.) como algo esencial para poder conseguir el éxito. Y aunque parece de sentido común, esto lleva a conclusión de que el "agilismo" no es para todos. Es decir, debes de tener un equipo experimentado, multidisciplinar, que conozca las tecnologías a utilizar y con un alto nivel de auto-aprendizaje, bueno si, puede haber alguna persona más junior para que vaya aprendiendo, pero el resto tiene que ser gente senior contrastada. 

Esto choca con el modelo de venta de muchas consultoras de software, precisamente porque no pueden ofrecer (o no siempre) a sus clientes equipos con este nivel de experiencia y fiabilidad. Por tanto, si en vez de "vender" un contrato cerrado con fecha de inicio y fin, ofrecieran un contrato por semanas en donde el cliente tras ver que le van ofreciendo decidiera si continua o no, habría un alto porcentajes de ventas que se cancelarían al poco tiempo. 

Ahora bien, desde un punto de vista de cliente, a veces se quiere un contrato cerrado para cubrirse las espaldas y poder exigir al proveedor la entrega del software en los plazos acordados. Pero esto, en muchas ocasiones, es totalmente contraproducente porque lo entregado suele distar de lo que realmente se  necesita, por no hablar de la calidad, mantenibilidad, etc., del software desarrollado bajo la presión de los tiempos marcados. 

Por eso, si tienes equipos con gran experiencia, debería de ser más sencillo vender proyecto sin riesgo para los clientes, que en vez de contratar un paquete cerrado puedan evaluar la capacidad que le ofrece el equipo e ir disponiendo de productos funcionales, a medida que se van añadiendo mas requerimientos. Este modelo funciona muy bien con startups pues es un claro exponente de requisitos cambiantes, evolución para adaptarse a la competencia y sobretodo porque no se pueden comprometer al coste de un proyecto cerrado ante la posibilidad de quedarse sin fondos para su patrocinio. 

En resumen, la mejor estrategia, salvo que se tenga muy claro lo que se quiere construir y se está seguro que no va necesita cambios, sería pedir una presupuesto estimado al inicio, y luego ir evaluando el rendimiento ofrecido por el proveedor en intervalos cortos (unas semanas, un mes como máximo) de iteraciones completas y funcionales de parte del producto. Claro que esto supone un esfuerzo e implicación por parte de todos, incluidos los propios clientes. 

# Construyendo ecosistema para desarrolladores (David Bonilla)

Fue la última presentación a la que asistí y, al margen de la publicidad encubierta de los productos de Atlassian, bien enfocada y no excesiva, anote varias cosas que me parecieron interesantes:

* Estamos demasiados acostumbrados al "todo gratis" y no hay nada malo en vender y potencial la parte comercial del desarrollo software. Al margen de que también podamos dedicar esfuerzos a la comunidad y el software libre.
* Un producto da rentabilidad incluso cuando estamos durmiendo, mientras que si realizamos servicios sólo cobraremos por el tiempo que dediquemos.
* Para convertir un producto en una plataforma es necesario la involucración de la comunidad de desarrolladores. Pero para esto hay que ganarse su "hamor" (¿patrocinar eventos?) y ofrecer una buena API, documentación, ejemplos, foros, publicidad, oportunidades de negocio, etc. Llegar a conseguir esto implicar invertir una gran cantidad recursos económicos durante mucho tiempo. Por esta razón los principales exponentes de plataformas están en las grandes compañías de software (facebook, google,  atlassian, etc.).
* Realizar plugins para plataformas también puede ser una gran oportunidad de darse a conocer como desarrolladores y/o obtener beneficios económicos. Entre otras cosas porque se puede aprovechar la inmensa comunidad de usuarios que tienen.

Por último os paso algunos enlaces interesantes:

* [Impresiones, reacciones y repercusión](http://codemotion.es/follow-up) en la página de codemotion
* [Recopilación de recursos, artículos y tweets interesantes](http://asanzdiego.blogspot.com.es/2012/03/codemotion-es-2012-recopilando-datos.html) que ha hecho @asanzdiego