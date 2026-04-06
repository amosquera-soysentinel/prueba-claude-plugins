---
name: create-usecase
description: Crea un use case nuevo siguiendo exactamente la estructura real del proyecto y agrega auditoría solo si aplica.
---

# Objetivo
Crear un use case dentro de un módulo existente, replicando exactamente la estructura, estilo, imports, nombres, patrón de constructor, documentación y organización del proyecto.

# Parámetros requeridos
Solicita solo si no están presentes:
- `USE_CASE_NAME`: PascalCase
- `MODULE_NAME`: módulo destino
- `HAS_AUDIT`: `true` o `false`

# Instrucciones

## 1. Análisis previo (solo el módulo indicado)
Antes de generar, analiza únicamente el módulo objetivo. Identifica:
- nombre de archivo, clase, imports, interfaces, DTOs, repositorio
- constructor, `runUseCase`, métodos privados, JSDoc
- patrón de auditoría si `HAS_AUDIT = true`

Solo sal del módulo para consultar dependencias compartidas realmente usadas (`BaseUseCase`, enums, interfaces globales, utilidades de auditoría). No hagas exploración amplia.

Prioridad de referencia:
1. Use cases del mismo módulo
2. Use cases similares de otros módulos
3. Código entregado por el usuario (como referencia funcional, no plantilla)

## 2. Replica el patrón exacto
Copia fielmente: estructura, orden de imports/propiedades/métodos, nombres, visibilidad, `readonly`, JSDoc, firmas, `async/await`. No mejores, no refactorices, no cambies convenciones.

## 3. Auditoría condicional
**`HAS_AUDIT = true`:** incluye exactamente lo que usa el proyecto: imports, inyección, `AuditGenerator`, `LogType`, `LogAction`, `createAuditUser`, `getAuditCache`, `cacheManager`, `moduleName`, `registerAudit` y el punto de invocación.

**`HAS_AUDIT = false`:** omite todo lo anterior sin dejar código muerto.

## 4. Reglas generales
- Solo incluye dependencias, imports y propiedades realmente usados
- No inventes nombres: valida interfaces, DTOs, repositorios, métodos y rutas contra el proyecto
- Si algo no puede inferirse con seguridad, indícalo brevemente
- Archivos con finales de línea `CRLF`, sin mezclar con `LF`

# Salida
Responde únicamente con:
1. Ruta objetivo
2. Código final

Agrega observaciones solo si falta algo o hay una inconsistencia. Sin análisis, resúmenes ni explicaciones del proceso.

## Ruta objetivo
`<ruta>`

## Código final
```ts
...codigo...
```