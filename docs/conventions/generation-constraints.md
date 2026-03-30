# generation-constraints.md

## Cómo debe comportarse una IA al generar código

### Debe hacer
- respetar `hard-rules.md`
- respetar `naming-rules.md`
- respetar `typescript-rules.md`
- respetar `angular-rules.md` cuando aplique
- respetar `documentation-rules.md`
- respetar `testing-rules.md`
- respetar `sonar-rules.md`

### No debe hacer
- inferir reglas corporativas distintas a las ya documentadas
- generar excepciones silenciosas a naming o tipado
- omitir JSDoc cuando el proyecto o la tarea lo exijan
- usar `any` o `unknown` sin justificar
- crear métodos con más de 7 parámetros
- usar `::ng-deep` sin encapsulación
- crear elementos Angular sin `data-test` cuando aplique
- introducir nombres de negocio hardcodeados en la base reusable
- replicar patrones que violen umbrales SonarQube/SonarLint

## Orden de prioridad

1. Reglas corporativas
2. Reglas SonarQube/SonarLint
3. Arquitectura base del proyecto
4. Convenciones específicas del proyecto
5. Preferencias locales del desarrollador
