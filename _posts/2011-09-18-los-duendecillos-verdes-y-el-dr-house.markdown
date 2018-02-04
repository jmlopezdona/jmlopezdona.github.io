---
layout: single
title: Duendecillos verdes y el Dr. House
date: '2011-09-18T12:00:00.000+02:00'
author: José Manuel López
tags: 
modified_time: '2011-09-29T23:21:44.539+02:00'
thumbnail: http://3.bp.blogspot.com/-7l6GukQeWII/TnUFTvqEx1I/AAAAAAAAAgQ/cZDScz4S6mo/s72-c/duende_verde.jpg
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-5151997452437545170
blogger_orig_url: http://josemlopez.blogspot.com/2011/09/los-duendecillos-verdes-y-el-dr-house.html
---

De vez en cuando se encuentra algún problema o error que a primera vista no tiene mucho sentido, es más, parece que no hay una explicación razonable de lo que está pasando. Es como si hubiera un duendecillo verde en algún lado que está haciendo de las suyas.

![Duendecillo verde](http://3.bp.blogspot.com/-7l6GukQeWII/TnUFTvqEx1I/AAAAAAAAAgQ/cZDScz4S6mo/s200/duende_verde.jpg){: .align-center }

En este tipo de problemas, a priori, no parece imperar lógica alguna y muchas veces se tiene la tentación de dejarlo de lado, de hacer como si no existiera, pues no resulta fácil dar con su origen para poder solucionarlo. Pero, son muchas las ocasiones en las que el impacto es importante y hay que hacer todo lo posible por entender el problema y resolverlo.

Hay personas a las que este tipo de retos les entusiasma y otras, en cambio, les aburre o se bloquean a las primeras de cambio con frases del tipo "por más vueltas que le demos no habrá forma de encontrar lo qué está pasando", "esto no tiene sentido, vamos a tener que dejarlo", etc.

La principal ventaja que uno cuenta cuando va a resolver un problema software es que casi siempre hay una solución o cuando menos podremos de dar con el origen del problema que nos ayudará a ser capaces de ver con claridad a qué afecta y cual es su alcance.

Partiendo de este principio de confianza, y siendo optimistas, será suficiente con disponer de una estrategia que ayude a minimizar el tiempo de resolución. Esto es muy importante, pues una persona con interés, cierta capacidad y tiempo puede resolver cualquier problema, pero el tiempo suele estar limitado, bien porqué hay necesidad de resolverlo cuanto antes o porque si se dilata en el tiempo nos acabaremos desanimando o el coste de la resolución empezará a no ser asumible.

Ante un problema o error en una aplicación se pueden seguir las siguientes pautas:

1. Entender bien lo que está pasando, esto es fundamental.
2. Recopilación de toda la información de la que tengamos disponible: ficheros de log, volcado de hilos de ejecución, configuración del sistema, librerías utilizadas, experiencias previas, etc.
3. Realizar una búsqueda en Internet del problema para ver si a alguien más le pasa algo parecido. La intuición a veces resulta efectiva y si disponemos de una traza de excepción es posible que encontremos fácilmente el origen del problema e incluso su solución. Si el problema sólo nos pasa a nosotros, lo más probable es que sea realmente algo raro o, todo lo contrario, más sencillo de lo que parece.
4. Análisis detallado de los procesos, flujos de llamadas, etc., que puedan estar involucrados.
5. Realizar pruebas para intentar reproducir el problema o que al menos logren descartar situaciones que puedan estar causándolo.
6. De forma iterativa ir acotando el origen del problema repitiendo los pasos anteriores.

Si el problema no es muy extraño, lo habitual es que una sóla persona, con la ayuda de las excepciones que aparezcan en los ficheros de log, logre fácilmente dar con el origen del problema y su resolución.

Pero claro, si esto sucede podríamos decir que el problema no era tal o al menos no lo suficiente para despertar interés. Lo bueno viene cuando se trata de un problema raro, donde tras unas horas o días intentando resolverlo se sigue sin ver que puede estar pasando y con la sensación de no avanzar. En esos momentos es cuando se convierte en un reto: algo similar a lo que pasa con los casos de enfermedades raras de la serie del Dr. House.

Alguien puede pensar, ¿qué tiene que ver una serie de médicos con la resolución de un problema software? Pues más de lo que en principio puede parecer. Si llegados al punto de catalogar un problema como una rareza, algo único que parece no tener razón de existir, es cuando mejor aplican los métodos del **Dr. House**.

En concreto es de gran ayuda realizar un trabajo en equipo, podemos decir que el número de personas a involucrar dependerá de la dificultad del problema y su prioridad, pero en términos generales entre 3-4 personas puede ser suficiente, alguna de ellas es conveniente que no esté "contaminada" con el problema. Es fundamental disponer siempre de al menos un facilicitador que en los momentos de desesperación, máxime si se trabaja contrarreloj, aporte pausa y criterio, que permita encauzar el proceso de análisis.

El proceso es similar al que se puede realizar de forma individual pero aumentado su efectividad gracias al análisis y razonamiento de varias personas a la vez, lo que ayuda a ver el problema desde diferentes perspectivas y aumentar la motivación en los momentos de desanimo. Se suele trabajar con reuniones de tormenta de ideas, que van acotando y definiendo las causas del problema, donde todo el mundo participa y de las que se surgen pruebas a realizar y/o la necesidad de seguir indigando en algún aspecto en concreto para tener más información.

Será de gran ayuda que todas las personas tengan una visión crítica e intenten comprender cada elemento que forma parte del problema, por intrascendente que en principio pueda parecer. Suele ser habitual que los pequeños detalles resultan ser los fundamentales.

La clave es una mezcla de experiencia, constancia, capacidad analítica y criterio.

En general, la mayoría de estos problemas "raros" no suelen tener un origen complejo, es más, cuando se resuelven producen cierto descrédito del propio problema en si. Pero, mientras esto sucede pueden ser tan extraños y graves que pongan en jaque a cualquiera. Por eso es importante, al resolver un problema de este tipo, celebrarlo convenientemente, ¡nos lo habremos ganado!  

Por último, un ejemplo de un problema del tipo **<span class="Apple-style-span" style="color: #38761d;">duendecillo verde</span>**:

Hace unos días, uno de mis equipos de desarrollo se encontró con un problema extraño, al parecer, de forma aleatoria, algunos de los ficheros que una aplicación guardaba en disco tenía un carácter ilegible. El problema se puso de manifiesto cuando afectó a una rutas de ficheros que se almacenaban en su contenido, haciéndolas ilegibles y no pudiendo acceder a ellas.

El problema era grave pues afectaba a una aplicación de importancia para el negocio del cliente y ocasionaba errores en en otros sistemas. Además, se tenía la dificultad de que no se podían utilizar los mismos datos en los entornos de pruebas ni mucho intentar reproducirlo en producción.

En una primera aproximación al problema, se comprobó que afectaba a las vocales acentuadas. Así que, a primera vista, se podría tratar de un problema de codificación de caracteres, pero no podía ser porque la cadena de caracteres afectada se encontraba bien en otras partes del mismo fichero. Además se usaba codificación unicode en toda la aplicación, incluido el fichero, lo que garantizaba el uso no sólo de vocales acentuadas si no de caracteres de cualquier idioma.

El análisis de la información disponible acotaba el error al grabar el fichero en el disco, ¿se estarían corrompiendo por un problema hardware en el servidor? Tras un análisis más detallado, usando un editor hexadecimal se identificó que los dos caracteres que aparecían por la vocal acentuada, por ejemplo Autorizaci��n.pdf, estaban compuestos por tres bytes: 0xEF 0xBF 0xBD. Tras una búsqueda en Internet se determinó que correspondían al carácter unicode [REPLACEMENT CHARACTER' (U+FFFD)](http://www.fileformat.info/info/unicode/char/fffd/index.htm) usado en las conversiones de caracteres cuando no se puede representar algo en unicode.

Esto dió una pista interesante tras comprobar que el problema afectaba a diferentes vocales acentuadas y en todos los casos aparecían siempre dos caracteres U+FFFD: las vocales acentuadas se codifican en UTF-8 con dos bytes, a diferencia de las sin acentuar (caracteres ASCII), por lo que podría ser un problema en algún buffer de conversión. Además, coincidía con que el problema sólo se produciera en algunos ficheros, pero siempre en alguna vocal acentuada.

Tras revisar de nuevo el proceso de grabación del fichero, se vio que el método usado para realizar una deserialización previa del contenido del fichero de una codificado binaria en [base64](http://es.wikipedia.org/wiki/Base64) a una cadena de caracteres en UTF-8, en vez de procesar todo el contenido de una vez, iba concatenando la decodificación de cada una de las lineas en las que se "rompe" cualquier contenido en base64:

![Base64](http://1.bp.blogspot.com/-JFUr0OjoiHQ/TnTstGq7BfI/AAAAAAAAAgM/cFPi_HCMm8U/s640/Base64.PNG){: .align-center }

Una sencilla prueba confirmó que ese era el problema y su resolución era tan simple como decodificar el contenido base64 completo sin tener en cuenta los retornos de linea. **¡Problema solucionado!**  

¿Quién se anima a contar algún problema curioso con el que se haya enfrentado? Entre todos seguro que nos da para hacer un libro...