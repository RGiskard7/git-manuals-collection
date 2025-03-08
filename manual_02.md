# Forks y Ramas en GitHub

Cuando haces un **fork** en GitHub, en realidad no estás creando una copia de una rama específica (como `main` o `develop`), sino que estás clonando el **repositorio completo**. Esto incluye todas las ramas del repositorio principal. Sin embargo, **la rama que estará activa por defecto en tu fork será la rama predeterminada del repositorio principal**, que normalmente es `main`, aunque en algunos proyectos podría ser `develop` u otra.

### Entonces, ¿qué sucede con `develop`?
- Si el repositorio principal tiene una rama `develop` y es donde se realiza el desarrollo activo, esa rama también estará disponible en tu fork.
- Para trabajar en ella, después de clonar tu fork localmente, simplemente debes asegurarte de **cambiar a la rama `develop` antes de comenzar tu trabajo**.

---

### Pasos recomendados:
1. **Hacer el fork del repositorio principal** en GitHub:
   - Esto copia el repositorio completo (todas las ramas, issues, etc.) a tu cuenta.

2. **Clonar tu fork a tu máquina local**:
   ```bash
   git clone <URL-de-tu-fork>
   ```

3. **Cambiar a la rama `develop`**:
   ```bash
   git checkout develop
   ```

4. **Crear una nueva rama desde `develop`** para tu trabajo:
   ```bash
   git checkout -b feature/nueva-funcionalidad develop
   ```

---

### Resumen
Aunque el **fork** incluye todas las ramas, tú decides en qué rama basar tu trabajo. Si el equipo utiliza `develop` para el desarrollo activo, asegúrate de trabajar siempre a partir de esa rama. La rama `main` suele ser solo para el código estable que va a producción, y no es habitual que trabajes directamente sobre ella. 
