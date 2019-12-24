# Variables, Objetos, Typeof y Condicionales

## Escritura dinámica - Tipos Primitivos

Tipos JavaScript

* Existen 6 tipos de datos primitivos:
   * Number
   * String
   * Boolean
   * Undefined
   * Null
   * Symbol (nuevo en ECMAScript 6)

* Object
   * object
   * function
   * array

Ejemplos de tipos primitivos:

```
var num = 10;
var str = "texto";
var bol = true;
var und = undefined;
var nul = null;
```

La **escritura dinámica** se refiere que a pesar de que una variable se inicializo con un valor de un tipo, puede almacenar el valor de otro tipo y no nos provocara error:

```
num = str;
console.log(num); // texto

bol = 50;
console.log(bol); // 50
``` 

#### Objetos

Un objeto es una colección de datos primitivos u otros objetos.

Un objeto vacío se declara así:

`var obj = {};`

Un objeto con valores usa la nomenclatura de pares para declararlos, si tiene más de una propiedad se separan con comas:

```
var obj = {
  numero: 10,
  texto: "Hola"
}

console.log( obj ); // {numero: 10, texto: "Hola"}
```

Un objeto puede contener más objetos:

```
var obj = {
  numero: 10,
  texto: "Hola",
  objHijo: {
    numero: 20,
    texto: "Hi"
  }
}

console.log( obj ); //{numero: 10, texto: "Hola", objHijo: {…}}
console.log( objHijo );

//output
numero: 10
objHijo: {numero: 20, texto: "Hi"}
texto: "Hola"
```

## Por Valor y por Referencia

Las **variables primitivas** siempre **se pasan por valor**. Cada variable tiene su espacio reservado en memoria y aun que se igualen dos variables cada una hace referencia a su localidad de memoria como podemos ver en el siguiente ejemplo:

```
var a = 10;
var b = a;

console.log("a:", a); //10
console.log("b:", b); //10

a = 20;

console.log("a:", a); //20
console.log("b:", b); //10

//output
a: 10
b: 10
a: 20
b: 10
```

Cuando cambiamos el valor de **a** sólo se cambia el valor de **a**,  **b** sigue conservando su valor asignado inicialmente, esto es lo que se conoce como **paso por valor**.

Vamos a ver qué pasa con los objetos:

```
var c = {
  nombre: "Juana"
}

var d = c;

console.log("c:", c); //{nombre: "Juana"}
console.log("d:", d); //{nombre: "Juana"}

c.nombre = "Gina"

console.log("c:", c); //{nombre: "Gina"}
console.log("d:", d); //{nombre: "Gina"}

//output
c: {nombre: "Juana"}
d: {nombre: "Juana"}
c: {nombre: "Gina"}
d: {nombre: "Gina"}
```

Nótese que se está haciendo algo similar a lo que se hizo con los datos primitivos, sin embargo, aquí cuando se cambia una propiedad en un objeto también se cambia el otro objeto. Esto es porque al haber asignado un objeto al otro esto se hace por referencia es decir los dos objetos apuntan al mismo lugar y si existe un cambio en los datos ambos objetos observaran dichos cambios por que apuntan al mismo sitio.

## Notación de Punto y Corchetes

Cuando declaramos objetos con propiedades, la forma de acceder a esas propiedades es a través de la **Notación de Punto** o la **Notación de Corchetes**.

### Notación de Punto

Ejemplo de la notación de punto:

```
var persona = {
  nombre : "Leonel",
  apellido : "Messi",
  edad : 30,
  direccion : {
    ciudad: "Barcelona",
      pais: "España"
  }
};

console.log(persona); //{nombre: "Leonel", apellido: "Messi", edad: 30, direccion: {…}}

console.log(persona.nombre); //Leonel
console.log(persona.apellido); //Messi
console.log(persona.edad); //30

console.log(persona.direccion);//{ciudad: "Barcelona", pais: "España"}

console.log(persona.direccion.ciudad);//Barcelona
console.log(persona.direccion.pais);//España

//output
{nombre: "Leonel", apellido: "Messi", edad: 30, direccion: {…}}
Leonel
Messi
30
{ciudad: "Barcelona", pais: "España"}
Barcelona
España
```

Es posible añadir campos adicionales a un objeto que no se declararon inicialmente:

```
persona.direccion.zipcode = 29055;
console.log(persona.direccion);//{ciudad: "Barcelona", pais: "España", zipcode: 29055}
console.log(persona.direccion.zipcode);//29055

//output
{ciudad: "Barcelona", pais: "España", zipcode: 29055}
29055
```

JS no tiene ningún problema para añadir este campo al objeto.

Los objetos pueden ser tan complejos como se necesite, anidando objetos sobre objetos:

```
var persona = {
  nombre : "Leonel",
  apellido : "Messi",
  edad : 30,
  direccion : {
    ciudad: "Barcelona",
    pais: "España"
    edificio: {
      nombre: "Edificio Principal",
      telefono: "999-88-77-66"
    }
  }
};
```

¿Cómo accedemos al teléfono?

`console.log(persona.direccion.edificio.telefono);`

Cuando necesitamos trabajar con muchas propiedades de edificio se podría volver tedioso estar escribiendo siempre `persona.direccion.edificio.propiedad` para cada una de las propiedades, gracias a la **asignación por referencia** de los objetos podríamos crear una variable con el valor del objeto edificio.

```
var edificio = persona.direccion.edificio;
console.log(edificio.telefono);//999-88-77-66
```

De esta manera podríamos ahorrarnos el hecho de estar escribiendo muchas veces `persona.direccion.edificio` y solo escribir `edificio`.

### Notación por corchetes

La notación por corchetes es otra forma de recuperar los valores de las propiedades del objeto:

```
var persona = {
  nombre : "Leonel",
  apellido : "Messi",
  edad : 30,
  direccion : {
    ciudad: "Barcelona",
    pais: "España"
    edificio: {
       nombre: "Edificio Principal",
       telefono: "999-88-77-66"
    }
  }
};

console.log(persona["nombre"]); //Leonel
console.log(persona["apellido"]); //Messi
console.log(persona["edad"]); //30
console.log(persona["direccion"]["pais"]); //España

//output
Leonel
Messi
30
España
```

El verdadero potencial de la **notación de corchetes** es que podemos recuperar valores dinámicamente ya que, en los corchetes podríamos colocar el valor de una variable que represente el valor de un campo, por ejemplo:

```
var nom = "nombre";
console.log(persona[nom]); //Leonel

//output
Leonel
```

## Funciones

Vamos a ver un ejemplo de una función sencilla:

```
//Declaración de la función
function primeraFuncion(){
  var a = 20;
  console.log( a );
}

//Invocación de la función
primeraFuncion();

//output
20
```

Vemos que la variable `a` esta definida dentro del contexto de la función, podríamos tener una variable definida a nivel global.

```
var a = 30;

//Declaración de la función
function primeraFuncion(){
  var a = 20;
  console.log( a );
}

//Invocación de la función
primeraFuncion();
```

Lo que se sigue mostrando en la consola es: `20` ya que lo primero que hace es ver si existe definida una variable `a` en su contexto y como existe es la que imprime.

Vamos a quitar la variable definida en la función para ver qué pasa:

```
var a = 30;

//Declaración de la función
function primeraFuncion(){  
  console.log( a );
}

//Invocación de la función
primeraFuncion();
```

En este caso lo que se imprime es `30` ya que como no existe una variable `a` en el contexto de la función lo busca fuera y se encuentra una con valor de 30.

Que pasa si quitamos la variable declarada de forma global.

```
//Declaración de la función
function primeraFuncion(){  
  console.log( a );
}

//Invocación de la función
primeraFuncion();
```

Aquí busca primero en el contexto de la función la variable `a` no la encuentra busca a nivel global y tampoco la encuentra, mostrándonos el error `Uncaught ReferenceError: a is not defined` y deteniendo la ejecución del programa.

La última posibilidad que tenemos es declarar la variable a nivel global pero después de haber invocado la función.

```
//Declaración de la función
function primeraFuncion(){  
  console.log( a );
}

//Invocación de la función
primeraFuncion();

var a=40;
```

Aquí el resultado que nos devuelve es el de `undefined` ya que, si se ha declarado la variable, pero en el momento de su uso no tenía aún valor.

Esta última forma de declarar una variable no es muy recomendable, pero JS lo permite y no existe error, solo que puede provocar errores lógicos o situaciones inesperadas.

En JS podremos invocar a funciones, aunque su definición este en una ubicación posterior:

```
var a = 40;

//Invocación de la función
primeraFuncion();

//Declaración de la función
function primeraFuncion(){
  console.log( a );
}

//output
40
```

Todas las funciones en JavaScript cuando se ejecutan regresan un valor, para los ejemplos que hemos visto hasta el momento el valor que regresan es el de `undefined`.

Si escribimos en la consola:

```
> primeraFuncion()
40
undefined
```

Ejecuta las instrucciones de la función y cuando finaliza devuelve el valor de la función

Nótese que no es lo mismo escribir la función con paréntesis que sin ellos:

```
> primeraFuncion
ƒ primeraFuncion(){
  console.log( a );
}
```

Si solo escribimos el nombre de la función nos regresara la definición de la función.

Podríamos asignar el resultado de una función a una variable de la siguiente forma:

```
var a = 40;

//Declaración de la función
function primeraFuncion(){
  console.log( a );
}

var f = primeraFuncion();

console.log(f);

//output
40
undefined
```

Pero si lo que asignamos a la variable es la función tenemos:

```
var a = 40;

//Declaración de la función
function primeraFuncion(){
  console.log( a );
}

var f = primeraFuncion;

console.log(f);
```

Nótese que en este caso no se ejecuta la función solo se asigna por eso f es:

```
//output
ƒ primeraFuncion(){
  console.log( a );
}
```

## Parámetros para las funciones

Una muy buena práctica es colocar todas las definiciones de nuestras funciones al inicio del archivo.

### Paso de valores primitivos a una Función como parámetro.

Vamos a ver el ejemplo de una función que recibe un parámetro.

```
function imprimir(nombre){
  console.log( nombre );
}

imprimir("Juan"); //"Juan" se conoce como variable anónima

//output
Juan
```

Vamos a hacer que reciba dos parámetros:

```
//Declaración de la función
function imprimir(nombre, apellido){
  console.log( nombre + " " + apellido);
}

imprimir("Juan", "Padilla");

//output
Juan Padilla
```

Que sucede si la función recibe dos parámetros, pero solo le mandamos uno:

```
function imprimir(nombre, apellido){
  console.log( nombre + " " + apellido);
}

imprimir("Juan");

//output
Juan undefined
```

Cuando se colocan los nombres de los argumentos de la función se reserva el lugar en memoria por eso en este caso es **undefined** cuando lo imprime por que previamente se declaró, pero no fue posible asignarle algún valor.

Ahora vamos a quitar de los argumentos a apellidos y veamos que pasa:

```
function imprimir(nombre){
  console.log( nombre + " " + apellido);
}

imprimir("Juan");
```

Lo esperado muestra `Uncaught ReferenceError: apellido is not defined` porque se trata de usar una propiedad no definida en ningún lado.

Podríamos validar si nuestro parámetro tiene un valor `undefined` para asignarle un valor predeterminado:

```
function imprimir(nombre, apellido){
  if( apellido === undefined ){
  	apellido = "XXXXX";
  }
  console.log( nombre + " " + apellido);
}

imprimir("Juan");

//output
Juan XXXXX
```

Existe una alternativa más corta de escribir lo mismo sin el uso de un if:

```
function imprimir(nombre, apellido){  
  apellido = apellido || "XXXXX";  
  console.log( nombre + " " + apellido);
}

imprimir("Juan");
```

Si apellido es `undefined` le asigna "XXXXX" y si no le asigna el valor de apellido.

El resultado en este caso es `Juan XXXXX`

Si le mando el apellido:


```
function imprimir(nombre, apellido){  
  apellido = apellido || "XXXXX";  
  console.log( nombre + " " + apellido);
}

imprimir("Juan", "Padilla");

//output
Juan Padilla
```

### Paso de un Objeto a una Función como parámetro.

Vamos a realizar un ejemplo de una función que recibe como parámetro un objeto.

```
function imprimir(persona){    
  console.log( persona.nombre + " " + persona.apellido);
}

imprimir({nombre: "Juan", apellido: "Padilla"});

//output
Juan Padilla
```

En este ejemplo estamos pasando como parámetro un objeto anónimo es decir no existe su declaración simplemente se pasa su definición como parámetro.

Pero podríamos primero definir el objeto y ya definido pasarlo como parámetro.

```
function imprimir(persona){    
  console.log( persona.nombre + " " + persona.apellido);
}

obj = {
  nombre: "Juan", 
  apellido: "Padilla"
}

imprimir(obj);

Juan Padilla
```

Si dentro de la función se cambia algún valor del objeto persona:

```
function imprimir(persona){    
  console.log( persona.nombre + " " + persona.apellido);
  persona.nombre = "José";
}

obj = {
  nombre: "Juan", 
  apellido: "Padilla"
}

imprimir(obj);

console.log(obj);
```

y posteriormente se imprime el objeto obj, este tendrá los cambios gracias a que los objetos se pasan por referencia:

```
Juan Padilla
{nombre: "José", apellido: "Padilla"}
 ```

### Paso de una función como parámetro a otra función

En este caso vamos a ver un ejemplo de una función que recibe como parámetro otra función que se le pasa de forma anónima:

```
function imprimir( fn ){    
  fn();
}

imprimir( function() {
	console.log("Función anónima");
});

//output
Función anónima
```

Ahora vamos a definir una función que es la que pasaremos como parámetro:

```
function imprimir( fn ){    
  fn();
}

var miFuncion = function(){
  console.log("Función declarada");
}

imprimir( miFuncion );

//output
Función declarada
```

## El retorno de las funciones

Hasta el momento todas las funciones que hemos visto de ejemplo regresan un tipo **undefined**, pero también pueden regresar **valores primitivos**, **objetos**, **funciones** o `null`.

Para que una función regrese algo se utiliza la palabra reservada `return`.

Función que retorna un **Number**:

```
function obtenerAleatorio(){    
  //Regresa un número aleatorio entre 0-1
  return Math.random();
}

console.log( obtenerAleatorio() );

//output
0.7339542870086062
```

**Math** es un objeto incorporado que tiene propiedades y métodos para constantes y funciones matemáticas. No es un objeto de función. Si escribe Math en la consola podrá ver todas sus propiedades y métodos.

```
E: 2.718281828459045
LN2: 0.6931471805599453
LN10: 2.302585092994046
LOG2E: 1.4426950408889634
LOG10E: 0.4342944819032518
PI: 3.141592653589793
SQRT1_2: 0.7071067811865476
SQRT2: 1.4142135623730951
abs: ƒ abs()
acos: ƒ acos()
acosh: ƒ acosh()
asin: ƒ asin()
asinh: ƒ asinh()
atan: ƒ atan()
atan2: ƒ atan2()
atanh: ƒ atanh()
cbrt: ƒ cbrt()
ceil: ƒ ceil()
clz32: ƒ clz32()
cos: ƒ cos()
cosh: ƒ cosh()
exp: ƒ exp()
expm1: ƒ expm1()
floor: ƒ floor()
fround: ƒ fround()
hypot: ƒ hypot()
imul: ƒ imul()
log: ƒ log()
log1p: ƒ log1p()
log2: ƒ log2()
log10: ƒ log10()
max: ƒ max()
min: ƒ min()
pow: ƒ pow()
random: ƒ random()
round: ƒ round()
sign: ƒ sign()
sin: ƒ sin()
sinh: ƒ sinh()
sqrt: ƒ sqrt()
tan: ƒ tan()
tanh: ƒ tanh()
trunc: ƒ trunc()
```

Función que retorna un **String**:

```
function obtenerNombre(){
  return "Juan";
}

console.log( obtenerNombre() + " Padilla");

var nombre = obtenerNombre();
console.log(nombre);

//output
Juan Padilla
Juan
```

Función que retorna un **Booleano**.

```
function obtenerAleatorio(){    
  //Regresa un número aleatorio entre 0-1
  return Math.random();
}

function esMayor05(){
  var num = obtenerAleatorio()
  console.log(num);
  if( num > 0.5 ){
    return true;
  }else{
    return false;
  }
}

if ( esMayor05() ){
  console.log("Es mayor que 0.5");
} else{
  console.log("Es menor que 0.5");
}

//output
0.9466023550745175
Es mayor que 0.5

0.2531383311209956
Es menor que 0.5
```

Función que regresa un **objet (anónimo)**.

```
function crearPersona( nombre, apellido){
  return {
    nombre: nombre,
    apellido: apellido
  }
}

var persona = crearPersona("Penelope", "Cruz");
console.log( persona );
console.log( persona.nombre );
console.log( persona.apellido );

//output
{nombre: "Penelope", apellido: "Cruz"}
Penelope
Cruz
```

Funciones que regresan una **function**.

```
function crearFuncion(){
  return function(){
    console.log("Soy la función anónima...")
  }
}

var nuevaFuncion = crearFuncion();
nuevaFuncion();

//output
Soy la función anónima...
```

```
function crearSaludo(){
  return function(nombre){
    console.log("Hola " + nombre)
  }
}

var saludar = crearSaludo();
saludar("Penelope");

//output
Hola Penelope
```

```
function crearSaludo(){
  return function(nombre){
    console.log("Hola " + nombre);

    return function() {
      console.log("Hello Everybody!!!");
    }
  }
}

var saludar = crearSaludo();
var greet = saludar("Penelope");
greet();

//output
Hola Penelope
Hello Everybody!!!
```

## Funciones de primera clase

Un lenguaje de programación se dice que tiene Funciones de primera clase cuando las funciones en ese lenguaje son tratadas como cualquier otra variable. Por ejemplo, en ese lenguaje, una función puede ser pasada como argumento a otras funciones, puede ser retornada por otra función y puede ser asignada a una variable.

Veamos el siguiente ejemplo:

```
function a(){
  console.log("Función a");
}

a();

//output
Función a
```

Una función llamada **a** que al ser invocada pinta en la consola `Función a`, hasta aquí todo normal.

Como se había mencionado anteriormente **las funciones son objetos**. 

Si en la consola escribimos `a.` veremos una lista de propiedades de las funciones:

```
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
```

Como `a` es un objeto podemos añadirle un campo de la siguiente forma:

`a.nombre = "Adolfo"`

Si en la consola veo el valor de `a`, veremos su definición:

```
a
ƒ a(){
  console.log("Función a");
}
```

¿Dónde quedo nombre? nombre aparece si en la consola escribo `a.` paso a ser una propiedad más del objeto (función) `a`:

```
a.nombre
"Adolfo"
```

Debemos tener precaución con remplazar alguna de las propiedades que ya vienen configuradas para los objetos (lista anterior), aunque hay algunas que, aunque las intentemos cambiar no se cambiar, por ejemplo:

`a.name = "Adolfo"`

`"a"` (Nombre de la función)

Su valor sigue conservando su valor original, pero hay otras propiedades que, si aceptan el cambio, por lo que hay que tener precaución con eso y evitar cambiar dichos valores.

## Métodos y el objeto THIS

Un método es una función la cual es propiedad de un Objeto.

Ejemplo:

```
var persona = {
  nombre: "Adolfo",
  apellido: "De la Rosa",
  imprimirNombre: function(){
    console.log("Nombre completo... ");
  }
}

persona.imprimirNombre();

//output
Nombre completo... 
```

Simplemente muestra el mensaje que está en el `console.log`, si en lugar de mostrar ese mensaje quisiera mostrar el valor de nombre:

```
var persona = {
  nombre: "Adolfo",
  apellido: "De la Rosa",
  imprimirNombre: function(){
    console.log(nombre);
  }
}

persona.imprimirNombre();
```

Al ejecutar este código nos da el error:

`Uncaught ReferenceError: nombre is not defined`

Esto es porque el busca la declaración de una variable llamada `nombre` y no la encuentra, es decir:

```
var nombre = "Alfredo"

var persona = {
  nombre: "Adolfo",
  apellido: "De la Rosa",
  imprimirNombre: function(){
    console.log(nombre);
  }
}

persona.imprimirNombre();

//output
Alfredo
``` 

Pero realmente esto no es lo que nosotros queremos, lo que queremos es hacer referencia a la propiedad nombre que se encuentra en el objeto persona.

### This

En la mayoría de los casos, el valor de **this** está determinado por cómo se llama una función (enlace de tiempo de ejecución). No se puede establecer mediante asignación durante la ejecución, y puede ser diferente cada vez que se llama a la función.

Veamos un ejemplo:

```
var persona = {
  nombre: "Adolfo",
  apellido: "De la Rosa",
  imprimirNombre: function(){
    console.log(this);
  }
}

persona.imprimirNombre();
```

En este caso el valor `this` hace referencia al *objeto persona*:

`{nombre: "Adolfo", apellido: "De la Rosa", imprimirNombre: ƒ}`

Por lo que si quisiera desplegar el nombre completo de la persona lo haría de la siguiente forma:

```
var persona = {
  nombre: "Adolfo",
  apellido: "De la Rosa",
  imprimirNombre: function(){
    console.log(this.nombre + " " + this.apellido);
  }
}

persona.imprimirNombre();

//output
Adolfo De la Rosa
```

Inclusive si hay declaradas dos variables con esos mismos nombres:

```
var nombre = "Alfredo";
var apellido = "Landa";

var persona = {
  nombre: "Adolfo",
  apellido: "De la Rosa",
  imprimirNombre: function(){
    console.log(this.nombre + " " + this.apellido);
  }
}

persona.imprimirNombre();

//output
Adolfo De la Rosa
```

Si cambiamos el valor de las propiedades `this` siempre va a hacer referencia al valor actual de la misma:

```
var persona = {
  nombre: "Adolfo",
  apellido: "De la Rosa",
  imprimirNombre: function(){
    console.log(this.nombre + " " + this.apellido);
  }
}

persona.nombre = "Alfredo";
persona.imprimirNombre();

//output
Alfredo De la Rosa
```

Como se mencionó al inicio de esta sección el valor de `this` dependerá de cómo se ejecuta la función, veámoslo con un ejemplo:

```
var persona = {
  nombre: "Adolfo",
  apellido: "De la Rosa",
  imprimirNombre: function(){
    console.log(this);
  },
  direccion: {
    pais: "México",
    imprimirPais: function(){
      console.log(this);
    }
  }
}

persona.imprimirNombre();
persona.direccion.imprimirPais();
```

En el primer caso `this` hace referencia al *objeto persona*:

`{nombre: "Adolfo", apellido: "De la Rosa", imprimirNombre: ƒ, direccion: {…}}`

Y en el segundo caso hace referencia al *objeto direccion*:

`{pais: "México", imprimirPais: ƒ}`

Así que debemos tener esto en cuenta cuando usemos `this`.

Para desplegar todos los valores de los campos el código quedaría así:

```
var persona = {
  nombre: "Adolfo",
  apellido: "De la Rosa",
  imprimirNombre: function(){
    console.log(this.nombre + " " + this.apellido);
  },
  direccion: {
    pais: "México",
    imprimirPais: function(){
      console.log(this.pais);
    }
  }
}

persona.imprimirNombre();
persona.direccion.imprimirPais();

//output
Adolfo De la Rosa
México
```

Hay veces que no `this` no valga lo que nosotros esperamos o imaginamos, veamos el siguiente ejemplo:

```
var persona = {
  nombre: "Adolfo",
  apellido: "De la Rosa",
  imprimirNombre: function(){
    console.log(this.nombre + " " + this.apellido);
  },
  direccion: {
    pais: "México",
    imprimirPais: function(){
      console.log("País de nacimiento: " + this.pais);
      var paisResidencia = function(){
        console.log( this );
      }
      paisResidencia();
    }
  }
}

persona.imprimirNombre();
persona.direccion.imprimirPais();
```

Vamos a desglosar el código, tenemos el *objeto persona* dentro de él tenemos el *objeto direccion* el cual contiene la función *imprimirPais* y dentro de esta función hemos declarado la función *paisResidencia* que lo que hace es imprimir el valor e `this`, la pregunta es ¿Qué nos va a regresar `this`?

Lo que nos regresa `this` a este nivel es el **Objeto Global Window**:

`Window {postMessage: ƒ, blur: ƒ, focus: ƒ, close: ƒ, parent: Window, …}`

¿Realmente esperábamos este valor? ¿Es un fallo de JS?¿Esperábamos que el resultado fuera el valor de la función imprimirPais?

Pues no lo sé, pero por eso es importante siempre antes de usar `this` ver qué valor regresa para evitar sorpresas.

Vamos a modificar nuestro código para mostrar una posible solución de cómo acceder a  valores que esperamos encontrar en `this` pero que por alguna razón no nos es posible:

```
var persona = {
  nombre: "Adolfo",
  apellido: "De la Rosa",
  imprimirNombre: function(){
    console.log(this.nombre + " " + this.apellido);
  },
  direccion: {
    pais: "México",
    imprimirPais: function(){
      var self = this;
      var paisResidencia = function(){
        console.log("País de nacimiento: " + self.pais);
      }
      paisResidencia();
    }
  }
}

persona.imprimirNombre();
persona.direccion.imprimirPais();
```

Aquí lo que estamos haciendo es pasar por referencia el objeto this (direccion) a la variable self(por convención se usa este nombre) y de esta manera podemos llevar los valores de `this` a otro contexto en el cual no tenía acceso.

El resultado es:

```
Adolfo De la Rosa
País de nacimiento: México
```

## La palabra reservada... new

El operador **new** permite crear una instancia de un tipo de objeto definido por el usuario o de uno de los tipos de objeto integrados que tiene una función constructor. La palabra reservada **new** hace lo siguiente:

1. Crea un objeto JavaScript plano en blanco
2. Vincula (establece el constructor de) este objeto a otro objeto
3. Pasa el objeto recién creado en el paso 1 como el contexto `this`
4. Devuelve `this` si la función no devuelve su propio objeto.

Vamos a ver el siguiente ejemplo:

```
function Persona(){

}

var persona = Persona();

console.log( persona );
```

Si pensamos un poco ya sabemos que esto nos va a regresar:

`undefined`

Vamos a hacer un pequeño cambio en el código añadiendo la palabra reservada `new` al crear a *persona*, es decir:

```
function Persona(){

}

var persona = new Persona();

console.log( persona );
```

Con este pequeño cambio el resultado que obtenemos es:

`Persona {}`

Un objeto Persona vacío. Es decir, estamos creando una instancia de un tipo de objeto definido por nosotros.

Podemos insertar "propiedades" a la función:

```
function Persona(){
  this.nombre = "Penelope";
  this.apellido = "Cruz";
  this.edad = 30;
}

var persona = new Persona();

console.log( persona );
```

Y lo que tendremos es una instancia de Persona que contiene propiedades:

`Persona {nombre: "Penelope", apellido: "Cruz", edad: 30}`

Si le quitamos el `new` nuevamente me regresaría `undefined`, al crear la variable *persona* se invoca la función *Persona* y se crean las tres propiedades definidas así que las 4 propiedades se almacenan en el objeto global Window.

Pero si usamos `new` para crear a *persona* solo tenemos esta propiedad en el objeto global Window, las propiedades de *Persona* son propiedades de *persona*, si las desplegar es con `persona.nombre` por ejemplo.

Podríamos también incluir un método en *Persona*:

```
function Persona(){
  this.nombre = "Penelope";
  this.apellido = "Cruz";
  this.edad = 30;

  this.nombreCompleto = function(){
    return this.nombre + " " + this.apellido;
  }
}

var persona = new Persona();

console.log( persona );
console.log( persona.nombre );
console.log( persona.nombreCompleto() );

//output
Persona {nombre: "Penelope", apellido: "Cruz", edad: 30, nombreCompleto: ƒ}
Penelope
Penelope Cruz
```

También podría mandar parámetros a mi función para que de alguna manera inicialice el objeto que creo:

```
function Persona(nombre, apellido, edad){
  this.nombre = nombre;
  this.apellido = apellido;
  this.edad = edad;

  this.nombreCompleto = function(){
    return this.nombre + " " + this.apellido;
  }
}

var persona = new Persona("Salma", "Hayek", 31);

console.log( persona );
console.log( persona.nombre );
console.log( persona.nombreCompleto() );

//output
Persona {nombre: "Salma", apellido: "Hayek", edad: 31, nombreCompleto: ƒ}
Salma
Salma Hayek
```

## El señor de los anillos :: The JavaScript Game

Código de ejemplo:

```
function Jugador( nombre){
  this.nombre = nombre;
  this.pv = 100;
  this.sp = 100;

  this.curar = function ( jugadorObjetivo ){
    if( this.sp >= 40){
      this.sp -= 40;
      jugadorObjetivo.pv += 20; 
    }else{
      console.info( this.nombre + " no tiene sp suficiente para curar");
    }
    this.estado( jugadorObjetivo );
  }

  this.tirarFlecha = function( jugadorObjetivo ){
    if( jugadorObjetivo.pv > 40 ){
      jugadorObjetivo.pv -= 40; 
    }else{
      jugadorObjetivo.pv = 0; 
      console.error(jugadorObjetivo.nombre + " murio!!!");
    }
    
    this.estado( jugadorObjetivo );
  }

  this.estado = function( jugadorObjetivo ){
    console.info( this );
    console.info( jugadorObjetivo );
  }   
}

var gandalf = new Jugador("Gandalf");
var legolas = new Jugador("Legolas");

console.log( gandalf );
console.log( legolas );

gandalf.tirarFlecha(legolas);
gandalf.curar(legolas);

legolas.tirarFlecha(gandalf);
legolas.tirarFlecha(gandalf);
legolas.tirarFlecha(gandalf);
```

```
//output
Jugador {nombre: "Gandalf", pv: 100, sp: 100, curar: ƒ, tirarFlecha: ƒ, …}
Jugador {nombre: "Legolas", pv: 100, sp: 100, curar: ƒ, tirarFlecha: ƒ, …}

Jugador {nombre: "Gandalf", pv: 100, sp: 100, curar: ƒ, tirarFlecha: ƒ, …}
Jugador {nombre: "Legolas", pv: 60, sp: 100, curar: ƒ, tirarFlecha: ƒ, …}

Jugador {nombre: "Gandalf", pv: 100, sp: 60, curar: ƒ, tirarFlecha: ƒ, …}
Jugador {nombre: "Legolas", pv: 80, sp: 100, curar: ƒ, tirarFlecha: ƒ, …}

Jugador {nombre: "Legolas", pv: 80, sp: 100, curar: ƒ, tirarFlecha: ƒ, …}
Jugador {nombre: "Gandalf", pv: 60, sp: 60, curar: ƒ, tirarFlecha: ƒ, …}

Jugador {nombre: "Legolas", pv: 80, sp: 100, curar: ƒ, tirarFlecha: ƒ, …}
Jugador {nombre: "Gandalf", pv: 20, sp: 60, curar: ƒ, tirarFlecha: ƒ, …}

Gandalf murio!!!

{nombre: "Legolas", pv: 80, sp: 100, curar: ƒ, tirarFlecha: ƒ, …}
{nombre: "Gandalf", pv: 0, sp: 60, curar: ƒ, tirarFlecha: ƒ, …}
```

## Prototipos: prototype

Un prototipo es un modelo que muestra la apariencia y el comportamiento de una aplicación o producto al principio del ciclo de vida del desarrollo.

El objetivo de los prototipos es hacer más eficiente el uso de los objetos.

Vamos a tener una función de primer orden:

```
function Persona(){
  this.nombre   = "Pablo";
  this.apellido = "Alborán";
  this.edad     = 32;

  this.imprimirInfo = function(){
    console.log( this.nombre + " " + this.apellido + " (" + this.edad + ")" );
  }
}

var persona = new Persona();

persona.imprimirInfo();

//output
Pablo Alborán (32)
```

Ya hemos visto la manera de añadir propiedades o métodos a una función una vez que está ya se definió:

```
function Persona(){
  this.nombre   = "Pablo";
  this.apellido = "Alborán";
  this.edad     = 32;

  this.imprimirInfo = function(){
    console.log( this.nombre + " " + this.apellido + " (" + this.edad + ")" );
  }
}

var persona = new Persona();

persona.imprimirInfo();

persona.pais = "España";

console.log( persona );

//output
Persona {nombre: "Pablo", apellido: "Alborán", edad: 32, imprimirInfo: ƒ, pais: "España"}
```

El código anterior define un objeto (función) Persona el cual tiene tres propiedades y un método, creamos la instancia *persona* de tipo *Persona*, invocamos el método y posteriormente agregamos una propiedad a la instancia *persona* llamada *pais* y finalmente mostramos en consola el valor final de la instancia *persona*.

Vamos a usar otra forma diferente para añadir la propiedad a la función *Persona* una vez que ya se definió, pero usando prototipos.

```
function Persona(){
  this.nombre   = "Pablo";
  this.apellido = "Alborán";
  this.edad     = 32;

  this.imprimirInfo = function(){
    console.log( this.nombre + " " + this.apellido + " (" + this.edad + ")" );
  }
}

Persona.prototype.pais = "España";

var persona = new Persona();

console.log(persona);

//output
Persona {nombre: "Pablo", apellido: "Alborán", edad: 32, imprimirInfo: ƒ}
```

Observemos que de entrada no vemos la propiedad país, pero si desplegamos el objeto en la consola tenemos:

```
Persona {nombre: "Pablo", apellido: "Alborán", edad: 32, imprimirInfo: ƒ}
  apellido: "Alborán"
  edad: 32
  imprimirInfo: ƒ ()
  nombre: "Pablo"
  __proto__:
    pais: "España"
    constructor: ƒ Persona()
    __proto__: Object
```

Tenemos una sección llamada **__proto__** y allí dentro se encuentra la  propiedad que añadimos.

Aunque la propiedad se encuentre en la sección *proto* yo la puedo seguir invocando con `persona.pais` para recuperar su valor.

Aquí el uso de los prototipos no tiene mucho sentido para añadir propiedades ya que las podemos añadir desde la definición, la verdadera utilidad de los prototipos esta al definir los métodos.

En el ejemplo anterior al instanciar el objeto Persona siempre creara 3 propiedades y un método, si tenemos 1000 instancias tendremos 1000 datos de personas diferentes, pero 1000 el mismo método repetido para cada uno de ellos y esto puede provocar un uso inadecuado de memoria entre otras cosas.

Si nosotros colocamos el método en el prototipo tendremos 1000 datos de personas diferentes, pero solamente una vez la definición del método, veamos el siguiente ejemplo:

```
function Persona(){
  this.nombre   = "Pablo";
  this.apellido = "Alborán";
  this.edad     = 32;
}

Persona.prototype.imprimirInfo = function(){
    console.log( this.nombre + " " + this.apellido + " (" + this.edad + ")" );
}

var persona = new Persona();

persona.imprimirInfo();
console.log(persona);

//output
Pablo Alborán (32)
Persona {nombre: "Pablo", apellido: "Alborán", edad: 32}
```

Si desplegamos *Persona* vemos que el método **imprimirInfo** se encuentra dentro de *proto*:

```
Persona {nombre: "Pablo", apellido: "Alborán", edad: 32}
  apellido: "Alborán"
  edad: 32
  nombre: "Pablo"
  __proto__:
    imprimirInfo: ƒ ()
    constructor: ƒ Persona()
    __proto__: Object
```

Los prototipos no tienen límites, es decir que tienen un nivel de anidación infinito.

Cabe resaltar que todos los tipos de datos primitivos usan los prototipos para almacenar allí todos los métodos que podemos usar con cada uno de ellos por ejemplo `texto.substring` o `numero.toFixed`.

Inclusive podríamos meter un nuevo prototipo al tipo Number (nada recomendable).

```
Number.prototype.esPositivo = function(){
  if( this > 0){
    return true;
  }else{
    return false;
  }
}
```

En la consola podemos ver:

```
var a = 1;
undefined

a.esPositivo()
true

a = -10
-10

a.esPositivo()
false
```

Como ya se mencionó no es muy recomendable usar prototipos para los tipos de datos de JS, usarlos para los tipos definidos por el usuario.

## Funciones Anónimas

Ayudan a mantener el código encapsulado, permitiendo que otras secciones del código cambien accidentalmente valores de propiedades generalmente definidas en el objeto global window.

Véase el siguiente código.

```
var a = 10;

console.log( a );

function cambiarA(){
  a = 20;
}

cambiarA();

console.log( a );

//output
10
20
```

Tenemos un código que declara una variable global y que "accidentalmente" cambiamos el valor dentro de nuestra función, esto podría causar errores inesperados.

Para evitar esto podemos tener una función anónima que encapsule nuestro código y lo mantenga aislado del resto.

Veamos el siguiente código.

```
(function(){
  var a = 10;
  console.log( a );

  function cambiarA(){
    a = 20;
  }

  cambiarA();

  console.log( a );
})();

//output
10
20
```

De esta manera se define una función anónima, nótese que no tienen ningún nombre y la forma de invocarla es con **()**.

El resultado obtenido es el mismo que con la función definida, pero existe **una gran diferencia**, que en el objeto global no tenemos definida la variable `a` y en caso de que otro proceso la definiera, nuestra función anónima haría referencia a la variable dentro de su contexto, evitando cambiar accidentalmente el valor de una variable global.

Otro uso de las funciones anónimas puede ser cuando pasamos como parámetro una función a otra función, podemos armar la función dentro de los paréntesis de los parámetros. Veamos el siguiente ejemplo:

```
function ejecutarFuncion( fn ){
  fn();
}

ejecutarFuncion(function(){  
  console.log("Función anónima ejecutada...");
});

//output
Función anónima ejecutada...
```

La función anónima incluso podría regresar un valor;

```
function ejecutarFuncion( fn ){
  if(fn()){
    console.log("Todo ha ido bien!!!!");
    return 1;
  }
}

ejecutarFuncion(function(){  
  console.log("Función anónima ejecutada...");
  return true;
});
```

## Funciones typeof e instanceof... interesante

### typeof

Nos permitirá saber el tipo de una variable.

```
function identificaTipo( dato ){
  console.log( typeof dato );
}

identificaTipo(1);
identificaTipo("1");
identificaTipo(true);
identificaTipo(undefined);
identificaTipo(null);
identificaTipo(['1','2']);
identificaTipo(function(){});
identificaTipo({a:1});

//output
number
string
boolean
undefined
object
object
function
object
```

Podríamos usar el operador **typeof** para validar los datos que se reciben y dependiendo de su tipo realizar diferentes acciones:

```
function identificaTipo( dato ){
  if( typeof dato == "function" ){
    dato();
  }else{
    console.log( dato )
  }
}

identificaTipo(function(){console.log("Ejecuta función anónima")});
identificaTipo({a:1});
identificaTipo("Hola Mundo!!!");

//output
Ejecuta función anónima
{a: 1}
Hola Mundo!!!
```

### instanceof 

Recordemos que tenemos los tipos definidos por el usuario y puede ser que lo que queramos saber si un objeto es de un tipo de instancia determinada, para eso usamos el operador **instanceof**, el cual nos regresara un true o un false si es o no de una determinada instancia.

```
function identifica( dato ){
  console.log( typeof dato );
  console.log( dato instanceof Persona );
}

function Persona(){
  this.nombre = "Penelope";
  this.edad = 30;
}

var persona = new Persona();

identifica(persona);
identifica(persona.nombre);

//output
object
true
string
false
```
