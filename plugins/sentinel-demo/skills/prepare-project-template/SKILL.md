---
name: bootstrap-project-from-zip
description: Extrae un proyecto base desde un archivo zip ubicado en la raíz, analiza su estructura, solicita o usa parámetros de personalización, reemplaza variables de configuración, elimina el módulo demo y limpia archivos/configuración sobrante para dejar una nueva base de proyecto consistente.
---

# Bootstrap Project From Zip

## Propósito
Esta skill toma un proyecto base comprimido en un archivo `.zip` ubicado en la carpeta raíz del workspace, lo extrae, analiza su estructura real y lo transforma en un nuevo proyecto eliminando el módulo `demo` y ajustando configuraciones clave.

## Cuándo usar esta skill
Usa esta skill cuando:
- exista un proyecto base empaquetado en un `.zip`
- se necesite crear una nueva base a partir de ese template
- se deban reemplazar valores del `.env` y `package.json`
- se deba eliminar completamente el módulo `demo`
- se requiera dejar el proyecto limpio y consistente después de la personalización

No uses esta skill si:
- el proyecto ya está extraído y no hay zip en la raíz
- no se desea modificar estructura ni eliminar el módulo `demo`
- se requiere solamente un cambio puntual y no un bootstrap completo

---

## Entradas esperadas

La skill debe intentar usar estos parámetros si fueron proporcionados por el usuario o por el comando que invoca la skill.

### Parámetros requeridos
- `NAME`
- `PORT`
- `PROJECT_INITIALS`
- `ROUTER_COMPONENT`
- `ISSUER`
- `PACKAGE_NAME`

### Parámetros opcionales
- `ZIP_FILE_NAME`: nombre exacto del archivo zip si el usuario lo proporciona
- `EXTRACT_FOLDER_NAME`: nombre de la carpeta destino para la extracción, si aplica

Si faltan parámetros requeridos, debes solicitarlos antes de ejecutar cambios.

---

## Reglas obligatorias

1. **No modifiques ningún archivo antes de terminar el análisis inicial.**
2. **No inventes rutas.** Debes trabajar únicamente con la estructura real encontrada.
3. **No elimines archivos fuera del alcance definido.**
4. Si existen múltiples ubicaciones posibles para el módulo `demo`, debes detectarlas todas y reportarlas.
5. Si encuentras referencias indirectas al módulo `demo`, debes limpiarlas también para evitar imports rotos.
6. Si algún archivo o variable no existe, debes reportarlo sin fallar innecesariamente.
7. Debes priorizar dejar el proyecto consistente por encima de seguir ciegamente una instrucción incompatible con la estructura real.

---

## Flujo de ejecución

### Paso 1. Detectar el zip en raíz
- Busca en la carpeta raíz del workspace un archivo `.zip`.
- Si se recibió `ZIP_FILE_NAME`, úsalo como prioridad.
- Si hay varios `.zip`, identifica el más probable como proyecto base y repórtalo.
- Si no existe ningún `.zip`, detén la ejecución y explica el problema.

### Paso 2. Extraer el contenido
- Extrae el `.zip` en una carpeta de trabajo.
- Si se recibió `EXTRACT_FOLDER_NAME`, úsalo.
- Si no, usa una carpeta con nombre claro derivado del zip o del proyecto.
- Confirma que la extracción fue exitosa antes de continuar.

### Paso 3. Analizar la estructura
Inspecciona la estructura del proyecto extraído e identifica como mínimo:

- archivo `.env`
- archivo `package.json`
- ubicación del módulo `demo`
- referencias al módulo `demo` en:
  - módulos
  - rutas
  - imports
  - exports
  - bootstrap
  - configuración
  - test
  - mocks
  - fixtures
- archivo:
  - `src\modules\common\application\enum\action-upsert.enum.ts`

Debes reportar:
- estructura general encontrada
- archivos clave detectados
- ubicación exacta de cada coincidencia del módulo `demo`
- posibles dependencias o referencias que deban ajustarse al eliminarlo

### Paso 4. Validar parámetros requeridos
Debes verificar si ya tienes estos valores:

- `NAME`
- `PORT`
- `PROJECT_INITIALS`
- `ROUTER_COMPONENT`
- `ISSUER`
- `PACKAGE_NAME`

Si falta uno o más, solicita solamente los faltantes.
No continúes con los cambios hasta tenerlos todos.

### Paso 5. Reemplazar configuraciones
Una vez tengas todos los parámetros:

#### En `.env`
Reemplaza los valores de:
- `NAME`
- `PORT`
- `PROJECT_INITIALS`
- `ROUTER_COMPONENT`
- `ISSUER`

Además elimina completamente la línea o variable:
- `PARALLEL_PROMISES_LIMIT`

#### En `package.json`
Reemplaza:
- `name` con el valor de `PACKAGE_NAME`

### Paso 6. Eliminar el módulo demo
Debes eliminar completamente todo lo relacionado con el módulo `demo`.

Esto incluye, cuando exista:
- carpeta del módulo `demo`
- controladores
- servicios
- casos de uso
- repositorios
- entidades
- DTOs
- interfaces
- enums
- registros de módulo
- imports y exports
- rutas
- archivos de configuración
- pruebas unitarias
- pruebas de integración
- pruebas e2e
- mocks
- fixtures
- referencias en bootstrap o loaders

Después de eliminarlo, ajusta cualquier referencia residual para que el proyecto no quede inconsistente.

### Paso 7. Eliminar archivo adicional
Elimina el archivo:

- `src\modules\common\application\enum\action-upsert.enum.ts`

Si no existe, repórtalo sin marcar la ejecución como fallida.

### Paso 8. Validaciones finales
Después de todos los cambios, valida como mínimo:

- que no existan referencias remanentes al módulo `demo`
- que no existan imports rotos evidentes causados por la eliminación
- que `.env` contenga:
  - `NAME`
  - `PORT`
  - `PROJECT_INITIALS`
  - `ROUTER_COMPONENT`
  - `ISSUER`
  con los nuevos valores
- que `.env` ya no contenga `PARALLEL_PROMISES_LIMIT`
- que `package.json` tenga el nuevo `name`
- que el archivo `src\modules\common\application\enum\action-upsert.enum.ts` ya no exista
- que la estructura resultante siga siendo coherente

Si detectas problemas, repórtalos claramente.

---

## Estrategia de trabajo esperada
Trabaja siempre en este orden:

1. detectar zip
2. extraer
3. analizar
4. pedir parámetros faltantes
5. reemplazar configuraciones
6. eliminar módulo demo
7. eliminar archivo adicional
8. validar consistencia
9. entregar resumen final

No alteres este orden salvo que la estructura real del proyecto lo exija para mantener consistencia.

---

## Formato de salida

Tu respuesta debe estar organizada en estas secciones:

### 1. Hallazgos del análisis
Incluye:
- zip detectado
- carpeta extraída
- estructura general encontrada
- ubicación de `.env`
- ubicación de `package.json`
- ubicación de módulo `demo`
- referencias relevantes encontradas
- existencia o ausencia de `action-upsert.enum.ts`

### 2. Parámetros requeridos
Si faltan datos, solicita únicamente los faltantes.

### 3. Plan de cambios
Resume brevemente:
- qué archivos serán modificados
- qué carpetas/archivos serán eliminados
- qué referencias serán ajustadas

### 4. Resultado final
Al finalizar, incluye:
- archivos modificados
- archivos eliminados
- carpetas eliminadas
- referencias limpiadas
- validaciones realizadas
- advertencias o pendientes

---

## Criterios de éxito
La ejecución se considera exitosa si:
- el zip fue extraído correctamente
- el proyecto fue analizado antes de modificar
- se actualizaron correctamente `.env` y `package.json`
- se eliminó todo lo relacionado con `demo`
- se eliminó `PARALLEL_PROMISES_LIMIT`
- se eliminó `src\modules\common\application\enum\action-upsert.enum.ts`
- no quedaron referencias obvias rotas relacionadas con lo eliminado
- se entregó un resumen claro y verificable

---

## Manejo de errores
Si ocurre algún problema:
- explica exactamente qué falló
- indica en qué paso ocurrió
- muestra qué sí alcanzó a validarse o modificarse
- no afirmes que el proceso terminó correctamente si hay errores no resueltos

---

## Notas adicionales
- Si el proyecto tiene una arquitectura distinta, adapta la ejecución a la estructura encontrada sin salirte del alcance funcional pedido.
- Si hay múltiples coincidencias ambiguas para `demo`, debes reportarlas y resolverlas de la forma más consistente con la arquitectura del proyecto.
- Si la eliminación del módulo `demo` obliga a ajustar imports, barrels o registros de módulos, debes hacerlo.