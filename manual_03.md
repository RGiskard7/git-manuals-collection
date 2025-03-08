# Guía rápida - Subir cambios directamente a la rama main en GitHub

## **1. Clonar el repositorio**
Primero, necesitas tener el proyecto en tu máquina local:

1. Copia la URL del repositorio de GitHub.
2. En tu terminal, ejecuta:
   ```bash
   git clone <URL-del-repositorio>
   ```

Ejemplo:
```bash
git clone https://github.com/tu-equipo/proyecto.git
```

Esto descargará todo el repositorio, incluyendo la rama principal `main`.

3. Cambia al directorio del proyecto:
   ```bash
   cd proyecto
   ```

---

## **2. Verifica que estás en la rama `main`**
Git debería colocarte automáticamente en la rama principal después de clonar, pero puedes confirmarlo con:
```bash
git branch
```

El asterisco (`*`) debe aparecer junto a `main`. Si no estás en la rama `main`, cámbiate con:
```bash
git checkout main
```

---

## **3. Realiza tus cambios**
Modifica los archivos necesarios del proyecto en tu editor. Una vez que hayas terminado:

1. **Verifica el estado del repositorio** para asegurarte de que tus cambios sean reconocidos:
   ```bash
   git status
   ```

2. **Añade los archivos modificados al área de preparación**:
   ```bash
   git add .
   ```

3. **Haz un commit** para confirmar los cambios localmente:
   ```bash
   git commit -m "Descripción de los cambios realizados"
   ```

Ejemplo:
```bash
git commit -m "Corregidos errores en el módulo de autenticación"
```

---

## **4. Sincroniza con el repositorio remoto**
Antes de subir tus cambios, asegúrate de que tienes la última versión de la rama `main` para evitar conflictos:

1. Descarga los últimos cambios del repositorio remoto:
   ```bash
   git pull origin main
   ```

2. Si hay conflictos, resuélvelos manualmente, luego haz un nuevo commit si es necesario:
   ```bash
   git add .
   git commit -m "Conflictos resueltos"
   ```

---

## **5. Sube tus cambios**
Una vez que estés seguro de que tu copia local está actualizada, sube tus cambios al repositorio remoto:
```bash
git push origin main
```

Esto actualizará la rama `main` en GitHub con tus cambios.

---

### **Resumen de Comandos**

| Acción                        | Comando                                           |
|-------------------------------|---------------------------------------------------|
| Clonar el repositorio         | `git clone <URL>`                                 |
| Verificar la rama actual      | `git branch`                                      |
| Cambiar a la rama `main`      | `git checkout main`                               |
| Añadir cambios                | `git add .`                                       |
| Hacer commit                  | `git commit -m "Descripción del cambio"`          |
| Descargar últimos cambios     | `git pull origin main`                            |
| Subir cambios al remoto       | `git push origin main`                            |

---

### **Notas importantes**
- Trabajar directamente en `main` es común en proyectos pequeños o personales, pero en equipos más grandes puede ser mejor usar ramas separadas para evitar conflictos.
- Siempre realiza un `git pull` antes de un `git push` para evitar sobrescribir cambios de otros colaboradores.