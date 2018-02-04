---
layout: single
title: 'Google Chrome Frame: esteroides para Internet Explorer'
date: '2012-04-15T16:40:00.001+02:00'
author: José Manuel López
tags: 
modified_time: '2012-05-09T08:58:55.394+02:00'
thumbnail: http://1.bp.blogspot.com/-Zof_WgbcyGk/T4q2sIGh-mI/AAAAAAAAAn8/55VXhisxdec/s72-c/compatibildad-navegadores.PNG
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-6627859623755362493
blogger_orig_url: http://josemlopez.blogspot.com/2012/04/google-chrome-frame-esteroides-para_15.html
---
Una de las dificultades de desarrollar una aplicación Web moderna (HTML5, CSS3, JavaScript 5, SVG, etc.) es conseguir que funcione correctamente y tenga un rendimiento óptimo en los principales navegadores, como se puede apreciar en los resultados de compatibilidad ofrecidos por la web [Caniuse](http://caniuse.com/#agents=desktop) para navegadores de escritorio:

[![](http://1.bp.blogspot.com/-Zof_WgbcyGk/T4q2sIGh-mI/AAAAAAAAAn8/55VXhisxdec/s640/compatibildad-navegadores.PNG)](http://1.bp.blogspot.com/-Zof_WgbcyGk/T4q2sIGh-mI/AAAAAAAAAn8/55VXhisxdec/s1600/compatibildad-navegadores.PNG){: .align-center}

Como se podía intuir los principales problemas suelen surgir con Internet Explorer por su falta de cumplimento de los estándares,agravándose la situación conforme bajamos en su número de versión, aunque parece que con la futura versión 10 se acerca a los niveles de compatibilidad y rendimiento ofrecidos por la competencia. En cualquier caso, el número de equipos que utilizan versiones de Internet Explorer (¡incluso IE 6!) es bastante alto por lo que obliga a "casi" tener que realizar un versión independiente de nuestra aplicación para cada una de las versiones de Internet Explorer, con el esfuerzo que esto conlleva.

¿Qué podemos hacemos en estos casos?  

* Dejar para la próxima década :-(( la adopción de los nuevos estándares que, por otra parte, proporcionan mayor compatibilidad entre los nuevos navegadores, mas y mejores funcionalidades, mayor rendimiento, etc.
* Desarrollar varias versiones de la aplicación para abarcar la compatibilidad de navegadores, con el coste que esto supone y la posible perdida de funcionalidades.
* No soportar navegadores que no cumplen los estándares que necesitemos. Poco factible teniendo en cuenta la proporción actual de uso de navegadores como Internet Explorer.

El problema es que muchas veces podemos encontrarnos con el desarrollo de una aplicación Web para una organización que emplea a nivel corporativo una versión determinada versión de Internet Explorer (a veces bastante antigua) para poder mantener la compatibilidad con aplicaciones desarrolladas con anterioridad.

Para estos casos puede ser de gran utilidad el plugin [**Google Chrome Frame**](http://es.wikipedia.org/wiki/Google_Chrome_Frame), proyecto de [Chromium](http://www.chromium.org/), que permite reemplazar el motor de renderizado de Internet Explorer por el de Chrome, consiguiendo de esta forma:  

* Compatiblidad con la mayor parte de los estándares
* Cerca de [10 veces mayor rendimiento en la ejecución de JavaScript](http://www.telegraph.co.uk/technology/6232744/IE8-browser-runs-faster-with-Google-Chrome-plug-in.html).
* Mayor seguridad gracias a la liberación continua de nuevas actualizaciones de Chrome

Una de las ventajas es que la instalación de este plugin en Internet Explorer sólo reemplaza el motor de renderizado en el caso que la página accedida así lo indique incluyendo el siguiente código en la cabecera:

```html
<meta http-equiv="X-UA-Compatible" content="chrome=1" />
```

De esta forma, al no ser intrusivo, no afecta al funcionamiento de las aplicaciones que necesitan una determinada versión de Internet Explorer para funcionar.

Entre las principales características de Google Chrome Frame se encuentran:

*   **Instalación rápida y sencilla**. Además de la instalación online, se puede descargar una versión msi para poder ser distribuida e instalada en entornos empresariales por los administradores. También facilita mediante ficheros de configuración habilitar/automatizar las páginas en las que se puede o no utilizar, etc.
*   **Compatible** con todas las versiones de **Internet Explorer: 6, 7 8 y 9**.
*   **No es intrusivo**, como ya se ha comentado, aunque si se necesita se puede configurar para reemplazar por defecto el motor de renderizado, a excepción de las paginas que se indiquen.
*   Una vez instalado el plugin se puede puede **comprobar el uso** del motor de Chrome con cualquier página simplemente añadiendo "gcf:" a la dirección Web. Previamente sólo hay que configura una entrada en el registro de Windows como se indica en [Testing-Your-Sites](http://www.chromium.org/developers/how-tos/chrome-frame-getting-started#TOC-Testing-Your-Sites)
*   Proporciona una librería JavaScript que permite **detectar si está instalado el plugin** y ofrecer de forma automatizada un enlace para su instalación.

A continuación se incluyen varias referencias que permiten profundizar más en los detalles de instalación, configuración y uso de Google Chrome Frame:  

1. [Descargar e instalación del plugin](http://www.google.com/chromeframe/?quickenable=true)  
2. [Página inicial del proyecto en Google Developers](https://developers.google.com/chrome/chrome-frame/?hl=es-ES)  
3. [FAQ con las preguntas y respuestas más importantes](http://www.chromium.org/developers/how-tos/chrome-frame-getting-started/chrome-frame-faq): recomendada para conocer todas las posibilidades y limitaciones.
4. [Guía de Desarrollo](http://www.chromium.org/developers/how-tos/chrome-frame-getting-started)  
5. [Guía de Administración](http://www.chromium.org/developers/how-tos/chrome-frame-getting-started/chrome-frame-administrator-s-guide)