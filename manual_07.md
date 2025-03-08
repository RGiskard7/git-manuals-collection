# Cómo clonar un proyecto, crear una rama y subir cambios sin mezclar con main

## **1. Clona el repositorio del proyecto**
Clona el repositorio en tu máquina local para trabajar con una copia completa del proyecto:
```bash
git clone <URL-del-repositorio>
```

Esto descargará todas las ramas existentes, incluida `main`.

---

## **2. Crea una nueva rama para tus cambios**
Cambia al directorio del proyecto y crea una nueva rama basada en `main` o en otra rama como `develop`, según lo que decida el equipo:
```bash
git checkout -b nombre-de-tu-rama
```

Ejemplo:
```bash
git checkout -b feature/nueva-funcionalidad
```

---

## **3. Realiza tus cambios**
Haz las modificaciones necesarias en el proyecto. Una vez que termines, añade y confirma los cambios en la nueva rama:

1. Añade los archivos modificados al área de preparación:
   ```bash
   git add .
   ```

2. Haz un commit con un mensaje descriptivo:
   ```bash
   git commit -m "Implementada nueva funcionalidad X"
   ```

---

## **4. Sube tu rama al repositorio en GitHub**
Para que tus compañeros vean tu rama en GitHub, súbela al repositorio remoto sin tocar `main`:
```bash
git push origin nombre-de-tu-rama
```

Ejemplo:
```bash
git push origin feature/nueva-funcionalidad
```

Ahora, la rama `feature/nueva-funcionalidad` aparecerá en el repositorio de GitHub como una rama separada.

---

## **5. Crear un Pull Request en GitHub**
1. Ve a la página del repositorio en GitHub.
2. GitHub te sugerirá crear un **Pull Request (PR)** para la rama que acabas de subir.
3. Haz clic en **"New Pull Request"** y selecciona:
   - **Base branch**: La rama contra la que deseas fusionar, usualmente `main` o `develop`.
   - **Compare branch**: Tu rama (`feature/nueva-funcionalidad`).
4. Escribe una descripción detallada de los cambios y solicita la revisión.

---

## **6. Revisión y fusión (Merge)**
- Tus compañeros revisarán el PR. Si es aprobado, ellos podrán fusionarlo con la rama `main` o la rama objetivo.
- GitHub facilita opciones como:
  - **Merge commit**: Fusiona con un commit adicional.
  - **Squash and merge**: Combina todos los commits en uno.
  - **Rebase and merge**: Aplica los commits encima de la base.

---

## **7. Mantén tu rama sincronizada**
Si el equipo realiza cambios en `main` mientras trabajas, sincroniza tu rama para evitar conflictos:

1. Obtén los últimos cambios del remoto:
   ```bash
   git fetch origin
   ```

2. Actualiza tu rama con los cambios de `main`:
   ```bash
   git merge origin/main
   ```

---

## **Resumen de Comandos**

| Acción                              | Comando                                   |
|-------------------------------------|-------------------------------------------|
| Clonar el repositorio               | `git clone <URL>`                         |
| Crear una nueva rama                | `git checkout -b nombre-de-tu-rama`       |
| Añadir cambios al área de preparación | `git add .`                              |
| Hacer commit                        | `git commit -m "Descripción del cambio"`  |
| Subir una rama al remoto            | `git push origin nombre-de-tu-rama`       |
| Sincronizar tu rama con `main`      | `git merge origin/main`                   |