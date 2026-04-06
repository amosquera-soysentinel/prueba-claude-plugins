---
name: create-usecase
description: Crea un use case nuevo siguiendo exactamente la estructura real del proyecto y agrega auditoría solo si aplica.
---

# Objetivo

Crear un use case nuevo dentro de un módulo existente, replicando exactamente la estructura, estilo, imports, nombres, patrón de constructor, documentación y organización de los use cases reales del proyecto.

Debes ser conservador:
- no inventes patrones
- no cambies la estructura del proyecto
- no agregues explicaciones largas
- no muestres razonamientos extensos
- no generes salidas innecesarias

# Parámetros requeridos

Solicita solo si faltan:

- `USE_CASE_NAME`: nombre del use case en PascalCase
- `MODULE_NAME`: módulo donde se creará
- `HAS_AUDIT`: `true` o `false`

No hagas más preguntas si con eso puedes resolver.

# Instrucciones

## 1. Analiza antes de generar
Antes de crear el archivo:

- ubica el módulo objetivo
- busca use cases existentes del mismo módulo
- identifica el patrón real de:
  - nombre de archivo
  - nombre de clase
  - imports
  - interfaces
  - DTOs
  - repositorio
  - constructor
  - `runUseCase`
  - métodos privados
  - JSDoc
  - auditoría si existe

Usa como prioridad:
1. use cases del mismo módulo
2. use cases similares de otros módulos
3. código de referencia entregado por el usuario

## 2. Replica el patrón exacto del proyecto
Debes copiar el estilo real del repositorio en:

- estructura del archivo
- orden de imports
- orden de propiedades
- orden de métodos
- nombres
- visibilidad
- uso de `readonly`
- JSDoc
- firma del constructor
- firma de métodos
- uso de `async/await`

No mejores el diseño.
No simplifiques.
No refactorices.
No cambies convenciones existentes.

## 3. Auditoría condicional
### Si `HAS_AUDIT = true`
Incluye auditoría solo si el proyecto realmente usa ese patrón.

Debes replicar exactamente lo existente:
- imports de auditoría
- inyección de dependencias
- uso de `AuditGenerator`
- `LogType`
- `LogAction`
- `createAuditUser`
- `getAuditCache`
- `cacheManager`
- `moduleName`
- método `registerAudit` o equivalente
- punto exacto donde se invoca

### Si `HAS_AUDIT = false`
No incluyas nada de auditoría:
- sin imports de auditoría
- sin `auditGenerator`
- sin `cacheManager` si solo era para auditoría
- sin `moduleName` si solo era para auditoría
- sin `registerAudit`
- sin código muerto

## 4. Usa solo dependencias necesarias
Incluye únicamente dependencias realmente usadas.

No dejes:
- imports no usados
- propiedades no usadas
- parámetros no usados
- métodos no usados

## 5. No inventes nombres
Valida contra el proyecto real antes de asumir nombres de:

- interfaces
- DTOs
- repositorios
- métodos del repositorio
- enums
- rutas de import
- nombre del archivo

Si algo no existe o no puede inferirse con seguridad, indícalo brevemente.

## 6. Salida mínima
Responde solo con:

1. ruta objetivo
2. código final del use case
3. observaciones mínimas solo si falta algo o hubo una inconsistencia

No incluyas:
- análisis extensos
- resúmenes largos
- explicaciones del proceso
- listas de validaciones completadas
- texto redundante

Si todo está claro, entrega directamente el resultado.

# Restricciones

- no inventes carpetas nuevas
- no inventes DTOs si ya existen
- no inventes métodos de repositorio
- no mezcles estilos entre módulos
- no dejes lógica parcial de auditoría
- no agregues helpers nuevos
- no escribas texto innecesario
- no muestres logs del proceso
- no imprimas razonamiento paso a paso

# Referencia de comportamiento

Usa el código entregado por el usuario solo como referencia funcional, no como plantilla absoluta. La prioridad siempre es el patrón real del proyecto.

# Formato final obligatorio

## Ruta objetivo
`<ruta>`

## Código final
```ts
...codigo...