# Profundizando objetos

## Arreglos

Un array es una colección ordenada de datos (ya sea primitiva u objeto). Los arrays se utilizan para almacenar múltiples valores en una sola variable. 

Cada elemento de un array tiene un número adjunto, llamado índice numérico, que le permite acceder a él. En JavaScript, los arrays comienzan en el índice cero y pueden manipularse con varios métodos.

```
var arreglo = [5,4,3,2,1];
console.log( arreglo );

//output
[5,4,3,2,1]
```

Si queremos acceder a los elementos del array lo hacemos mediante su índice:

```
console.log( arreglo[0], arreglo[4], arreglo[5] );

//output
5 1 undefined
```

El primer elemento es 0 y el último el numero total de elementos - 1, si ponemos un índice fuera del rango nos responde con un `undefined`, en otros lenguajes esto sería un error de desbordamiento.

### Métodos de Arrays

Los arrays en JS cuentan con varios métodos (incluidos en su prototipo) para su manipulación.

#### reverse()

El método reverse() invierte un array en su lugar. El primer elemento del array se convierte en el último, y el último elemento del array se convierte en el primero.

```
arreglo.reverse();
console.log( arreglo );

//output
[1, 2, 3, 4, 5]
```

#### map()

El método map() crea un nuevo array con los resultados de invocar una función que recibe como parámetro cada elemento del array y realiza alguna transformación del mismo.

```
arreglo = arreglo.map( function(elemento){
	elemento *= elemento;
	return elemento;
});
console.log( arreglo );

arreglo = arreglo.map( Math.sqrt );
console.log( arreglo );

//output
[1, 4, 9, 16, 25]
[1, 2, 3, 4, 5]
```

En el anterior ejemplo vemos dos usos diferentes de *map* en el primero se le ha pasado como parámetro una función anónima que recibe explícitamente un elemento (cada elemento del array) y en el segundo una función ya existente que no necesita que le mandemos el parámetro ya que lo recibe de forma implícita. 

#### join()

El método join() crea y devuelve una nueva cadena concatenando todos los elementos en un array (o un objeto similar a un array), separados por comas o una cadena de separación especificada. Si la matriz tiene solo un elemento, ese elemento se devolverá sin usar el separador.

```
arr1 = arreglo.join();
console.log( arr1 );

arr2 = arreglo.join("|");
console.log( arr2 );

//output
1,2,3,4,5
1|2|3|4|5
```

#### split() (Método de Strings)

El método split() divide un objeto String en un array de cadenas separando la cadena en subcadenas, utilizando una cadena de separación especificada para determinar dónde hacer cada división.

```
arreglo = arr2.split("|");
console.log( arreglo );

//output
["1", "2", "3", "4", "5"]
```

#### push()

El método push() agrega uno o más elementos al final de un array y devuelve la nueva longitud del array.

```
arreglo.push("6");
console.log( arreglo );

//output
["1", "2", "3", "4", "5", "6"]
```

#### unshift()

El método unshift() agrega uno o más elementos al comienzo de un array y devuelve la nueva longitud del array.

```
arreglo.unshift("0");
console.log( arreglo );

//output
["0", "1", "2", "3", "4", "5", "6"]
```

#### toString()

El método toString() devuelve una cadena que representa el objeto especificado.

```
console.log( arreglo.toString() );

//output
0,1,2,3,4,5,6
```

Como vemos es muy similar a .join()

#### pop()

El método pop() elimina el último elemento de un array y devuelve ese elemento. Este método cambia la longitud del array.

```
var elementoEliminado = arreglo.pop();
console.log( arreglo,  elementoEliminado);

//output
["0", "1", "2", "3", "4", "5"] "6"
```

#### splice()

El método splice() cambia el contenido de un array al eliminar o reemplazar elementos existentes y/o agregar nuevos elementos en su lugar.

Vamos a ver varios ejemplos para comprender su uso. splice() recibe como primer parámetro un número que va a representar el índice del elemento con el cual queremos trabajar, y el segundo parámetro numérico indicara cuantos elementos queremos eliminar.

Vamos a partir de que siempre el arreglo inicial es:

```
["0", "1", "2", "3", "4", "5"]
```

Eliminar un elemento:

```
arreglo.splice(1,1);
console.log(arreglo);

//output
["0", "2", "3", "4", "5"]
```

Eliminar 3 elementos:

```
arreglo.splice(1,3);
console.log(arreglo);

//output
["0", "5"]
```

Además de eliminar elementos al mismo tiempo podemos insertarlos (lo que parecería un remplazo):

```
arreglo.splice(1,1,"10");
console.log(arreglo);

//output
["0", "10"]
```

Pero podríamos insertar varios elementos a la vez:

```
arreglo.splice(1,1,"10", "20", "30");
console.log(arreglo);

//output
["0", "10", "20", "30"]
```

También podríamos no eliminar nada y solo insertar nuevos elementos a partir de una posición:

```
arreglo.splice(1,0,"10", "20", "30");
console.log(arreglo);

//output
["0", "10", "20", "30", "10", "20", "30"]
```

#### slice()

El método slice() devuelve una copia superficial de una parte de un array en un nuevo objeto array seleccionado desde `begin` a `end` (`end` no incluido) donde `begin` y `end` representan el índice de elementos en el array. El array original no se modificará.

Estamos partiendo de que el array inicial es:

```
["0", "1", "2", "3", "4", "5"] 

console.log(arreglo.slice(1,3));
console.log(arreglo.slice(0,2));
console.log(arreglo.slice(3,3));

//output
["1", "2"]
["0", "1"]
[]
```

#### length

La propiedad length de un array devuelve el número de elementos en el array, siempre es numéricamente mayor que el índice más alto del array.

```
console.log(arreglo.length);

//output
6
```

## Arreglos - Parte 2

Los arrays pueden contener valores primitivos, objetos, funciones, arrays y todo combinándolo como sea necesario, a continuación vamos a ver un ejemplo de un objeto que contienen todos esos elementos y cómo podemos acceder a sus elementos:

```
var arreglo = [
  true,
  {
    nombre: "Penelope",
	apellido: "Cruz"
  },
  function(){
    console.log("Soy una función que vivo en un array...");
  },
  function ( persona ){
    console.log( persona.nombre + " " + persona.apellido);
  },
  [
    "Antonio",
	"Basi",
	"Carlos",
	"Elena",
	[
	  "Vicky",
	  "Gina",
	  "Veronica",
	  "Diana",
	  function(){
	    console.log( this );
	  }
	]
  ]
];

console.log( arreglo );
console.log( arreglo[0] );
console.log( arreglo[1].nombre + " " + arreglo[1].apellido );

arreglo[2]();
arreglo[3]( arreglo[1] );

console.log( arreglo[4][3]);
console.log( arreglo[4][4][0]);
console.log( arreglo[4][4][1]);

var arregloEXs = arreglo[4][4];

arregloEXs[0] = "Victoria";

console.log( arregloEXs );
console.log( arreglo );

arregloEXs[4]();
```

Los resultados obtenidos son:

```
(5) [true, {…}, ƒ, ƒ, Array(5)]
true
Penelope Cruz
Soy una función que vivo en un array...
Penelope Cruz
Elena
Vicky
Gina
["Victoria", "Gina", "Veronica", "Diana", ƒ]
[true, {…}, ƒ, ƒ, Array(5)]
["Victoria", "Gina", "Veronica", "Diana", ƒ]
```

## Argumentos - arguments

Recordemos que todos los tipos de datos tienen una propiedad -proto- la cual contiene una serie de métodos asociados a cada tipo y las funciones no son la excepción.

```
function miFuncion(){
	
}
```

Hemos definido una función que no hace absolutamente nada, pero con el hecho solo de ser declarada ya hereda ciertas propiedades y métodos que podemos visualizar si en la consola escribimos:

```
miFuncion.
  arguments
  caller
  length
  name
  prototype
  apply
  bind
  call
  constructor
  toString
  hasOwnProperty
  isPrototypeOf
  propertyIsEnumerable
  toLocaleString
  valueOf
  __defineGetter__
  __defineSetter__
  __lookupGetter__
  __lookupSetter__
  __proto__
```

En esta lección vamos a trabajar con la primera llamada **arguments**.

```
function miFuncion(){
  console.log( arguments );
}

miFuncion();
```

Esto regresa:

`[]`

Esto nos regresa `[]` pero no nos regresa ningún error, a pesar de que no hemos definido la variable *arguments*, inclusive podríamos definir la variable a nivel global `var arguments` y nos seguiría regresando `[]` ya que como hemos visto es una propiedad heredad al crear la función y se encuentra dentro del contexto de la misma.

Un argumento es un valor (primitivo u objeto) pasado como entrada a una función y como en este caso no estamos pasando nada nos regresa *undefined*.

Nosotros podemos mandar argumentos a la función como sigue:

```
function miFuncion(a,b){
  console.log( arguments );
  console.log( arguments[0] );
  console.log( arguments[2] );
}

miFuncion(1, 2);

//output
[1, 2]
1
undefined
```

Como podemos apreciar mandamos 2 argumentos y en **arguments** se almacena un array con todos los argumentos mandados a la función, y como en cualquier array podemos acceder a sus elementos con su índice.

Pero recuerde que JS nos permite mandar más argumentos de los parámetros enumerados en una función o incluso menos ( lo ideal sería igual).

Más parámetros que argumentos:

```
function miFuncion(a,b){
  console.log( arguments );
  console.log( arguments[0] );
  console.log( arguments[2] );
}

miFuncion(1, 2, 3);

//output
[1, 2, 3]
1
3
```

Más argumentos que parámetros:

```
function miFuncion(a,b){
  console.log( arguments );
  console.log( arguments[0] );
  console.log( arguments[2] );
}

miFuncion(1);

//output
[1]
1
undefined
undefined
```

**arguments** siempre contendrá un array con los argumentos pasados a la función, no importando los parámetros colocados en la función.

Recordemos que en las funciones también podemos pasar como argumentos arrays, objetos y funciones:

```
function miFuncion(a,b){
  console.log( arguments );
  console.log( arguments[0] );
  console.log( arguments[2] );
}

miFuncion(1, [1, 2], {a:1}, function(){});
```

**arguments** también almacena esos argumentos en su array:

`Arguments(4) [1, Array(2), {…}, ƒ]`

En situaciones concretas deberíamos validar el número de argumentos que recibimos para no encontrarnos con resultados inesperados:

```
function miFuncion(a,b,c,d){
  console.log( a + b + c + d);
}

miFuncion(10, 20, 30);
```

El resultado obtenido es: `NaN`, ya que al sumar un `undefined`(d) a un número retorna `NaN`.

Para evitar estas situaciones inesperadas podríamos añadir validaciones con respecto a los argumentos.

```
function miFuncion(a,b,c,d){
  if( arguments.length !== 4){
	console.error("La función necesita 4 parámetros.");
  }
  console.log("La suma es: " + (a + b + c + d));
}

miFuncion(10, 20, 30);

//output
La función necesita 4 parámetros.
```

```
function miFuncion(a,b,c,d){
  if( arguments.length !== 4){
	console.error("La función necesita 4 parámetros.");
  }
  console.log("La suma es: " + (a + b + c + d));
}

miFuncion(10, 20, 30, 40);

//output
La suma es: 100
```

Si mando más de cuatro argumentos ¿que pasa?:

```
function miFuncion(a,b,c,d){
  if( arguments.length !== 4){
    console.log("La función necesita 4 parámetros.");
  }
  console.log("La suma es: " + (a + b + c + d));
}

miFuncion(10, 20, 30, 40, 50, 60, 70);

//output
La función necesita 4 parámetros.
```

## Sobre carga de operadores en JavaScript

Este concepto se refiere a lo que en otros lenguajes existe como sobrecarga de métodos, por ejemplo:

```
function crearProducto(){
  console.log("Función sin parámetros...");
}

function crearProducto( p1 ){
  console.log("Función con 1 parámetro...");
}

function crearProducto( p1, p2 ){
  console.log("Función con 2 parámetros...");
}

crearProducto();
```

El resultado obtenido es: `Función con 2 parámetros...`

Lo que sucede aquí es que cuando se tienen varias funciones con el mismo nombre solo se queda la última porque se van reemplazando.

Una forma para "simular la sobrecarga" la veremos con el siguiente ejemplo:

```
function crearProducto( nombre, precio ){
  nombre = nombre || "XXXXX";
  precio = precio || "00000";
  console.log("Producto: ", nombre, " Precio:", precio);
}

crearProducto();
crearProducto("Libro");
crearProducto("Libro", 50);

//output
Producto:  XXXXX  Precio: 00000
Producto:  Libro  Precio: 00000
Producto:  Libro  Precio: 50
```

Hasta aquí simplemente estamos llamando una función mandando diferente número de  argumentos y dependiendo de ello muestra un mensaje.

Para simular la "sobrecarga", podríamos tener la necesidad de crear productos que todos ellos tengan valor de 10 o camisas con diferentes precios:

```
function crearProducto( nombre, precio ){
  nombre = nombre || "XXXXX";
  precio = precio || "00000";
  console.log("Producto: ", nombre, " Precio:", precio);
}

function crearProducto10( nombre ){
  crearProducto( nombre, 100 );
}

function crearProductoCamisa( precio ){
  crearProducto( "Camisa", precio);
}

crearProducto10("Lapiz");
crearProducto10("Pluma");
crearProducto10("Goma");

crearProductoCamisa(60);
crearProductoCamisa(100);
crearProductoCamisa(150);

//output
Producto:  Lapiz  Precio: 100
Producto:  Pluma  Precio: 100
Producto:  Goma  Precio: 100
Producto:  Camisa  Precio: 60
Producto:  Camisa  Precio: 100
Producto:  Camisa  Precio: 150
```

Aquí aprovechamos el uso de una función definida llamándola a partir de otra para aprovechar la funcionalidad de la primera.

## Polimorfismo en JavaScript

El concepto de polimorfismo (del griego muchas formas) implica que si en una porción de código se invoca un determinado método de un objeto, podrán obtenerse distintos resultados según la clase del objeto. Esto se debe a que distintos objetos pueden tener un método con un mismo nombre, pero que realice distintas operaciones.

Esto en JS nuevamente debemos simularlo, vamos a ver el siguiente ejemplo en el cual se llama a un mismo "método" (función) pasándolo diferentes tipos de datos y de acuerdo a su tipo de dato realiza una acción.

```
function determinarDato( a ){
  if( a === undefined){
	console.log("A es undefined... no se que hacer");
  }
  if( typeof a === "number"){
	console.log("A es número, puedo hacer operaciones numéricas...");
  }
  if( typeof a === "string"){
    console.log("A es texto, puedo hacer operaciones con textos...");
  }
  if( typeof a === "object"){
	console.log("A es objeto, que lindos somos los objetos...");
	if ( a instanceof Number ){
	  console.log("A también es un Number...");
	}
  }
}

determinarDato();
determinarDato(100);
determinarDato("Penelope");
determinarDato({nombre:"Penelope"});

var n = new Number(3);
determinarDato(n);

//output
A es undefined... no se que hacer
A es número, puedo hacer operaciones numéricas...
A es texto, puedo hacer operaciones con textos...
A es objeto, que lindos somos los objetos...
A es objeto, que lindos somos los objetos...
A también es un Number...
```

## Cuidado con las funciones y su contexto

Veamos el siguiente ejemplo de una función que regresa un array de funciones:

```
//Función que regresa un arreglo de funciones
function crearFunciones(){
  var arreglo = [];
  var numero = 1;

  arreglo.push( function(){
	console.log( numero );
  });

  return arreglo;
}

var funciones = crearFunciones();

funciones[0]();
```

Lo que se pinta en la consola es `1`.

Vamos a añadir más funciones al array:

```
//Función que regresa un arreglo de funciones
function crearFunciones(){
  var arreglo = [];
  var numero = 1;

  arreglo.push( function(){
    console.log( numero );
  });

  var numero = 2;

  arreglo.push( function(){
	console.log( numero );
  });

  var numero = 3;

  arreglo.push( function(){
	console.log( numero );
  });

  return arreglo;
}

var funciones = crearFunciones();

funciones[0]();
funciones[1]();
funciones[2]();

//output
3
3
3
```

Lo que sucede aquí es que cuando se ejecuta la función ya se invoca a la función, esta regresa al contexto a recuperar el valor de número y como está ya ha sido barrida por completa la variable número es igual a 3.

Pero no nos engañemos lo que realmente esperábamos recuperar era:

```
//output
1
2
3
``` 

Pero por el contexto no está pasando esto. Que modificaciones deberíamos hacer al código para realmente obtener ese resultado, tendríamos que aislar los contextos y eso lo podemos realizar con un función anónima:

```
//Función que regresa un arreglo de funciones
function crearFunciones(){
  var arreglo = [];
  var numero = 1;

  arreglo.push( 
    (function(numero) {
      return function(){
	    console.log( numero );
	  }
    })(numero)
  );

  var numero = 2;

  arreglo.push( 
    (function(numero) {
	  return function(){
	    console.log( numero );
	  }
	})(numero)
  );

  var numero = 3;

  arreglo.push( 
    (function(numero) {
      return function(){
	    console.log( numero );
	  }
	})(numero)
  );

  return arreglo;
}

var funciones = crearFunciones();

funciones[0]();
funciones[1]();
funciones[2]();

//output
1
2
3
``` 

Podríamos simplificar nuestra función usando un ciclo for:

```
//Función que regresa un arreglo de funciones
function crearFunciones(){
  var arreglo = [];
  var numero = 1;

  for ( var numero = 1; numero <= 5; numero++){
	arreglo.push( 
	  (function(numero) {
		return function(){
		  console.log( numero );
		}
	  })(numero)
	);
  }

  return arreglo;
}

var funciones = crearFunciones();

funciones[0]();
funciones[1]();
funciones[2]();
funciones[3]();
funciones[4]();

//output
1
2
3
4
5
```

## Objeto Number

El objeto Number no es lo mismo que el valor primitivo number como veremos en el siguiente ejemplo:

```
var a = 10;
var b = new Number(10);

//output
a
10
b
Number {10}
a===b
false
a==b
true
```

Los números tienen las constantes `-infinity` e `infinity` que representan los valores menor y mayor que soportan.

También existe otra `NaN` que representa algo que no es un número suele ser asignado a una variable cuando se multiplican números por letras o se suma un numero con undefined.

En el siguiente código vemos algunas de las funciones de los number:

```
var a = 10.456789;

console.log(a);
console.log(a.toFixed(2));
console.log(a.toString);
console.log(a.toPrecision(3));
console.log(a);

var b = new Number("20");
console.log( b );
console.log( b.valueOf() );

//output
10.456789
10.46
ƒ toString() { [native code] }
10.5
10.456789
Number {20}
20
```

## Objeto Booleano

Tenemos los tipos primitivos boolean y los objetos Boolean. Para crear un objeto de tipo Booleano se usa la siguiente sintaxis:

```
var b = new Boolean();
```

Por defecto el valor de b = false.

Nosotros podemos colocar un parámetro dentro de los paréntesis de Boolean() y dependiendo de lo que coloquemos el resultado será verdadero o falso.

Los únicos valores que nos dan un false son los siguientes:

```
var a = new Boolean();
var b = new Boolean(false);
var c = new Boolean(undefined);
var d = new Boolean(null);
var e = new Boolean("");
var f = new Boolean(0);
var g = new Boolean(-0);

console.log(a); //false
console.log(b); //false
console.log(c); //false
console.log(d); //false
console.log(e); //false
console.log(f); //false
console.log(g); //false
```

Cualquier otro valor que pongamos me dará true, incluso:

`var b = new Boolean("false");`

Un error común que se tiene es el de intentar usar directamente el objeto Booleano en una condición:

```
if(a){
  console.log("Solo se imprime si es true");
}
```

Al evaluar este código en la consola aparece:

`Solo se imprime si es true`

Pero ¿El valor de `a` no es false?

Lo que sucede que lo que evalúa el if(a), es que exista `a` y como `a` existe la condición es true y se imprime el mensaje, lo que realmente deberíamos usar es su valor primitivo, es decir:

```
if(a.valueOf()){
	console.log("Solo se imprime si es true");
}
```

De esta manera el mensaje no se imprimirá, porque la condición es false.

## Objetos String

En JS existe el tipo primitivo string y el objeto String, para crear una variable de tipo String lo hacemos de la siguiente forma:

```
var s = new String("Adolfo");

console.log(s);

String {"Adolfo"}
  0: "A"
  1: "d"
  2: "o"
  3: "l"
  4: "f"
  5: "o"
  length: 6
```

Nos crea un objeto String que también es una especie de array de caracteres, por lo que podemos acceder a sus elementos con s[0] por ejemplo.

Los Strings también heredan muchos métodos y propiedades para la manipulación de los Strings, veámoslo en el siguiente ejemplo:

```
var a = new String("Adolfo");

console.log( a );

console.log( a.toUpperCase() );
console.log( a.toLowerCase() );

var i = a.indexOf("f");
console.log("La letra f esta en la posición: " + i);

i = a.lastIndexOf("o");
console.log("La última letra o esta en la posición: " + i);

var nombre = "Adolfo de la Rosa";

var subcadena = nombre.substr(7,5);
console.log(subcadena);

var subcadena = nombre.substr(13);
console.log(subcadena);

var subcadena = nombre.substr(0, nombre.indexOf(" ") );
console.log(subcadena);

var split = nombre.split(" ");
console.log( split );

//Funciones antiguas
document.write( nombre.italics() + "<br>");
document.write( nombre.blink() + "<br>");
document.write( nombre.strike() + "<br>");
document.write( nombre.bold() + "<br>");
document.write( nombre.fontcolor("red") + "<br>");

//output
String {"Adolfo"}
ADOLFO
adolfo
La letra f esta en la posición: 4
La última letra o esta en la posición: 5
de la
Rosa
Adolfo
["Adolfo", "de", "la", "Rosa"]
```

## Objeto Fecha (Date)

Para crear un objeto de tipo fecha usamos:

```
var hoy = new Date();
console.log( hoy );

//output
Mon Aug 05 2019 10:30:59 GMT+0200 (hora de verano de Europa central)
```

Podemos inicializar la fecha mandando como parámetros milisegundos y JS me recupera la fecha equivalente a ese número de milisegundos.

```
var fechaMilisegundos = new Date(1000004565567);
console.log( fechaMilisegundos );

//output
Sun Sep 09 2001 05:02:45 GMT+0200 (hora de verano de Europa central)
```

Existe otra opción de inicializar la fecha con una fecha fija, para lo cual podemos pasar hasta 7 argumentos:

`var fechaFFija = new Date( anio, mes, dia, hora, min, seg, mili)`

aunque no todos los atributos son necesarios, depende de lo exacto que quieramos la fecha:

```
var fechaFija = new Date(2019, 08, 05);
console.log(fechaFija);

//output
Thu Sep 05 2019 00:00:00 GMT+0200 (hora de verano de Europa central)

var fechaFija = new Date(2019, 08, 05, 11, 02, 15, 23);
console.log(fechaFija);

//output
Thu Sep 05 2019 11:02:15 GMT+0200 (hora de verano de Europa central)
```

Existen muchos métodos y propiedades para manipular fechas:

```
var hoy = new Date();

console.log( hoy.getFullYear() ); //Recupera el año
console.log( hoy.getDate() ); //Recupera el día
console.log( hoy.getHours() );//Recupera horas
console.log( hoy.getMilliseconds() ); //Recupera milisegundos
console.log( hoy.getMonth() ); //Recupera mes empieza en 0
console.log( hoy.getSeconds() ); //Recupera segundos
console.log( hoy.getTime() ); //Representación númerica de una fecha en segundos

var inicio = new Date();

for( var i= 0; i < 15000; i++) {
	console.log("Algo...")
}

var fin = new Date();

var duracion = fin.getTime() - inicio.getTime();

console.log("El proceso tardo: " + duracion/1000 + " segundos");

//output
2019
5
11
824
7
47
1564996367824
15000 Algo...
El proceso tardo: 2.3 segundos
```

### Librería momentjs

Analiza, valida, manipula y muestra fechas y horas en JavaScript.

[momentjs](https://momentjs.com/)

## Operaciones con Fechas

Existen métodos y propiedades para manipular las fechas, veamos un ejemplo:

```
var fecha = new Date(2016, 9, 20);
console.log( fecha );

//Cambiar el valor de los días
fecha.setDate( 25);
console.log( fecha );

//Sumar días
fecha.setDate( fecha.getDate() + 5);
console.log( fecha );

//output
Thu Oct 20 2016 00:00:00 GMT+0200 (hora de verano de Europa central)
Tue Oct 25 2016 00:00:00 GMT+0200 (hora de verano de Europa central)
Sun Oct 30 2016 00:00:00 GMT+0200 (hora de verano de Europa central)
```

Inclusive podríamos meter una función en el prototipo que nos insertara días o años:

```
var fecha = new Date(2016, 9, 20);

Date.prototype.sumarDias = function( dias ){
	this.setDate( this.getDate() + dias );
	return this;
}

Date.prototype.sumarAnios = function( anio ){
	this.setFullYear( this.getFullYear() + anio );
	return this;
}

console.log( fecha );
console.log( fecha.sumarDias(5) );
console.log( fecha.sumarDias(-10) );
console.log( fecha.sumarAnios(3) );
console.log( fecha.sumarAnios(-19) );

//output
Thu Oct 20 2016 00:00:00 GMT+0200 (hora de verano de Europa central)
Tue Oct 25 2016 00:00:00 GMT+0200 (hora de verano de Europa central)
Sat Oct 15 2016 00:00:00 GMT+0200 (hora de verano de Europa central)
Tue Oct 15 2019 00:00:00 GMT+0200 (hora de verano de Europa central)
Sun Oct 15 2000 00:00:00 GMT+0200 (hora de verano de Europa central)
```

## Objeto Math

Math es un objeto incorporado que tiene propiedades y métodos para constantes y funciones matemáticas. No es un objeto de función.

Propiedades
  Math.E
  Math.LN10
  Math.LN2
  Math.LOG10E
  Math.LOG2E
  Math.PI
  Math.SQRT1_2
  Math.SQRT2
Métodos
  Math.abs()
  Math.acos()
  Math.acosh()
  Math.asin()
  Math.asinh()
  Math.atan()
  Math.atan2()
  Math.atanh()
  Math.cbrt()
  Math.ceil()
  Math.clz32()
  Math.cos()
  Math.cosh()
  Math.exp()
  Math.expm1()
  Math.floor()
  Math.fround()
  Math.hypot()
  Math.imul()
  Math.log()
  Math.log10()
  Math.log1p()
  Math.log2()
  Math.max()
  Math.min()
  Math.pow()
  Math.random()
  Math.round()
  Math.sign()
  Math.sin()
  Math.sinh()
  Math.sqrt()
  Math.tan()
  Math.tanh()
  Math.trunc()

Veamos algunos usos de Math:

```
var PI = Math.PI;
var E  = Math.E;

console.log( PI );
console.log( E );

var num = 10.456789;

console.log( num );
console.log( Math.round(num) );
console.log( Math.round(num * 100)/100 ); 
console.log( Math.floor(num) ); 
console.log( Math.sqrt( 10 ) );
console.log( Math.pow( 7, 2 ) );

var rnd = Math.random();
console.log( rnd );

function randomEntre( min, max ){
  return Math.floor( Math.random() * (max-min + 1) + min);
}

console.log( randomEntre(1,6) );
console.log( randomEntre(500,1000) );

//output
3.141592653589793
2.718281828459045
10.456789
10
10.46
10
3.1622776601683795
49
0.6441876042142185
1
747
```

## Expresiones Regulares

Expresiones regulares (o regex) son reglas que definen las secuencias de caracteres obtenidas en una búsqueda.

Las expresiones regulares están incluidas en varios lenguajes, pero las más conocida es la de Perl, que ha dado lugar a su propio ecosistema llamado PCRE (Perl Compatible Regular Expression). En la web, JavaScript proporciona otra implementación de expresiones regulares a través del objeto RegExp.

Para más información de [Expresiones Regulares](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Regular_Expressions)

En JS tenemos dos formas de definir una expresión regular

* Explicita usando RegExp
* Implícita definiendo un literal

Veamos el siguiente ejemplo:

```
var reg1 = RegExp("a");
var reg2 = /a/;

var texto = "Hola mundo";

var arreglo1 = texto.match( reg1 );
var arreglo2 = texto.match( reg2 );

console.log(arreglo1);
console.log(arreglo2);

//output
["a", index: 3, input: "Hola mundo", groups: undefined]
["a", index: 3, input: "Hola mundo", groups: undefined]
```

Lo que estamos haciendo es mediante el método `match()` estamos evaluando si dentro de nuestro texto existe una letra a, si es afirmativo nos regresa un array con "a".

En caso de que no la encontrara nos regresa null:

```
var reg1 = RegExp("a");
var reg2 = /z/;

var texto = "Hola mundo";

var arreglo1 = texto.match( reg1 );
var arreglo2 = texto.match( reg2 );

console.log(arreglo1);
console.log(arreglo2);

//output
["a", index: 3, input: "Hola mundo", groups: undefined]
null
```

Las expresiones regulares cuaetan con varios caracteres especiales que nos indican diferentes cosas:

### ^

Buscar en la primera posición:

```
var texto = "Hola mundo";
var arreglo = texto.match( /^a/ );

console.log(arreglo);
console.log(texto.match(/^H/));

//output
null
["H", index: 0, input: "Hola mundo", groups: undefined]
```

### $

Buscar en la última posición:

```
var texto = "Hola mundo";
var arreglo = texto.match( /a$/ );

console.log(arreglo);
console.log(texto.match(/o$/));

//output
null
["o", index: 9, input: "Hola mundo", groups: undefined]
```

### .

Representa cualquier carácter.

```
var texto = "Hola mundo";
var arreglo = texto.match( /.../ );

console.log(arreglo);
console.log(texto.match(/^.o/));

//output
["Hol", index: 0, input: "Hola mundo", groups: undefined]
["Ho", index: 0, input: "Hola mundo", groups: undefined]
```

### []

Los corchetes son usados para definir rangos de valores:

```
var texto = "Hola mundo, feliz 2019";
var arreglo = texto.match( /[a-z]/ );

console.log(arreglo);
console.log(texto.match(/[a-zA-Z]/));
console.log(texto.match(/[0-9]/));
console.log(texto.match(/[369]/));
console.log(texto.match(/[48]/));
console.log(texto.match(/[3-5;6-8]/));
console.log(texto.match(/[3-5;6-8;9]/));

//output
["o", index: 1, input: "Hola mundo, feliz 2019", groups: undefined]
["H", index: 0, input: "Hola mundo, feliz 2019", groups: undefined]
["2", index: 18, input: "Hola mundo, feliz 2019", groups: undefined]
["9", index: 21, input: "Hola mundo, feliz 2019", groups: undefined]
null
null
["9", index: 21, input: "Hola mundo, feliz 2019", groups: undefined]
```

```
var texto = "Hola mundo, feliz 2019";
var arreglo = texto.match( /^H[aeiou]/ );

console.log(arreglo);
console.log(texto.match(/[aeiou].$/));
console.log(texto.match(/[aeiou]./));

//output
["Ho", index: 0, input: "Hola mundo, feliz 2019", groups: undefined]
["ol", index: 1, input: "Hola mundo, feliz 2019", groups: undefined]

```

### \s

Buscar separaciones (espacios, tabulaciones, etc.):

```
var texto = "Hola mundo, feliz 2019";
var arreglo = texto.match( / / ); //Busca espacio, no muy recomendado

console.log(arreglo);
console.log(texto.match(/\s/));

//output
[" ", index: 4, input: "Hola mundo, feliz 2019", groups: undefined]
[" ", index: 4, input: "Hola mundo, feliz 2019", groups: undefined]
```

### \w

\w equivale a [a-zA-Z0-9]

```
var texto = "Hola Mundo 2019";
var arreglo = texto.match( /\w/ );

console.log(arreglo);

//output
["H", index: 0, input: "Hola Mundo 2019", groups: undefined]
```

### \d

\d equivale a [0-9]

```
var texto = "Hola Mundo 2019";
var arreglo = texto.match( /\d/ );

console.log(arreglo);

//output
["2", index: 11, input: "Hola Mundo 2019", groups: undefined]
```

### i (insensible) g (todas las apariciones) m (multilínea)

i permite ignorar si es mayúscula o minúscula.
g recupera todas las apariciones
m busca en múltiples líneas (lo hace aunque no se lo indiquemos)

```
var texto = "Hola Mundo";
var arreglo = texto.match( /m/ );

console.log(arreglo);
console.log(texto.match(/m/i));
console.log(texto.match(/[aeiou]/g));
console.log("HolA mUndo".match(/[aeiou]/ig));
console.log("HolA mUndo\n Que tal!!!".match(/[aeiou]/ig));
console.log("HolA mUndo\n Que tal!!!".match(/[aeiou]/igm));

//output
null
["M", index: 5, input: "Hola Mundo", groups: undefined]
(4) ["o", "a", "u", "o"]
(4) ["o", "A", "U", "o"]
(7) ["o", "A", "U", "o", "u", "e", "a"]
(7) ["o", "A", "U", "o", "u", "e", "a"]
```
### | 

Operador OR

```
var texto = "Hola Mundo\n Qué tal?";
var arreglo = texto.match( /[aeiou]|[áéíóú]/g);

console.log(arreglo);

//output
["o", "a", "u", "o", "u", "é", "a"]
```

### +

Operador de repetición:

```
var texto = "Hola Mundoo, ooooh";
var arreglo = texto.match( /o+/g);

console.log(arreglo);

//output
["o", "oo", "oooo"]
```

### ?

```
var texto = "Hola Mundoo, ooooh";
var arreglo = texto.match( /o?/g);

console.log(arreglo);

//output
(19) ["", "o", "", "", "", "", "", "", "", "o", "o", "", "", "o", "o", "o", "o", "", ""]
```

### *

```
var texto = "Hola Mundoo, ooooh";
var arreglo = texto.match( /o*/g);

console.log(arreglo);

//output
(15) ["", "o", "", "", "", "", "", "", "", "oo", "", "", "oooo", "", ""]
```

### {}

Las llaves nos permiten indicar las veces que debe aparecer un elemento:

```
var texto = "Hola Mundoo, oooh";
var arreglo = texto.match( /o{2}/g);

console.log(arreglo);

//output
(2) ["oo", "oo"]
```

Puedo indicar un rango de opciones en las llaves:

```
var texto = "Hola Mundooo, ooooh";
var arreglo = texto.match( /o{3,4}/g);

console.log(arreglo);

//output
(2) ["ooo", "oooo"]
```

```
var texto = "Hola Mundooo, ooooh, weoooooooo";
var arreglo = texto.match( /o{3,5}/g);

console.log(arreglo);

//output
(4) ["ooo", "oooo", "ooooo", "ooo"]
```

## Expresiones regulares - Segunda Parte

Un ejemplo de una expresión regular para buscar diptongos sería:

```
var texto = "Aeropuerto";
var arreglo = texto.match( /[aeiou]{2,2}/ig);

console.log(arreglo);

//output
["Ae", "ue"]
```

O dividir la palabra de dos en dos:

```
var texto = "Aeropuerto";
var arreglo = texto.match( /\w{2,2}/ig);

console.log(arreglo);

//output
(5) ["Ae", "ro", "pu", "er", "to"]
```

Vamos a suponer que queremos recuperar un arreglo con todos los números de 2 y 3 cifras en una cadena:

```
var texto = "La respuesta de la suma es: 45 + 60 = 105";
var arreglo = texto.match( /[0-9]{2,3}/g);

console.log(arreglo);

//output
(3) ["45", "60", "105"]
```

Y si quisieramos recuperar los números de 2 o más cifras:

```
var texto = "La respuesta de la suma es: 45 + 60 = 105 y 850 * 1000 = 850000";
var arreglo = texto.match( /[0-9]{2,}/g);

console.log(arreglo);
console.log( texto.match( /\d{2,}/g) );

//output
(6) ["45", "60", "105", "850", "1000", "850000"]
(6) ["45", "60", "105", "850", "1000", "850000"]
```
