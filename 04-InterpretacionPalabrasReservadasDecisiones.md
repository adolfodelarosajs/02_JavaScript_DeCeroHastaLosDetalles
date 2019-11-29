# Interpretación, palabras reservadas, decisiones, escape y cookies

## El ";" (punto y coma) es opcional?

El punto y coma es opcional en JS.

```
var a = 1
var b = 2
var c = 3
var nombre = "Penélope"

console.log(a)
console.log(b)
console.log(c)
console.log(nombre)

//output
1
2
3
Penélope
```

Pero podría pensarse que cuando se pone el ; siempre se termina una sentencia, existe un caso que no es así:

```
function getNumero(){
	return 
	10;
}

console.log( getNumero() );

//output
undefined
```

Aquí es porque el return se ejecuta y como él ; es opcional ignora todo lo que sigue regresando un `undefined`.

## Comentarios en Javascript y espaciado.

Los comentarios son usados para añadir notas explicativas o prevenir que el navegador interprete partes de la hoja de estilos.

Los comentarios se pueden colocar en cualquier espacio en blanco que se permita.

JS es tan permisivo con los espacios y comentarios que podemos insertar que puede ser una ventaja o desventaja para seguir el código:

```
// Comentario línea

/* 
  Comentario
  multilínea
*/

var arreglo = [
	//El primer elemento de mi arreglo
	//es un dato de tipo String
	//que hace referencia 
	//al nombre de una persona
	"Penélope",

	//El segundo elemento 
	//es un objeto que 
	//contiene los datos completos
	{
		nombre: "Penélope",
		apellido: "Herrera",
		getNombreCompleto: function(){
			return this.nombre + " " + this.apellido;
		}
	},

true, function() { console.log( this ); }];
```

Como podemos observar el archivo ha crecido por los comentarios y espaciado insertado, además de que cualquiera que visite nuestra web puede visualizar los comentarios y saber cómo funciona mi sitio, lo ideal es que cuando subamos los archivos a producción quitemos los comentarios y comprimamos el archivo.

### Programas para comprimir nuestro código

[compressor](https://htmlcompressor.com/compressor/)
[smaller](http://25.io/smaller/)

## Palabras reservadas de JavaScript

La siguiente es una lista de las palabras reservadas de JS:

abstract, boolean, break, byte, case, catch, char, class, const, continue, debugger, default, delete, do, double, else, enum, export, extends, false, final, finally, float, for, function, goto, if, implements, import, in, instanceof, int, interface, long, native, new, null, package, private, protected, public, return, short, static, super, switch, synchronized, this, throw, throws, transient, true, try, typeof, var, void, volatile, while, with

## Manejo de errores en JavaScript

La declaración `try...catch` señala un bloque de instrucciones a intentar (try), y especifica una respuesta si se produce una excepción (catch).

La declaración try consiste en un bloque try que contiene una o más sentencias (se debe usar siempre {} incluso para una sola sentencia) y al menos una cláusula catch o una cláusula finally, o bien ambas. Esto nos da tres formas posibles para la declaración try:

1. try...catch
2. try...finally
3. try...catch...finally

Con JS es complicado que algo nos dé un error pero hay algunas causas por ejemplo:

```
console.log( a );
console.log("Continua la ejecución...");

//output
Uncaught ReferenceError: a is not defined
```

En este ejemplo se encuentra un error y la ejecución del programa se detiene, para hacer que la ejecución de nuestro programa continue se usa el `try`:

```
try {
	console.log( a );
}catch(error) {
  console.error(error);
}
console.log("Continua la ejecución...");

//output
ReferenceError: a is not defined
Continua la ejecución...
```

Hay otros casos que producen errores:

```
try {
  nonExistentFunction();
}
catch(error) {
  console.error(error);
  // expected output: ReferenceError: nonExistentFunction is not defined
  // Note - error messages will vary depending on browser
}
console.log("Continua la ejecución...");

//output
ReferenceError: nonExistentFunction is not defined
Continua la ejecución...
```

### throw

Lanza una excepción definida por el usuario.

```
function dividir(dividendo, divisor){
	try {
		if(divisor===0)
			throw "Error: Imposible dividir entre 0."
	}catch(error) {
  		console.error(error);
	}finally{
		console.log("División finalizada...");
	}
}
var cociente = dividir(100, 0);
console.log("Continua la ejecución...");

//output
Error: Imposible dividir entre 0.
División finalizada...
Continua la ejecución...
```

Existe una manera más elaborada de crear nuestros errores para mostrar información sobre los mismos y nos ayuda a resolverlos:

```
function dividir(dividendo, divisor){
	try {
		if(divisor===0)
			throw new Error("Error: Imposible dividir entre 0.")
	}catch(error) {
  		console.error(error);
  		console.error(error.message);
	}finally{
		console.log("División finalizada...");
	}
}
var cociente = dividir(100, 0);
console.log("Continua la ejecución...");

//output
Error: Error: Imposible dividir entre 0.
    at dividir (app.js:4)
    at app.js:12
Error: Imposible dividir entre 0.
División finalizada...
Continua la ejecución..
```

En throw podemos mandar un objeto:

```
function dividir(dividendo, divisor){
	try {
		if(divisor===0)
			throw {
				codeError: 1,
				tipoError: "Error matématico",
				descripcion: "Se intenta dividir entre cero"
			}
	}catch(error) {
  	console.error(error);
  	console.error(error.codeError);
  	console.error(error.tipoError);
  	console.error(error.descripcion);
	}finally{
		console.log("División finalizada...");
	}
}
var cociente = dividir(100, 0);
console.log("Continua la ejecución...");

//output
{codeError: 1, tipoError: "Error matématico", descripcion: "Se intenta dividir entre cero"}
1
Error matématico
Se intenta dividir entre cero
División finalizada...
Continua la ejecución...
```

En el throw también podemos mandar una función:

```
function dividir(dividendo, divisor){
	try {
		if(divisor===0)
			throw function(){
				      console.error("Se intenta dividir entre cero");				
				    }
	}catch(error) {
  	error()
	}finally{
		console.log("División finalizada...");
	}
}
var cociente = dividir(100, 0);
console.log("Continua la ejecución...");

//output
Se intenta dividir entre cero
División finalizada...
Continua la ejecución...
```

Tener precaución si colocamos un throw al inicio del código porque detiene la ejecución de ese archivo .js

Podríamos almacenar nuestros errores en una BD para poder hacer un seguimiento de los mismos:

```
function registrarError(error){
	var fecha = new Date();
	console.log("Se registro un error del tipo " + error + " a las: " + fecha );
	//Esto se almacenaría en la BD
}

function dividir(dividendo, divisor){
	try {
		if(divisor===0)
			throw 1
	}catch(error) {
  		registrarError(error);
	}finally{
		console.log("División finalizada...");
	}
}
var cociente = dividir(100, 0);
console.log("Continua la ejecución...");

//output
Se registro un error del tipo 1 a las: Mon Aug 05 2019 18:05:48 GMT+0200 (hora de verano de Europa central)
División finalizada...
Continua la ejecución...
```

## Cookies - Instalación de node.js en Mac OSX

:+1:

## Cookies - Instalación de node.js en Windows

[node](https://nodejs.org/es/)

[http-server](https://www.npmjs.com/package/http-server)

## escape, unescape y cookies

### Cookies

Las cookies es información que se puede almacenar en la máquina del cliente.

Para ver las cookies en el navegador Chrome:

1. Abre Chrome en tu ordenador.
2. Arriba a la derecha, haz clic en Más Configuración.
3. Abajo, haz clic en Configuración avanzada.
4. En "Privacidad y seguridad", haz clic en Configuración del sitio web.
5. Haz clic en Cookies Ver todas las cookies y datos de sitios web.

Un ejemplo sencillo para crear las cookies es el siguiente:

```
document.cookie ="nombre=Penélope";
document.cookie ="apellido=De la Rosa";

var cookies = document.cookie;
console.log( cookies );

nombre=Penélope; apellido=De la Rosa
```

### escape()

La función obsoleta escape() crea una nueva cadena de caracteres en los que ciertos caracteres han sido sustituidos por una secuencia hexadecimal de escape.

La función escape es una propiedad del objeto global. Los caracteres especiales son codificados a excepción de: @*_+-./

La forma hexadecimal de los caracteres cuyo valor es 0xFF o menor, es una secuencia de escape de dos dígitos: %xx. Para caracteres un valor superior, se usa el formato de cuatro dígitos: %uxxxx.

```
escape('abc123');     // "abc123"
escape('äöü');        // "%E4%F6%FC"
escape('ć');          // "%u0107"

// caracteres especiales
escape('@*_+-./');    // "@*_+-./"
```

### unescape()

La función deprecada unescape() calcula un nuevo string  en el cual secuencia de valores hexadecimales son reemplazados con el carácter que representa. La secuencia de cálculo debería ser introducida por una función como escape. Porque unescape está deprecada, usar decodeURI or decodeURIComponent.

```
unescape("abc123");     // "abc123"
unescape("%E4%F6%FC");  // "äöü"
unescape("%u0107");     // "ć"
```

Todas las cookies que insertemos deben estar "escapadas".

```
function crearCookie( nombre, valor){
  valor = escape(valor);
  document.cookie = nombre + "=" + valor + ";";
}

crearCookie("nombre","Penélope");
crearCookie("apellido","De la Rosa");

var cookies = document.cookie;
console.log( cookies );

//output
nombre=Penélope; apellido=De la Rosa; 
apellidonombreDe%20la%20Rosa
```

### expires

Nos permite indicar la fecha de expiración de una fecha. Por default la cookie caduca al finalizar la sesión de navegación.

```
function crearCookie( nombre, valor){
  valor = escape(valor);
  var fechaExpiracion = new Date();
  fechaExpiracion.setMonth( fechaExpiracion.getMonth() + 1 );
 
  document.cookie = nombre + "=" + valor + ";expires=" + fechaExpiracion.toUTCString() + ";";
}

crearCookie("nombre","Penélope");
crearCookie("apellido","De la Rosa");

var cookies = document.cookie;
console.log( cookies );

//output
nombre=Penélope; apellido=De%20la%20Rosa
```

Si revisamos en las [cookies del navegador](chrome://settings/cookies/detail?site=localhost) nos indicara:

```
Caduca
viernes, 6 de septiembre de 2019, 10:22:14
```

### Borrar cookies.

Podríamos eliminar una cookie asignándole una fecha anterior a hoy:

```
function borrarCookie( nombre ){
  var fechaExpiracion = new Date();
  fechaExpiracion.setMonth( fechaExpiracion.getMonth() - 1 );
 
  document.cookie = nombre + "=X;expires=" + fechaExpiracion.toUTCString() + ";";
}

//crearCookie("nombre","Penélope");
//crearCookie("apellido","De la Rosa");

borrarCookie("nombre","Penélope");

var cookies = document.cookie;
console.log( cookies );

//output
apellido=De%20la%20Rosa
```

En el código solo hemos "borrado" la cookie del nombre, por eso el apellido sigue apareciendo.

### Recuperar una cookie.

Veamos un ejemplo de una función para recuperar los valores de las cookies:

```
function getCookie( nombre ){
  var cookies = document.cookie;
  var cookiesArreglo = cookies.split("; ");

  for( var i=0; i < cookiesArreglo.length; i++ ){
    //Separo nombre/valor y se mete en un array
    //nombre=penélope => [nombre,penélope]
    var parCookie = cookiesArreglo[i].split("=");
    //y lo meto en el array (aquí no sirve da nada pero es interesante ver la transformación)
    cookiesArreglo[i] = parCookie;

    if( parCookie[0] === nombre ){
      return unescape( parCookie[1] );
    }
  }
  return undefined;
}

console.log(getCookie("apellido"));
console.log(getCookie("nombre"));

//output
De la Rosa
Penélope
```

## Funciones especiales: Call(), Apply() y Bind()

Todas las funciones declaradas en JS tienen 3 métodos que se encuentran en el prototype, llamados `call(), apply() y bind()`.

Veamos el siguiente ejemplo:

```
var carro = {
  color: "Blanco",
  marca: "Mazda",
  imprimir:function(){
    //this hace referencia al objeto carro
    var salida = this.marca + " - " + this.color;
    return salida;
  }
}

console.log( carro.imprimir() );

var logCarro = function( arg1, arg2 ){
  console.log("Carro: ", this.imprimir());
}

logCarro();

//output
Mazda - Blanco
app.js:14 Uncaught TypeError: this.imprimir is not a function
    at logCarro (app.js:14)
    at app.js:17
```

En el código se está tratando de ejecutar `this.imprimir()` pero esto hace referencia a una función global que no existe y por eso nos indica el error `Uncaught TypeError: this.imprimir is not a function`.

### bind()

El método `bind()` crea una nueva función que, cuando se llama establece su `this`, pasándolo como parámetro.

El método `bind()` no invoca la función solo "settea" el nuevo objeto en `this`.

Vamos a usar el método `bind()` con el código anterior para evitar el error.

```
var carro = {
  color: "Blanco",
  marca: "Mazda",
  imprimir:function(){
    //this hace referencia al objeto carro
    var salida = this.marca + " - " + this.color;
    return salida;
  }
}

console.log( carro.imprimir() );

var logCarro = function(caracteristica1, caracteristica2 ){
  console.log("Carro: ", this.imprimir());
  console.log("Características: ", caracteristica1, caracteristica2 );
}

var logDatosCarro = logCarro.bind( carro );

logDatosCarro("Rápido", "Económico");

//output
Mazda - Blanco
app.js:14 Carro:  Mazda - Blanco
Características:  Rápido Económico
```

Estamos asignando otro `this` y mandando argumentos, en dos pasos separados.

### call()

El método `call()` invoca a una función pasándole como primer argumento el valor que tomara el  `this` seguido de los demás argumentos de la función.

```
var carro = {
  color: "Blanco",
  marca: "Mazda",
  imprimir:function(){
    //this hace referencia al objeto carro
    var salida = this.marca + " - " + this.color;
    return salida;
  }
}

console.log( carro.imprimir() );

var logCarro = function(caracteristica1, caracteristica2 ){
  console.log("Carro: ", this.imprimir());
  console.log("Características: ", caracteristica1, caracteristica2 );
}

var logDatosCarro = logCarro.bind( carro );
logDatosCarro("Rápido", "Económico");

logCarro.call(carro, "Rápido", "Económico" );

//output
Mazda - Blanco
Carro:  Mazda - Blanco
Características:  Rápido Económico
Carro:  Mazda - Blanco
Características:  Rápido Económico
```

### apply()

El método `apply()` invoca a una función pasándole como primer argumento el valor que tomara el  `this` seguido de los demás argumentos que se proporcionan como un array.

```
//output
Mazda - Blanco
Mazda - Blanco
Características:  Rápido Económico
Carro:  Mazda - Blanco
Características:  Rápido Económico
Carro:  Mazda - Blanco
Características:  Rápido Económico
```

Todo esto nos sirve para lo que se conoce como **Funciones Prestadas**, vea el siguiente ejemplo:

```
var carro = {
  color: "Blanco",
  marca: "Mazda",
  imprimir:function(){
    //this hace referencia al objeto carro
    var salida = this.marca + " - " + this.color;
    return salida;
  }
}

var carro2 = {
  color: "Rojo",
  marca: "Toyota"
}

console.log( carro.imprimir.call(carro2));

//output
Toyota -Rojo
``` 

## IF... ELSE....

### if-else

La instrucción if ejecuta una instrucción si una condición específica es verdadera. Si la condición es falsa, se puede ejecutar otra declaración.

### ? :

Operador ternario, nos permite tener una especie de if simplificado.

### ||

Operador OR selecciona el primer dato diferente de null y undefined, si solo estan estos dos valores retorna undefined.

Ejemplo:

```
var a = 10;
var b = 20;
var x = undefined;
var c = 0;

console.log("a=" + a, "b="+b);

//Uso de if-else
if (a > b){
  c = a;
}else{
  c = b
}
console.log("Uso if; mayor = " + c);


//Uso operador terciario
c = ( a > b ) ? a : b;
console.log("Uso operador ternario; mayor = " + c);

c = ( a > b ) ? function(){
  console.log("Ternario con funciones: a > b ");
  return a;
}() : function(){
  console.log("Ternario con funciones: a < b ");
  return b;
}();

console.log("Ternario con funciones: " + c);

//Uso operador ||
var d = x || a;
console.log("Operador || " + d); 

function getNombre( nombre, apellido ){
  var nom = nombre || apellido || "<sin datos>";
  console.log("Función || " + nom );
}

getNombre();

//output
a=10 b=20
Uso if; mayor = 20
Uso operador ternario; mayor = 20
Ternario con funciones: a < b 
Ternario con funciones: 20
Operador || 10
Función || <sin datos>
```

## Switch... condicional múltiple

Una instrucción `switch` permite que un programa evalúe una expresión e intente hacer coincidir el valor de la expresión con una etiqueta de caso. Si se encuentra una coincidencia, el programa ejecuta la declaración asociada.

```
var mes = 8;

switch( mes ){
  case 1:
    console.log("Enero");
    break;
  case 2:
    console.log("Febrero");
    break;
  case 3:
    console.log("Marzo");
    break;
  case 8:
    console.log("Agosto");
    break;
  default:
    console.log("Cualquier otro mes");
}

var hoy = new Date();
mes = hoy.getMonth();

switch( mes ){
  case (mes <= 4):
    console.log("1er Cuatrimestre");
    break;
  case (mes <= 8):
    console.log("2do Cuatrimestre");
    break;
  default:
    console.log("3er Cuatrimestre");
}

//output
Agosto
3er Cuatrimestre
```

##JSON y breve historia

Antes de existir JSON los datos se transferían en formato XML, pero muchas veces las etiquetas ocupaban más peso que los datos. La alternativa es JSON que es un formato de dato más condensado, un buen ejemplo seria ver un archivo en XML y otro en JSON.

```
<employees>
  <employee>
    <firstName>John</firstName> <lastName>Doe</lastName>
  </employee>
  <employee>
    <firstName>Anna</firstName> <lastName>Smith</lastName>
  </employee>
  <employee>
    <firstName>Peter</firstName> <lastName>Jones</lastName>
  </employee>
</employees>

{"employees":[
  { "firstName":"John", "lastName":"Doe" },
  { "firstName":"Anna", "lastName":"Smith" },
  { "firstName":"Peter", "lastName":"Jones" }
]}
```

Como se puede apreciar la notación JSON ocupa menos espacio que la notación XML, algo importante para la transferencia de datos.

La notación JSON es muy similar a la notación de los objetos de JS, veamos un ejemplo:

### Transformar un ObjetoJS a JSON

Use `JSON.stringify`

```
objetoJS = {
   nombre:"Penélope",
   edad: 30
};

console.log(objetoJS);

//Parseamos el objetoJS a un String JSON
var jsonString = JSON.stringify( objetoJS );
console.log( jsonString );

//output
{nombre: "Penélope", edad: 30}
{"nombre":"Penélope","edad":30}
```

Note la diferencia entre el objeto JS y el JSON solo son las comillas en los nombres de las propiedades.

Tenemos una página para verificar que un JSON escrito está bien generado:

[json.parser.online](http://json.parser.online.fr/)

### Transformar un JSON a un ObjetoJS

Use `JSON.parse`

```
objetoJS = {
  nombre:"Penélope",
  edad: 30
};

console.log(objetoJS);

//Parseamos el objetoJS a un String JSON
var jsonString = JSON.stringify( objetoJS );
console.log( jsonString );

//Parsear desde un JSON a un objetoJS
var objetoDesdeJSON = JSON.parse( jsonString );
console.log( objetoDesdeJSON );

console.log( objetoDesdeJSON.nombre );
console.log( objetoDesdeJSON.edad );
```

Nuestro objeto como ya sabemos puede tener funciones, pero que pasa con ellas all transformarlas a JSON (no tiene ninguna lógica).

```
objetoJS = {
  nombre:"Penélope",
  edad: 30,
  imprimir: function(){
    console.log( "Nombre: " +  this.nombre + " Edad: " + this.edad);
  }
};

console.log(objetoJS);

//Parseamos el objetoJS a un String JSON
var jsonString = JSON.stringify( objetoJS );
console.log( jsonString );

//Parsear desde un JSON a un objetoJS
var objetoDesdeJSON = JSON.parse( jsonString );
console.log( objetoDesdeJSON );

console.log( objetoDesdeJSON.nombre );
console.log( objetoDesdeJSON.edad );

//output
{nombre: "Penélope", edad: 30, imprimir: ƒ}
{"nombre":"Penélope","edad":30}
{nombre: "Penélope", edad: 30}
Penélope
30
```

Nótese que la función del objeto se ha perdido al hacer el parseo a JSON ya que le es imposible representar eso en un String, y ya al recuperar el objetoDesdeJSON ni rastro de la función. Si definiéramos la función imprimir en los prototipos tal vez ayudaría a no confundir cuando se tenga objetos con funciones que se deban parsear a JSON.
