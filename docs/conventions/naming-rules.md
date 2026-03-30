# naming-rules.md

## Variables y constantes

- Usar `camelCase`.
- Deben estar en inglés.
- Deben ser descriptivas.
- Evitar nombres como `x`, `ml`, `af`.

## Métodos y funciones

- Usar `camelCase`.
- Deben estar en inglés.
- Deben ser descriptivos.

## Clases

- Usar `PascalCase`.

## Interfaces

- Usar `PascalCase`.
- Deben iniciar con `I`.
- Ejemplo: `IUserCredentials`.

## Enums

- Usar `PascalCase`.
- Deben terminar en `Enum`.
- Los miembros deben usar `UPPER_SNAKE_CASE`.
- No usar prefijos redundantes en miembros del enum.
- El archivo debe seguir la convención:
  - `nombre.enumerable.enum.ts`

## Variables de entorno

- Usar `SCREAMING_SNAKE_CASE`.
- Ejemplo:
  - `SESSION_TIMEOUT`

## Módulos y directorios

- Usar `kebab-case`.
- En plural cuando se trate de módulos.
- Ejemplo:
  - `modules/dynamic-catalogs`

## URLs y rutas

- Nombre de proyecto en `kebab-case`.
- Ruta del método en `kebab-case`.
- Identificadores en `camelCase`.

## Cache de auditoría

- Formato:
  - `{PERMISSION_CONTROLLER}::{recordId}`
- Ejemplo:
  - `WORKGROUP::2`
