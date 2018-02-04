---
layout: single
title: 'Código fuente en el blog: SyntaxHighlighter'
date: '2011-09-12T23:38:00.000+02:00'
author: José Manuel López
tags:
- SyntaxHighlighter
modified_time: '2011-09-25T13:29:34.390+02:00'
thumbnail: http://1.bp.blogspot.com/-GG6i9JhasKs/TnS5LuJMGzI/AAAAAAAAAgI/14t3OpQPJ14/s72-c/SyntaxHighlighter_con_scroll_vertical.PNG
blogger_id: tag:blogger.com,1999:blog-1239096147248949874.post-955905613949240297
blogger_orig_url: http://josemlopez.blogspot.com/2011/09/codigo-fuente-en-el-blog.html
---

Tarde o temprano tendrá que llegar la necesidad de incluir algún extracto de código en una entrada del blog y, en vista de que blogger no incluye esta funcionalidad, he realizado una búsqueda rápida para ver alguna alternativa. El que más me gusta por el momento es [SyntaxHighlighter](http://alexgorbatchev.com/SyntaxHighlighter/), un cliente JavaScript open source interesante, vistoso y al mismo tiempo sencillo de utilizar.

Una de las ventajas de usar este cliente JavaScript es que el autor ha subido a un servidor de [Amazon S3](http://aws.amazon.com/es/s3//184-5914720-1650965/) los recursos que utiliza (librerías y hojas de estilos) por lo que no necesitamos de un almacenamiento externo para poder utilizarlo.

Su instalación es bastante sencilla y basta con incluir las siguientes lineas en el código HTML de la página:  

1.- Al final de la cabecera de la página, antes de la sentencia </head>, la importanción de las librerias y estilos necesarios:

```html
<script type="text/javascript" src="http://alexgorbatchev.com/pub/sh/current/scripts/shCore.js"> </script>  

<!-- At least one brush, here we choose JS.You need to include a brush for every language you want to highlight -->  
<script type="text/javascript" src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushJScript.js"> </script>  
<script type="text/javascript" src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushJava.js"> </script>  
<script type="text/javascript" src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushXml.js"> </script>  

<!-- Include *at least* the core style and default theme -->  
<link href="http://alexgorbatchev.com/pub/sh/current/styles/shCore.css" rel="stylesheet" type="text/css" />  
<link href="http://alexgorbatchev.com/pub/sh/current/styles/shThemeDefault.css" rel="stylesheet" type="text/css" />  
</pre>

<div style="text-align: justify;">2.- Antes del final del cuerpo de la página, antes de la sentencia </body>, el código JavaScript que realiza la transformación y aplica los estilos:</div>

<pre class="brush: js"><!-- Finally, to actually run the highlighter, you need to include on your page -->  
<script type="text/javascript">  
     SyntaxHighlighter.all()  
</script>  
```

La librería permite importar diferentes tipos de lenguajes para luego poder incluirlos como código en nuestra página, y el [listado](http://alexgorbatchev.com/SyntaxHighlighter/manual/brushes/) es bastante completo. También es posible cambiar los estilos por alguno de los [temas](http://alexgorbatchev.com/SyntaxHighlighter/manual/themes/) que se incluyen (si no nos gustan siempre los podemos editar y crear otros).

Por último, para que veáis lo sencillo que es utilizar en una página este cliente JavaScript, copio un ejemplo de uso, aunque en la pagina del proyecto SyntaxHighlighter podéis encontrar una completa [explicación de su instalación](http://alexgorbatchev.com/SyntaxHighlighter/manual/installation.html).

```html
<pre class="brush: js">  
function foo()  
{  
}  
</pre>  
```

Como se aprecia el resultado es interesante, dando también algo de colorido a la página, que siempre queda bien.  

<u style="font-weight: bold;">Actualización</u>: Si os sale una barra de desplazamiento vertical a la izquierda del componente, similar a la imagen de abajo, podéis quitarla sobreescribiendo uno de los estilos del fichero shCore.css (obtenido de [Willie's Weblog](http://xbfish.com/2011/04/26/remove-vertical-scrollbar-in-syntaxhighlighter/))  

[![](http://1.bp.blogspot.com/-GG6i9JhasKs/TnS5LuJMGzI/AAAAAAAAAgI/14t3OpQPJ14/s1600/SyntaxHighlighter_con_scroll_vertical.PNG)](http://1.bp.blogspot.com/-GG6i9JhasKs/TnS5LuJMGzI/AAAAAAAAAgI/14t3OpQPJ14/s1600/SyntaxHighlighter_con_scroll_vertical.PNG)  

Si no podéis modificar el fichero de estilos es posible incluir, después de su importación, las siguientes lineas para sobreescribirlo:  

```css
<style type="text/css">  
     <!--  
	.syntaxhighlighter table td.code .container {  
		padding-bottom: 5px !important;  
		position: relative !important;  
	}  
    -->  
</style>
```