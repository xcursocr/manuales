
# JavaScript Tutorial Completo

## 1. Introducción a JavaScript

JavaScript es un lenguaje de programación de alto nivel, interpretado y orientado a objetos. Se utiliza principalmente para crear interactividad en páginas web.

### ¿Qué puedes hacer con JavaScript?
- Manipulación de la estructura de la página (DOM).
- Validación de formularios.
- Interactividad dinámica, como animaciones y respuestas a las acciones del usuario.
- Desarrollo de aplicaciones web del lado del servidor (Node.js).

---

## 2. Sintaxis Básica

### 2.1 Variables

En JavaScript, puedes declarar variables de tres maneras principales:

```javascript
let x = 10; // Puede ser reasignada
const y = 20; // No puede ser reasignada
var z = 30; // En desuso, pero aún válido
```

### 2.2 Tipos de Datos

JavaScript tiene los siguientes tipos de datos:

- **Primitivos**: `string`, `number`, `boolean`, `undefined`, `null`, `symbol`, `bigint`.
- **Objetos**: Objetos literales, arreglos, funciones, entre otros.

Ejemplo:

```javascript
let nombre = "Juan"; // string
let edad = 30; // number
let esAdulto = true; // boolean
let usuario = { nombre: "Juan", edad: 30 }; // objeto
```

---

## 3. Operadores

### 3.1 Operadores Aritméticos

```javascript
let a = 10;
let b = 5;

console.log(a + b); // Suma
console.log(a - b); // Resta
console.log(a * b); // Multiplicación
console.log(a / b); // División
console.log(a % b); // Módulo
console.log(a ** b); // Exponente
```

### 3.2 Operadores de Comparación

```javascript
console.log(a == b); // Igualdad
console.log(a === b); // Igualdad estricta
console.log(a != b); // Desigualdad
console.log(a !== b); // Desigualdad estricta
console.log(a > b); // Mayor que
console.log(a < b); // Menor que
console.log(a >= b); // Mayor o igual que
console.log(a <= b); // Menor o igual que
```

---

## 4. Funciones

### 4.1 Declaración de Funciones

```javascript
function saludar(nombre) {
    return "Hola, " + nombre;
}

console.log(saludar("Juan")); // "Hola, Juan"
```

### 4.2 Funciones Anónimas y Funciones Flecha

```javascript
const saludar = (nombre) => "Hola, " + nombre;

console.log(saludar("Ana")); // "Hola, Ana"
```

---

## 5. Estructuras de Control

### 5.1 Condicionales

```javascript
let edad = 18;

if (edad >= 18) {
    console.log("Eres adulto.");
} else {
    console.log("Eres menor de edad.");
}
```

### 5.2 Bucles

#### Bucle `for`

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

#### Bucle `while`

```javascript
let i = 0;
while (i < 5) {
    console.log(i);
    i++;
}
```

#### Bucle `do...while`

```javascript
let i = 0;
do {
    console.log(i);
    i++;
} while (i < 5);
```

---

## 6. Arreglos

```javascript
let frutas = ["Manzana", "Banana", "Cereza"];

console.log(frutas[0]); // "Manzana"
frutas.push("Uva"); // Agregar al final
frutas.unshift("Fresa"); // Agregar al principio
frutas.pop(); // Eliminar el último elemento
```

---

## 7. Objetos

```javascript
let persona = {
    nombre: "Juan",
    edad: 30,
    saludar: function() {
        return "Hola, mi nombre es " + this.nombre;
    }
};

console.log(persona.saludar()); // "Hola, mi nombre es Juan"
```

---

## 8. Programación Asíncrona

### 8.1 Callbacks

```javascript
function saludo(nombre, callback) {
    console.log("Hola, " + nombre);
    callback();
}

saludo("Juan", () => console.log("¡Bienvenido!"));
```

### 8.2 Promesas

```javascript
let promesa = new Promise((resolve, reject) => {
    let exito = true;
    if (exito) {
        resolve("Operación exitosa");
    } else {
        reject("Operación fallida");
    }
});

promesa.then((mensaje) => console.log(mensaje))
       .catch((error) => console.log(error));
```

### 8.3 Async/Await

```javascript
async function obtenerDatos() {
    let datos = await fetch("https://jsonplaceholder.typicode.com/posts");
    let json = await datos.json();
    console.log(json);
}

obtenerDatos();
```

---

## 9. Manipulación del DOM

```javascript
// Obtener un elemento
let boton = document.getElementById("miBoton");

// Agregar un evento
boton.addEventListener("click", function() {
    alert("¡Haz hecho clic!");
});

// Cambiar el contenido
let titulo = document.querySelector("h1");
titulo.textContent = "Nuevo Título";
```

---

## 10. ES6+ Características Avanzadas

### 10.1 Desestructuración

```javascript
const persona = { nombre: "Juan", edad: 30 };
const { nombre, edad } = persona;

console.log(nombre); // "Juan"
console.log(edad); // 30
```

### 10.2 Operador Spread

```javascript
let arreglo1 = [1, 2, 3];
let arreglo2 = [...arreglo1, 4, 5];

console.log(arreglo2); // [1, 2, 3, 4, 5]
```

---

## 11. Módulos

### 11.1 Importar y Exportar

```javascript
// archivo.js
export const saludar = (nombre) => "Hola, " + nombre;

// otroArchivo.js
import { saludar } from './archivo.js';

console.log(saludar("Juan"));
```

---

## 12. Conclusión

JavaScript es un lenguaje poderoso y flexible, ampliamente utilizado en el desarrollo web tanto del lado del cliente como del servidor. Con las características de ES6 y más allá, su potencial se ha expandido enormemente.


```js
// JavaScript - Parte 2

// 13. Clases y Objetos en JavaScript

// En JavaScript, las clases son una forma de definir objetos y sus métodos. 
// Aunque JavaScript es un lenguaje basado en prototipos, las clases proporcionan una forma más sencilla de crear y gestionar objetos.

// 13.1 Definición de una Clase

class Persona {
    constructor(nombre, edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    saludar() {
        return `Hola, soy ${this.nombre} y tengo ${this.edad} años.`;
    }
}

const juan = new Persona("Juan", 30);
console.log(juan.saludar()); // "Hola, soy Juan y tengo 30 años."

// 13.2 Herencia

// Las clases pueden heredar propiedades y métodos de otras clases.

class Empleado extends Persona {
    constructor(nombre, edad, puesto) {
        super(nombre, edad); // Llamada al constructor de la clase base
        this.puesto = puesto;
    }

    mostrarPuesto() {
        return `${this.nombre} trabaja como ${this.puesto}.`;
    }
}

const maria = new Empleado("Maria", 25, "Desarrolladora");
console.log(maria.mostrarPuesto()); // "Maria trabaja como Desarrolladora"

// 14. Desestructuración Avanzada

// La desestructuración es una característica poderosa para extraer datos de arreglos u objetos de manera más limpia y fácil.

// 14.1 Desestructuración de Arreglos

const arreglo = [1, 2, 3, 4];

let [a, b] = arreglo;
console.log(a); // 1
console.log(b); // 2

// 14.2 Desestructuración de Objetos con Nuevos Nombres

const usuario = {
    nombre: "Juan",
    edad: 30,
    profesion: "Desarrollador"
};

const { nombre: usuarioNombre, edad: usuarioEdad } = usuario;

console.log(usuarioNombre); // "Juan"
console.log(usuarioEdad); // 30

// 15. Promesas y Manejo de Errores Avanzado

// Las promesas son fundamentales para manejar código asíncrono en JavaScript.

// 15.1 Cadena de Promesas

function obtenerDatos() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("Datos obtenidos con éxito");
        }, 2000);
    });
}

obtenerDatos()
    .then(res => {
        console.log(res); // "Datos obtenidos con éxito"
        return "Otro paso";
    })
    .then(res => console.log(res)) // "Otro paso"
    .catch(error => console.log("Error:", error));

// 15.2 Manejo de Errores con Async/Await

async function obtenerDatos() {
    try {
        let datos = await fetch("https://jsonplaceholder.typicode.com/posts");
        let json = await datos.json();
        return json;
    } catch (error) {
        console.log("Error:", error);
    }
}

obtenerDatos();

// 16. Módulos Avanzados y Exportación

// 16.1 Exportar Múltiples Elementos

// archivo.js
export const saludar = (nombre) => `Hola, ${nombre}`;
export const despedir = (nombre) => `Adiós, ${nombre}`;

// otroArchivo.js
import { saludar, despedir } from './archivo.js';

console.log(saludar("Juan")); // "Hola, Juan"
console.log(despedir("Juan")); // "Adiós, Juan"

// 16.2 Importación por Defecto

// archivo.js
const saludo = "Hola, mundo";
export default saludo;

// otroArchivo.js
import saludo from './archivo.js';

console.log(saludo); // "Hola, mundo"

// 17. Métodos Estáticos en Clases

// Los métodos estáticos se definen en una clase pero no se pueden invocar a través de una instancia de la clase, sino directamente desde la clase misma.

class MathHelper {
    static sumar(a, b) {
        return a + b;
    }
}

console.log(MathHelper.sumar(3, 4)); // 7

// 18. Funciones Generadoras

// Las funciones generadoras son aquellas que pueden pausar su ejecución y continuarla en otro momento, utilizando la palabra clave `yield`.

function* generador() {
    yield 1;
    yield 2;
    yield 3;
}

const gen = generador();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3

// 19. Set y Map en JavaScript

// 19.1 Set

// Un `Set` es una colección de valores únicos, es decir, no permite elementos duplicados.

let numeros = new Set([1, 2, 3, 3, 4]);
console.log(numeros); // Set {1, 2, 3, 4}

// 19.2 Map

// Un `Map` es una colección de pares clave-valor, donde las claves pueden ser de cualquier tipo.

let mapa = new Map();
mapa.set('nombre', 'Juan');
mapa.set('edad', 30);

console.log(mapa.get('nombre')); // "Juan"
console.log(mapa.get('edad')); // 30

// 20. Eventos y Propagación

// JavaScript ofrece un sistema de eventos para manejar interacciones con el usuario.

// 20.1 Manejo de Eventos

document.getElementById("miBoton").addEventListener("click", function() {
    alert("¡Botón clickeado!");
});

// 20.2 Propagación de Eventos

// La propagación de eventos se refiere a cómo los eventos viajan a través del DOM. 
// Pueden ocurrir en dos fases: la fase de captura (de arriba hacia abajo) y la fase de burbuja (de abajo hacia arriba).

document.getElementById("miBoton").addEventListener("click", function(event) {
    event.stopPropagation(); // Detiene la propagación del evento
    alert("Botón clickeado");
}, false);

// Conclusión Final

// JavaScript es un lenguaje increíblemente potente y versátil, que va mucho más allá de ser simplemente un lenguaje para interactividad en páginas web. 
// Con sus características más avanzadas, como las promesas, clases, módulos, y la programación asíncrona, es posible desarrollar aplicaciones completas tanto en el cliente como en el servidor.
// JavaScript - Parte 3

// 21. Manipulación del DOM

// El DOM (Document Object Model) es una interfaz de programación que permite acceder, modificar y manipular el contenido de una página web.

// 21.1 Acceder a Elementos del DOM

// Utilizando métodos como `getElementById`, `getElementsByClassName` o `querySelector`, podemos acceder a los elementos HTML.

const elemento = document.getElementById("miElemento");
console.log(elemento); // Accede al elemento con el id "miElemento"

// 21.2 Modificar Elementos del DOM

// Cambiar el contenido, los estilos o atributos de los elementos del DOM.

elemento.textContent = "Nuevo texto";
elemento.style.color = "red"; // Cambiar el color del texto

// 21.3 Crear Nuevos Elementos

// Crear elementos HTML dinámicamente utilizando JavaScript.

const nuevoElemento = document.createElement("div");
nuevoElemento.textContent = "Soy un nuevo elemento";
document.body.appendChild(nuevoElemento);

// 22. Funciones de Orden Superior

// Las funciones de orden superior son aquellas que aceptan otras funciones como argumentos o devuelven funciones como resultado.

// 22.1 `map()`, `filter()` y `reduce()`

// Ejemplo de `map()` que crea un nuevo arreglo con los resultados de aplicar una función a cada elemento de un arreglo.

const numeros = [1, 2, 3, 4];
const cuadrados = numeros.map(num => num * num);
console.log(cuadrados); // [1, 4, 9, 16]

// `filter()` crea un nuevo arreglo con los elementos que pasan una condición.

const mayoresQueDos = numeros.filter(num => num > 2);
console.log(mayoresQueDos); // [3, 4]

// `reduce()` aplica una función acumulativa a los elementos del arreglo.

const suma = numeros.reduce((acumulador, valor) => acumulador + valor, 0);
console.log(suma); // 10

// 23. Async/Await y Manejo de Errores

// `async/await` proporciona una forma más fácil de trabajar con código asíncrono que las promesas tradicionales.

// 23.1 Uso de `async/await`

// La palabra clave `async` indica que una función siempre devuelve una promesa. La palabra clave `await` se usa dentro de una función `async` para esperar que una promesa se resuelva.

async function obtenerDatos() {
    const respuesta = await fetch("https://jsonplaceholder.typicode.com/posts");
    const datos = await respuesta.json();
    return datos;
}

obtenerDatos().then(datos => console.log(datos));

// 23.2 Manejo de Errores con `try/catch`

// El bloque `try/catch` se usa para manejar errores que puedan ocurrir durante la ejecución de código asíncrono.

async function obtenerDatos() {
    try {
        const respuesta = await fetch("https://jsonplaceholder.typicode.com/posts");
        const datos = await respuesta.json();
        console.log(datos);
    } catch (error) {
        console.log("Error:", error);
    }
}

obtenerDatos();

// 24. Closures

// Un closure es una función que "recuerda" el entorno en el que fue creada, incluso después de que el entorno de ejecución haya terminado.

// 24.1 Ejemplo de Closure

function crearContador() {
    let contador = 0;
    return function() {
        contador++;
        return contador;
    };
}

const contador = crearContador();
console.log(contador()); // 1
console.log(contador()); // 2

// 25. Operadores en JavaScript

// Los operadores son símbolos que realizan operaciones sobre valores.

// 25.1 Operadores Aritméticos

// Los operadores aritméticos son utilizados para realizar operaciones matemáticas.

const suma = 5 + 3; // 8
const resta = 10 - 4; // 6
const multiplicacion = 6 * 2; // 12
const division = 8 / 2; // 4

// 25.2 Operadores Lógicos

// Los operadores lógicos se utilizan para combinar expresiones booleanas.

const verdadero = true;
const falso = false;

console.log(verdadero && falso); // false
console.log(verdadero || falso); // true
console.log(!verdadero); // false

// 25.3 Operadores de Comparación

// Los operadores de comparación se utilizan para comparar valores.

const esIgual = 5 == 5; // true
const esMayor = 10 > 5; // true
const esMenor = 3 < 5; // true

// 26. Debugeo y Herramientas de Desarrollo

// Las herramientas de desarrollo en los navegadores, como la consola y el depurador, son esenciales para depurar y entender el flujo de código.

// 26.1 `console.log()`

// `console.log()` es una forma básica de imprimir información para depurar el código.

console.log("Este es un mensaje de depuración");

// 26.2 `debugger`

// `debugger` es una instrucción que se puede utilizar para detener la ejecución del código y examinar el estado del programa.

function prueba() {
    debugger; // Detiene la ejecución aquí
    let a = 10;
    let b = 20;
    return a + b;
}

prueba();

// 27. Métodos de Arreglo Avanzados

// JavaScript proporciona varios métodos avanzados para trabajar con arreglos.

// 27.1 `find()` y `findIndex()`

// `find()` devuelve el primer elemento que cumple con una condición.

const arreglo = [1, 2, 3, 4, 5];
const encontrado = arreglo.find(num => num > 3);
console.log(encontrado); // 4

// `findIndex()` devuelve el índice del primer elemento que cumple con la condición.

const indice = arreglo.findIndex(num => num > 3);
console.log(indice); // 3

// 27.2 `some()` y `every()`

// `some()` verifica si al menos un elemento cumple con una condición.

const tieneMayorQueCinco = arreglo.some(num => num > 5);
console.log(tieneMayorQueCinco); // false

// `every()` verifica si todos los elementos cumplen con la condición.

const todosMenoresQueCinco = arreglo.every(num => num < 5);
console.log(todosMenoresQueCinco); // true

// 28. Web APIs en JavaScript

// JavaScript ofrece muchas APIs web integradas para interactuar con diferentes tecnologías web como el almacenamiento local, geolocalización, etc.

// 28.1 Local Storage

// `localStorage` permite almacenar datos en el navegador sin fecha de caducidad.

localStorage.setItem("nombre", "Juan");
console.log(localStorage.getItem("nombre")); // "Juan"

// 28.2 Geolocalización

// Podemos obtener la ubicación del usuario a través de la API de Geolocalización.

navigator.geolocation.getCurrentPosition(function(position) {
    console.log(position.coords.latitude);  // Latitud
    console.log(position.coords.longitude); // Longitud
});

