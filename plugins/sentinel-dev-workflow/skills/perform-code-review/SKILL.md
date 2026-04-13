Realiza un code review completo de los cambios actuales antes de subir el PR. Revisa únicamente el código modificado usando `git diff develop` y evalúa tanto los estándares de desarrollo de SmartSoft/Sentinel como las reglas de SonarQube.

## Pasos

1. Ejecuta en paralelo:
   - `git diff develop` para obtener los cambios respecto a la rama base
   - `git diff develop --name-only` para obtener la lista de archivos modificados
2. Ejecuta en paralelo:
   - `npm run lint -- --max-warnings=9999 2>&1 | head -200` para obtener alertas del linter (incluye reglas SonarJS). Si el comando falla, usa únicamente el análisis estático del diff.
   - `npm run test:server 2>&1 | tail -80` para ejecutar las pruebas unitarias en modo CI y capturar errores de compilación, SCSS o specs fallidos.
3. Revisa cada archivo modificado leyéndolo completo si es necesario para entender el contexto.
4. Incluye una sección **Tests** al inicio del reporte con el resultado de las pruebas: si pasaron todas, si hay errores de compilación/build o specs fallidos, indicando el archivo y el mensaje exacto del error.
5. Genera un reporte estructurado dividido en tres secciones independientes: **Tests**, **Code Review** y **SonarQube**.

---

## Estándares a verificar

### Generalidades (TypeScript / Angular)

- **Imports**: debe haber espacio dentro de las llaves → `import { Foo } from '...'`
- **Indentación**: 2 espacios, sin tabs
- **Condición `if`**: espacio entre `if` y `(`, espacio entre `)` y `{` → `if (cond) {`
- **`else`**: en la misma línea que el cierre del `if` → `} else {`
- **Triple igualdad**: siempre `===`, nunca `==`
- **Validación antes de acceso**: verificar existencia antes de acceder a propiedades anidadas → `(data && data[0]) ? data[0].name : ''`
- **Sin `var`**: usar `const` si el valor no cambia, `let` si cambia
- **Punto y coma**: obligatorio al final de cada línea
- **Espacios en asignaciones**: `const x = value;` (espacio a ambos lados del `=`)
- **Máximo 7 parámetros** por función; si se superan, usar una interface o un objeto
- **Llaves de apertura** en la misma línea que la definición de función/clase/objeto
- **Arrow functions**: usar para callbacks y funciones anónimas; simplificar cuando sea posible → `(a, b) => a + b`
- **Interfaces para objetos complejos**: siempre que un objeto sea reutilizado en el módulo o la app
- **Selectores CSS**: kebab-case
- **`::ng-deep`**: nunca sin `:host` o un selector único de la interfaz que lo encierre

### Variables y Constantes

- **Notación**: camelCase (`localAmount`, no `local_amount` ni `LocalAmount`)
- **Nombres**: descriptivos y en inglés
- **Variables de entorno** (archivos `.env`): SCREAMING_SNAKE_CASE

### Métodos / Funciones

- **Notación**: camelCase y en inglés (`addRow`, no `agregarFila`)
- **Tipos explícitos**: parámetros y retorno tipados → `onClick(event: Event): void`
- **Prefijo `_`**: solo para métodos y propiedades privadas

### Clases

- **Notación**: PascalCase
- **Constructor**: cada dependencia en su propia línea (no todo en una sola línea)
- **Prefijo `_`**: solo para miembros privados

### Interfaces

- **Prefijo `I` + PascalCase** → `IProjectedBehavior`, nunca `projectedBehavior`

### Enums

- **Nombre**: PascalCase + sufijo `Enum` → `HttpStatusEnum`
- **Miembros**: UPPER_SNAKE_CASE → `BAD_REQUEST`, no `BadRequest`
- **Sin prefijos redundantes**: no repetir el nombre del enum en los miembros
- **Archivo**: `nombre.enumerable.enum.ts`

### Tipo `any`

- Evitar. Solo permitido cuando se desconoce la estructura del objeto o supera 20 propiedades.
- Evitar también `unknown` cuando no sea necesario.

### Comentarios

- Escritos en **español**
- **Sin código comentado** (líneas de código desactivadas con `//`)
- Fuera de un método, una línea: `/** Comentario */`
- Dentro de un método, una línea: `// Comentario`
- Múltiples líneas fuera de método: `/** \n * línea1 \n * línea2 \n **/`
- Múltiples líneas dentro de método: `// línea1` + `// línea2`
- **Clases**: JSDoc con `@class`, `@author Nombre – email@soysentinel.com`, `@copyright Sentinel-{año}`
- **Métodos**: JSDoc con descripción, `@param {tipo} nombre - descripción`, `@return {tipo}`
  - Constructores: agregar `@constructor`
  - Parámetros opcionales: usar corchetes `[paramName]`
  - Parámetros con default: documentar el valor → `@param {number} [id=1]`
  - Destructuring de parámetros: documentar objeto + propiedades individuales
- **Importaciones en Angular**: comentarios de sección antes de cada grupo (`/** Dependencias Angular */`, `/** Servicios */`, etc.)

### Atributos `data-test` (Angular)

- Todo componente nuevo en la UI debe tener `data-test`
- Estructura: `[tipo]-[identificador]-[contenedores]` en minúsculas y alfanumérico
- Tipos válidos: `action`, `grid`, `select`, `input`, `div`
- Identificadores comunes de `action`: `new`, `edit`, `delete`, `export`, `cancel`
- Contenedores: `page`, `panel`, `tab0..n`, `modal`, `editor`, `prime`, `kendo`, `window`

### Pruebas Unitarias

- Los datos de prueba deben ser **realistas y coherentes** con el dominio (no `'qqqqqqqqq'` ni `'gegegeg'`)

---

## Reglas SonarQube a verificar

Analiza el diff en busca de las siguientes categorías de problemas. Combina los resultados del linter (`npm run lint`) con análisis estático propio sobre el código modificado.

### Bugs

- Promesas no manejadas (`async` sin `await`, `.then()` sin `.catch()`)
- Comparaciones siempre verdaderas o falsas por tipo incorrecto
- Variables usadas antes de ser asignadas
- Retornos inconsistentes en funciones (a veces retornan valor, a veces no)
- Condiciones que nunca pueden cumplirse (`if (x === null && x === undefined)`)

### Code Smells

- **Complejidad cognitiva** alta: funciones con más de 15 niveles de anidamiento o ramificaciones
- **Funciones demasiado largas**: más de 40 líneas de lógica efectiva
- **Código duplicado**: bloques de 5+ líneas repetidos dentro del diff
- **Dead code**: variables declaradas y nunca usadas, imports no utilizados
- **Parámetros booleanos** en funciones públicas (señal de función que hace dos cosas)
- **Magic numbers**: literales numéricos sin nombre (`width: 100`, timeouts como `1000`) sin contexto
- **Retorno de `null`/`undefined`** mezclado en una misma función sin razón aparente

### Vulnerabilidades

- Interpolación de strings en queries o comandos sin sanitización
- Datos sensibles logueados con `console.log`
- URLs o tokens hardcodeados en el código

### Mantenibilidad

- **Acoplamiento alto**: componente que importa más de 10 dependencias distintas en el diff
- **Métodos con múltiples responsabilidades** detectables por nombre genérico (`process`, `handle`, `manage`)
- **`any` explícito** en tipos donde la estructura es conocida
- **Interfaces o tipos inline** repetidos que deberían extraerse

---

## Formato del reporte

Organiza la respuesta con las **tres secciones separadas**:

```
---
# 🧪 TESTS — Resultado de pruebas unitarias
---

## Estado
[✅ Todas las pruebas pasaron | ❌ X prueba(s) fallaron | 🔴 Error de compilación]

## Detalle de errores
[Si hay errores, listar por archivo con el mensaje exacto. Si no hay errores, escribir "Sin errores".]

---
# 🔍 CODE REVIEW — Estándares Sentinel
---

## Resumen
[N críticos / N advertencias / N sugerencias]

## Hallazgos por archivo

### path/al/archivo.ts

#### ❌ Crítico
- Línea X: [descripción] → [cómo corregirlo]

#### ⚠️ Advertencia
- Línea X: [descripción]

#### 💡 Sugerencia
- Línea X: [descripción]

## ✅ Aspectos correctos destacables
[Breve mención de lo bien hecho]


---
# 🟠 SONARQUBE — Análisis estático
---

## Resumen
[N bugs / N code smells / N vulnerabilidades]

## Hallazgos por archivo

### path/al/archivo.ts

#### 🐛 Bug
- Línea X: [descripción] → [cómo corregirlo]

#### 🧹 Code Smell
- Línea X: [descripción]

#### 🔒 Vulnerabilidad
- Línea X: [descripción]

#### 📐 Mantenibilidad
- Línea X: [descripción]

## ✅ Sin alertas Sonar destacables
[Si no hay hallazgos Sonar, indicarlo aquí]
```

Si una sección no tiene hallazgos, indicarlo explícitamente con "Sin hallazgos". No omitir la sección.
