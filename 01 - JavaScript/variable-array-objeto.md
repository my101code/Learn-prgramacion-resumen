# Variables, arrays y objetos en JavaScript

> **Resumen rápido:** Las variables guardan valores para reutilizarlos. Los arrays agrupan varios valores en una lista ordenada y los objetos reúnen datos relacionados mediante propiedades.

## Variables

Una **variable** es un espacio con nombre que permite guardar un valor. En JavaScript se declara normalmente con `const` o `let`.

```js
const nombre = "Lucía";
let edad = 20;

edad = 21;
```

- **`const`:** se usa cuando la variable no se volverá a asignar.
- **`let`:** se usa cuando el valor puede cambiar.
- **`var`:** es una forma antigua de declarar variables; normalmente se evita en código moderno.

### Tipos de valores frecuentes

```js
const texto = "Hola";       // string
const cantidad = 10;        // number
const activo = true;        // boolean
const sinValor = null;      // ausencia intencional de valor
let noDefinido;             // undefined
```

💡 JavaScript determina automáticamente el tipo según el valor asignado.

## Arrays

Un **array** es una lista ordenada de valores. Se escribe entre corchetes `[]` y cada elemento ocupa una posición llamada **índice**. Los índices comienzan en `0`.

```js
const frutas = ["manzana", "pera", "naranja"];

console.log(frutas[0]); // "manzana"
console.log(frutas[2]); // "naranja"
```

### Operaciones comunes

```js
const tareas = ["estudiar", "practicar"];

tareas.push("descansar"); // añade al final
tareas.pop();              // elimina el último elemento

console.log(tareas.length); // cantidad de elementos
```

Para recorrer un array:

```js
const colores = ["rojo", "verde", "azul"];

for (const color of colores) {
  console.log(color);
}
```

## Objetos

Un **objeto** agrupa información relacionada mediante pares de **propiedad y valor**. Se escribe entre llaves `{}`.

```js
const persona = {
  nombre: "Lucía",
  edad: 21,
  estudiante: true
};
```

Las propiedades pueden consultarse con notación de punto o de corchetes:

```js
console.log(persona.nombre);     // "Lucía"
console.log(persona["edad"]);   // 21
```

También se pueden modificar o añadir propiedades:

```js
persona.edad = 22;
persona.ciudad = "Madrid";
```

Aunque el objeto se haya declarado con `const`, sus propiedades pueden cambiar. Lo que no se puede hacer es asignar otro objeto completo a la misma variable.

## Arrays y objetos combinados

Es habitual guardar objetos dentro de un array. Por ejemplo, una lista de productos:

```js
const productos = [
  { nombre: "Cuaderno", precio: 4 },
  { nombre: "Lápiz", precio: 1 }
];

console.log(productos[0].nombre); // "Cuaderno"

for (const producto of productos) {
  console.log(`${producto.nombre}: ${producto.precio} €`);
}
```

## Comparación rápida

| Estructura | Para qué sirve | Ejemplo |
|---|---|---|
| Variable | Guardar un valor con un nombre | `const edad = 21` |
| Array | Guardar una lista ordenada | `const notas = [8, 7, 9]` |
| Objeto | Agrupar datos mediante propiedades | `const alumno = { nombre: "Ana" }` |

## Ejemplo práctico

```js
const curso = {
  nombre: "JavaScript básico",
  alumnos: ["Ana", "Luis", "Marta"],
  activo: true
};

curso.alumnos.push("Pablo");

console.log(curso.nombre);       // "JavaScript básico"
console.log(curso.alumnos[1]);   // "Luis"
console.log(curso.alumnos.length); // 4
```

En este ejemplo, `curso` es una variable que contiene un objeto. Dentro del objeto, `alumnos` es una propiedad cuyo valor es un array.

## 💡 Para recordar

- Usa `const` por defecto y `let` cuando necesites reasignar la variable.
- Los arrays son listas ordenadas y sus índices comienzan en `0`.
- Los objetos organizan datos relacionados mediante propiedades.
- Los arrays y objetos se pueden combinar para representar información más compleja.
