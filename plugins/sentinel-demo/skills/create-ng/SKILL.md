---
description: Crea una carpeta con el nombre indicado y dentro genera un componente Angular base
disable-model-invocation: true
argument-hint: [nombre-del-componente]
---

Usa "$ARGUMENTS" como nombre del componente.

Si no hay argumentos, indica al usuario que debe invocar:
`/sentinel-demo:create-ng nombre-del-componente`

Crea una carpeta con ese nombre en el directorio actual.

Dentro crea:
- `$ARGUMENTS.component.ts`
- `$ARGUMENTS.component.html`
- `$ARGUMENTS.component.scss`