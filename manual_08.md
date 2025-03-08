# Guía para la gestión de ramas en proyectos con Git Flow

Esta guía está diseñada para ayudarte a gestionar las ramas en un proyecto de manera efectiva utilizando la metodología **Git Flow**. Incluye instrucciones detalladas para trabajar con las ramas principales (`main` y `develop`), así como las ramas específicas (`feature`, `release` y `hotfix`).

---

## Índice

- [Guía para la gestión de ramas en proyectos con Git Flow](#guía-para-la-gestión-de-ramas-en-proyectos-con-git-flow)
  - [Índice](#índice)
  - [Conceptos Básicos](#conceptos-básicos)
    - [Ramas Principales](#ramas-principales)
    - [Ramas Secundarias](#ramas-secundarias)
  - [Configuración Inicial del Repositorio](#configuración-inicial-del-repositorio)
  - [Flujo de Trabajo con Git Flow](#flujo-de-trabajo-con-git-flow)
    - [Trabajar con Ramas Feature](#trabajar-con-ramas-feature)
    - [Preparar una Release](#preparar-una-release)
    - [Aplicar un Hotfix](#aplicar-un-hotfix)
  - [Sincronización entre Main y Develop](#sincronización-entre-main-y-develop)
  - [Buenas Prácticas](#buenas-prácticas)
  - [Comandos Esenciales](#comandos-esenciales)

---

## Conceptos Básicos

### Ramas Principales

- **`main`**: Contiene el código listo para producción. Solo se actualiza al realizar un merge desde `release` o `hotfix`.
- **`develop`**: Rama principal para el desarrollo. Sirve como base para las ramas `feature` y `release`.

### Ramas Secundarias

- **`feature/*`**: Utilizadas para desarrollar nuevas funcionalidades. Se crean a partir de `develop`.
- **`release/*`**: Usadas para preparar una versión lista para producción. Se crean a partir de `develop` y se fusionan en `main` y `develop`.
- **`hotfix/*`**: Diseñadas para corregir errores críticos en producción. Se crean a partir de `main` y se fusionan en `main` y `develop`.

---

## Configuración Inicial del Repositorio

Antes de comenzar, asegúrate de que tu repositorio está correctamente configurado:

1. Crea las ramas principales:

   ```bash
   git checkout -b main
   git push -u origin main

   git checkout -b develop
   git push -u origin develop
   ```

2. Configura el repositorio remoto:

   ```bash
   git remote add upstream https://github.com/<usuario>/<repositorio>.git
   ```

3. Asegúrate de que `main` y `develop` están sincronizadas correctamente:

   ```bash
   git fetch upstream
   git checkout main
   git pull upstream main

   git checkout develop
   git pull upstream develop
   ```

---

## Flujo de Trabajo con Git Flow

### Trabajar con Ramas Feature

1. **Crear una rama feature**:

   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/<nombre-de-la-funcionalidad>
   ```

2. **Hacer cambios en la rama**:

   Realiza los cambios necesarios en el código y haz commits:

   ```bash
   git add .
   git commit -m "Implementar nueva funcionalidad"
   ```

3. **Fusionar la rama feature en develop**:

   Una vez completada la funcionalidad:

   ```bash
   git checkout develop
   git pull origin develop
   git merge feature/<nombre-de-la-funcionalidad>
   ```

4. **Eliminar la rama feature**:

   ```bash
   git branch -d feature/<nombre-de-la-funcionalidad>
   git push origin --delete feature/<nombre-de-la-funcionalidad>
   ```

---

### Preparar una Release

1. **Crear una rama release**:

   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b release/<versión>
   ```

2. **Realizar ajustes finales**:

   Realiza los últimos cambios necesarios, como actualizar el número de versión o la documentación:

   ```bash
   git add .
   git commit -m "Actualizar versión a <versión>"
   ```

3. **Fusionar en main y develop**:

   ```bash
   git checkout main
   git merge release/<versión>
   git push origin main

   git checkout develop
   git merge release/<versión>
   git push origin develop
   ```

4. **Eliminar la rama release**:

   ```bash
   git branch -d release/<versión>
   git push origin --delete release/<versión>
   ```

---

### Aplicar un Hotfix

1. **Crear una rama hotfix**:

   ```bash
   git checkout main
   git pull origin main
   git checkout -b hotfix/<descripción>
   ```

2. **Realizar los cambios**:

   Realiza los cambios necesarios para solucionar el problema:

   ```bash
   git add .
   git commit -m "Hotfix: corregir <problema>"
   ```

3. **Fusionar en main y develop**:

   ```bash
   git checkout main
   git merge hotfix/<descripción>
   git push origin main

   git checkout develop
   git merge hotfix/<descripción>
   git push origin develop
   ```

4. **Eliminar la rama hotfix**:

   ```bash
   git branch -d hotfix/<descripción>
   git push origin --delete hotfix/<descripción>
   ```

---

## Sincronización entre Main y Develop

1. **Actualizar develop con cambios de main (por ejemplo, tras un hotfix):**

   ```bash
   git checkout develop
   git pull origin develop
   git merge main
   git push origin develop
   ```

2. **Actualizar main con cambios de develop (por ejemplo, tras una release):**

   ```bash
   git checkout main
   git pull origin main
   git merge develop
   git push origin main
   ```

---

## Buenas Prácticas

1. **No trabajar directamente en `main` ni `develop`.**
   Siempre utiliza ramas secundarias (`feature`, `release`, `hotfix`).

2. **Mantén las ramas sincronizadas.**
   Realiza merges regulares para evitar conflictos al final del desarrollo.

3. **Escribe mensajes de commit claros y descriptivos.**

4. **Elimina ramas que ya no sean necesarias.**

5. **Actualiza tu rama local antes de comenzar a trabajar:**

   ```bash
   git pull origin develop
   ```

---

## Comandos Esenciales

| Acción                       | Comando                                                                 |
|-------------------------------|-------------------------------------------------------------------------|
| Crear una rama                | `git checkout -b <nombre-de-rama>`                                      |
| Cambiar a otra rama           | `git checkout <nombre-de-rama>`                                         |
| Fusionar ramas                | `git merge <nombre-de-rama>`                                            |
| Eliminar una rama local       | `git branch -d <nombre-de-rama>`                                        |
| Eliminar una rama remota      | `git push origin --delete <nombre-de-rama>`                             |
| Ver historial de commits      | `git log --oneline --graph`                                             |
| Sincronizar con el remoto     | `git pull origin <nombre-de-rama>`                                      |
| Subir cambios al remoto       | `git push origin <nombre-de-rama>`                                      |

---

Esta guía te proporcionará una base sólida para gestionar ramas en proyectos utilizando Git Flow. Si necesitas más detalles, consulta la [documentación oficial de Git](https://git-scm.com/doc).

