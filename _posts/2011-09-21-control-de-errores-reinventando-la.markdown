---
layout: single
title: Control de errores, ¿reinventando la rueda?
date: '2011-09-21T23:18:00.001+02:00'
author: José Manuel López
tags:
- SOAP
- Servicios Web
- Faults
modified_time: '2011-09-25T20:46:33.664+02:00'
thumbnail: http://1.bp.blogspot.com/-oiHN9VTD7VY/Tn8Cq2AeXyI/AAAAAAAAAgs/bTD8pyUwyuI/s72-c/servicioWeb.png
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-2049623434179245481
blogger_orig_url: http://josemlopez.blogspot.com/2011/09/control-de-errores-reinventando-la.html
---

Cuando se define la interfaz de un servicio no suele haber demasiada confusión en qué incluir en el mensaje de entrada, parece claro que debe ser la información necesaria para poder realizar la operación, ni más ni menos. En cambio, en el mensaje de salida, se tiende a incluir en algunas ocasiones, además de la propia información de respuesta, estructuras de control de excepciones, con las siguientes consecuencias:

1. La definición del mensaje de respuesta tiene que incluir una estructura de datos adicional para cuando se producen excepciones.
2. Si se usa una estructura genérica para el control de errores, dificulta poder especificar información diferente para cada excepción. Esto no suele tener importancia si lo que se busca es que el sistema cliente se limite a registrar el problema, pero es fundamental si se devuelve información, que aun no siendo habitual, es parte del funcionamiento del servicio.
3. Obliga a documentar el mecanismo de control de excepciones del servicio para que los sistemas cliente lo puedan interpretar.
4. El sistema cliente para usar el servicio tiene que incluir en su código un procesado específico de la estructura de control de excepciones definida.

¿No estamos en estos casos reinventado la rueda? ¿No está definido en la especificación de servicios como realizar el control de excepciones?

Antes de ver los mecanismos disponibles para representar fallos en un servicio es conveniente identificar los tipos de excepciones que se pueden producir:

* Originadas por el propio el funcionamiento del servicio, representado escenarios alternativos al uso principal donde se devuelve el mensaje de respuesta. Suelen ser especificadas en la fase de diseño del servicio y son de utilidad para los sistemas clientes, que deben de capturarlas y tenerlas en cuenta en la lógica de sus procesos.

* Debidos a errores en la ejecución del servicio: errores de conectividad, de infraestructura, defectos de implementación, mensajes de entrada que no cumplen la interfaz, etc. Suelen ser excepciones demasiado genéricas como para ser incluidas en la definición del servicio. En estos casos los sistemas clientes se limitan a registrar la información en su log de errores. 

El primer tipo de excepciones, al ser parte del funcionamiento del servicio, conviene incluirlas en la documentación de la interfaz, de forma similar a como se realiza con la excepciones del tipo _checked_ en cualquier lenguaje de programación.

Por suerte, si revisamos los tipos de mensajes que se pueden incluir en la definición de un servicio, además de los mensajes de petición y respuesta se pueden especificar tantos mensajes de fallos como sean necesarios:  

[![](http://1.bp.blogspot.com/-oiHN9VTD7VY/Tn8Cq2AeXyI/AAAAAAAAAgs/bTD8pyUwyuI/s1600/servicioWeb.png)](http://1.bp.blogspot.com/-oiHN9VTD7VY/Tn8Cq2AeXyI/AAAAAAAAAgs/bTD8pyUwyuI/s1600/servicioWeb.png)

* **Petición **(_request_): mensaje de entrada al servicio. Se define siempre, aunque su contenido puede estar vacío, a excepción de las interfaces callback en el caso de servicios asíncronos.
* **Respuesta **(_response_): mensaje de salida "principal" del servicio. En el caso de servicios asíncronos no se define puesto que el cliente no espera una respuesta inmediata del servidor. En el caso de estar definido un mensaje de respuesta inplica que el servicios es síncrono, aunque es valido que el contenido sea vacío.
* **Fallos **(_faults_): puede haber definidos de 0 a N mensajes de salida de fallos en el caso de un servicio síncrono. Si es asíncrono el servicio, al no puede haber mensajes salida, ni de respuesta ni de fallos.

La definición de mensajes de fallos resulta útil cuando se necesitan devolver información de situaciones de excepción que deben de tenerse en consideración por el sistema que llama al servicio. Es decir, el mensaje de respuesta representa el escenario principal y los mensajes de fallos los escenario alternativos en el funcionamiento del servicio.

En una implementación del servicio sobre el protocolo SOAP, tanto los fallos definidos en la interfaz del servicio, excepciones _checked_, como los errores que se puedan producir, excepciones _unchecked_, son representadas mediante mensajes [SOAP Fault](http://www.w3.org/TR/2000/NOTE-SOAP-20000508/#_Toc478383507).  

A modo de ejemplo, se muestra el código de un servicio Web en Java para realizar reservas en un hotel. Se provee un método para la reserva de una habitación que devuelve una excepción cuando no hay una habitación libre para las plazas y fechas requeridas:  

```java
package es.servicios.servidor;  

import java.util.Date;  

import javax.jws.WebMethod;  
import javax.jws.WebParam;  
import javax.jws.WebService;  

@WebService  
public class Hotel {  
    public Hotel() {  
        super();  
    }  

    @WebMethod  
    public String reservaHabitacion(@WebParam(name = "plazas")  
        int plazas, @WebParam(name = "fechaInicio")  
        Date fechaInicio, @WebParam(name = "fechaFin")  
        Date fechaFin) throws HabitacionNoDisponible {  

        boolean disponible = false;  
        String codigoReserva = null;  

        // Se procesa la peticion y se genera un codigo de reserva si hay una disponible  
        // [...]  

        if (disponible) {  
            return codigoReserva;  
        }  
        else {  
            throw new HabitacionNoDisponible();  
        }  
    }  
}  
```

A continuación se puede ver parte del código fuente de un cliente generado con JAX-WS a partir del WSDL del servicio. Como se aprecia, la llamada al servicio es similar a la realizada para cualquier método Java que tiene declarada una excepción de tipo _checked_:  

```java
int plazas;  
XMLGregorianCalendar fechaInicio = null;  
XMLGregorianCalendar fechaFin = null;  

// Se configuran los valores de los parametros de entrada al metodo  
// [...]  

try {  
    String codigoReserva = hotel.reservaHabitacion(plazas, fechaInicio, fechaFin);  
}  
catch (HabitacionNoDisponible e) {  
    // Se captura la excepción y se procesa  
}  
```

Ejemplo de mensajes de entrada a la operación de reserva de habitación:  

```xml
<env:envelope xmlns:env="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://servidor.servicios.es/">  
  <env:body>  
      <ns1:reservahabitacion>  
          <plazas>2<s/plazas>  
          <fechainicio>2011-09-24T18:30:09+01:00</fechainicio>  
          <fechafin>2011-09-26T18:30:15+01:00</fechafin>  
      </ns1:reservahabitacion>  
  <env:body>  
</env:envelope>  
```

Ejemplo de mensaje de salida del servicio si no hay habitación disponible:  

```xml
<s:envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:body>  
      <s:fault xmlns:ns4="http://www.w3.org/2003/05/soap-envelope">  
          <faultcode>S:Server<s/faultcode>  
          <faultstring>es.servicios.servidor.HabitacionNoDisponible</faultstring>  
          <s:detail/>  
     <s:fault>  
  <s:body>  
<s:envelope>  
```

En este ejemplo no se ha definido contenido en el mensaje de fallo, siendo este vacío, pero podría contener cualquier información de utilidad para el sistema cliente cuando se produce la excepción: otras fechas disponibles, otros hoteles del grupo que si tienen habitación en esas fechas, etc.  

Referencias utilizadas:  

* [Interoperable WSDL faults](http://www.gridlab.org/WorkPackages/wp-5/guide/faults.html)
* [Simple Object Access Protocol (SOAP) 1.1](http://www.w3.org/TR/2000/NOTE-SOAP-20000508/)
* [Building a JAX-WS Application in the Metro Environment ](http://metro.java.net/getting-started/basic.html)