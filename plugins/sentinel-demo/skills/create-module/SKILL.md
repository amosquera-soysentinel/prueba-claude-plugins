Genera un módulo CRUD para un proyecto Sentinel en Express.js + TypeScript + Awilix, replicando exactamente la estructura, organización y estilo de los módulos de negocio ya existentes en el proyecto.

## Objetivo
Crear un nuevo módulo CRUD siguiendo **el patrón real del proyecto**, tanto en:
- estructura de carpetas
- ubicación de archivos
- nombres
- estilo de implementación
- firmas
- herencia
- forma de inyección
- logging
- JSDoc
- validaciones
- registro en container
- registro en router
- aliases
- convenciones internas

**La prioridad no es inventar una solución nueva, sino copiar el patrón real existente y adaptarlo al nuevo módulo.**

---

## Parámetros esperados

### Requerido
- `MODULE_NAME`: nombre del nuevo módulo

### Opcional
- `ENTITY_FIELDS`: definición de campos de la entidad
- `GENERATE_TESTS`: `true` o `false` (por defecto `false`)

Si no se proporcionan campos, usa:
- `id: number`
- `name: string`
- `description: string`
- `isActive: boolean`
- `createdAt: Date`
- `updatedAt: Date`

---

## Regla principal de ahorro de cuota

Minimiza consumo:
- no hagas inventarios completos del proyecto
- no listes árboles enormes si no son necesarios
- no expliques decisiones obvias
- no analices más de lo necesario
- no repitas reglas ya aplicadas
- no generes variantes alternativas
- no propongas caminos distintos al patrón existente
- no uses estructuras genéricas si puedes copiar una real

Trabaja así:
1. detectar patrón real
2. elegir módulo de referencia
3. clonar patrón estructural y de contenido
4. adaptar nombres y tipos
5. registrar módulo
6. validar reglas críticas
7. finalizar

---

## FASE 1 — Lectura mínima obligatoria

Antes de crear archivos, lee solo estos documentos si existen:

1. `../../docs/conventions/hard-rules.md`
2. `../../docs/conventions/naming-rules.md`
3. `../../docs/conventions/typescript-rules.md`
4. `../../docs/conventions/documentation-rules.md`
5. `../../docs/conventions/generation-constraints.md`

Lee `testing-rules.md` y `sonar-rules.md` **solo si**:
- `GENERATE_TESTS=true`, o
- el proyecto ya exige pruebas junto al módulo

Si algún archivo obligatorio no existe, continúa con el patrón real del proyecto y repórtalo brevemente.

---

## FASE 2 — Detección del patrón real del proyecto

### Paso 2.1 — Elegir referencias
Analiza únicamente:

1. `src/modules/common`
2. **un solo módulo de negocio existente** que esté más completo y sea representativo del proyecto

No analices todos los módulos.  
No recorras `src/modules/` de forma exhaustiva si no es necesario.  
Solo identifica el módulo de negocio más útil como referencia.

### Paso 2.2 — Extraer patrón estructural real
A partir del módulo de negocio de referencia, detecta:

- carpetas reales del módulo
- subcarpetas reales
- archivos reales del módulo
- ubicación real de:
  - entity
  - interface
  - enum
  - dto
  - use-case
  - service
  - controller
  - repository
  - router
  - container

Construye un **mapa de ubicaciones reales** y úsalo como única fuente de verdad.

### Paso 2.3 — Extraer patrón de contenido real
Además de la estructura, inspecciona un archivo real de cada tipo que exista en el módulo de referencia:

- un controller
- un router
- un repository
- un use case
- un application service
- el container del módulo

Y extrae de ellos el patrón real de:

- orden de imports
- alias usados
- estilo de clase
- herencia
- firma de constructor
- destructuring de dependencias
- nombres de propiedades privadas
- estilo de logs
- JSDoc
- manejo de errores
- tipado
- forma de respuesta HTTP
- patrón de validación
- patrón de registro en Awilix
- patrón de router con adapter
- nombres y sufijos reales

### Paso 2.4 — Regla obligatoria de replicación exacta
El nuevo módulo debe respetar **no solo la estructura**, sino también el **contenido y forma de implementación** del módulo de referencia.

Eso significa:

- si el proyecto usa `infrastructure/http/controller/`, usa esa ruta
- si el proyecto usa `infrastructure/controller/`, usa esa ruta
- si el repository usa cierto patrón de constructor, repítelo
- si el router usa cierto orden de endpoints, repítelo
- si los use cases usan cierto estilo de logs, repítelo
- si el container registra con un patrón específico, repítelo
- si los controllers usan una forma concreta de `validateInputData`, repítela
- si el proyecto usa un estilo concreto de JSDoc, repítelo

**Está prohibido introducir una variante distinta si ya existe un patrón real en el proyecto.**

### Paso 2.5 — Selección de plantilla de referencia
Antes de generar archivos, define internamente cuál será la plantilla base para cada artefacto:

- controller de referencia
- router de referencia
- repository de referencia
- use case de referencia
- application service de referencia
- container de referencia

A partir de esa selección, genera el nuevo módulo como una **adaptación directa** de esas plantillas, no como una invención nueva.

---

## FASE 3 — Archivos base a revisar

Lee solo los archivos necesarios para registrar correctamente el nuevo módulo:

1. `tsconfig.json`
2. `src/modules/common/common.container.ts`
3. `src/modules/common/domain/enum/module-name.enum.ts`
4. archivo real donde se registran routers principales
5. clases base realmente usadas por el módulo de referencia
6. interfaces HTTP realmente usadas por el módulo de referencia

No abras archivos extra si no aportan a la generación del módulo.

---

## FASE 4 — Generación del módulo

Genera el módulo `src/modules/<MODULE_NAME>/` usando **únicamente**:
- el mapa de ubicaciones reales
- el patrón real del módulo de referencia
- las reglas obligatorias de convenciones

No inventes carpetas.  
No inventes clases base.  
No inventes patrones nuevos.  
No cambies la arquitectura real del proyecto.

### Archivos a crear
Crea solo los artefactos que el módulo de referencia realmente tenga para un CRUD equivalente.

Como mínimo, si el patrón del proyecto los usa:

#### Domain
- entidad
- interfaces de dominio necesarias
- interfaces de request HTTP necesarias
- enums del módulo

#### Application
- DTOs
- use cases CRUD
- application service

#### Infrastructure
- controllers CRUD
- repository
- router

#### Container
- `<module>.container.ts`

### Archivos a modificar
Solo si el proyecto realmente lo requiere:
1. enum de módulos
2. main router
3. `tsconfig.json` para alias `@<module>/*`

---

## REGLA OBLIGATORIA — RESPETAR ESTRUCTURA Y CONTENIDO

No basta con respetar la estructura.  
Debes respetar también el contenido del proyecto.

Por lo tanto, cada archivo nuevo debe parecer escrito como si hubiera sido creado por el mismo equipo que creó el módulo de referencia.

Verifica que coincidan:

- estilo de imports
- orden de secciones
- nombres de clases
- sufijos
- nombres de métodos
- herencia
- constructor
- dependencias inyectadas
- uso de logger
- validaciones
- manejo de errores
- respuesta HTTP
- uso de aliases
- estilo de JSDoc
- nivel de detalle del código
- patrón de registro en container
- patrón del router
- patrón del repository

Si dudas entre dos caminos, usa el que más se parezca al módulo existente de referencia.

---

## REGLA OBLIGATORIA — PROHIBIDO INVENTAR VARIANTES

Está prohibido:
- crear carpetas no existentes en el patrón detectado
- usar rutas distintas a las observadas
- cambiar nombres de sufijos si ya existe una convención real
- usar otra forma de DI distinta a la observada
- usar otro estilo de controllers, routers, repositories o services
- agregar capas no presentes en el módulo de referencia
- omitir capas que sí estén presentes en el módulo de referencia

---

## REGLA OBLIGATORIA — TIPADO DE REQUESTS

No uses casteos con objetos anónimos `as { ... }`.

Crea interfaces dedicadas en la ubicación real de interfaces del módulo si el patrón del proyecto las usa.  
Si el módulo de referencia ya tiene una forma concreta de tipar params/query/body, replica exactamente esa forma.

---

## REGLA OBLIGATORIA — COPYRIGHT DINÁMICO

Todo `@copyright` debe usar el año calendario actual.

Usa:
`Sentinel-{{AÑO_ACTUAL}}`

Reemplaza `{{AÑO_ACTUAL}}` por el año vigente durante la ejecución.

---

## REGLA OBLIGATORIA — CRLF

Todos los archivos generados deben usar terminación CRLF (`\r\n`).

---

## FASE 5 — Validación mínima final

Antes de finalizar, valida de forma breve:

1. la estructura creada coincide con el módulo de referencia
2. la ubicación de cada archivo coincide con el mapa detectado
3. el contenido sigue el mismo patrón del módulo de referencia
4. no hay `as { ... }`
5. el alias del módulo fue agregado si aplica
6. el módulo fue registrado donde corresponde
7. el copyright usa el año actual
8. los archivos están en CRLF

No hagas validaciones largas ni reportes extensos.

---

## Formato de salida

### 1. Referencia detectada
- módulo de referencia elegido
- mapa de ubicaciones detectado

### 2. Archivos creados
- listado breve de archivos creados

### 3. Archivos modificados
- listado breve de archivos modificados

### 4. Verificación final
- estructura replicada: sí/no
- contenido replicado: sí/no
- alias agregado: sí/no/no aplica
- registro en router: sí/no
- copyright actual: sí/no
- CRLF: sí/no

---

## Criterio de éxito

La tarea es exitosa solo si:
- el nuevo módulo sigue la estructura real del proyecto
- el contenido sigue el patrón real del módulo de referencia
- no introduce variantes ajenas al proyecto
- los archivos están ubicados correctamente
- el módulo queda integrado al proyecto siguiendo el estilo ya existente