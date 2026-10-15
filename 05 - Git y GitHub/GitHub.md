# Git y GitHub

> **Resumen rápido:** Git es un sistema de control de versiones que registra los cambios realizados en un proyecto. GitHub es una plataforma en línea que permite alojar repositorios Git, colaborar con otras personas y gestionar el desarrollo de software.

## Conceptos clave

- **Repositorio:** carpeta de un proyecto cuyo historial de cambios administra Git.
- **Commit:** registro de uno o varios cambios en un momento concreto.
- **Rama (branch):** línea de trabajo independiente que permite desarrollar sin modificar directamente la versión principal.
- **Repositorio remoto:** copia del repositorio alojada en un servicio como GitHub.
- **Clonar:** descargar un repositorio remoto y su historial completo.
- **Pull request:** propuesta para revisar e integrar los cambios de una rama en otra.
- **Merge:** unión de los cambios de dos ramas.

## Diferencia entre Git y GitHub

| Git | GitHub |
|---|---|
| Se instala y ejecuta en el equipo. | Es un servicio alojado en Internet. |
| Registra versiones de archivos. | Aloja repositorios Git y facilita la colaboración. |
| Puede utilizarse sin conexión. | Requiere conexión para sincronizar cambios. |
| Se maneja mediante comandos o aplicaciones gráficas. | Añade pull requests, issues, revisiones y automatizaciones. |

Git no depende de GitHub. También existen otras plataformas compatibles con Git, como GitLab y Bitbucket.

## Flujo de trabajo básico

1. Se crea o clona un repositorio.
2. Se modifican los archivos del proyecto.
3. Se seleccionan los cambios que formarán parte del próximo commit.
4. Se crea un commit con un mensaje descriptivo.
5. Se envían los commits al repositorio remoto de GitHub.

El recorrido habitual de un cambio es:

```text
Archivos modificados → Área de preparación → Commit local → Repositorio remoto
```

## Comandos esenciales

### Configuración inicial

```bash
git config --global user.name "Tu nombre"
git config --global user.email "tu-correo@ejemplo.com"
```

Estos datos identifican al autor de los commits.

### Crear o descargar un repositorio

```bash
# Iniciar Git en la carpeta actual
git init

# Descargar un repositorio existente
git clone https://github.com/usuario/repositorio.git
```

### Revisar y guardar cambios

```bash
# Consultar el estado del repositorio
git status

# Añadir un archivo al área de preparación
git add nombre-del-archivo

# Añadir todos los cambios de la carpeta actual
git add .

# Crear un commit
git commit -m "Describe brevemente el cambio"

# Consultar el historial
git log --oneline
```

### Trabajar con ramas

```bash
# Mostrar las ramas
git branch

# Crear una rama y cambiar a ella
git switch -c nueva-funcionalidad

# Cambiar a una rama existente
git switch main

# Integrar otra rama en la rama actual
git merge nueva-funcionalidad
```

### Sincronizar con GitHub

```bash
# Consultar los repositorios remotos configurados
git remote -v

# Descargar e integrar cambios remotos
git pull origin main

# Enviar commits a GitHub
git push origin main
```

`origin` es el nombre convencional del repositorio remoto principal y `main` suele ser la rama principal.

## Ejemplo práctico

Después de crear un repositorio vacío en GitHub, un proyecto local puede publicarse así:

```bash
git init
git add .
git commit -m "Crea la versión inicial del proyecto"
git branch -M main
git remote add origin https://github.com/usuario/repositorio.git
git push -u origin main
```

La opción `-u` relaciona la rama local con la remota. Después, normalmente bastará con ejecutar `git push` y `git pull`.

## Colaboración mediante GitHub

Un flujo frecuente de colaboración consiste en:

1. Crear una rama para una tarea concreta.
2. Realizar cambios y commits pequeños.
3. Enviar la rama a GitHub con `git push`.
4. Abrir un **pull request**.
5. Revisar, comentar y corregir el código.
6. Integrar la rama cuando los cambios estén aprobados.

Los **issues** permiten registrar errores, ideas y tareas. Pueden asignarse a personas, etiquetarse y relacionarse con pull requests.

## El archivo `.gitignore`

`.gitignore` indica qué archivos o carpetas no debe registrar Git. Suele excluir dependencias instaladas, archivos temporales, configuraciones personales y secretos.

```gitignore
node_modules/
.env
*.log
dist/
```

⚠️ No deben publicarse contraseñas, claves privadas ni tokens. Añadir un secreto a `.gitignore` después de haberlo confirmado no lo elimina del historial anterior.

## Buenas prácticas

- Escribir commits breves, descriptivos y centrados en un solo cambio.
- Consultar `git status` antes de crear un commit.
- Usar ramas para nuevas funcionalidades y correcciones.
- Actualizar la rama antes de integrar cambios importantes.
- Revisar el contenido antes de enviarlo a GitHub.
- Incluir un archivo `README.md` que explique el propósito y uso del proyecto.

## 💡 Para recordar

- **Git controla versiones; GitHub aloja y facilita la colaboración.**
- `git add` prepara cambios, `git commit` los registra y `git push` los publica.
- Las ramas permiten trabajar de forma aislada y segura.
- Un pull request sirve para revisar los cambios antes de integrarlos.
