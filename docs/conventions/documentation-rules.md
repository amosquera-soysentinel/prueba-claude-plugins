# documentation-rules.md

## Idioma

- Los comentarios deben escribirse en español.

## Propósito

- Los comentarios deben ayudar a comprender el código.
- No dejar líneas de código comentadas.

## Formato de comentarios

### Fuera de métodos
- Usar bloque `/** */`

### Dentro de métodos
- Usar comentario de línea `//`

## Comentarios de clases

Deben incluir:
- descripción breve
- `@class`
- `@author`
- `@copyright`

## Comentarios de métodos

Usar sintaxis JSDoc con:
- descripción breve
- `@param {tipo} nombre - descripción`
- `@return {tipo}`

## Reglas adicionales de JSDoc

- El nombre y la descripción del parámetro deben separarse con ` - `
- La descripción del parámetro es obligatoria
- En constructores usar `@constructor`
- Los parámetros opcionales se documentan con corchetes:
  - `@param {ICredential} [credentials]`
- Los parámetros opcionales con valor por defecto deben indicar el default:
  - `@param {number} [id=1]`
- En destructuración, documentar el objeto principal y sus propiedades internas

## Imports Angular

Las importaciones deben agruparse y comentarse por secciones, por ejemplo:
- Dependencias Angular
- Servicios
- Componentes
- Kendo Grid
