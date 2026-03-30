# angular-rules.md

## data-test

Al crear un nuevo componente o elemento de interfaz, agregar identificador único `data-test` cuando aplique.

### Formato
`[tipo-elemento]-[identificador]-[contenedores]`

### Tipos permitidos
- `action`
- `grid`
- `select`
- `input`
- `div`

### Reglas
- Solo caracteres alfanuméricos en minúscula.
- El identificador debe estar en inglés.
- Debe reflejar el contexto del componente.
- Los contenedores representan jerarquía visual o funcional.

### Contenedores permitidos
- `page`
- `panel`
- `tab{n}`
- `modal`
- `editor`
- `prime`
- `kendo`
- `window`

### Casos especiales
- Si el componente lo genera una librería y no permite `data-test`, definirlo en el contenedor general.
- Si aparece un componente nuevo no contemplado, debe ampliarse el estándar.
- En pantallas nuevas, los elementos globales deben mantener nombres consistentes.

## Uso de ::ng-deep

- Evitar al máximo `::ng-deep`.
- Solo usarlo si es estrictamente necesario.
- Siempre encapsularlo con:
  - `:host`
  - o un selector único de la interfaz

### Ejemplos válidos
- `:host ::ng-deep .mat-dialog`
- `#tls-rules ::ng-deep .mat-dialog`

## Reglas operativas para IA

- No generar componentes Angular nuevos sin `data-test` cuando aplique.
- No usar `::ng-deep` sin encapsulación.
- Mantener identificadores de UI en inglés.
