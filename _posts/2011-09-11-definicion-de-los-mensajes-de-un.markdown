---
layout: single
title: 'Definir bien un servicio: esquemas XML'
date: '2011-09-11T18:44:00.000+02:00'
author: José Manuel López
tags:
- Schema XML
- JAXB
- Servicios Web
modified_time: '2011-09-25T13:25:16.606+02:00'
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-6606108239009511471
blogger_orig_url: http://josemlopez.blogspot.com/2011/09/definicion-de-los-mensajes-de-un.html
---

En el diseño de la interfaz de un servicio es conveniente definir en detalle los mensajes de entrada, de salida y de los posibles fallos que se pueden intercambiar.

Para la descripción de estos mensajes, aunque hay otras alternativas, es habitual emplear el lenguaje [Schema XML](http://www.w3.org/XML/Schema) que permite establecer en detalle las estructuras de campos, tipos de datos, restricciones en los valores (patrones, listas...), obligatoriedades, estructuras alternativas, etc.

Es demasiado habitual encontrar interfaces diseñadas sin haber tenido suficiente conocimiento en el diseño de esquemas XML. Típicos ejemplos son mensajes donde todos los campos son del tipo xsd:string, lo que no permite acotar de forma detallada los valores que pueden contener. Por ejemplo, es particularmente problemático, en estos casos, el intercambio de valores de fechas, donde por no emplear el tipo xsd:date o xsd:datetime obliga a establecer (y a documentar, en el mejor de los casos) el formato de fecha a intercambiar.

Esto, además de ser un foco de problemas, supone trabajo adicional en la posterior implementación, tanto del servicio en si, como de los clientes que lo utilizan, pues lo habitual, por no decir lo recomendado, es utilizar una librería, por ejemplo, en el caso de Java, la especificación [JAXB](http://jcp.org/en/jsr/detail?id=222), que transforme un documento XML en una estructura de objetos. No ofrece el mismo trabajo que un campo fecha se transforme en un objeto del tipo GregorianCalendar, específico para la representación de fechas, que un uno String empleado para texto en general.

En otros casos, por desconocimiento del elemento [xsd:choice](http://www.w3schools.com/Schema/el_choice.asp), estructuras que deberían de definirse bien diferenciadas se opta por agruparlas, teniendo que diferenciarlas en ejecución por el valor de alguno de sus campos. Un ejemplo puede ser la definición de la estructura de los datos de una persona que incluye su dirección, pudiendo ser ésta una dirección española o extranjera, con diferentes estructuras de campos, tipos, obligatoriedades para cada una. Con el elemento xsd:choice no hay problema en definir dos tipos diferentes de datos para cada dirección y en función de la residencia de la persona incluir el valor de una de ellas.

Para evitar errores de diseño como los comentados es necesario conocer bien las estructuras y [tipos de datos](http://www.w3.org/TR/xmlschema-0/#simpleTypesTable) (texto, fechas, numéricos, binarios en base 64, direcciones Web, etc.) incluidos en el lenguaje para la definición de esquemas XML.

Si se realiza un desarrollo en Java es conveniente entender el uso que se realiza en la especificación JAXB de los esquemas XML, siendo un buen punto de partida la lectura del tutorial de la implementación de referencia de la especificación: [GlassFish > Metro > Tutorial](http://jaxb.java.net/tutorial/)

n general, cuanto más restrictiva sea la declaración de la interfaz de un servicio, y por consiguiente la estructura de los mensajes intercambiados, menos propensos son los errores de interpretación de los sistemas que consumen dichos servicios. Esto es crítico en servicios de integración, donde pueden haber diferentes equipos de desarrollo involucrados y una correcta documentación del servicio es fundamental.

La definición de los esquemas XML de los menajes intercambiados en un servicio, además de ser la base de la documentación de su interfaz, es un mecanismo de validación de gran utilidad al poder automatizar, en la llamada al servicio, que los mensajes intercambiados son los que se han definido. Por ejemplo, si un sistema llama a un servicio y el mensaje de entrada no cumple con el esquema establecido, si se ha habilitado en el servicio su validación, directamente se devolverá una excepción al sistema origen, delimitando de forma clara el error.