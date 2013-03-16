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

	sass --watch estilos.scss:estilos.css

Esto creara automáticamente un archivo llamado `estilos.css` que nos servirá para verificar si la sintaxis que escribamos sean la correcta, ahora tenemos a Sass traduciendo nuestro código y no debemos de cerrar la terminal o pronpt, pues bien comencemos.

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

Las operaciones soportadas son suma, multiplicación y división.

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

Integración de argumentos
--------------------------------

En muchas ocasiones necesitaremos de especificar los argumentos que se deberán de tener en cuenta, las cuales pueden ser obligatorias o llevar un valor por defecto.

Ejemplo:

Archivo **.SCSS**

	@mixin borde($radio:10px,$color:#123456){
		border:2px solid $color;
		border-radius:$radio;
		-moz-border-radius: $radio;
		-webkit-border-radius: $radio;}
	ul li{	@include borde(15px,green);}
	h1{	@include borde;}

Archivo **.CSS**

	ul li {
		border: 2px solid green;
		border-radius: 15px;
		-moz-border-radius: 15px;
		-webkit-border-radius: 15px; }

	h1 {
		border: 2px solid #123456;
		border-radius: 10px;
		-moz-border-radius: 10px;
		-webkit-border-radius: 10px; }

Funciones
-------------
Las diferentes funciones que se puede utilizar en **Sass** están en la [documentación de Sass](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html) y las cuales tocaremos las más resaltantes a detalle.

Función RGB
-------------------

**RGBA**: Opacidad de un color.

	$color:#123456;
	$opacidad:0,5;//numero entre 0 y 1
	rgba($color,$opacidad);//rgba(18,52,86,0,5)
	
**MIX**: Mezcla de un color.

	$rojo:red;
	$azul:#123456;
	$peso:50%;//siempre en porcentaje
	mix($rojo,$azul,$peso);//#881a2b

Función HSL
----------------

**HSL**:Convierte tres colores en uno sólo.

	$matiz:200deg;//entre 0 y 360
	$saturacion:75%;
	$luz:50%;
	hsl($matiz,$saturacion,$luz);//#209fdf

**HSLA**: Esta función es una variación de **hsl** sólo que en esta se incluye la variable de opacidad.

	$matiz:200deg;
	$saturacion:75%;
	$luz:50%;
	$opacidad:0.5;
	hsla($matiz,$saturacion,$luz,$opacidad);//rgba(32,159,223,0.5)

**ADJUST-HUE**: Cambia la tonalidad de un color, manteniendo la luminosidad y la saturación.

	$color:#123456;
	$grados:200deg;//entre -360deg y 360deg
	adjust-hue($color,$grados);//#564b12

**LIGHTEN**: Hace un color mucho mas claro.

	$color:#123456;
	$luz:30%;
	lighten($color,$luz);//#2e80d3

**DARKEN**: Oscurece un color.

	$color:#123456;
	$dark:10%;
	darken($color,$dark);//#091a2c

**SATURATE**: Hace un color más saturado.

	$color:#123456;
	$saturacion:60%;
	saturate($color,$saturacion);//#003468

**DESATURETE**: Realiza lo inverso a **saturate** ose hace un color menos saturado.

	$color:#123456;
	$desaturacion:60%;
	desaturate($color,$desaturacion);//#313437

**GRAYSCALE**: Convierte un color a escala de grises.

	$color:;
	grayscale($color);//#343434

**COMPLEMENT**: Devuelve el complemento de un color.

	$color:#123456;
	complement($color);//#563412

**INVERT**: Devuelve el inverso de un color.

	$color:#123456;
	invert($color);//#edcba9

Funciones con cadenas
-----------------------------

**QUOTE**: Agrega comillas de una cadena.

	$font:Arial;
	quote($font)//”Arial”

**UNQUOTE**: Elimina las comillas de una cadena.

	$font:”Arial”;
	unquote($font)//Arial

Funciones con números
-----------------------------

**PERCENTAGE**: Multiplica un número por 100% y lo vuelve en porcentaje.

	$num:2.5;
	percentage($num);//250%

**ROUND**: Redondea un número al entero más cercano, en caso de el decimal este en 5 se optara por el entero superior.

	$num1:2.4;
	$num2:2.5;
	percentage($num1);//2
	percentage($num2);//3

**CEIL**: Redondea un número al entero superior próximo.

	$num:2.3;
	ceil($num);//3

**FLOOR**: Redondea un número al entero inferior próximo.

	$num:2.3;
	floor($num);//2

**ABS**: Devuelve el valor absoluto de un número.

	$num:-2.5;
	abs($num);//2.5

**MIN**: Devuelve el menor número de varios.

	min(6,8,5,3,9,7)//3

**MAX**: Devuelve el mayor número de varios.

	max(6,8,5,3,9,7)//9

Funciones con listas
-------------------------

Una lista puede ser declarada de dos formas:

	$list:10px 15px 10px 15px;
	$otro:(10px 15px 10px 15px);

**LENGTH**: Devuelve la longitud o tamaño de una lista.

	$list:10px 15px 10px 15px;
	length($list);//4

**NTH**: Devuelve un elemento específico de una lista.

	$list:10px 15px 10px 15px;
	nth($list,3);//10px

**JOIN**: Fusiona o une dos listas en una nueva.

	$mar1:10px 15px;
	$mar2:15px 10px;
	join($mar1,$mar2);//10px 15px 15px 10px

**APPEND**:  Añade un valor o una lista a otra variable, separados por lo que queramos.

	append($valor, $valor_a_agregar,$separador)

	$list:10px, 15px;
	$val:15px 10px;
	append($list,$val,auto);//10px, 15px, 15px 10px
	append($list,$val,space);//10px 15px 15px 10px
	append($val,$list,comma);//10px, 15px, 15px, 10px