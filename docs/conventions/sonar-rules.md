# sonar-rules.md

## Objetivo

Estas reglas de calidad deben considerarse obligatorias al:
- analizar el proyecto fuente
- decidir qué partes forman la base reusable
- refactorizar piezas para convertirlas en base
- generar código nuevo a partir de la base

## Principio general

La base reusable extraída del proyecto no solo debe parecerse a la arquitectura existente; también debe quedar alineada con las reglas corporativas de SonarQube/SonarLint.

Si el proyecto fuente contiene patrones que contradicen estas reglas, Claude debe:
1. señalarlos como desviaciones del estándar
2. evitar replicarlos en la base reusable
3. proponer una versión corregida para la base

## Umbrales y restricciones clave

### Estructura y tamaño
- Longitud máxima por línea: **200** caracteres.
- Máximo por archivo: **1000** líneas.
- Máximo por función o método: **200** líneas.

### Complejidad
- Complejidad cognitiva máxima por función o método: **15**.
- Complejidad máxima de función: **10**.
- Máximo nivel de anidación: **5**.
- Máximo de operadores condicionales en una expresión: **5**.
- Máximo de casos en un `switch`: **30**.

### Parámetros
- Máximo **7 parámetros** por función o método.
- Si una operación requiere más de 7 parámetros, se debe refactorizar usando un objeto o estructura tipada.

### Duplicación y mantenibilidad
- Evitar bloques duplicados.
- Evitar strings literales repetidos; si una cadena se repite varias veces, debe extraerse a constante.
- No dejar código comentado ni secciones vacías sin intención clara.
- No dejar variables sin uso.
- No dejar ramas condicionales redundantes o simplificables.

### Naming y formato
- Respetar reglas de nombres para funciones, clases y variables según convenciones corporativas.
- Mantener estilo consistente de llaves.
- Mantener comillas simples cuando aplique.
- Mantener archivos y expresiones legibles y con baja complejidad.

### Seguridad
- No introducir credenciales hardcodeadas.
- No replicar patrones inseguros detectados en el proyecto fuente.
- Si el proyecto fuente expone posibles secretos, consultas inseguras o construcciones riesgosas, deben marcarse como deuda técnica y no heredarse a la base.

## Regla operativa para análisis del proyecto

Cuando Claude analice el proyecto fuente para extraer una base reusable debe clasificar cada hallazgo así:

- **Apropiado para heredar**: patrón reusable y alineado con Sonar.
- **Reusable con refactor**: patrón útil pero que debe corregirse para cumplir calidad.
- **No heredar**: patrón acoplado, frágil o contrario a reglas Sonar o corporativas.

## Regla operativa para generación de la base

Al generar una base nueva a partir del análisis:
- no copiar archivos o módulos que ya nazcan fuera de umbrales de Sonar
- no heredar funciones demasiado largas o complejas
- no heredar archivos gigantes como patrón
- no conservar nombres ambiguos solo por venir del proyecto fuente
- no reproducir duplicación, secretos, comentarios basura o code smells

La base final debe reflejar:
- la arquitectura útil detectada en el proyecto
- pero refinada según estándares corporativos y reglas Sonar
