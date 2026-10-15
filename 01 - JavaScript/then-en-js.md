# `.then()` en JavaScript

> **Resumen rápido:** `.then()` se utiliza para indicar qué debe ocurrir cuando una promesa se resuelve correctamente. Devuelve una nueva promesa, lo que permite encadenar varias operaciones asíncronas en orden.

## Antes de empezar: qué es una promesa

Una **promesa** representa el resultado futuro de una operación asíncrona, como solicitar datos a una API o leer información de una base de datos.

Puede encontrarse en tres estados:

- **Pendiente (`pending`):** la operación todavía no ha terminado.
- **Cumplida (`fulfilled`):** terminó correctamente y produjo un valor.
- **Rechazada (`rejected`):** ocurrió un error.

## Sintaxis básica

```js
promesa.then((resultado) => {
  // Se ejecuta cuando la promesa se resuelve.
  console.log(resultado);
});
```

`.then()` recibe una función que se ejecutará cuando la promesa se cumpla. El parámetro `resultado` contiene el valor con el que fue resuelta.

## Ejemplo sencillo

```js
const promesa = Promise.resolve("Operación completada");

promesa.then((mensaje) => {
  console.log(mensaje);
});
```

Resultado:

```text
Operación completada
```

El código pasado a `.then()` no se ejecuta inmediatamente: JavaScript espera a que la promesa se resuelva.

## Encadenar varios `.then()`

Cada llamada a `.then()` devuelve una **nueva promesa**. El valor retornado por una función pasa al siguiente `.then()`:

```js
Promise.resolve(5)
  .then((numero) => {
    return numero * 2;
  })
  .then((resultado) => {
    return resultado + 3;
  })
  .then((resultadoFinal) => {
    console.log(resultadoFinal); // 13
  });
```

También se puede usar el retorno implícito de una función flecha:

```js
Promise.resolve(5)
  .then((numero) => numero * 2)
  .then((resultado) => console.log(resultado)); // 10
```

⚠️ Si no se utiliza `return`, el siguiente `.then()` recibe `undefined`.

## Encadenar otra promesa

Si un `.then()` devuelve otra promesa, la cadena espera a que esta termine antes de continuar:

```js
obtenerUsuario()
  .then((usuario) => {
    return obtenerPedidos(usuario.id);
  })
  .then((pedidos) => {
    console.log(pedidos);
  });
```

Esto evita anidar muchas funciones y mantiene las operaciones en un orden claro.

## Gestionar errores con `.catch()`

Si una promesa se rechaza o se produce un error dentro de un `.then()`, se puede capturar con `.catch()`:

```js
obtenerDatos()
  .then((datos) => {
    console.log(datos);
  })
  .catch((error) => {
    console.error("Ocurrió un error:", error);
  });
```

Un único `.catch()` al final puede capturar errores de cualquiera de los pasos anteriores de la cadena.

## Ejecutar código al finalizar

`.finally()` ejecuta una función tanto si la promesa se cumple como si se rechaza:

```js
obtenerDatos()
  .then((datos) => console.log(datos))
  .catch((error) => console.error(error))
  .finally(() => console.log("Proceso terminado"));
```

Es útil para ocultar indicadores de carga o liberar recursos.

## Ejemplo con `fetch()`

```js
fetch("https://api.example.com/usuarios/1")
  .then((respuesta) => {
    if (!respuesta.ok) {
      throw new Error(`Error HTTP: ${respuesta.status}`);
    }

    return respuesta.json();
  })
  .then((usuario) => {
    console.log(usuario);
  })
  .catch((error) => {
    console.error("No se pudo obtener el usuario:", error);
  });
```

El primer `.then()` transforma la respuesta a JSON. Como `respuesta.json()` devuelve una promesa, el segundo `.then()` espera y recibe los datos ya convertidos.

## `.then()` frente a `async/await`

Los dos estilos trabajan con promesas y pueden producir el mismo resultado:

```js
// Con .then()
obtenerDatos()
  .then((datos) => console.log(datos))
  .catch((error) => console.error(error));
```

```js
// Con async/await
async function mostrarDatos() {
  try {
    const datos = await obtenerDatos();
    console.log(datos);
  } catch (error) {
    console.error(error);
  }
}
```

`.then()` resulta útil para cadenas breves y transformaciones. `async/await` suele facilitar la lectura cuando existen muchos pasos o condiciones.

## Errores frecuentes

- Olvidar devolver un valor o una promesa dentro de `.then()`.
- No añadir `.catch()` para gestionar posibles errores.
- Anidar llamadas a `.then()` cuando podrían encadenarse.
- Pensar que `.then()` detiene todo el programa mientras espera.
- Usar `.then(miFuncion())`, que ejecuta la función inmediatamente, en vez de `.then(miFuncion)`.

## 💡 Para recordar

- `.then()` se ejecuta cuando una promesa se resuelve correctamente.
- Cada `.then()` devuelve una nueva promesa y permite continuar la cadena.
- El valor retornado pasa al siguiente `.then()`.
- `.catch()` gestiona errores y `.finally()` ejecuta tareas finales.
