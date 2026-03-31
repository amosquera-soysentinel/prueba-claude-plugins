# Skill: Configuración Rápida de Proyecto desde ZIP

Extrae un proyecto base desde un archivo zip, reemplaza variables de configuración, limpia referencias heredadas, instala dependencias y ejecuta tests.

---

## Cuándo usar
- Existe un `.zip` en la raíz del workspace
- Se necesita crear un nuevo proyecto desde ese template
- Se requiere personalización básica de configuración

No usar si:
- No hay `.zip` en raíz
- El proyecto ya está configurado
- Solo se necesita un cambio puntual

---

## Parámetros

### Requeridos
- `NAME`: nombre del proyecto
- `DESCRIPTION`: descripción del proyecto

### Opcionales con defaults
- `PORT` (default: `3000`)
- `PROJECT_INITIALS` (default: primeras 3 letras de NAME en mayúsculas)
- `ROUTER_COMPONENT` (default: `${NAME}Router`)
- `ISSUER` (default: `localhost`)
- `ZIP_FILE_NAME` (default: auto-detectar)
- `COVERAGE_TARGET` (default: `90`)
- `MAX_TEST_RETRIES` (default: `2`)
- `VERBOSE` (default: `false`)

---

## Ejecución

### 1. Detectar y extraer ZIP
- Buscar `.zip` en raíz (usar `ZIP_FILE_NAME` si se proporciona)
- Extraer directamente al mismo nivel, sin carpeta adicional
- Identificar raíz del proyecto (buscar `package.json`)

### 2. Aplicar parámetros (solo si faltan `NAME` o `DESCRIPTION`, solicítalos)

Calcular defaults:
```javascript
PROJECT_INITIALS = PROJECT_INITIALS || NAME.substring(0,3).toUpperCase()
ROUTER_COMPONENT = ROUTER_COMPONENT || `${NAME}Router`
```

### 3. Reemplazos automáticos

**`.env`:**
```env
NAME=${NAME}
PORT=${PORT}
PROJECT_INITIALS=${PROJECT_INITIALS}
ROUTER_COMPONENT=${ROUTER_COMPONENT}
ISSUER=${ISSUER}
# Eliminar línea: PARALLEL_PROMISES_LIMIT
```

**`package.json`:**
```json
{
  "name": "${NAME}",
  "description": "${DESCRIPTION}"
}
```

**`README.md`:**
- Insertar `${DESCRIPTION}` en línea 3

**Búsqueda global (solo en estos paths):**
- `package.json`, `.env`, `README.md`, `src/**/*.ts`
- Reemplazar `BackendTsTemplate` → `${NAME}`
- Reemplazar `backend-ts-template` → `${NAME}`

**Eliminar:**
- `src\modules\common\application\enum\action-upsert.enum.ts`

### 4. Instalación y tests
```bash
pnpm install
pnpm test --coverage

# Si coverage < COVERAGE_TARGET, ajustar tests (máximo MAX_TEST_RETRIES intentos)
```

### 5. Limpieza
- Eliminar archivo `.zip`

---

## REGLA CRÍTICA: Formato CRLF

**TODOS los archivos generados DEBEN usar `\r\n` (CRLF)**. Si la herramienta usa LF por defecto, convertir explícitamente a CRLF.

---

## Formato de salida

### Si `VERBOSE=false` (default):
```
✅ Proyecto configurado exitosamente

Cambios aplicados:
- Nombre: ${NAME}
- Puerto: ${PORT}
- Coverage: ${COVERAGE_ACTUAL}%

⚠️ Advertencias: [si hay]
```

### Si `VERBOSE=true`:
```
### Configuración aplicada
- ZIP: [nombre]
- Raíz: [path]
- Archivos modificados: [lista]
- Referencias limpiadas: [cantidad]

### Validaciones
✅ .env actualizado
✅ package.json actualizado
✅ README.md línea 3 actualizado
✅ Referencias heredadas eliminadas
✅ Dependencias instaladas
✅ Tests: PASS
✅ Coverage: ${COVERAGE_ACTUAL}%
✅ ZIP eliminado

⚠️ Advertencias: [si hay]
❌ Errores: [si hay]
```

---

## Criterios de éxito
- `.env` y `package.json` actualizados
- `README.md` línea 3 contiene `DESCRIPTION`
- Referencias heredadas reemplazadas
- `PARALLEL_PROMISES_LIMIT` eliminado
- `action-upsert.enum.ts` eliminado
- `pnpm install` exitoso
- `pnpm test` exitoso
- Coverage ≥ `COVERAGE_TARGET`%
- `.zip` eliminado

---

## Manejo de errores

**Si falla instalación o tests:** Reportar error y detener.

**Si coverage < target después de MAX_TEST_RETRIES:** Reportar estado actual y continuar.

**Si falla eliminación del .zip:** Continuar (advertencia).

**Formato de error:**
```
❌ Fallo en: [paso]
Detalle: [mensaje de error principal]
Estado: [qué se completó exitosamente]
```

---