---
layout: single
title: 'Social Coding: GitHub'
date: '2012-02-27T21:02:00.000+01:00'
author: José Manuel López
tags: 
modified_time: '2012-03-31T19:02:01.003+02:00'
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-7241380141633982752
blogger_orig_url: http://josemlopez.blogspot.com/2012/02/social-coding-github.html
---

Hace unos días, revisando el blog de springsource para ver sus últimas novedades me llamó la atención la entrada "[Spring Framework moves to GitHub](http://blog.springsource.org/2011/12/21/spring-framework-moves-to-github/)" porque llevaba tiempo escuchando del éxito de [GitHub](https://github.com/) como sistema de alojamiento de proyectos de software y alternativa a otros "Project Hosting" como [SourceForge](http://sourceforge.net/) o [GoogleCode](http://code.google.com/).  

Hasta ese momento reconozco que no había tenido suficiente tiempo y/o curiosidad para probarlo, pero esta noticia me ha animó: algo bueno tiene que haber cuando una referencia como Spring Framework realiza una migración de su repositorio de código a GitHub.  

Lo primero que encontramos al ir alojar un proyecto en GitHub es que, como su nombre indica, usa [Git](http://git-scm.com/) como sistema distribuido de control  de versiones, pieza clave en torno a la que gira la "magia" del sitio.  

Git es un DVCS (Distributed Version Control System), creado inicialmente por Linus Torvalds para gestión del código del nucleo de Linux, que en los últimos años se está convirtiendo en una de las referencias para proyectos Open Source, avalado por el uso en proyectos como Linux Kernel, Android, Eclipse, Ruby on Rails, etc. Si hacemos un [Google Trend](http://www.google.com/insights/search/#cat=0-5-32&q=git%2Csubversion&cmpt=q) podemos ver que incluso supera en interés a un sistema como [Subversion](http://subversion.apache.org/).  

Acostumbrado a trabajar los últimos años con Subversion como VCS, algunas de las características que proporciona Git resultan de los más interesantes:  

* No depender de una conexión de red y tener tu propia copia local del repositorio, con lo que esto supone de velocidad, por ejemplo para realizar consultas al histórico.
* Disponer de tantas copias de respaldo del sistemas como usuarios lo están utilizando.
* Trabajar con ramas y unificaciones de código de una manera natural y rápida.
* Poder establecer flujos de trabajo complejos y personalizados. 

Está última característica me gusta bastante y puede dar bastante juego. Por ejemplo, puedes tener de forma sencilla y natural una topología en donde los desarrolladores envían cambios a un repositorio donde el responsable del proyecto los revisa y una vez validados los envía al repositorio consolidado al que los desarrolladores se sincronizan con acceso de sólo lectura.  

Si estáis interesando en el funcionamiento de Git recomiendo el siguiente [manual](http://progit.org/book/es/), que por cierto está alojado en GitHub por lo que es fácil hacer un fork y colaborar en mejorarlo.  

Si nos centramos en GitHub a parte de lo habitual en este tipo de sistemas (almacenar nuestros ficheros, poder navegar/editarlos, wiki, gestión de defectos, estadísticas, etc.) ofrece la funcionalidad de poder realizar de forma sencilla un clonado de cualquier repositorio, realizar cambios y hacer una petición al propietario del proyecto original para incorporarlo: [Pull Request](http://help.github.com/send-pull-requests/).  

Sin duda ésta es una de las funcionalidades que hace tan popular a GitHub para proyectos Open Source pues evita la complejidad de tener que solicitar acceso para poder subir modificaciones de código en proyecto y fomenta el "social coding".  

Por ejemplo, podemos realizar una copia del repositorio de Spring Framework, realizar una mejora o corregir ese error que tantos problemas no está dando sin tener esperar a  una nueva versión y proponer su incorporación al proyecto original.  

Como no hay nada mejor para valorar algo que utilizarlo, os animo a abrir vuestro proyecto en GitHub. Por cierto es totalmente gratis si es un proyecto público, en cambio si queréis que sea privado tiene un pequeño coste.