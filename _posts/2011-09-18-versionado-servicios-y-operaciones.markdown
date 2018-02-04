---
layout: single
title: Versionado de servicios
date: '2011-09-18T21:54:00.003+02:00'
author: José Manuel López
tags:
- Servicios Web
- Versionado
modified_time: '2011-09-25T13:23:00.752+02:00'
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-1470387030699160097
blogger_orig_url: http://josemlopez.blogspot.com/2011/09/versionado-servicios-y-operaciones.html
---

En una arquitectura SOA los servicios van evolucionando con el tiempo, lo que afecta a la definición de sus interfaces. Por eso, es de gran utilidad disponer de un procedimiento que permita minimizar el impacto de los cambios en los sistemas que usan los servicios. De esta forma, conseguiremos reducir las situaciones en las que es preciso regenerar los clientes de acceso, facilitando las tareas de mantenimiento y la adopción de los servicios.

Lo primero es comprender bien como se usa un servicio y que implicaciones tiene, porque, a veces, por la el propio lenguaje, se tiende a confundir o no diferenciar entre el propio servicio y las operaciones que lo componen. Es importante tener claro que un sistema sólo consume realmente un servicio si usa al menos una de las operaciones.

En adelante se asumen las siguientes condicionantes para encontrar el procedimiento de versionado más adecuado:  

1.  Los servicios pueden ser consumidos por sistemas de diversa índole: diferentes equipos de soporte, diferentes calendarios de subidas a producción, diferentes tiempos de desarrollo, diferentes prioridades, etc., lo que dificulta coordinar los cambios en los servicios.
2.  Se busca minimizar el número de servicios publicados, de forma que se pueda reducir la complejidad de uso, las tareas de mantenimiento y los recursos de infraestructura.

En una primera aproximación al versionado de un servicio podemos pensar en disponer de tantas versiones de éste como cambios se realicen en alguna de sus operaciones. Esto significará que se deberán de tener publicados las N versiones del servicio o todos los sistemas que lo consuman tendrán que regenerar sus clientes para utilizar la última versión del servicio.

Esta opción no es está demasiado alejada a lo que habitualmente se realiza en muchas organizaciones, de hecho, por poner un ejemplo, la SOA Suite de Oracle da mecanismos a nivel de despliegue en el servidor de aplicaciones para disponer de varias versiones de un mismo servicio e incluso marcar una de ellas como por defecto en el caso de que el cliente no especifique una versión específica. Pero esta estrategia conlleva varios inconvenientes que explicaré continuación.

Diferentes publicaciones de un servicio implica también diferentes punto de acceso (_endpoint_, ver [Web Service Glossary](http://www.w3.org/TR/ws-gloss/)). Es decir, los sistemas tienen que modificar la URI utilizada para acceder a las diferentes versiones de un servicio. Esto es un problema porque realizar modificaciones en un servicio no significa que estas vayan a afectar a todos los sistemas que lo utilizan, pero, al cambiar la versión y por tanto la URI de acceso, involucra cambios, sin excepción, en todos los sistemas que usen el servicio.

Es precisamente uno de los principales inconvenientes de realizar un versionado a nivel global del servicio, al obligar a regenerar todos los clientes de acceso de todos los sistemas o tener que mantener publicadas todas las versiones del servicio. Además, normalmente se suele mantener durante un tiempo las versiones antiguas, de forma que será preciso comunicar y coordinar la regeneración de los clientes de acceso y la nueva URI de acceso a todos los sistemas que lo consuman o estos dejaran de funcionar.

Para mejorar el proceso de versionado vamos a identificar las situaciones que motivan una nueva publicación de un servicio:

1. Se elimina una operación.
2. Se añade una operación nueva.
3. Se modifica una operación existente para corregir un error de implementación, pero no se modifica el funcionamiento especificado ni los mensajes de entrada, salida y fallos, es decir su interfaz.
4. Se modifica una operación existente para cambiar su funcionamiento a nivel interno pero no los mensajes de entrada, salida y fallos.
5. Se modifica una operación existente para cambiar su funcionamiento a nivel interno y también los mensajes de entrada, salida y/o fallos.

Una de las ventajas de trabajar con servicios, en vez de por ejemplo con EJB, es que el cliente es más "transparente" a las modificaciones, por ejemplo puede seguir consumiendo un servicio en el que hayan añadido y/o eliminado operaciones si no hace uso de estas. También puede seguir utilizando una operación en la que se añaden nuevos parámetros a los mensajes de su interfaz, si estos son opcionales, pues no se va incumplir el esquema XML de los mensajes intercambiados.

Esto puede hacernos pensar en aprovechar al máximo dicha versatilidad y no especificar versiones a nivel de servicio, por lo que la dirección de la definición del servicio (WSDL) y de acceso (endpoint) no tendrían que cambiar en diferentes publicaciones de un mismo servicio. Por supuesto, a nivel de desarrollo (versiones en el repositorio CVS, documentos de cambios, etc.) se deberá de tener el servicio correctamente versionado e incluso incluir el número de versión en el contenido (no en su URI) de su WSDL de forma que se pueda tener totalmente identificada.

Donde si será necesario incluir la versión de forma explicita es en el nombre de cada operación y en sus  mensajes de entrada, salida y fallos.

Es decir, en los casos 1 y 2 se verá modificdo el contenido del WSDL, pues la definición del servicio cambia, pero los sistemas que no quiera usar las nueva operaciones o no estuvieran utilizando las operaciones eliminadas (que habitualmente son reemplazadas por otras en el propio servicio o en otros servicios) no tienen que regenerar sus clientes en ningún caso.

El caso 3 es totalmente transparente para todos los sistemas, pues sólo es una corrección interna del servicio. Aunque a nivel de documentación, el servicio si puede aumentar de versión para reflejar el cambio realizado al ser un nuevo despliegue, eso sí, ni se modifica la URI de acceso ni su definición (WSDL).

Los casos 4 y 5 suponen aumentar la versión de la operación de forma que los sistemas pueden, de forma progresiva, ir utilizando la nueva versión. En función del alcance y prioridad del cambio la adopción de la nueva versión de la operación se deberá de realizar con más o menos rapidez por los sistemas que la usan. Pero, al no tener que eliminar la operación (se puede dejar un tiempo suficiente de convivencia de diferentes versiones) se pueden efectuar los cambiar en producción sin que los sistemas que no les ha dado tiempo a realizar el cambio se puedan ver afectados. Es más, puede planificarse el cambio sin la necesidad de coordinación con los sistemas que consumen el servicio.

En resumen, el procedimiento propuesto opta por versionar las operaciones de los servicios así como los mensajes de entrada, salida y fallos, de forma que un servicio, aunque a nivel formal cambie su versión, pueda contener durante el tiempo que sea establezca para el cambio, las versiones diferentes de sus operaciones que en cada momento se están consumiendo. Con este planteamiento una operación incluye una nueva versión cuando sucede alguna de las siguientes situaciones:

1. Cambia el funcionamiento definido para la operación
2. Cambia la estructura de los menajes de entrada, salida o fallo

Esta versionado de operaciones es simplemente cambiar el nombre de ésta. Por ejemplo, un servicio inicialmente puede tener una operacionaA_v1 y tras un cambio en la interfaz de esta operación pasa a tener una operacionA_v1 (en estado obsoleta y con fecha de caducidad) y una operacionA_v2.

El servicio como tal sigue manteniendo un versionado, pero, a diferencia de sus operaciones, sólo desde un punto de vista de documentación, de forma que se pueda tener un histórico que recoja los cambios, errores corregidos, etc. sobre sus operaciones

A nivel de mensajes de entrada, salida o fallos los tipos XSD, que no el nombre de los elementos XML, también son versionados cuando sufren cambios (por ejemplo, MensajeEntrada_v1, MensajeEntrada_v2, etc.) de forma que estén disponibles para versiones anteriores de las operaciones hasta que finalmente sean suprimidas del servicio. Ademas, así es fácilmente identificable por cada sistema la versión de los mensajes de interfaz que está usando del servicio en cada momento.

Destacar que sólo en el caso de cambios a nivel de funcionamiento o interfaz en una operación se aumenta la versión de ésta, siendo necesario, sólo para el sistema que necesite consumir la nueva versión, tener que regenerar el cliente de acceso al servicio y recompilar su código. Siempre será mejor adaptar en tiempo de compilación el uso del servicio que no encontrarse con errores en tiempo de ejecución.  

Con el procedimiento de versionado expuesto sólo hay necesidad de tener publicada una única versión del servicio, con diferentes versiones de sus operaciones, de forma que:  

* Simplifica la localización y configuración de la definición del servicio y de la URI de acceso por parte de los sistemas que van a consumir el servicio
* Reduce la necesidad de tener que regenerar los clientes de acceso al servicio cuando se realiza una nueva publicación.
* Reduce la complejidad de las tareas de evolución, mantenimiento y monitorización del servicio.
* Disminuyen el número de recursos necesarios para la publicación y ejecución del servicio.