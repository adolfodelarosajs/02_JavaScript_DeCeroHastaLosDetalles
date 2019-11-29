# Eventos

## Eventos 101

Los eventos son acciones que hacen que se dispare una función. Ver el documento **Eventos.pdf""

### onclick() y ondblclick()

Vamos a ver un ejemplo muy sencillo:

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style type="text/css">
    div{
      width: 100px;
      height: 100px;
      background-color: red;
    }
  </style>
</head>
<body>
  <h1>Eventos!!!</h1>
  <button onclick="evento()">Soy un botón</button>
  <div ondblclick="evento()">
    <p>Presiona doble click</p>
  </div>
  <script src="app.js"></script>	
</body>
</html>
```

```
function evento( arg ){
  console.log("Me disparé");
  console.log( arg );
}

//output
Me disparé
undefined
```

### onfocus(), onblur() y onmouseout()

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <h1>Eventos!!!</h1>
  <input type="text" onfocus="evento(onfocus)" placeholder="onfocus">
  <input type="text2" onblur="evento(onblur)" placeholder="onblur">
  <input type="text3" onmouseout="evento(onmouseout)" placeholder="onmouseout">
  <script src="app.js"></script>	
</body>
</html>
```

Esta forma de añadir los eventos en nuestro HTML no es nada recomendable, ensucia mucho nuestro código.

Se debe identificar a cada componente con el atributo `id` y manipularlo en el archivo JS.

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <h1>Eventos!!!</h1>
  <input type="text1" id="texto1" placeholder="onfocus">
  <input type="text2" id="texto2" placeholder="onblur">
  <input type="text3" id="texto3" placeholder="onmouseout">
  <script src="app.js"></script>	
</body>
</html>
```

```
function evento( arg ){
  console.log("Me disparé");
  console.log( arg );
}

var objeto1 = document.getElementById("texto1");
var objeto2 = document.getElementById("texto2");
var objeto3 = document.getElementById("texto3");

console.log( objeto1 );
console.log( objeto2 );
console.log( objeto3 );

//output
<input type="text1" id="texto1" placeholder="onfocus">
<input type="text2" id="texto2" placeholder="onblur">
<input type="text3" id="texto3" placeholder="onmouseout">
```

Como podemos ver lo que se nos muestra en la consola es todo el elemento asociado a ese `id`, y si pasamos el mouse sobre él en la consola, se ilumina en nuestro navegador para identificarlo.

Podemos añadir al elemento que escuche eventos para que realice una acción, vamos a realizar exactamente lo mismo que hacíamos en el HTML:

```
function evento( arg ){
  console.log("Me disparé");
}

var objeto1 = document.getElementById("texto1");
var objeto2 = document.getElementById("texto2");
var objeto3 = document.getElementById("texto3");

objeto1.addEventListener("focus",evento);
objeto2.addEventListener("blur", evento);
objeto3.addEventListener("mouseout", evento);
```

Nótese que aquí el nombre de los eventos no lleva el `on` eso es solo cuando se está en el HTML y la función que se invoca va sin ().

Cabe hacer notar que para cada diferente evento que se dispara le llegan diferentes argumentos que se almacenan el arreglo `arg` y que como tal se pueden recuperar sus valores para ver qué cosa le llega en cada caso.

Existen dos formas de disparar un evento:

1. Que el usuario lo invoque 
2. Hacerlo vía código

```
function evento( arg ){
  console.log("Me disparé");
  console.log( arg );
}

var objeto1 = document.getElementById("texto1");

objeto1.addEventListener("click",evento);
objeto1.click();

//output
Me disparé
MouseEvent {isTrusted: false, screenX: 0, screenY: 0, clientX: 0, clientY: 0, …}

Me disparé
MouseEvent {isTrusted: true, screenX: 128, screenY: 188, clientX: 128, clientY: 85, …}
```

Nótese que el primer evento es el que hace vía código y dentro de los argumentos que se regresan esta:

`isTrusted: false`

Y en el segundo que lo realiza el usuario obtenemos:

`isTrusted: true`

Precisamente esto es lo que indica esta propiedad si lo ha realizado el usuario (true) o se ha realizado vía código (false).

La información que se puede obtener gracias a los argumentos recuperados en cada evento es muy diversa, en el siguiente ejemplo desplegaremos las coordenadas del punto donde se pulso click:

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <h1>Eventos!!!</h1>
  <button id="boton">Soy un botón</button>
  <script src="app.js"></script>	
</body>
</html>
```

```
function evento( arg ){
  console.log("Me disparé");
  console.log( arg.x, arg.y );
}

var objeto1 = document.getElementById("boton");

objeto1.addEventListener("click",evento);

//output
Me disparé
144 90
Me disparé
57 89
Me disparé
10 80
```

## Bloqueando el click derecho de la página.

Para evitar que se despliegue el menú contextual con click derecho usamos `oncontextmenu="return false"`, veamos el siguiente código:

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript</title>
</head>
<body oncontextmenu="return false">
  Lorem Ipsum es simplemente el texto de relleno de las imprentas y archivos de texto. Lorem Ipsum ha sido el texto de relleno estándar de las industrias desde el año 1500, cuando un impresor (N. del T. persona que se dedica a la imprenta) desconocido usó una galería de textos y los mezcló de tal manera que logró hacer un libro de textos especimen. No sólo sobrevivió 500 años, sino que tambien ingresó como texto de relleno en documentos electrónicos, quedando esencialmente igual al original. Fue popularizado en los 60s con la creación de las hojas "Letraset", las cuales contenian pasajes de Lorem Ipsum, y más recientemente con software de autoedición, como por ejemplo Aldus PageMaker, el cual incluye versiones de Lorem Ipsum.
  <script src="app.js"></script>	
</body>
</html>
```

Con el siguiente código desplegaremos un `alert` cuando den click en el navegador.

```
document.onmousedown = function(arg){
  alert("Click bloqueado");
  console.log( arg );
}
```

Lo que pasa que esto lo hace para todos los botones del mouse, inclusive si tuviera el botón central es otro botón, en los argumentos tenemos la propiedad `button`.

0. Botón izquierdo
1. Botón central
2. Botón derecho.

Sabiendo esto vamos a mostrar el `alert` solo para el click con el botón derecho:

```
document.onmousedown = function(arg){
  if( arg.button === 2 ){
    alert("Click bloqueado");
    return;
  }   
}
```

De todos modos esto no es infalible si mi `body` no está al 100% podrían dar click derecho, o podría desactivar el JS y podría hacer otras cosas.

Podemos tener otro ejemplo que nos va a permitir escribir en consola el texto que que marque el usuario con el mouse, para eso usamos el evento `onmouseup` que se dispara cuando soltamos el click del botón.

```
document.onmouseup = function(){
  var texto = window.getSelection().toString();
  console.log( texto );
}
```

## Evento "onsubmit" y parámetros URL

El `onsubmit` se ejecuta antes de que se llame al servidor, con lo que podríamos realizar validaciones del lado del servidor antes de mandar los datos al servidor.

El evento `on submit` retornara `true` si el formulario es válido realiza el posteo de los datos al servidor y si retorna `false` el formulario no es válido por lo tanto no se realiza el posteo de datos al servidor.

Veamos un ejemplo para validar un formulario sencillo:

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript</title>
</head>
<body>
  <form action="" onsubmit="return validar();">
    <input type="text" id="txtNombre" name="txtNombre">
    <input type="text" id="txtApellido" name="txtApellido">	
    <button type="submit">Postear Data</button>
  </form>
  <script src="app.js"></script>	
</body>
</html>
```

```
function validar(){
  var nombre = document.getElementById("txtNombre").value;
  var apellido = document.getElementById("txtApellido").value;

  if( nombre.length < 1 ){
    console.log("Nombre no valido");
    return false;
  }

  if( apellido.length < 1 ){
    console.log("Apellido no valido");
    return false;
  }

  return true;
}
```

El código valida que los dos campos tengan algún dato, si alguno de los dos la función retorna `false` y el posteo de datos no se hace, si los datos son validos y se postean, el URL cambia añadiendo los datos posteados.

`index.html?txtNombre=Adolfo&txtApellido=De+La+Rosa`

Es obvio que esta forma de mandar no es segura si los datos son sensibles.

Esta forma de validar es como volver a inventar la rueda ya que existen muchos validadores, por ejemplo:

[angular-auto-validate](https://github.com/jonsamwell/angular-auto-validate)

[jQuery AutoValidation](http://phrogz.net/js/FormAutoValidate/formautovalidate_docs.html)

Muchas veces lo que queremos es recuperar los parámetros desde el URL que se despliega, el objeto global window tiene la propiedad `location` la cual a su vez es un objeto con muchas propiedades entre ellas `search` que tendrá como valor `search: "?txtNombre=Adolfo&txtApellido=De+La+Rosa"` o sea los parámetros mandados.

Una vez que ya tenemos la cadena con todos los parámetros hay que ver cómo obtener el valor de los campos, a continuación tenemos un código con una función que usa las expresiones regulares para recuperar el valor de un campo:

```
function getParamURL(name) {
  return decodeURIComponent((new RegExp('[?|&]' + name + '=' + '([^&;]+?)(&|#|;|$)').exec(location.search)||[,""])[1].replace(/\+/g, '%20'))||null
}

console.log( window.location.search);
console.log( window.location.search.split("&"));

console.log( getParamURL("txtNombre") );
```

## Cajas de dialogo

Existen varias formas de desplegar cajas de dialogo con JS, veamos el ejemplo:

```
alert("Hola Mundo!!!");
var acepto =confirm("¿Esta seguro que desea borraló?")
console.log(acepto);
var nombre = prompt("Ingrese su nombre: ", "Nombre");
console.log( nombre );

//output
true
Adolfo
```

Estas cajas de dialogo de alguna manera bloquen nuestro código, veamos el siguiente ejemplo:

```
var i = 0;
setInterval(function(){
   i++;
   console.log("Segundo : ", i);
}, 1000);
alert("Código pausado....");
```

La ejecución del código no continuará hasta que se pulse aceptar en la ventana emergente.

Existen algunas librerías interesantes para pintar ventanas emergentes:

[Sweet Alert 2](https://sweetalert2.github.io/)

## JavaScript - "use strict" - Modo estricto

El modo estricto hace que JS sea más riguroso en algunos aspectos de la programación como la declaración de variables.

Por ejemplo el siguiente código en un JS normal no tendría ningún problema con el modo estricto nos marca un error:

```
"use strict"

nombre = "Adolfo";
console.log( nombre );

//output
Uncaught ReferenceError: nombre is not defined
    at app.js:3
```

Tendríamos que declarar nombre con `var`, es decir:

`var nombre = "Adolfo";`

Cabe destacar que si ponemos al principio de un archivo JS el uso estricto todos los que estén declarados posteriormente se evaluaran con este modo, esto incluye el uso de librerías de terceros.

Para evitar este posible error podemos hacer uso del modo estricto dentro de funciones solamente.

```
function getNombre(){
  "use strict"
  nombre2 = "Penélope";
  return nombre2;
}

nombre = "Adolfo";
console.log( nombre );
```

Pero si ejecutamos este código no nos da error, ya que no estamos invocando la función.

Cuando la invocamos es el momento en que detecta el fallo y nos marca el error:

```
app.js:4 Uncaught ReferenceError: nombre2 is not defined
    at getNombre (app.js:4)
    at app.js:12
```

Por eso lo importante de ver cómo trabaja JS.

Pero si es imprescindible que todo nuestro archivo JS presente use el modo estricto sin afectar a los demás lo que podemos es aislarlo del exterior usando una función anónima:

```
(function(){
  "use strict"
   
  function getNombre(){
    nombre2 = "Penélope";
    return nombre2;
  }

  nombre = "Adolfo";
  console.log( nombre );
  console.log( getNombre() );
})();
```

Como es obvio esperar aquí si nos marca un error:

```
app.js:10 Uncaught ReferenceError: nombre is not defined
    at app.js:10
    at app.js:15
```

si pongo `var` en nombre se presentara el siguiente error:

```
Uncaught ReferenceError: nombre2 is not defined
    at getNombre (app.js:5)
    at app.js:13
    at app.js:15
```

Por lo que también debo definir a nombre 2 con `var`.

Y ya obtendría la salida 

```
Adolfo
Penélope
```