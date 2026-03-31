Analiza la estructura del proyecto actual, detecta todas las referencias al módulo `demo`, elimínalo completamente junto con sus dependencias, ajusta imports y pruebas, y verifica que el proyecto quede consistente y con 100% de coverage.

## Propósito
Elimina de forma exhaustiva y segura el módulo `demo` de un proyecto backend TypeScript, incluyendo:
- carpetas y archivos del módulo
- controladores, servicios, casos de uso, repositorios
- entidades, DTOs, interfaces, enums
- registros de módulo, imports y exports
- rutas y archivos de configuración
- pruebas unitarias, de integración y e2e
- mocks, fixtures
- referencias en bootstrap o loaders
- cualquier referencia residual que pueda generar inconsistencias

Después de la eliminación, ajusta pruebas y código para mantener 100% de coverage.

---

## Cuándo usar esta skill
Usa esta skill cuando:
- existe un módulo `demo` en el proyecto que debe eliminarse
- se requiere limpiar referencias heredadas de un template base
- se necesita dejar el proyecto sin código de ejemplo o demostración
- se busca mantener la consistencia del proyecto después de eliminar el módulo

No uses esta skill si:
- no existe un módulo `demo` en el proyecto
- el módulo `demo` debe conservarse por razones funcionales
- solo se requiere modificar el módulo sin eliminarlo

---

## Entradas esperadas

### Parámetros
No se requieren parámetros externos. Esta skill trabaja con la estructura actual del proyecto.

---

## Reglas obligatorias

1. No modifiques ningún archivo antes de terminar el análisis inicial completo.
2. No inventes rutas. Trabaja únicamente con la estructura real encontrada.
3. Detecta TODAS las ubicaciones posibles del módulo `demo` antes de eliminar.
4. Si existen múltiples ubicaciones, repórtalas todas antes de proceder.
5. Identifica referencias indirectas (imports, exports, registros) y elimínalas también.
6. Después de eliminar, ajusta cualquier referencia residual para evitar imports rotos.
7. Ejecuta `pnpm test` después de cada eliminación importante.
8. Si el coverage baja, ajusta las pruebas inmediatamente.
9. No finalices hasta alcanzar 100% de coverage nuevamente.
10. Reporta claramente cualquier bloqueo o inconsistencia detectada.

---

## Flujo de ejecución

### Paso 1. Análisis exhaustivo de la estructura
Inspecciona todo el proyecto y detecta:

- Ubicación principal del módulo `demo` (ej: `src/modules/demo`)
- Archivos del módulo:
  - controladores (ej: `demo.controller.ts`)
  - servicios (ej: `demo.service.ts`)
  - casos de uso (ej: `create-demo.use-case.ts`)
  - repositorios (ej: `demo.repository.ts`)
  - entidades (ej: `demo.entity.ts`)
  - DTOs (ej: `create-demo.dto.ts`, `update-demo.dto.ts`)
  - interfaces (ej: `demo.interface.ts`)
  - enums (ej: `demo-status.enum.ts`)
  - módulos (ej: `demo.module.ts`)
  
- Referencias en otros archivos:
  - imports del módulo `demo` en otros módulos
  - exports del módulo `demo` en barrels o índices
  - registros en `app.module.ts` o bootstrap
  - rutas registradas en configuración de routing
  - configuraciones específicas del módulo
  
- Pruebas relacionadas:
  - tests unitarios (ej: `demo.service.spec.ts`)
  - tests de integración (ej: `demo.integration.spec.ts`)
  - tests e2e (ej: `demo.e2e-spec.ts`)
  - mocks (ej: `demo.mock.ts`)
  - fixtures (ej: `demo.fixture.ts`)

- Estado actual de coverage:
  - porcentaje global
  - archivos con menor cobertura
  - líneas, ramas o funciones sin cubrir

Reporta:
- estructura del módulo `demo` encontrada
- cantidad de archivos detectados
- ubicaciones exactas
- referencias en otros archivos
- pruebas relacionadas
- coverage actual antes de la eliminación

### Paso 2. Plan de eliminación
Genera un plan detallado que incluya:

1. Archivos a eliminar (listado completo)
2. Carpetas a eliminar
3. Imports a remover de otros archivos
4. Exports a remover de barrels
5. Registros de módulo a eliminar
6. Rutas a desregistrar
7. Pruebas a eliminar
8. Mocks/fixtures a eliminar
9. Archivos que necesitarán ajustes después de la eliminación

Solicita confirmación antes de proceder (opcional, según contexto).

### Paso 3. Eliminación del módulo demo

#### 3.1 Eliminar archivos y carpetas principales
- Elimina la carpeta principal del módulo `demo` con todo su contenido
- Confirma que la eliminación fue exitosa

#### 3.2 Limpiar imports y referencias
- Busca en todo el proyecto imports que referencien al módulo `demo`
- Elimina esos imports
- Busca exports en archivos índice (barrels) que referencien `demo`
- Elimina esos exports
- Verifica archivos de configuración de rutas
- Elimina registros del módulo `demo`

#### 3.3 Ajustar registros de módulos
- Busca en `app.module.ts` o archivos equivalentes
- Elimina el registro del módulo `demo` del array de imports
- Elimina imports del archivo si ya no se usan
- Busca en archivos de bootstrap o loaders
- Elimina cualquier referencia al módulo `demo`

#### 3.4 Eliminar pruebas relacionadas
- Elimina todos los archivos de prueba del módulo `demo`
- Elimina mocks y fixtures relacionados
- Si existen pruebas en otros módulos que dependan de `demo`, ajústalas o elimínalas

### Paso 4. Validación intermedia
- Ejecuta `pnpm test` para verificar que no hay imports rotos
- Si hay errores de compilación, repórtalos y ajústalos
- Verifica que el proyecto compile correctamente
- Analiza el coverage actual

### Paso 5. Ajuste de coverage
Si el coverage bajó después de la eliminación:

- Identifica qué archivos perdieron cobertura
- Analiza qué caminos, ramas o funciones quedaron sin cubrir
- Ajusta las pruebas existentes para cubrir esos casos
- Si es necesario, crea nuevas pruebas
- Vuelve a ejecutar `pnpm test`
- Repite hasta alcanzar 100% de coverage

### Paso 6. Validaciones finales
Verifica:

- ✅ No existen carpetas del módulo `demo`
- ✅ No existen archivos del módulo `demo`
- ✅ No hay imports rotos relacionados con `demo`
- ✅ No hay referencias a `demo` en registros de módulos
- ✅ No hay rutas registradas del módulo `demo`
- ✅ No hay pruebas relacionadas con `demo`
- ✅ `pnpm test` ejecuta correctamente
- ✅ El coverage es del 100%
- ✅ El proyecto compila sin errores
- ✅ La estructura resultante es coherente

Si alguna validación falla, repórtala claramente.

---

## Estrategia de trabajo esperada

1. Análisis exhaustivo de ubicaciones y referencias del módulo `demo`
2. Generación de plan detallado de eliminación
3. Eliminación de archivos y carpetas principales
4. Limpieza de imports, exports y registros
5. Eliminación de pruebas relacionadas
6. Validación intermedia con `pnpm test`
7. Ajuste de pruebas para mantener 100% coverage
8. Validaciones finales de consistencia
9. Reporte de resultados

No alteres este orden salvo necesidad técnica justificada.

---

## REGLA OBLIGATORIA — ARCHIVOS CON FORMATO CRLF

**TODOS** los archivos modificados DEBEN mantener terminación de línea **CRLF** (`\r\n`).

- Al modificar archivos existentes, conserva el formato CRLF.
- Si se crean nuevos archivos de prueba, usa CRLF.
- Esto aplica a **TODOS** los archivos: `.ts`, `.json`, `.md`, etc.

---

## Formato de salida

### 1. Hallazgos del análisis
- ubicación del módulo `demo` detectada
- cantidad de archivos encontrados
- listado de archivos principales
- referencias encontradas en otros módulos
- pruebas relacionadas detectadas
- coverage actual antes de la eliminación

### 2. Plan de eliminación
- archivos a eliminar (listado completo)
- carpetas a eliminar
- imports a limpiar
- exports a limpiar
- registros a ajustar
- pruebas a eliminar

### 3. Resultado de la eliminación
- archivos eliminados (confirmación)
- carpetas eliminadas
- imports limpiados
- exports limpiados
- registros ajustados
- pruebas eliminadas

### 4. Resultado de validaciones
- resultado de `pnpm test` después de la eliminación
- errores de compilación detectados (si existen)
- coverage después de la eliminación
- ajustes realizados para recuperar coverage

### 5. Validaciones finales
- confirmación de eliminación completa
- confirmación de ausencia de referencias rotas
- confirmación de 100% coverage
- advertencias o problemas pendientes (si existen)

---

## Criterios de éxito

La ejecución se considera exitosa si:

- ✅ El módulo `demo` fue eliminado completamente
- ✅ No quedan referencias al módulo `demo` en el proyecto
- ✅ No hay imports rotos
- ✅ `pnpm test` ejecuta correctamente
- ✅ El coverage es del 100%
- ✅ El proyecto compila sin errores
- ✅ Se entregó un reporte claro y verificable

---

## Manejo de errores

Si ocurre algún problema:
- explica exactamente qué falló y en qué paso
- muestra qué sí alcanzó a eliminarse o ajustarse
- si hay errores de compilación, muéstralos completos
- si el coverage no alcanzó 100%, reporta qué falta cubrir
- no afirmes que el proceso terminó correctamente si hay errores no resueltos

---

## Notas adicionales

- Si el proyecto tiene múltiples módulos `demo` (ej: `demo-users`, `demo-posts`), detecta y repórtalos todos.
- Si la arquitectura usa nombres diferentes para el módulo de ejemplo, adáptate pero mantén el objetivo funcional.
- Si la eliminación obliga a ajustar otros módulos que dependían de `demo`, hazlo cuidadosamente.
- Si existen pruebas compartidas que usan datos del módulo `demo`, ajústalas para usar datos de otros módulos o crea fixtures genéricos.