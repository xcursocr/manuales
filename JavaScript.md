
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
