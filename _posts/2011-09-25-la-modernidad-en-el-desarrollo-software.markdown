---
layout: single
title: La modernidad en el desarrollo software
date: '2011-09-25T19:49:00.000+02:00'
author: José Manuel López
tags:
- Java EE 6
- IMDG
modified_time: '2011-09-26T09:02:07.862+02:00'
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-5403382291039708428
blogger_orig_url: http://josemlopez.blogspot.com/2011/09/la-modernidad-en-el-desarrollo-software.html
---

El jueves pasado pude asistir al evento [Oracle Enterprise Java Developer Day](http://www.oracle.com/webapps/events/ns/EventsDetail.jsp?p_eventId=135262&src=7307403&src=7307403&Act=10). En general fue bastante interesante, sobre todo las exposiciones que se realizaron en la primera parte, luego las prácticas se hicieron un poco aburridas, quizás influyó que las herramientas presentadas me eran familiares.

Lo que más llamó mi atención fue el comentario de [Alfredo Casado](http://www.linkedin.com/pub/alfredo-casado/16/156/a15) (javaHispano), en su exposición sobre "Desarrollo Moderno y Ligero con Java EE 6", sobre el significado de la modernidad en el desarrollo de software: no es sólo utilizar las últimas tecnologías, es hacerlo aprendiendo de los errores del pasado.

Me identifico bastante con esta definición de modernidad y creo que es una buena reflexión. Realizar desarrollos modernos no es sólo utilizar tecnologías vanguardistas, es mucho más, es usarlas con criterio para hacer el proceso mas sencillo, productivo y de calidad, con el objetivo de poder construir aplicaciones más robustas, mantenibles, eficientes e innovadoras.  

Volviendo a los temas que se trataron en el evento, la revisión de lo nuevo que trae Java EE 6 me gustó bastante y me creo inquietud suficiente para retomar varias lecturas pendientes y realizar otras tantas pruebas de concepto. Lo curioso es que esta "nueva" versión de Java EE es de finales de 2009, pero como es comprensible los fabricantes necesitan cierto tiempo para poder adaptar sus productos, por lo que ahora es un buen momento para empezar a usar todo lo nuevo que trae.

Para el que quiera probar Java EE 6 puede optar por algunas de las [plataformas certificadas](http://en.wikipedia.org/wiki/Java_Platform,_Enterprise_Edition#Java_EE_6_certified). También os dejo un enlace interesante con el resumen de las diferencias respecto a la versión anterior: [Java EE 5 vs Java EE 6](http://alexander.holbreich.org/2011/01/javaee5-vs-javaee6/)

Otros temas de los que se hablaron fueron el uso de herramientas de construcción de proyectos (Maven), integración continua (Hudson/Jenkins, Sonar, etc.), desarrollo basado en pruebas (BDD, [Behaviour Driven Development](http://behaviour-driven.org/) y TDD, [Test Driven Development](http://www.agiledata.org/essays/tdd.html)), etc. Temas muy a tener en cuenta y que recomiendo incorporar en los proyectos, siempre que se pueda.

Por último se hablo sobre de In-Memory Data Grid (IMDG) y casos de uso para el procesamiento de transacciones extremas. Sin duda una tecnología cada vez con mayor adopción y que tiene toda la pinta que ha llegado para quedarse, por lo que va a ser necesario profundizar en el funcionamiento de productos como [Terracotta](http://www.terracotta.org/), [Oracle Coherence](http://www.oracle.com/es/products/middleware/coherence/index.html), etc. Por cierto, muy interesante la integración como cache de segundo nivel en JPA.
