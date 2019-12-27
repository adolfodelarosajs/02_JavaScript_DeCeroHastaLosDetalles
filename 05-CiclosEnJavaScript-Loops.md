# Ciclos en JavaScript: Loops

## Ciclo While y Do While

### while

Crea un bucle que ejecuta una sentencia especificada mientras cierta condición se evalúe como verdadera. Dicha condición es evaluada antes de ejecutar la sentencia

### do...while

La sentencia `do...while` crea un bucle que ejecuta una sentencia especificada, hasta que la condición de comprobación se evalúa como falsa. La condición se evalúa después de ejecutar la sentencia, dando como resultado que la sentencia especificada se ejecute al menos una vez.

### break y continue

`break`: interrumpe la ejecuión de un ciclo.
`continue`: se salta a la siguiente interacción del número.

Ejemplo while

```
function imprimirDias(dias){
  var dia = 0;
  while( dias <= 31 ){         
    dia++;
    if( dia == 13)
      continue;
    console.log(dia);
    if( dia == dias )
      break;
  }
}

var dia = 0;
var hoy = new Date();
var mes = hoy.getMonth()+1;
console.log("Mes: " + mes);
console.log("Días: ");

switch (mes) {
  case 1:
  case 3:
  case 5:
  case 7: 
  case 8:
  case 10:
  case 12: 
    imprimirDias(31);
    break;
  case 4:
  case 6:
  case 9:
  case 11:
    imprimirDias(30);
    break;
  case 2:
    imprimirDias(28);
    break;
    default: console.log("Otro caso...")
}
```

Ejemplo do...while

```
function imprimirDias(dias){
  var dia = 0;
  do{
    dia++;
    if( dia == 13)
      continue;
     console.log(dia);
     if( dia == dias )
       break;
  }while(dias <= 31)
}

var dia = 0;
var hoy = new Date();
var mes = hoy.getMonth()+1;
console.log("Mes: " + mes);
console.log("Días: ");

switch (mes) {
  case 1:
  case 3:
  case 5:
  case 7: 
  case 8:
  case 10:
  case 12: 
    imprimirDias(31);
    break;
  case 4:
  case 6:
  case 9:
  case 11:
    imprimirDias(30);
    break;
  case 2:
    imprimirDias(28);
    break;
  default: console.log("Otro caso...")
}
```

## Ciclo For y For in - Reflejo

### for

La instrucción for crea un bucle que consta de tres expresiones opcionales, encerradas entre paréntesis y separadas por punto y coma, seguidas de una instrucción (generalmente una instrucción de bloque) que se ejecutará en el bucle.

```
var str = "";

for (var i = 0; i < 9; i++) {
  str = str + i;
}

console.log(str);
// expected output: "012345678"
```

### for in

La instrucción `for... in` itera sobre todas las propiedades enumerables no simbólicas de un objeto.

```
var Persona = function(){
  this.nombre = "Penélope";
  this.apellido = "Cruz";
  this.edad = "30";
}

var persona = new Persona();

for ( propiedad in persona ){
  console.log( propiedad );
}

//output
nombre
apellido
edad
```

Si queremos sacar los valores de la propiedad usamos la notación de corchetes:

```
for ( propiedad in persona ){
  console.log( propiedad, " : ", persona[propiedad] );
}

//output
nombre  :  Penélope
apellido  :  Cruz
edad  :  30
```

Vamos a suponer que añadimos la propiedad dirección en el prototipo de Persona:

```
var Persona = function(){
  this.nombre = "Penélope";
  this.apellido = "Cruz";
  this.edad = "30";
}

var persona = new Persona();

Persona.prototype.direccion = " Madrid, España."

for ( propiedad in persona ){
  console.log( propiedad, " : ", persona[propiedad] );
}

//output
nombre  :  Penélope
apellido  :  Cruz
edad  :  30
direccion  :   Madrid, España.
```

La propiedad dirección se imprimió en el ciclo a pesar de estar definida en el prototipo.

Existe una manera de saber si una propiedad es propia o no, es decir si se definió en el prototipo se dice que no es propia, para lo cual usamos el método `hasOwnProperty()`.

```
var Persona = function(){
  this.nombre = "Penélope";
  this.apellido = "Cruz";
  this.edad = "30";
}

var persona = new Persona();

Persona.prototype.direccion = " Madrid, España."

for ( propiedad in persona ){
  console.log( propiedad, " : ", persona.hasOwnProperty( propiedad ) );
}

//output
nombre  :  true
apellido  :  true
edad  :  true
direccion  :  false
```

Esta habilidad de que un objetos se pueda conocer a si mismo se conoce como Reflejo (Reflexion)

Vamos a ver el siguiente ejemplo del uso del `for...in`

```
for (num in [100,200,300,400,500]){
  console.log( num );
}

//output
0
1
2
3
4
```

Si quisiera imprimir los valores del arreglo usaría el método `foreach` de los arrays:

```
[100,200,300,400,500].forEach( function( num ) {
  console.log( num );
});

//output
100
200
300
400
500
```

num no toma el valor del índice si no el elemento del array.

```
var string1 = "";
var object1 = {a: 1, b: 2, c: 3};

for (var property1 in object1) {
  string1 += object1[property1];
}

console.log(string1);
// expected output: "123"
```

## Rotulando los ciclos

El rotular los ciclos nos permite indicar a que ciclo debe retornar un `continue` o un `break`:

```
for_pricipal:
for( var i = 1; i<=5; i++ ){
  console.log("i: " + i);

  for_secundario:
  for( var j= 1; j<=5; j++ ){
    console.log("j: " + j);
    if (i==3){
      break for_pricipal;
    }   

    for( var k= 1; k<=5; k++ ){
      console.log("k: " + k);
      if ( k==1){
        continue for_pricipal;
      }
    }
  }
}

//output
i: 1
j: 1
k: 1
i: 2
j: 1
k: 1
i: 3
j: 1
```

## Funciones de tiempo en JavaScript

JS tiene dos funciones para manipular el tiempo:

Una es para ejecutar un código cuando pasa determinada cantidad de segundos.

```
setTimeout( function(){
  console.log("Este mensaje se imprime cuando han pasado 2 segundos");
}, 2000);

//output
Este mensaje se imprime cuando han pasado 2 segundos
```

Otra es cuando queremos que un código se repita X cantidad de veces en X cantidad de segundos.

```
var segundos = 0;

setInterval( function(){
  segundos++;
  console.log("Segundo: " + segundos);
}, 1000);

//output
Segundo: 1
Segundo: 2
Segundo: 3
Segundo: 4
Segundo: 5
```

Pero esto lo haría infinitamente.

Para limitar el número de ejecuciones:

```
var segundos = 0;

var intervalo = setInterval( function(){
  segundos++;
  console.log("Segundo: " + segundos);
  if(segundos === 3 ){
    clearInterval( intervalo );
  }
}, 1000);
```

Vamos a ver otro ejemplo:

```
var persona = {
  nombre: "Penélope",
  edad: 30,
  imprimir: function(){
    setTimeout( function() {
      console.log( this.nombre, this.edad);
    }, 1000);
  }
}

persona.imprimir();

//output
undefined undefined
```

Nos está regresando `undefined undefined` el programa es parecido a anteriores programas pero con la excepción de que dentro de la funciones estamos metiendo otra función y por esto this ya a punta al objeto global, por eso no encuentra los datos.

Ya habíamos visto la solución:

```
var persona = {
  nombre: "Penélope",
  edad: 30,
  imprimir: function(){
    var self = this;
    setTimeout( function() {
      console.log( self.nombre, self.edad);
    }, 1000);
  }
}

persona.imprimir();

//output después de un segundo
Penélope 30
```
