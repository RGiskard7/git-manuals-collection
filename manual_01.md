# **Manual básico de Git y GitHub**

## **1. Configuración inicial**
Antes de usar Git, asegúrate de configurarlo con tus credenciales.

### Configuración global:
```bash
git config --global user.name "TuNombre"
git config --global user.email "TuEmail@example.com"
```

Verifica la configuración:
```bash
git config --list
```

---

## **2. Crear un repositorio**
### Crear un repositorio local:
```bash
git init
```

### Clonar un repositorio existente:
```bash
git clone <URL_DEL_REPOSITORIO>
```

---

## **3. Estados del archivo en Git**
### Verificar el estado de los archivos:
```bash
git status
```

### Añadir archivos al área de preparación:
```bash
git add <archivo>      # Añade un archivo específico
git add .              # Añade todos los archivos del directorio
```

### Confirmar los cambios:
```bash
git commit -m "Mensaje descriptivo del cambio"
```

---

## **4. Trabajar con ramas**
### Crear una nueva rama:
```bash
git branch <nombre_de_rama>
```

### Cambiar a otra rama:
```bash
git checkout <nombre_de_rama>
```

### Crear y cambiar a una nueva rama:
```bash
git checkout -b <nombre_de_rama>
```

### Ver las ramas disponibles:
```bash
git branch
```

---

## **5. Sincronizar con GitHub**
### Vincular el repositorio local a un repositorio remoto:
```bash
git remote add origin <URL_DEL_REPOSITORIO>
```

### Subir los cambios al repositorio remoto:
```bash
git push -u origin <nombre_de_rama>
```

### Actualizar el repositorio local con cambios del remoto:
```bash
git pull origin <nombre_de_rama>
```

---

## **6. Fusionar ramas**
### Fusionar una rama a la rama actual:
```bash
git merge <nombre_de_rama>
```

---

## **7. Resolver conflictos**
1. Git marcará los archivos con conflictos después de un `merge` o `pull`.
2. Edita los archivos y elige qué cambios mantener.
3. Una vez resueltos, añade los archivos al área de preparación:
   ```bash
   git add <archivo>
   ```
4. Finaliza con un commit:
   ```bash
   git commit -m "Conflictos resueltos"
   ```

---

## **8. Ignorar archivos**
Crea un archivo `.gitignore` para especificar qué archivos o directorios ignorar.

Ejemplo:
```
# Ignorar archivos binarios
*.exe

# Ignorar el directorio temporal
/temp/
```

---

## **9. Inspeccionar el historial**
### Ver el historial de commits:
```bash
git log
```

### Ver cambios en un archivo:
```bash
git diff <archivo>
```

---

## **10. Eliminar o deshacer cambios**
### Eliminar un archivo del control de versiones:
```bash
git rm <archivo>
```

### Deshacer cambios en un archivo antes de hacer un commit:
```bash
git checkout -- <archivo>
```

### Deshacer el último commit (sin eliminar los cambios):
```bash
git reset --soft HEAD~1
```

---

## **11. Trabajo en equipo con GitHub**
### Crear un Pull Request (PR):
1. Sube tus cambios a una nueva rama.
2. Ve a GitHub y selecciona "New Pull Request".
3. Revisa los cambios y solicita la revisión.

### Revisar PRs:
- Comenta en los cambios.
- Aprueba o solicita modificaciones antes de hacer el merge.

---

## **12. Plantilla básica de comandos**
| Acción                            | Comando                                    |
|-----------------------------------|-------------------------------------------|
| Configurar usuario                | `git config --global user.name` y `user.email` |
| Inicializar repositorio           | `git init`                                |
| Añadir cambios                    | `git add <archivo>` o `git add .`         |
| Confirmar cambios                 | `git commit -m "mensaje"`                 |
| Ver estado                        | `git status`                              |
| Ver historial                     | `git log`                                 |
| Crear rama                        | `git branch <nombre_de_rama>`             |
| Cambiar de rama                   | `git checkout <nombre_de_rama>`           |
| Fusionar ramas                    | `git merge <nombre_de_rama>`              |
| Subir cambios                     | `git push -u origin <rama>`               |
| Actualizar desde el remoto        | `git pull origin <rama>`                  |
