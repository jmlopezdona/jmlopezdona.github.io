---
layout: single
title: Da prioridad a tus librerías en WebLogic
date: '2012-04-01T17:22:00.000+02:00'
author: José Manuel López
tags: 
modified_time: '2012-04-19T21:52:15.536+02:00'
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-284880454340774739
blogger_orig_url: http://josemlopez.blogspot.com/2012/04/da-prioridad-tus-librerias-en-weblogic.html
---

Si vas a desplegar una aplicación con una versión de Spring en Oracle WebLogic Server 10.3.x puedes encontrarte con que el funcionamiento no es el esperado o que obtienes un error al intentar desplegar el WAR del tipo al comentado en [https://jira.springsource.org/browse/SEC-1397](https://jira.springsource.org/browse/SEC-1397)

En el fichero de log del servidor se puede ver un mensaje de advertencia bastante esclarecedor indicando que se ha detectado una versión anterior de Spring incompatible con algún módulo determinado, en mi caso con Spring Security. Pero, ¿cómo puede ser si mi aplicación funciona correctamente en un entorno local con Tomcat?


La razón está en que Weblogic carga en el system classpath una versión 2.5.6 de Spring que por defecto toma preferencia en el classloader y "oculta" otras clases con el mismo paquete, en mi caso la versión 3.1.0 de Spring.

La solución es sencilla y pasa por indicarle a Weblogic que determinados paquetes tengan preferencia con las librerías que se incluyan en el WAR. Esto se consigue con la opción [prefer-application-packages](http://docs.oracle.com/cd/E23943_01/web.1111/e13712/weblogic_xml.htm#autoId24) en el fichero de configuración weblogic.xml. A continuación copio un ejemplo para usar las librerías de Spring incluidas en un WAR:  

```xml
<?xml version = '1.0' encoding = 'UTF-8'?>  
<weblogic-web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
xsi:schemaLocation="http://xmlns.oracle.com/weblogic/weblogic-web-app  
http://xmlns.oracle.com/weblogic/weblogic-web-app/1.1/weblogic-web-app.xsd"  
xmlns="http://xmlns.oracle.com/weblogic/weblogic-web-app">  
   <container-descriptor>  
      <prefer-application-packages>  
         <package-name>org.springframework.*</package-name>  
      </prefer-application-packages>  
   </container-descriptor>  
</weblogic-web-app>  
```