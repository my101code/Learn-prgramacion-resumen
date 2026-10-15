# Dependencias útiles para proyectos Node.js

> **Resumen rápido:** las dependencias de producción son necesarias para que la aplicación funcione cuando está desplegada. Las dependencias de desarrollo solo ayudan a programar, probar, revisar o compilar el proyecto. No es necesario instalar todos los paquetes de esta lista: hay que elegirlos según las necesidades reales.

## Diferencia entre producción y desarrollo

| Tipo | Se guarda en | Cuándo se necesita |
|---|---|---|
| Producción | `dependencies` | Durante la ejecución de la aplicación. |
| Desarrollo | `devDependencies` | Al programar, probar, formatear o compilar. |

Instalación con npm:

```bash
# Dependencia de producción
npm install nombre-del-paquete

# Dependencia de desarrollo
npm install --save-dev nombre-del-paquete

# Forma abreviada para desarrollo
npm install -D nombre-del-paquete
```

## Dependencias de producción recomendadas

Son paquetes utilizados directamente por la aplicación cuando se ejecuta. Los ejemplos siguientes son opciones habituales, pero algunos son alternativos entre sí.

### Servidor web y API

- **`express`:** framework sencillo y muy extendido para crear servidores y API REST.
- **`fastify`:** alternativa a Express centrada en rendimiento, validación y una arquitectura basada en plugins.
- **`cors`:** configura qué orígenes pueden hacer peticiones a una API. Es especialmente útil con Express.
- **`helmet`:** añade cabeceras HTTP que ayudan a proteger aplicaciones Express.

Normalmente se elige **Express o Fastify**, no ambos.

```bash
# Ejemplo de API con Express
npm install express cors helmet
```

### Cliente HTTP

- **`axios`:** cliente HTTP basado en promesas para Node.js y el navegador. Permite crear instancias con una URL base, definir tiempos de espera e interceptar peticiones o respuestas desde un punto común.

```bash
npm install axios
```

Ejemplo básico:

```js
import axios from "axios";

const api = axios.create({
  baseURL: "https://api.example.com",
  timeout: 5000,
});

const respuesta = await api.get("/usuarios");
console.log(respuesta.data);
```

Axios resulta útil cuando el proyecto necesita configuración compartida, interceptores o una API uniforme en el navegador y Node.js. Para peticiones sencillas, el `fetch()` nativo puede ser suficiente.

### Validación de datos

- **`zod`:** define esquemas y valida datos recibidos en formularios, parámetros o cuerpos de peticiones.
- **`joi`:** alternativa madura para validar objetos y configuraciones.

Conviene elegir una sola biblioteca principal de validación.

```bash
npm install zod
```

### Registro de eventos

- **`pino`:** genera logs estructurados y rápidos.
- **`pino-http`:** integra Pino con servidores HTTP y registra peticiones y respuestas.
- **`winston`:** permite configurar niveles, formatos y varios destinos de salida, llamados **transports**, como la consola, archivos o servicios externos.

```bash
# Opción 1: Pino
npm install pino pino-http

# Opción 2: Winston
npm install winston
```

Normalmente se elige **Pino o Winston**, no ambos. Pino destaca por los logs estructurados y el rendimiento; Winston resulta práctico cuando se necesitan distintos formatos y destinos configurables.

Ejemplo básico con Winston:

```js
import winston from "winston";

const logger = winston.createLogger({
  level: "info",
  format: winston.format.json(),
  transports: [new winston.transports.Console()],
});

logger.info("Servidor iniciado", { puerto: 3000 });
logger.error("No se pudo conectar a la base de datos");
```

En producción es preferible usar un sistema de logs configurable en lugar de depender únicamente de `console.log()`.

### Bases de datos

La elección depende del motor utilizado:

- **`pg`:** conexión directa con PostgreSQL.
- **`mysql2`:** conexión con MySQL y MariaDB.
- **`mongoose`:** modelado de datos para MongoDB.
- **`better-sqlite3`:** acceso sencillo a SQLite en aplicaciones compatibles con su modelo síncrono.

```bash
# Instalar solo el controlador necesario
npm install pg
```

Los ORM y generadores de consultas, como Prisma, Drizzle o Sequelize, pueden simplificar el acceso a datos, pero deben elegirse después de valorar el tipo y la complejidad del proyecto.

### Autenticación y seguridad

- **`jose`:** trabaja con JWT, firmas y cifrado basados en estándares JOSE.
- **`argon2`:** permite generar hashes seguros para contraseñas.
- **`express-rate-limit`:** limita peticiones repetidas en aplicaciones Express.

```bash
npm install jose argon2 express-rate-limit
```

⚠️ Instalar estas bibliotecas no hace segura una aplicación por sí solo. La autenticación requiere una configuración correcta, validación, gestión segura de claves y controles de autorización.

### Variables de entorno

- **`dotenv`:** carga variables desde un archivo `.env`; sigue siendo útil en proyectos o entornos que no emplean la carga nativa de Node.js.

```bash
npm install dotenv
```

Las versiones modernas de Node.js también pueden cargar estos archivos sin un paquete adicional:

```bash
node --env-file=.env src/index.js
```

El archivo `.env` con secretos debe incluirse en `.gitignore`. Se puede publicar un `.env.example` sin credenciales para documentar las variables necesarias.

## Dependencias de desarrollo recomendadas

Estos paquetes ayudan durante el desarrollo, pero normalmente no son necesarios para ejecutar la aplicación ya preparada.

### Calidad y formato del código

- **`eslint`:** detecta problemas y aplica reglas de calidad al código.
- **`prettier`:** aplica un formato consistente automáticamente.
- **`eslint-config-prettier`:** desactiva reglas de ESLint que entrarían en conflicto con Prettier.

```bash
npm install -D eslint prettier eslint-config-prettier
```

### TypeScript

- **`typescript`:** compila y comprueba código TypeScript.
- **`@types/node`:** proporciona los tipos de las API de Node.js.
- **`tsx`:** ejecuta archivos TypeScript durante el desarrollo sin una compilación manual previa.
- **`@types/express`:** añade tipos de Express si el proyecto utiliza Express y TypeScript.

```bash
npm install -D typescript @types/node tsx
```

Si el proyecto está escrito únicamente en JavaScript, estas dependencias no son obligatorias.

### Pruebas

- **`vitest`:** ejecutor de pruebas rápido y con una API familiar.
- **`supertest`:** facilita pruebas de integración sobre servidores HTTP.

```bash
npm install -D vitest supertest
```

Node.js también incluye `node:test`, por lo que un proyecto sencillo puede realizar pruebas sin instalar un framework externo.

### Reinicio durante el desarrollo

- **`nodemon`:** reinicia la aplicación cuando detecta cambios en los archivos.

```bash
npm install -D nodemon
```

Antes de instalarlo, conviene valorar el modo observación incorporado en Node.js:

```bash
node --watch src/index.js
```

### Automatización antes de cada commit

- **`husky`:** configura acciones automáticas mediante hooks de Git.
- **`lint-staged`:** ejecuta comprobaciones únicamente sobre archivos preparados para el commit.

```bash
npm install -D husky lint-staged
```

Son útiles en equipos que quieren impedir commits con errores de formato o calidad, pero pueden resultar innecesarios en proyectos pequeños.

## Ejemplo de instalación equilibrada

Para una API sencilla con Express, validación, logs y pruebas:

```bash
# Producción
npm install express cors helmet zod pino pino-http

# Desarrollo
npm install -D eslint prettier vitest supertest
```

El resultado aproximado en `package.json` sería:

```json
{
  "dependencies": {
    "cors": "...",
    "express": "...",
    "helmet": "...",
    "pino": "...",
    "pino-http": "...",
    "zod": "..."
  },
  "devDependencies": {
    "eslint": "...",
    "prettier": "...",
    "supertest": "...",
    "vitest": "..."
  }
}
```

Los valores `"..."` representan las versiones que npm añadirá automáticamente. No deben copiarse literalmente en un archivo real.

## Paquetes que quizá no sean necesarios

Node.js ya incorpora varias funciones para las que antes se instalaban paquetes:

- **Peticiones HTTP:** `fetch()` está disponible de forma nativa.
- **Identificadores UUID:** `crypto.randomUUID()` cubre muchos casos comunes.
- **Pruebas:** `node:test` permite crear una suite básica.
- **Reinicio automático:** `node --watch` observa cambios.
- **Variables `.env`:** `--env-file` permite cargarlas desde la terminal.

Evitar una dependencia cuando la plataforma ya resuelve bien el problema reduce instalaciones, actualizaciones y posibles vulnerabilidades.

En el caso de las peticiones HTTP, Axios sigue siendo una opción válida cuando sus interceptores, instancias configurables o manejo común de respuestas simplifican el proyecto.

## Buenas prácticas

- Instalar solo lo que realmente utilice el proyecto.
- Revisar la documentación, el mantenimiento y la licencia antes de elegir un paquete.
- Conservar `package-lock.json` en Git para mantener instalaciones reproducibles.
- Ejecutar `npm audit` y actualizar dependencias de forma periódica.
- No mover una herramienta de compilación o pruebas a `dependencies` si solo se usa al desarrollar.
- Probar las actualizaciones antes de desplegarlas en producción.

## 💡 Para recordar

- `dependencies` contiene lo necesario para ejecutar la aplicación.
- `devDependencies` contiene herramientas para crearla, comprobarla o compilarla.
- No todas las recomendaciones deben instalarse juntas: se eligen por función.
- Antes de añadir un paquete, conviene comprobar si Node.js ya ofrece esa capacidad.
