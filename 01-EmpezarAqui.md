# Empezar aquí

## Introducción

:+1: 

## ¿Qué es JavaScript?

Origen en 1995 LiveScript => JavaScript

JavaScript y Java son muy diferentes.

JavaScript trabaja del lado del cliente (Client-Side)

Aunque con node.js JavaScript ya se puede ejecutar del lado del servidor.

Limitantes:

* No permite lectura ni escritura de archivos del lado del servidor.
* No puede ser utilizado para aplicaciones de red por sí solo.
* JavaScript no tiene capacidad multihilo o múltiples procesos simultáneos.

## Mi primer código de JavaScript

Vamos a crear el archivo **index.html**

```
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>JavaScript</title>
</head>
<body>
  <h1>Mi primer código de JavaScript</h1>
  <p>Abrir las herramientas de desarrollar con F12</p>
  <p>Escribir <b>window</b> en la consola</p>
  <script type="text/Javascript"></script>
</body>
</html>
```
### Objeto Global Window

Este código aparentemente no hace nada, si lo abrimos en un navegador se ve una pantalla blanca. Si abrimos las herramientas de desarrollador y en la consola escribimos:

`> windows`
`Window {postMessage: ƒ, blur: ƒ, focus: ƒ, close: ƒ, parent: Window, …}`

Se nos presenta el **objeto global** llamado **window** el cual contiene muchas propiedades y métodos que podemos usar.

Si modificamos nuestro archivo **index.html** para meter código dentro de la sección de JS:

```
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>JavaScript</title>
</head>
<body>
  <h1>Mi primer código de JavaScript</h1>
  <p>Abrir las herramientas de desarrollar con F12</p>
  <p>Escribir <b>window</b> en la consola</p>
  <script type="text/Javascript">
    var a = 1;
    var b = "Adolfo";
  </script>
</body>
</html>
```

Y volvemos a desplegar el valor de **window** en la consola veremos que los valores de **a** y **b** ya forman parte de **window**

**Advertencia** Debemos tener cuidado de no usar un nombre existente dentro de las propiedades de **window** porque podríamos remplazar su funcionalidad.

```
a: 1
alert: ƒ alert()
applicationCache: ApplicationCache {status: 0, oncached: null, onchecking: null, ondownloading: null, onerror: null, …}
atob: ƒ atob()
b: "Adolfo"
```

Esto pasa por que JS se ejecuta dentro del objeto global window.

### Donde se debe colocar el código JS.

El código JS casi se puede colocar en cualquier lugar y se ejecutara siempre, aunque algunos sitios no tienen mucho sentido:

* Dentro del body
* Dentro del head
* Entre `</head> y <body>`
* Al inicio de todo
* Al final de todo

## Explicación visual de lo que hace JavaScript con los objetos y variables

:+1:

## Comprendiendo la consola

Ya vimos donde podemos colocar el código JS dentro del archivo **index.html**, pero lo más común es que nuestro código JS se encuentre en un archivo independiente.

```
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>JavaScript</title>
</head>
<body>
  <script src="app.js"></script>
</body>
</html>
```

En este caso el archivo JS se llama **app.js**

```
var a = 1;
var b = "Adolfo"
```

Las variables se seguirán visualizando en el objeto **window**

### Uso de la consola

Si abrimos la consola y escribimos los nombres de nuestras variables, en la consola se mostrarán sus respectivos valores:

```
a
1
b
"Adolfo"
```

En la consola también podría cambiar los valores de mis variables:

```
a = 10
10
a
10
b = "María";
"María"
```

### Impresión en la consola

Existen situaciones en las que mientras se está ejecutando nuestro programa necesitamos saber el valor de alguna variable, una forma es usando la instrucción `alert( a );`, la cual nos mostraría en una ventana emergente el valor, el problema de esto es que detiene la ejecución de nuestro programa hasta aceptar.

La forma más profesional de hacerlo es usar la instrucción `console`. Existen varias formas de mostrar los resultados en la consola:

```
console.log( a );
console.info( a );
console.warn( a );
console.error( a );
```

Las cuatro instrucciones nos mostrarán el valor de a, pero con ciertas diferencias:

* **log** simplemente muestra el valor
* **info** igual a log
* **warn** además del valor muestra un icono de warning y un fondo amarillo
* **error** además del valor muestra un icono de error, un fondo rojo y la línea donde se encuentra. 

## Undefined

Vamos a suponer que tenemos el siguiente código:

```
var a = "Adolfo";
console.log( a );
```

Esto nos mostrará en consola:

`Adolfo`

Ahora vamos a hacer un cambio en el código:

```
console.log( a );
var a = "Adolfo";
```

Aquí estamos tratando de usar una variable antes de ser declarada e inicializada, en otros lenguajes esto daría un error y pararía la ejecución del programa, pero ¿que pasa en JS?

En la consola se muestra:

`undefined`

Pero la ejecución del programa no se ha detenido a continuado, no existe ningún error, como podemos ver si imprimimos el valor después de inicializarlo:

```
console.log( a );
var a = "Adolfo";
console.log( a );

undefined
Adolfo
```

Por lo que podemos concluir que si se usa una variable sin ser declarada e inicializada tendrá un valor `undefined`

**Nota** El valor `undefined` no es lo mismo que `null`.

```
undefined === null
false

undefined == null
true
```

## ¿JavaScript es Asíncrono? ¿Qué es Asíncrono?

JavaScript NO es Asíncrono

El adjetivo **asincrónico** califica a aquello que **no posee sincronía**. Este término **sincronía**, por su parte, alude a lo que **coincide en el tiempo**.

**Se denomina comunicación asincrónica al proceso comunicativo que se lleva a cabo sin coincidencia temporal. Esto quiere decir que la emisión y la recepción de los mensajes están separadas por un cierto periodo de tiempo**.

Vamos a tratar de demostrarlo, haciendo un programa que se ejecute 10000 veces y mientras se ejecuta, llamar otra función, para que caiga en la pila de funciones que tiene que ejecutar JS, si JS fuera de verdad asíncrono podría ejecutar las dos funciones simultáneamente.

**index.html**

```
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>JavaScript</title>
</head>
<body>
  <button onclick="presionoClick()"></button>
  <script src="app.js"></script>
</body>
</html>
```

**app.js**

```js
function imprimir(){
  for( var i = 0; i < 10000; i++){
    console.log("Imprimiendo")
  }
}

function presionoClick(){
  console.log("Click en botón")
}

imprimir();
```

La prueba consiste en ejecutar el programa y mientras se ejecuta el ciclo de 10000 repeticiones pulsar en el botón, si JS fuera asíncrono mientras ejecuta el ciclo también ejecutaría la función **presionoClick**, si espera a terminar el ciclo y después ejecuta la función **presionoClick** demostraremos que es síncrono.


```
10000 Imprimiendo
Click en botón
```

Acabamos de demostrar que **JS no es Asíncrono**.

Cuando presiono click en el botón el código que se debe ejecutar entra en una pila o stack, donde se encuentran todos los procesos que están esperando ser ejecutados, mientras espera que el proceso en ejecución termine para continuar con el siguiente.

## Orden de las importaciones

Dentro de un archivo **index.html** podemos incluir varios archivos JS:

**index.html**

```
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>JavaScript</title>
</head>
<body>
  <script src="app.js"></script>
  <script src="app2.js"></script>
</body>
</html>
```

**app.js**

```js
var nombre = "Adolfo";
```

**app2.js**

```js
console.log(nombre);
```

El resultado en la consola es:

`Adolfo`

Si en el archivo **index.html** cambiamos el orden en el que incluimos a los archivos JS:

**index.html**

```
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>JavaScript</title>
</head>
<body>
  <script src="app2.js"></script>
  <script src="app.js"></script>
</body>
</html>
```

El resultado que obtenemos es:

`Uncaught ReferenceError: nombre is not defined at app2.js:1`

¿Por qué pasa esto?

Lo que sucede es que después de crear el **objeto global window** recorre el archivo **index.html** y se encuentra con el archivo **app2.js** el cual empieza a recorrer y se encuentra con la instrucción `console.log(nombre);` la cual hace referencia a la variable **nombre** que no se ha definido en el objeto global. Aquí no hace un barrido global de todo.
