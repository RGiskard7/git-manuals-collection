# **Manual: ¿Qué es Git Flow?**

## **Descripción**
**Git Flow** es una metodología que define un flujo de trabajo estructurado para el uso de Git en equipos de desarrollo. Se basa en el uso de ramas bien definidas para organizar el ciclo de vida del desarrollo, desde la implementación de nuevas características hasta la publicación de versiones estables.

Git Flow es ideal para proyectos con ciclos de versiones bien definidos, como aplicaciones que lanzan versiones periódicas.

---

## **Principales Ramas en Git Flow**
1. **`main` (o `master`)**:
   - Contiene el código listo para producción.
   - Solo se actualiza cuando se publica una versión estable.

2. **`develop`**:
   - Contiene el código en desarrollo activo.
   - Es la base para integrar nuevas funcionalidades antes de fusionarlas con `main`.

3. **Ramas de soporte**:
   - **`feature`**: Para desarrollar nuevas funcionalidades o características.
   - **`release`**: Para preparar el código antes de lanzar una versión.
   - **`hotfix`**: Para corregir errores críticos en producción.

---

## **Flujo de Trabajo de Git Flow**

### **1. Crear una nueva funcionalidad (`feature`)**
- Basada en `develop`:
  ```bash
  git checkout develop
  git checkout -b feature/nombre-de-la-funcionalidad
  ```
- Realizas cambios, haces commits y sincronizas:
  ```bash
  git add .
  git commit -m "Añadida funcionalidad X"
  ```

- Cuando terminas, fusionas la rama `feature` en `develop`:
  ```bash
  git checkout develop
  git merge feature/nombre-de-la-funcionalidad
  git branch -d feature/nombre-de-la-funcionalidad
  ```

---

### **2. Preparar una nueva versión (`release`)**
- Basada en `develop`:
  ```bash
  git checkout develop
  git checkout -b release/vX.Y.Z
  ```

- Ajustas detalles finales (como números de versión o documentación) y haces commits.
- Fusionas la rama `release` en `main` y en `develop`:
  ```bash
  git checkout main
  git merge release/vX.Y.Z
  git tag -a vX.Y.Z -m "Lanzamiento versión X.Y.Z"
  
  git checkout develop
  git merge release/vX.Y.Z
  git branch -d release/vX.Y.Z
  ```

---

### **3. Corregir un error en producción (`hotfix`)**
- Basada en `main`:
  ```bash
  git checkout main
  git checkout -b hotfix/nombre-del-error
  ```

- Realizas cambios, haces commits y sincronizas.
- Fusionas la rama `hotfix` en `main` y `develop`:
  ```bash
  git checkout main
  git merge hotfix/nombre-del-error
  git tag -a vX.Y.Z -m "Hotfix versión X.Y.Z"
  
  git checkout develop
  git merge hotfix/nombre-del-error
  git branch -d hotfix/nombre-del-error
  ```

---

## **Ventajas de Git Flow**
- **Organización clara**: Cada rama tiene un propósito específico.
- **Colaboración efectiva**: Facilita el trabajo en equipo con ramas aisladas.
- **Control de versiones**: Se integra bien con lanzamientos versionados.
- **Seguridad en producción**: Evita errores al mantener el código estable aislado.

---

## **Herramientas para Simplificar Git Flow**
- Puedes usar herramientas como `git-flow`, una extensión que automatiza los comandos de Git Flow.
  ```bash
  git flow init
  ```

- Los comandos básicos con `git-flow`:
  - Iniciar una nueva rama `feature`:
    ```bash
    git flow feature start nombre-de-la-funcionalidad
    ```
  - Finalizar y fusionar la rama `feature`:
    ```bash
    git flow feature finish nombre-de-la-funcionalidad
    ```
  - Lo mismo aplica para `release` y `hotfix`.

---

## **Cuándo usar Git Flow**
- Proyectos con ciclos de lanzamientos bien definidos.
- Equipos que necesitan una estructura clara y organizada para gestionar ramas.
- Proyectos con múltiples desarrolladores trabajando en paralelo.

---

### **Resumen de Comandos**
| Propósito               | Comando                                |
|-------------------------|----------------------------------------|
| Crear rama `feature`    | `git checkout -b feature/nombre`       |
| Crear rama `release`    | `git checkout -b release/vX.Y.Z`       |
| Crear rama `hotfix`     | `git checkout -b hotfix/nombre`        |
| Fusionar rama a `develop` | `git merge nombre-de-la-rama`         |
| Fusionar rama a `main`  | `git checkout main && git merge nombre`|
| Eliminar rama           | `git branch -d nombre-de-la-rama`      |