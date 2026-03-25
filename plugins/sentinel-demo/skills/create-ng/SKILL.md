---
name: create-ng
description: Crea una carpeta con el nombre indicado y dentro genera un componente Angular base
argument-hint: ['nombre-del-componente']
disable-model-invocation: true
---

Tu tarea es crear un componente Angular básico usando como nombre `$ARGUMENTS`.

Sigue estas reglas:

1. Usa `$ARGUMENTS` como nombre del componente.
2. Si no se recibe ningún nombre, detente y dile al usuario que debe invocar el comando así:
   `/sentinel-demo:create-ng nombre-del-componente`
3. Convierte el nombre a kebab-case si hace falta.
4. Crea una carpeta con ese nombre en el directorio actual.
5. Dentro crea estos archivos:
   - `<nombre>.component.ts`
   - `<nombre>.component.html`
   - `<nombre>.component.scss`

Convenciones:
- Usa selector Angular con prefijo `app-`
- La clase debe ir en PascalCase
- Debe ser standalone
- No dependas de Angular CLI
- No ejecutes npm install
- No ejecutes ng generate
- Solo crea la estructura y el contenido base

Contenido esperado del archivo TypeScript:
- importar `Component` desde `@angular/core`
- `selector: 'app-<nombre>'`
- `standalone: true`
- `imports: []`
- `templateUrl` apuntando al html
- `styleUrl` apuntando al scss
- clase en PascalCase

Después de crear los archivos:
1. Muestra un resumen breve de lo creado
2. Muestra el árbol final de archivos