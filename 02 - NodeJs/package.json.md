# El archivo `package.json`

> **Resumen rápido:** `package.json` es el archivo principal de configuración de muchos proyectos de Node.js y JavaScript. Describe el proyecto, define comandos y registra los paquetes que necesita. Utiliza formato JSON, por lo que exige comillas dobles y no admite comentarios.

## Para qué sirve

`package.json` permite:

- Identificar el proyecto mediante su nombre y versión.
- Guardar información descriptiva, como licencia y autor.
- Definir comandos reutilizables en `scripts`.
- Declarar dependencias necesarias para ejecutar o desarrollar el proyecto.
- Configurar cómo se distribuye o interpreta el código.

Normalmente se encuentra en la **carpeta raíz del proyecto**.

## Cómo crearlo

Con npm se puede generar de forma interactiva:

```bash
npm init
```

El comando solicita datos como el nombre, la versión y el archivo principal. Para aceptar valores predeterminados y crearlo directamente:

```bash
npm init -y
```

## Estructura básica

```json
{
  "name": "mi-proyecto",
  "version": "1.0.0",
  "description": "Descripción breve del proyecto",
  "private": true,
  "type": "module",
  "scripts": {
    "start": "node src/index.js",
    "dev": "node --watch src/index.js",
    "test": "node --test"
  },
  "dependencies": {
    "express": "^5.0.0"
  },
  "devDependencies": {
    "eslint": "^9.0.0"
  }
}
```

## Campos más habituales

| Campo | Función |
|---|---|
| `name` | Nombre del paquete o proyecto. |
| `version` | Versión con formato `mayor.menor.parche`, por ejemplo `1.2.0`. |
| `description` | Explicación breve del propósito del proyecto. |
| `private` | Con `true`, ayuda a evitar que el proyecto se publique por accidente en npm. |
| `type` | Indica el sistema de módulos; `"module"` habilita `import` y `export` en archivos `.js`. |
| `main` | Archivo de entrada principal de un paquete. |
| `scripts` | Comandos que pueden ejecutarse con npm. |
| `dependencies` | Paquetes necesarios para ejecutar la aplicación. |
| `devDependencies` | Herramientas utilizadas durante el desarrollo. |
| `engines` | Versiones de Node.js o npm previstas para el proyecto. |
| `license` | Licencia con la que se distribuye el paquete. |

No todos los campos son obligatorios. Los necesarios dependen del tipo de proyecto y de si se publicará como paquete.

## Scripts

Los scripts asignan nombres sencillos a comandos frecuentes:

```json
{
  "scripts": {
    "start": "node src/index.js",
    "dev": "node --watch src/index.js",
    "test": "node --test"
  }
}
```

Se ejecutan de esta forma:

```bash
npm run dev
npm test
npm start
```

Para `start` y `test`, npm permite omitir `run`. En los demás scripts se utiliza normalmente `npm run nombre`.

## Dependencias

Al instalar un paquete, npm actualiza automáticamente `package.json`:

```bash
# Dependencia necesaria para ejecutar la aplicación
npm install express

# Herramienta necesaria solo durante el desarrollo
npm install --save-dev eslint
```

El resultado se guarda en uno de estos campos:

```json
{
  "dependencies": {
    "express": "^5.0.0"
  },
  "devDependencies": {
    "eslint": "^9.0.0"
  }
}
```

El símbolo `^` permite actualizaciones compatibles dentro de la misma versión mayor. La versión exacta instalada queda registrada normalmente en `package-lock.json`.

## Relación con otros archivos

- **`package-lock.json`:** registra las versiones exactas de las dependencias para obtener instalaciones reproducibles.
- **`node_modules/`:** contiene los paquetes instalados; normalmente se excluye de Git mediante `.gitignore`.
- **`.npmrc`:** permite establecer opciones adicionales de npm.

Después de descargar un proyecto que ya contiene `package.json` y `package-lock.json`, las dependencias pueden instalarse con:

```bash
npm install
```

## Errores frecuentes

- Usar comillas simples en lugar de comillas dobles.
- Dejar una coma después del último elemento.
- Añadir comentarios dentro del JSON.
- Escribir manualmente dependencias sin instalarlas.
- Confundir `dependencies` con `devDependencies`.
- Subir `node_modules/` al repositorio.

## 💡 Para recordar

- `package.json` describe y configura un proyecto de Node.js.
- `scripts` reúne los comandos habituales del proyecto.
- `dependencies` contiene paquetes de ejecución y `devDependencies`, herramientas de desarrollo.
- `package-lock.json` complementa este archivo fijando las versiones instaladas.
