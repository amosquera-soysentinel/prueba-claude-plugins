# typescript-rules.md

## Tipado

- Todos los parámetros de entrada deben tener tipo.
- Todo método o función debe declarar tipo de retorno.

## Parámetros

- Máximo 7 parámetros por método.
- Si se requieren más de 7, agrupar en un objeto o estructura.

## any

Evitar `any` en lo posible.

### Solo se permite cuando:
- se desconoce la estructura del objeto
- el objeto supera 20 propiedades
- el subtipo de propiedades supera 20

### No usar `any` cuando:
- se conoce el tipo
- el objeto tiene menos de 20 propiedades

## unknown

- Evitar `unknown` en lo posible.

## Clases y constructores

- Si el constructor tiene varias dependencias o parámetros, separarlos en líneas individuales.
- El prefijo `_` solo se permite en propiedades o métodos privados.

## Reglas operativas para IA

- No generar funciones sin tipo de retorno.
- No generar parámetros sin tipo.
- No generar métodos con más de 7 parámetros.
- No usar `any` o `unknown` salvo justificación explícita.
- Si la estructura es reusable, preferir interfaces.
