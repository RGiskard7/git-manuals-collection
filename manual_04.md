# Estructura y uso de Conventional Commits

La convención **Conventional Commits** utiliza un formato estructurado para los mensajes de commit, facilitando el entendimiento del historial de cambios. Los tipos más comunes son:

---

### **Estructura de un mensaje de commit**
```
<tipo>(<scope>): <descripción breve>

<cuerpo opcional del mensaje explicativo>

<footer opcional (por ejemplo, cerrando un issue o deprecando algo)>
```

### **Tipos principales**
1. **feat:** Añade una nueva funcionalidad al código.
   - Ejemplo: `feat(auth): añadir autenticación con tokens JWT`

2. **fix:** Soluciona un bug o error.
   - Ejemplo: `fix(transcription): corregir problema con timeout en la conexión WebSocket`

3. **refactor:** Reorganiza el código sin cambiar su comportamiento funcional.
   - Ejemplo: `refactor(main): dividir lógica de transcripción en función separada`

4. **perf:** Optimiza el rendimiento de una parte del código.
   - Ejemplo: `perf(audio): mejorar el manejo de buffers en el grabador`

5. **test:** Añade o actualiza pruebas.
   - Ejemplo: `test(llm): agregar pruebas para clasificar mensajes`

6. **docs:** Cambia o añade documentación.
   - Ejemplo: `docs(readme): actualizar instrucciones de instalación`

7. **style:** Cambia aspectos de formato o estilo del código (sin cambiar la lógica).
   - Ejemplo: `style: aplicar formateo de acuerdo a PEP 8`

8. **build:** Cambia aspectos del sistema de build o dependencias.
   - Ejemplo: `build: actualizar pyproject.toml con nueva dependencia`

9. **ci:** Cambia configuraciones de CI/CD (integración continua).
   - Ejemplo: `ci: ajustar script para despliegue en producción`

10. **chore:** Cambios menores o tareas que no afectan el código (mantenimiento).
    - Ejemplo: `chore: eliminar dependencias no usadas`

11. **revert:** Revierte un commit anterior.
    - Ejemplo: `revert: eliminar commit que rompió la integración`

---

### **Scope (opcional)**
El *scope* indica qué parte del proyecto se afecta. Por ejemplo:
- **auth**, **audio**, **transcription**, **main**, **config**.

---

### **Ejemplos completos**
1. **Con `feat` y scope:**
   ```
   feat(audio): añadir detección de silencio en grabaciones
   ```

2. **Con `fix` y cuerpo explicativo:**
   ```
   fix(llm): manejar excepciones al generar respuestas

   Se solucionó un error donde el LLM devolvía nulo si la clasificación fallaba.
   ```

3. **Con cierre de issue:**
   ```
   fix(recorder): solucionar pérdida de chunks de audio al reconectar

   Closes #45
   ```

---

### Herramientas relacionadas

- **semantic-release**: Genera versiones automáticamente basadas en Conventional Commits.
- **commitlint**: Valida mensajes de commits para cumplir con esta convención.

Si estás trabajando en un equipo o quieres automatizar versiones (*semver*), **Conventional Commits** es útil porque permite que herramientas como *semantic-release* generen cambios de versión basados en estos tipos. 