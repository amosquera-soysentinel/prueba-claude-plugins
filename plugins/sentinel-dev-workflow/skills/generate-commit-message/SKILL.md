Crea un commit siguiendo el estándar de Conventional Commits de Sentinel.

**Argumentos recibidos:** $ARGUMENTS
El formato de los argumentos es: `<tipo> <número-historia>` (ambos opcionales)
Ejemplo: `fix 32613`, `feat 0000`, `32613` o sin argumentos

## Pasos

1. Parsea los argumentos:
   - Si se reciben dos argumentos: el primero es el tipo, el segundo es el número de historia
   - Si se recibe un argumento que es un número: es el número de historia (el tipo se inferirá)
   - Si se recibe un argumento que es un tipo válido: es el tipo (el número de historia será `0000`)
   - Si no se recibe ningún argumento: tanto el tipo como el número se inferirán
   - Tipos válidos: `feat`, `fix`, `chore`, `docs`, `style`, `refactor`, `test`, `perf`, `build`, `ci`, `revert`
   - Número de historia por defecto: `0000`

2. Ejecuta `git diff HEAD` y `git status` para analizar los cambios actuales.

3. Con base en los archivos modificados y el contenido del diff, infiere el tipo si no fue proporcionado:
   - `feat` — se agregan archivos nuevos, componentes, servicios o funcionalidades
   - `fix` — se corrigen errores, comportamientos incorrectos o regresiones
   - `chore` — cambios en configuración, dependencias o archivos de build sin lógica de negocio
   - `docs` — solo se modifican comentarios o documentación
   - `style` — solo cambios de formato, indentación, orden de imports
   - `refactor` — reestructuración sin cambio de comportamiento observable
   - `test` — se agregan o modifican pruebas unitarias
   - `perf` — mejoras de rendimiento medibles
   - `build` — cambios en el proceso de build o bundling
   - `ci` — cambios en pipelines CI/CD

4. Con base en los archivos modificados y el contenido del diff:
   - Infiere el nombre de la funcionalidad afectada en **inglés y kebab-case** (máx. 4-5 palabras descriptivas). Por ejemplo: `relations-model-config`, `kendo-grid`, `transaction-filter`
   - Redacta una **descripción principal en español**, que inicie con "se" seguido de un verbo en infinitivo (agrega, corrige, ajusta, elimina, refactoriza...), máximo **60 caracteres**
   - Si hay cambios relevantes adicionales que no caben en 60 caracteres, redacta hasta dos descripciones adicionales en español, máximo **70 caracteres** cada una

5. Construye el mensaje del commit con el formato:
   ```
   <tipo>(<número>-<funcionalidad-kebab>): <descripción ≤60 chars>
   ```
   Ejemplos válidos:
   ```
   fix(32613-relations-model-config): se ajuste para evitar que se muestre el botón del editor
   feat(8786-notifications): se integra de funcionalidad para envío de notificaciones
   chore(0000-dependencies): se actualiza de librerías de kendo a la versión más reciente
   ```

6. **Antes de hacer el commit**, muestra al usuario:
   - El comando git que vas a ejecutar
   - Los archivos que se incluirán
   - Solicita confirmación explícita con: "¿Confirmas el commit con este mensaje? (sí/no)"

7. Si el usuario confirma, ejecuta el commit. Si hay archivos sin stagear que deberían incluirse, agrégalos primero.

## Reglas del estándar Sentinel

- El identificador va entre paréntesis junto al tipo: `fix(32613-feature-name):`
- Sin espacios entre el número y el nombre de funcionalidad (separados por `-`)
- Sin espacio antes de `:` al cerrar el paréntesis
- La descripción va después de `: ` (con espacio)
- La descripción NO lleva punto final
- La descripción inicia en minúscula
- Máximo 1 commit por PR para funcionalidades simples; usar `--amend` para ajustes de code review
- Si se necesita `--amend`, advertir al usuario antes de ejecutarlo

## Tipos válidos y cuándo usarlos

| Tipo | Cuándo usarlo |
|------|--------------|
| `feat` | Nueva funcionalidad, componente, servicio o endpoint |
| `fix` | Corrección de bug reportado por usuario o QA |
| `chore` | Mantenimiento: dependencias, configs, limpieza |
| `docs` | Solo documentación o comentarios |
| `style` | Formato, indentación, orden de imports (sin lógica) |
| `refactor` | Reestructuración sin cambio de comportamiento |
| `test` | Agregar o actualizar pruebas unitarias |
| `perf` | Mejora de rendimiento |
| `build` | Cambios en el proceso de build |
| `ci` | Cambios en pipelines CI/CD |
| `revert` | Revertir un commit anterior |
