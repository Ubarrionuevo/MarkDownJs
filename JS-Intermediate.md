# Javascript - Intermediate - Some concept that i dont remember

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

# Objetos

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

# Arrays (Comming soon)

# OOP (Comming soon)

# Expresiones regulares ?
