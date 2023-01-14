# Javascript - Intermediate - Some concept that i dont remember

<br>
<br>

> ## Thinks that i dont know if are necesary in this moment

>  <li>Expresiones regulares ?</li>
> <li>Typescript</li>
> <li>WebPack</li>
> <li>Babel</li>

<br>
<br>
<br>

# Resources

> https://lenguajejs.com/

> https://es.javascript.info/callbacks

<br>
<br>
<br>

# Peticiones HTTP con Fetch

> https://www.freecodecamp.org/espanol/news/tutorial-de-fetch-api-en-javascript-con-ejemplos-de-js-fetch-post-y-header/ (mas sobre HTTP)

<br>
<br>
FETCH - Es una API con la cual podemos realizar peticiones HTTP de manera mas facil que con XMLHttpRequest

Podemos realizar peticiones de manera asincronica utilizando promesas.
<br>
<br>
<br>
![Fetch](/img/js.PNG)

<br>
<br>
Lo primero, y más habitual, suele ser indicar el método HTTP a realizar en la petición. Por defecto, se realizará un GET, pero podemos cambiarlos a HEAD, POST, PUT o cualquier otro tipo de método. En segundo lugar, podemos indicar objetos para enviar en el body de la petición, así como modificar las cabeceras en el campo headers:

```js
const options = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(jsonData),
};
```

Por último, el campo credentials permite modificar el modo en el que se realiza la petición. Por defecto, el valor omit hace que no se incluyan credenciales en la petición, pero es posible indicar los valores same-origin, que incluye las credenciales si estamos sobre el mismo dominio, o include que incluye las credenciales incluso en peticiones a otros dominios.
<br>
<br>

## Cabeceras

```js
const headers = new Headers();
headers.set("Content-Type", "application/json");
headers.set("Content-Encoding", "br");
```

Para ello, a parte del método .set() podemos utilizar varios otros para trabajar con cabeceras, comprobar su existencia, obtener o cambiar los valores o incluso eliminarlos:

![Response](/img/cabecera.PNG)

---

<br>
<br>

## RESPONSE

propiedades para la respuesta de la peticion

![Response](/img/Response.PNG)

Por otra parte, la instancia response también tiene algunos métodos interesantes, la mayoría de ellos para procesar mediante una promesa los datos recibidos y facilitar el trabajo con ellos:
<br>
<br>
![Procesamiento](/img/procesamiento.PNG)

<br>
<br>
<br>
<br>

```javascript
fetch("/robots.txt").then(function (response) {
  /** Código que procesa la respuesta **/
});
```

Al método .then() se le pasa una función callback donde su parámetro response es el objeto de respuesta de la petición que hemos realizado. En su interior realizaremos la lógica que queramos hacer con la respuesta a nuestra petición. A la función fetch(url, options) se le pasa por parámetro la url de la petición y, de forma opcional, un objeto options con opciones de la petición HTTP.

El parámetro opcional "options" , puede tener estas propiedades
<br>
<br>

## CORS

(comming son)
<br>
<br>

> https://lenguajejs.com/javascript/peticiones-http/cors/ > <br> <br> > <br> > <br>

# Async - Await

Una forma mas simple de utilizar funciones asincronicas , dejando de lado el encadenamiento de .then

<strong>
Al implemente la palabra async en una funcion lo que devuelvera es una promesa ,esto reemplazara el newPromise.
</strong>
<br>
<br>
Async == promise , la cual puede utilizarse junto con la palabra <strong>await</strong> , que basicamente es un stopper dentro de la funcion asincronica , para que esta permita que se continue con el flujo normal y que al final cuando se resuelva la promesa , activarse y dar el valor.

<br>
<br>

# Callbacks

Los callbacks (a veces denominados funciones de retrollamada o funciones callback) no son más que un tipo de funciones que se pasan por parámetro a otras funciones.

```javascript
//El setTime pide una funcion callback y el tiempo com parametros

setTimeout(function () {
  console.log("He ejecutado la función");
}, 2000);

//Ejemplo con una constante
const action = () => console.log("He ejecutado la función");
setTimeout(action, 2000);
```

<br>
<br>

# ASINCRONYC

La asincronia lo que hará es mover esa tarea (especifica que necesita una accion para continuar y que podria bloquear todo el programa) a una lista de tareas pendientes a las que irá «prestándole atención» a medida que lo necesite, pudiendo continuar y retomar el resto de tareas a continuación de la segunda.

Nos referimos a JS como un lenguaje no bloqueante gracias al asincronismo que lleva en su interior.

Ejemplos de asincronismo

<li>
Un fetch() a una URL para obtener un archivo .json.
</li>
<li>
Un new Audio() de una URL con un .mp3 al que se hace .play() para reproducirlo.
</li>
<li>
Una tarea programada con setTimeout() que se ejecutará en el futuro.
</li>
<li> Una comunicación desde Javascript a la API del sintetizador de voz del navegador.</li>
<li>
Una comunicación desde Javascript a la API de un sensor del smartphone.
</li>

<br>
<br>

# PROMISE

Una promesa es un objeto que representa un valor que puede que esté disponible «ahora», en un «futuro» o que «nunca» lo esté. Como no se sabe cuándo va a estar disponible, todas las operaciones dependientes de ese valor, tendrán que posponerse en el tiempo
<strong>(Solo puede haber un único resultado, o un error)</strong>
<br>
<br>

### Creation of Constructor Promise - Example simple

```javascript
let promise = new Promise(function (resolve, reject) {
  // la función se ejecuta automáticamente cuando se construye la promesa

  // después de 1 segundo, indica que la tarea está hecha con el resultado "hecho"
  setTimeout(() => resolve("hecho"), 1000);
});
```

### Creation of Constructor Promise - Example more structurate

```javascript
const promise = new Promise((resolve, reject) => {
  const number = Math.floor(Math.random() * 12);
  setTimeout(
    () => (number > 4 ? resolve(number) : reject(new Error("Menor a 4"))),
    2000
  );
});

promise
  .then((number) => console.log(number))
  .catch((error) => console.error(error));
```

### Chainning - Promses en cadena

```javascript
readFile("./texto.txt")
  .then(readFile)
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

### Como se consumen ?

<Ul>
<li>
.THEN() - <strong> Este es el mas importante</strong>: Es el que va a consumir la promesa recien llegada.
</li>
<br>
<br>
<li>
.CATCH() - Manejo de errores - Este metodo va a mostrar si hubo un error en el consumo de la promesa (status)
<br>
<br>

<strong>
(.catch(errorHandlingFunction)) como uso en el trabajo (analizar)
</strong>
<br>
<br>
</li>
<li>
.FINALLY() - Es el metodo que cierra por completo la promesa independientemente el estado en el cual llego (bueno o malo) , este no recibe parametros ni nada por el estilo , simplemente es un pasamanos al metodo catch que es el que realmente muestra un estado de la promesa.
</li>
</Ul>
<br>
<br>

---

# OBJETCS

Que es un objeto?

En Javascript, existe un tipo de dato llamado objeto . Una primera forma de verlo, es como una variable especial que puede contener más variables en su interior. De esta forma, tenemos la posibilidad de organizar múltiples variables de la misma temática en el interior de un objeto.

Forma en que se llamaban los objetos

```js
const objeto = new Object(); // Evitar esta sintaxis en Javascript (no se suele usar)
```

Forma mas optima

> Los literales de los objetos en Javascript son las llaves {}. Este ejemplo es equivalente al anterior, pero es más corto, rápido y cómodo, por lo que se aconseja declararlos siempre así:

```js
const objeto = {}; // Esto es un objeto vacío
```

## Metodos de un objeto

```js
const user = {
  name: "Manz",
  talk: function () {
    return "Hola";
  },
};

user.name; // Es una variable (propiedad), devuelve "Manz"
user.talk(); // Es una función (método), se ejecuta y devuelve "Hola"
```

## Metodos especificos que podemos utilizar dentro del objet

```js
const number = 42.5;
number.toString(); // Devuelve "42.5" (Método de variables de tipo Object)
number.toLocaleString(); // Devuelve "42,5" (Método de variables de tipo Object)
number.toFixed(3); // Devuelve "42.500" (Método de variables de tipo Number)
```

```js
const player = {
  name: "Manz", // Nombre del jugador
  life: 4, // Cantidad de vida actual
  totalLife: 6, // Máximo de vida posible
  toString: function () {
    return `${this.name} (${this.life}/${this.totalLife})`;
  },
};
//en este console estamos lamando al metodo toString indirectamente , ya que concatenamos un comentario mas un objeto , como no es de tipo string , se dispara el metodo anteriormente aplicado.
console.log("Mi jugador es " + player); // "Mi jugador es Manz (4/6)"
```

<br>
<br>
<br>

## Propiedades de un objeto

Podemos acceder a las propiedades del objeto de dos formas (corchetes o punto)

<strong>La notacion de puntos es la mas utilizada</strong>

```js
// Notación con puntos (preferida)
console.log(player.name); // Muestra "Manz"
console.log(player.life); // Muestra 99)
```

Menos utilizada

```js
// Notación con corchetes
console.log(player["name"]); // Muestra "Manz"
console.log(player["life"]); // Muestra 99
```

Podemos agregar propiedades al objeto aunque ya este creado , a trasves de la notacion de puntos

```js
const player = {};

player.name = "Manz";
player.life = 99;
player.power = 10;
```

## Iteradores de objetos (me sirve?)

## Destructuracion de objetos (me sirve?)

# OOP

Es un estilo de programación muy utilizado, donde creas y utilizas estructuras de datos de una forma muy similar a la vida real, lo que facilita considerablemente la forma de planificar y preparar el código de tus programas o aplicaciones.

<strong> Es una palabra clave que se utiliza dentro de una clase para hacer referencia al objeto instanciado , no a la clases (no confundir)</strong>

```js
class Animal {
  name; // Propiedad (variable de clase sin valor definido)

  constructor(name) {
    this.name = name; // Hacemos referencia a la propiedad name del objeto instanciado
  }
}
```

# ARRAYS

Manera ideal para javascript

```js
// Mediante literales (notación preferida)
const letters = ["a", "b", "c"]; // Array con 3 elementos
const letters = []; // Array vacío (0 elementos)
const letters = ["a", 5, true]; // Array mixto (String, Number, Boolean)
```

El operador [] no sólo nos permite obtener o acceder a un elemento del array, sino que también nos permite modificar un elemento específico del array, si utilizamos la asignación:

```js
const letters = ["a", "b", "c"];

letters[1] = "Z"; // Devuelve "Z" y modifica letters a ["a", "Z", "c"]
letters[3] = "D"; // Devuelve "D" y modifica letters a ["a", "Z", "c", "D"]
letters[5] = "A"; // Devuelve "A" y modifica letters a ["a", "Z", "c", "D", undefined, "A"]
```

Añadir un elemento o quitar

```js
const elements = ["a", "b", "c"]; // Array inicial

elements.push("d"); // Devuelve 4.   Ahora elements = ['a', 'b', 'c', 'd']
elements.pop(); // Devuelve 'd'. Ahora elements = ['a', 'b', 'c']

elements.unshift("Z"); // Devuelve 4.   Ahora elements = ['Z', 'a', 'b', 'c']
elements.shift(); // Devuelve 'Z'. Ahora elements = ['a', 'b', 'c']
```

<strong>.concat() - no es lo mismo que .push()</strong>

.contact() itera arrays pero repitiendolos
.push() itera un nuevo array al existente pero diferente al mismo
.push() inserta un array , en cambio .catch() inserta elementos.

```js
const firstPart = [1, 2, 3];
const secondPart = [4, 5, 6];

firstPart.concat(firstPart); // Devuelve [1, 2, 3, 1, 2, 3]
firstPart.concat(secondPart); // Devuelve [1, 2, 3, 4, 5, 6]

// Se pueden pasar elementos sueltos
firstPart.concat(4, 5, 6); // Devuelve [1, 2, 3, 4, 5, 6]

// Se pueden concatenar múltiples arrays e incluso mezclarlos con elementos sueltos
firstPart.concat(firstPart, secondPart, 7); // Devuelve [1, 2, 3, 1, 2, 3, 4, 5, 6, 7]
```

Reducir el tamaño de un array , muy sencilo

<strong>(variable.length = tamaño nuevo del array)</strong>

```js
// Mediante .length
const numbers = [1, 2, 3, 4, 5, 6, 7, 8];
numbers.length = 4;

numbers; // [1, 2, 3, 4], numbers cambia
```

Ordenamiento de arrays

![ordenamient](/img/arerat3.PNG)

Metodo .reverse

```js
const elements = ["A", "B", "C", "D", "E", "F"];

const reversedElements = elements.reverse();

reversedElements; // ["F", "E", "D", "C", "B", "A"]
elements; // ["F", "E", "D", "C", "B", "A"]
reversedElements === elements; // true
```

Metodo Sort

```js
const names = ["Alberto", "Zoe", "Ana", "Mauricio", "Bernardo"];

const sortedNames = names.sort();

sortedNames; // ["Alberto", "Ana", "Bernardo", "Mauricio", "Zoe"]
names; // ["Alberto", "Ana", "Bernardo", "Mauricio", "Zoe"]
sortedNames === names; // true
```

## Destructuring of Arrays (cooming son)

> https://lenguajejs.com/javascript/arrays/desestructuracion-arrays/

## Class

una clase sólo es una forma de organizar código de forma entendible con el objetivo de simplificar el funcionamiento de nuestro programa. Además, hay que tener en cuenta que las clases son «conceptos abstractos» de los que se pueden crear objetos de programación, cada uno con sus características concretas.

Las variables y constantes incluidas en una clase se denominan propiedades, y se utilizan para guardar información relacionada (se suele denominar estado). Por otro lado, las funciones incluidas en una clase se denominan métodos y se utilizan para realizar una acción relacionada con la clase
<br>
<br>
![Clases](/img/clase.PNG)
<br>
<br>

<strong> instanciar una clase, crear un objeto o crear una instancia a la acción de crear un nuevo objeto basado en una clase particular </strong>

Las clases deben siempre empezar en mayúsculas (nomenclatura llamada PascalCase)

```js
// Declaración de una clase (de momento, vacía)
class Animal {}

// Crear (instanciar) un objeto basada en una clase
const pato = new Animal();
```

```js
//Las propiedades a grandes rasgos son las variables de clases

//Los metodos a gradnes rasgos son las funcionesd entro de las clases
class Animal {
  // Propiedades
  name = "Garfield";
  type = "cat";

  // Métodos
  hablar() {
    return "Odio los lunes.";
  }
}
```

## ARRAY FUNCTIONS

Basicamente son metodos que tienen cualqueir variable de tipo ARRAY y que permite realizar una operacion particular con todos los elementos de dicho array

Al metodo se le pasa como parametro una funcion callback y parametros opcionales.

![arrayfunctions](/img/array%20functions.PNG)
![arrayfunctions](/img/array%20functions%202.PNG)

El mas importante , que se utiliza con frecuencia

### For Each

Basicamente es un metodo que te pide por parametro una accion , la cual la replicara en todos los elementos del array , especie de bucle comun.

<li>Primer parametro : pasa el elemento</li>
<li>Segundo Parametro : pasa la posicion del array</li>
<li>Tercer Parametro pasa el array en cuestion</li>

```js
const letters = ["a", "b", "c", "d"];

letters.forEach((element) => console.log(element)); // Devuelve 'a' / 'b' / 'c' / 'd'
letters.forEach((element, index) => console.log(element, index)); // Devuelve 'a' 0 / 'b' 1 / 'c' 2 / 'd' 3
letters.forEach((element, index, array) => console.log(array[0])); // Devuelve 'a' / 'a' / 'a' / 'a'
```

### Maps

Este metodo nos va a devolver un nuevo array donde cada uno de sus elementos sera lo que devuelva la funcion callback por cada uno de los elementos del array original

```js
const names = ["Ana", "Pablo", "Pedro", "Pancracio", "Heriberto"];
const nameSizes = names.map((name) => name.length);

nameSizes; // Devuelve [3, 5, 5, 9, 9]
```

Observa que el array devuelto por map() es nameSizes, y cada uno de los elementos que lo componen, es el número devuelto por el callback (name.length), que no es otra cosa sino el tamaño de cada .

### Filter

Nos permite filtrar los elementos de un array y devolver un nuevo array con solo los elementos que queramos.

```js
const names = ["Ana", "Pablo", "Pedro", "Pancracio", "Heriberto"];
const filteredNames = names.filter((name) => name.startsWith("P"));

filteredNames; // Devuelve ['Pablo', 'Pedro', 'Pancracio']
```

### Find / FindIndex

Uno devuelve el elemento (find()) , el otro devuelve la posicion del elemento en el array (findIndex())

```js
const names = ["Ana", "Pablo", "Pedro", "Pancracio", "Heriberto"];

names.find((name) => name.length == 5); // 'Pablo'
names.findIndex((name) => name.length == 5); // 1
```

### FindLastIndex / FindLast

Buscan elementos pero desde derecha a izquierda

```js
const names = ["Ana", "Pablo", "Pedro", "Pancracio", "Heriberto"];

names.findLast((name) => name.length == 5); // 'Pedro'
names.findLastIndex((name) => name.length == 5); // 2
```

### Reduce / ReduceRight

Basicamente estos metodos cuentan todos los elementos del array , los suma y devuelve un resultado final.

tiene como parameteros (first , second , iteration , array)

first contiene el valor del primer elemento , y second del segundo.

First es el acumulador que contiene lo que devolvio el callback en la iteracion anterior , mientras que second es el siguiente elemento del array

<br>
<br>

```js
const numbers = [95, 5, 25, 10, 25];
numbers.reduce((first, second) => {
  console.log(`F=${first} S=${second}`);
  return first + second;
});

// F=95  S=5    (1ª iteración: elemento 1: 95 + elemento 2: 5) = 100
// F=100 S=25   (2ª iteración: 100 + elemento 3: 25) = 125
// F=125 S=10   (3ª iteración: 125 + elemento 4: 10) = 135
// F=135 S=25   (4ª iteración: 135 + elemento 5: 25) = 160

// Finalmente, devuelve 160
```

## Propiedades Computadas

Son un tipo de propiedad que se declara como una funcion , y que se ejecuta cuando accedemos a la propiedad con dicho nombre-

### Getters

```js
class Personaje {
  name;
  energy;

  constructor(name, energy = 10) {
    this.name = name;
    this.energy = energy;
  }

  get status() {
    return "⭐".repeat(this.energy);
  }
}

const mario = new Personaje("Mario");
mario.energy; // 10
mario.status; // '⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐'
```

Observa que aunque la definimos como una función status(), luego accedemos a ella como una propiedad mario.status. Por eso se llama propiedad computada. <strong>La idea de este tipo de propiedades, es permitir pequeñas modificaciones sobre propiedades ya existentes (en nuestro caso, energy). En lugar de devolver el valor numérico, devolvemos el número de estrellas que representa la vida del personaje.
</strong>

### Setters

```js
class Personaje {
  name;
  energy;

  constructor(name, energy = 10) {
    this.name = name;
    this.energy = energy;
  }

  get status() {
    return "⭐".repeat(this.energy);
  }

  set status(stars) {
    this.energy = stars.length;
  }
}

const mario = new Personaje("Mario");
mario.energy; // 10
mario.status = "⭐⭐⭐";
mario.energy; // 3
mario.status; // '⭐⭐⭐'
```

Observa que ahora la "magia" está en el set status(stars). Se comporta como una función, y al asignar tres estrellas a mario.status, automágicamente se ha cambiado el valor de mario.energy. Estas propiedades computadas nos pueden venir muy bien cuando queramos modificar ligeramente ciertos elementos de una forma automática y organizada.

## Methods CLASS

## Herency CLASS

## Mixins

## Try..Catch

## This (mucho cuidado como se utiliza .this)

# CONSTRUCTUR , OPERADOR NEW

> https://es.javascript.info/

# ENCADENAMIENTO OPCIONAL ?.

> https://es.javascript.info/

---

# Destructuring

# SPREAD OPERATOR
