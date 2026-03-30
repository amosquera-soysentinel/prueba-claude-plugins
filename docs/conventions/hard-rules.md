# hard-rules.md

## Objetivo

Estas son reglas obligatorias. Una IA, skill o plugin no debe romperlas.

## Reglas duras

- Usar interfaces para describir objetos complejos, especialmente si se reutilizan en varias partes del módulo o la aplicación.
- Los imports deben llevar espacios entre llaves y nombres.
- La indentación obligatoria es de 2 espacios.
- No usar tabs.
- Siempre usar punto y coma `;`.
- Siempre usar triple equivalencia:
  - `===`
  - `!==`
- Validar existencia de datos antes de acceder a propiedades o comparar valores.
- En asignaciones debe haber espacio a ambos lados del operador `=`.
- La llave de apertura debe ir en la misma línea de la declaración.
- El `else` debe ir en la misma línea de cierre del `if`.
- No usar `var`.
- Preferir `const` si no hay reasignación.
- Usar `let` si la variable sí puede cambiar.
- Los nombres deben ser descriptivos.
- Los perfiles y umbrales de SonarQube del equipo son obligatorios.

## Reglas de rechazo para IA

Rechazar o corregir cualquier salida que:
- use `var`
- use `==` o `!=`
- use tabs
- omita `;`
- use nombres ambiguos
- incumpla indentación de 2 espacios
- omita validación de existencia cuando haya acceso potencialmente inseguro
