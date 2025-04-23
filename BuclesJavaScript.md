# 🔁 Tipos de Bucles en JavaScript (Node.js)
En JavaScript (y por ende en Node.js), existen varios tipos de bucles para recorrer datos o repetir acciones. Aquí te muestro los más usados con ejemplos comentados.
---


```js
# 💡 Útil cuando necesitas saber la posición (índice) exacta o recorrer un número específico de veces.
# Ideal para recorrer arreglos con control total del índice.

for (let i = 0; i < 5; i++) {
  console.log(`Iteración: ${i}`);
}

.

🔹 2. for...of
# Recorre los valores de un array o iterable. ¡Súper limpio y legible!

const frutas = ["manzana", "pera", "banana"];

for (const fruta of frutas) {
  console.log(`Me gusta la ${fruta}`);
}

🔹 3. for...in
# Recorre las claves de un objeto (o índices de un array, aunque no es recomendable para eso).
# ⚠️ Evita usar for...in con arrays, ya que puede recorrer propiedades heredadas.

const usuario = {
  nombre: "Luis",
  edad: 25,
  activo: true,
};

for (const clave in usuario) {
  console.log(`${clave}: ${usuario[clave]}`);
}


🔹 4. while
# Repite mientras una condición sea verdadera. Ideal cuando no sabes cuántas veces ejecutarás algo.
# 💡 Úsalo cuando la condición depende de algo fuera del bucle.

let contador = 0;

while (contador < 3) {
  console.log(`Contador: ${contador}`);
  contador++;
}

🔹 5. do...while
# Igual que while, pero garantiza al menos una ejecución.
# 💡 Útil si necesitas ejecutar el bloque al menos una vez sí o sí.

let numero = 0;

do {
  console.log(`Número actual: ${numero}`);
  numero++;
} while (numero < 3);

🔹 6. .forEach() (método de arrays)
# Método moderno y limpio para recorrer arrays.
# 💡 No se puede usar break o return como en un bucle tradicional.

const numeros = [10, 20, 30];

numeros.forEach((num, index) => {
  console.log(`Índice ${index}: valor ${num}`);
});

```

🧠 Cuándo Usar Cada Uno

Tipo	Úsalo cuando...
for	Necesitas índice o control preciso
for...of	Quieres recorrer arrays de forma limpia
for...in	Recorres propiedades de objetos
while	La condición depende de un evento externo
do...while	Necesitas ejecutar al menos una vez
.forEach()	Quieres recorrer arrays sin preocuparte de la lógica del bucle


✅ Buenas Prácticas
Usa for...of para arrays simples.

No uses for...in para arrays.

forEach es ideal para funciones pequeñas y limpias.

Evita bucles infinitos (while (true)) sin condiciones de corte claras.

📚 Recursos Recomendados
1. MDN - Loops and iteration
2. JavaScript.info - Loops













