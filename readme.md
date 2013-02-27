Tutorial de Sass en español
=========================
Este Tutorial esta hecho por [@juliopalro](https://twitter.com/juliopalro) y que se basa en el tutorial de [Tutorial de Sass](http://sass-lang.com/tutorial.html) y mi propia experiencia.
Instalación
-------------
Para este paso necesitaremos de Ruby que podemos [Descargar](http://www.ruby-lang.org/es/downloads/) desde su pagina oficial. Una vez instalado procederemos a instalar la gema de Sass.
Instalando Sass
-------------------
Para instalar **Sass** abriremos el **Command Prompt** de Ruby (caso windows) o la terminal (caso Linux o OS), en algunos casos deberás de escribir antes `sudo` (en caso de OS o Linux):

	gem install sass 

Después comprobamos si se instalo correctamente y escribimos:

	sass -v

A lo cual les saldrá algo como `Sass 3.2.6 <Media Mark>` entonces tendremos lo necesario para comenzar con este tutorial.

Crearemos un archivo llamado `estilos.scss`, abriremos la terminal o pronpt, nos colocamos dentro de la carpeta que contenga el archivo y escribimos:

	sass –watch estilos.scss:estilos.css

Esto creara automáticamente un archivo llamado `estilos.css` que nos servirá para verificar si la sintaxis que escribamos sean la correcta, ahora tenemos a Sass traduciendo nuestro codigo y no debemos de cerrar la terminal o pronpt, pues bien comencemos.

Anidación
-------------
A muchos de los que escribimos **CSS** se nos es tedioso escribir siempre la etiqueta, identificador o clase antes de la etiqueta, por eso sass ofrece una forma más sencilla de hacerlo.

Ejemplo:

Archivo **.SCSS**

	#menu{
		ul{
			margin:0;
			li{
				display:inline-block;
				a{
					color:white;
				}
			}
		}
	}

Archivo **.CSS**

	#menu ul{	margin:0;	}
	#menu ul li{	display:inline-block;	}
	#menu ul li a{		color:white;	}

Si bien esto pareciese ser la solución a todo no lo es pues no es recomendable hacer uso excesivo de la anidación y más por el contrario el uso excesivo de esto conllevaría a una lentitud al momento de cargar la pagina.

La anidación no sólo es aplicable a etiquetas HTML si no también a  las propiedades.
-------------------------------------------------------------------------------------------------------

Ejemplo:

Archivo **.SCSS**

	a{
		color:white;
		font:{
			size:20px;
			weight:bold;
			style: uppercase;	}
	}

Archivo **.CSS**

	a {
		color: white;
		font-size: 20px;
		font-weight: bold;
		font-style: uppercase;	}

Sencillo verdad?

También se pueden hacer uso para las Pseudo-clases
---------------------------------------------------------------------

Ejemplo:

Archivo **.SCSS**

	a{
		color:white;
		&:hover{	color:#123456;	}
		&:visited{	color:green;	}
	}

Archivo **.CSS**

	a{	color:white;	}
	a:hover{	color:#123456;	}
	a:visited{	color:green;	}

Variables
------------

En muchos casos el programador coloca ciertos parámetros dentro de los comentarios para así poder recordarlos y utilizarlos dentro del archivo **CSS** pero que mejor tenerlos como variables y poder utilizarlos en cualquier momento, por lo común suelen ser declaradas al inicio del archivo.

Ejemplo:

Archivo **.SCSS**

	$azul:#123456;
	$pixel:20px;
	a{	
		color:$azul;
		font-size:$pixel;	}

Archivo **.CSS**

	a{
		color:#123456;
		font-size:20px;	}

La declaración de la variable no sólo se puede hacer fuera si no también dentro de las declaraciones de las etiquetas, con la salvedad de que sólo podrán ser utilizadas dentro de ellas y en las etiquetas hijas, mas si estas variables son usadas fuera de estas se acabara teniendo un error y que el nombre de la variable tomara también el nombre de la propiedad.

Ejemplo:

Archivo **.SCSS**

	p{
		$pixel-font-size:20px;
		a{	font-size:$pixel-font-size;	}
	}

Archivo **.CSS**

	p{	font-size:20px;	}
	a{	font-size:20px;	}

Operaciones
-----------------
Las operaciones soportadas son suma, multiplicación y division.

Archivo **.SCSS**

	$largo:1050px;
	$ancho:2px;
	#menu{
		background:#123456;
		width:$largo;
		ul{
			background:green;
			border:$border+5;
			width:$largo/2;  }
	}

Archivo **.CSS**

	#menu{
		background: #123456;
		width: 1050px;  }
	#menu ul{
		background: green;
		border: 7px;
		width: 525px;	}

Mixins
---------
Los mixins son uno de las características más potentes de **Sass**, esto es muy parecido a las funciones o métodos.

Ejemplo:

Archivo **.SCSS**

	@mixin borde{
		border:2px solid #12345;
		border-radius:15px;
		-moz-border-radius: 15px;
		-webkit-border-radius: 15px;
	}
	ul li{	@include borde;	}
	h1{	@include border;	}

Archivo **.CSS**

	ul li {
		border: 2px solid #123456;
		border-radius: 15px;
		-moz-border-radius: 15px;
		-webkit-border-radius: 15px; }

	h1 {
		border: 2px solid #123456;
		border-radius: 15px;
		-moz-border-radius: 15px;
		-webkit-border-radius: 15px; }

