---
name: create-endpoint
description: Crea un end-point nuevo dentro de un módulo existente siguiendo exactamente la estructura real del proyecto y genera DTOs solo si aplica.
---

# Objetivo

Crear un end-point nuevo en un proyecto con arquitectura limpia, respetando exactamente la estructura, estilo, nombres, imports, decorators, documentación y organización real del módulo indicado por el usuario.

Debes ser conservador:
- no inventes patrones
- no cambies la estructura del proyecto
- no recorras todo el repositorio
- no agregues explicaciones largas
- no muestres razonamientos extensos
- no generes salidas innecesarias

# Parámetros requeridos

Solicita solo si faltan:

- `MODULE_NAME`: módulo donde se debe crear el end-point
- `ENDPOINT_NAME`: nombre base del end-point o del caso que representa
- `HAS_DTO`: `true` o `false`

No hagas más preguntas si con eso puedes resolver.

# Instrucciones

## 1. Analiza antes de generar
Antes de crear cualquier archivo:

- ubica el módulo objetivo
- busca los controllers, routes o endpoints existentes dentro de ese módulo
- identifica el patrón real de:
  - nombre de archivo
  - nombre de clase
  - nombre de método
  - decorators
  - rutas
  - imports
  - DTOs
  - casos de uso inyectados
  - validaciones
  - manejo de parámetros
  - respuestas
  - JSDoc
  - estructura del constructor si aplica

Usa como prioridad:
1. endpoints del mismo módulo
2. endpoints similares de otros módulos solo si es estrictamente necesario
3. la estructura real del proyecto por encima de cualquier ejemplo externo

## 2. Limita el análisis al módulo indicado
No explores todo el proyecto.

Debes analizar solo el módulo indicado por el usuario y únicamente los archivos necesarios para construir el end-point correctamente.

Objetivo de este paso:
- determinar qué archivos escanear dentro del módulo
- identificar el patrón real del módulo
- reutilizar la estructura ya existente sin recorrer partes innecesarias del repositorio

Solo puedes salir del módulo si es estrictamente necesario para consultar una dependencia compartida, por ejemplo:
- clases base
- decorators comunes
- constantes compartidas
- enums comunes
- interfaces compartidas
- DTOs base
- contratos globales usados por el módulo

No hagas exploración amplia del repositorio.
No escanees módulos no relacionados.
No hagas búsquedas globales si el módulo ya contiene suficientes referencias.

## 3. Replica el patrón exacto del módulo
Debes copiar el estilo real del módulo en:

- estructura del archivo
- orden de imports
- orden de decorators
- orden de métodos
- nombres
- visibilidad
- uso de `readonly`
- JSDoc
- firma del método
- firma del constructor si existe
- uso de `async/await`
- patrón de respuesta
- patrón de inyección del use case o servicio correspondiente

No mejores el diseño.
No simplifiques.
No refactorices.
No cambies convenciones existentes.

## 4. Crea los archivos con saltos de línea CRLF
Todos los archivos nuevos o modificados deben guardarse usando finales de línea `CRLF`.

Reglas:
- respeta `CRLF` en el archivo final generado
- no mezcles `LF` y `CRLF`
- si el proyecto ya usa `CRLF`, mantén ese formato
- si el archivo de referencia del módulo usa `CRLF`, replica exactamente ese formato
- la salida final debe quedar lista para guardarse con `CRLF`

## 5. DTO condicional
### Si `HAS_DTO = true`
Debes crear o usar DTOs según el patrón real del módulo.

Valida en el código existente:
- dónde se ubican los DTOs
- cómo se nombran
- si usan interfaces, clases o types
- si existe DTO de request, response o ambos
- cómo se conectan al controller o endpoint
- cómo se documentan
- si usan validadores o decorators

Debes replicar exactamente ese patrón.

### Si `HAS_DTO = false`
No debes crear DTOs ni dejar referencias innecesarias a ellos.

Eso significa:
- no crear request DTO si no aplica
- no crear response DTO si el patrón del módulo no lo exige
- no dejar imports no usados
- no dejar tipos inventados
- no dejar validaciones ficticias

Si el módulo siempre exige un tipo aunque no haya parámetros, entonces usa el patrón real del módulo en vez de inventar uno nuevo.

## 6. Detecta qué debe crear realmente
Antes de escribir archivos, determina qué piezas se requieren de verdad según el módulo.

Por ejemplo, valida si para ese end-point normalmente se necesita:
- método nuevo dentro de un controller existente
- archivo controller nuevo
- ruta nueva
- DTO request
- DTO response
- actualización de index o barrel
- actualización de registro de dependencias
- conexión con use case existente o nuevo

Crea solo lo estrictamente necesario para que el end-point quede consistente con el módulo.

## 7. No inventes nombres
Valida contra el proyecto real antes de asumir nombres de:

- controller
- decorators
- rutas
- DTOs
- casos de uso
- servicios
- métodos
- constantes
- enums
- nombre del archivo
- ruta de import

Si algo no existe o no puede inferirse con seguridad, indícalo brevemente.

## 8. Usa solo dependencias necesarias
Incluye únicamente dependencias realmente usadas.

No dejes:
- imports no usados
- parámetros no usados
- métodos no usados
- DTOs no usados
- decorators innecesarios
- archivos huérfanos

## 9. Salida mínima
Responde solo con:

1. archivos a crear o modificar
2. código final
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
- no inventes rutas o decorators que el proyecto no use
- no mezcles estilos entre módulos
- no agregues helpers nuevos
- no escribas texto innecesario
- no muestres logs del proceso
- no imprimas razonamiento paso a paso
- no recorras el proyecto completo si el módulo objetivo basta para inferir el patrón

# Formato final obligatorio

## Archivos
- `<ruta 1>`
- `<ruta 2>`

## Código final
```ts
...codigo...