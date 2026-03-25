---
name: create-ng
description: Crea una carpeta con el nombre indicado y genera un componente Angular base dentro
---

Crea un nuevo componente Angular con el nombre proporcionado como argumento.

Si no se proporcionó ningún argumento, responde al usuario:
"Por favor indica el nombre del componente: /sentinel-demo:create-ng <nombre-del-componente>"

De lo contrario, crea la siguiente estructura de archivos dentro de una nueva carpeta con el nombre del argumento (en kebab-case):

**`<nombre>/<nombre>.component.ts`**
```typescript
import { Component } from '@angular/core';

@Component({
   selector: 'app-<nombre>',
   templateUrl: './<nombre>.component.html',
   styleUrls: ['./<nombre>.component.scss']
})
export class <NombreEnPascalCase>Component {
}

<nombre>/<nombre>.component.html
<div class="<nombre>">
   <p><nombre> works!</p>
</div>

<nombre>/<nombre>.component.scss
.<nombre> {
}

Usa el argumento provisto como nombre base para todos los archivos. Convierte el nombre a kebab-case para el selector y nombres de archivo, y a PascalCase para el nombre de  
  la clase.