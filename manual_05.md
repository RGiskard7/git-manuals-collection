# Flujo típico de Trabajo Profesional con Git y GitHub

### **Flujo típico**

1. **Ramas del proyecto en GitHub**:
   - **`main` o `master`**: Contiene el código estable que está listo para producción. Solo se fusionan cambios que han sido probados y revisados.
   - **`develop` o `development`**: Rama para desarrollo activo. Aquí se integran los cambios de los desarrolladores antes de fusionarse con `main`.

2. **Tu trabajo como desarrollador**:
   - Haces un **fork** del repositorio principal en GitHub. Esto crea una copia del proyecto en tu cuenta, en la que tienes control total.
   - **Clonas** tu fork en tu máquina local:
     ```bash
     git clone <URL-de-tu-fork>
     ```
   - Configuras el repositorio remoto del proyecto principal como `upstream` para mantener tu fork actualizado:
     ```bash
     git remote add upstream <URL-del-repositorio-principal>
     ```

3. **Crear una rama de trabajo**:
   - Basándote en `develop` (o la rama que indique la política del proyecto), creas una nueva rama para los cambios que harás:
     ```bash
     git checkout -b feature/nombre-de-tu-cambio develop
     ```

4. **Desarrollar y realizar commits**:
   - Realizas tus cambios localmente y haces commits con descripciones claras:
     ```bash
     git add .
     git commit -m "Descripción clara de los cambios"
     ```

5. **Sincronizar con `develop`**:
   - Antes de enviar tus cambios, asegúrate de que tu rama esté sincronizada con los últimos cambios en `develop`:
     ```bash
     git fetch upstream
     git merge upstream/develop
     ```
     (O `git rebase` si el equipo prefiere evitar commits de merge.)

6. **Subir cambios a tu fork**:
   - Envías tus cambios a tu fork en GitHub:
     ```bash
     git push origin feature/nombre-de-tu-cambio
     ```

7. **Crear un Pull Request (PR)**:
   - En GitHub, creas un Pull Request desde tu rama (`feature/nombre-de-tu-cambio`) en tu fork hacia la rama `develop` del repositorio principal.
   - Proporcionas una descripción detallada del PR, explicando qué problema resuelve o qué funcionalidad añade, cómo probarlo, y cualquier otro contexto relevante.

8. **Revisión del PR**:
   - Un encargado (como un líder técnico o revisor) revisa tu PR. Puede solicitar cambios, añadir comentarios o sugerir mejoras.
   - Respondes a los comentarios, haces los cambios necesarios, y actualizas tu PR subiendo nuevos commits o haciendo un `git rebase` y `git push --force`.

9. **Fusión del PR**:
   - Una vez aprobado, el encargado fusiona tu PR con la rama `develop`. Dependiendo de la política del equipo, podría hacerse un **merge commit**, un **squash merge** o un **rebase**.

---

### **Ventajas de este flujo de trabajo**
- **Aislamiento de cambios**: Tus cambios están en una rama separada hasta que se aprueben.
- **Revisión de calidad**: Los PR permiten que otros revisen el código antes de que se integre.
- **Colaboración fluida**: Facilita el trabajo en equipo y la resolución de conflictos.
- **Historial claro**: Las ramas y PRs documentan qué se ha cambiado y por qué.

---

### **Extras que podrían ser útiles**
- **Pruebas automatizadas**: Es habitual que un PR dispare un pipeline de CI/CD para ejecutar pruebas automáticas antes de que se fusione.
- **Protección de ramas**: Las ramas principales (`main`, `develop`) suelen estar protegidas para evitar fusiones sin revisión o sin pasar pruebas automáticas.
- **Políticas de código limpio**: Es común que haya guías sobre estilos de código, estándares, y convenciones que debas seguir.

Este flujo (con pequeñas variaciones) se utiliza en metodologías como **Git Flow**, **GitHub Flow**, o **Trunk-Based Development**, dependiendo de la preferencia del equipo.