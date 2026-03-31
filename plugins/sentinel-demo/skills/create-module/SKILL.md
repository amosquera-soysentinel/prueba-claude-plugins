Genera un módulo CRUD para `MODULE_NAME` replicando exactamente el patrón estructural y de contenido de un módulo de negocio ya existente del proyecto.

## Parámetros
- `MODULE_NAME` requerido
- `ENTITY_FIELDS` opcional
- `GENERATE_TESTS` opcional, por defecto `false`

## Reglas
1. Lee solo las convenciones mínimas obligatorias si existen.
2. Analiza `src/modules/common` y un único módulo de negocio de referencia.
3. Extrae el mapa real de ubicaciones.
4. Usa un controller, router, repository, use case, service y container reales como plantilla.
5. Genera el nuevo módulo copiando ese patrón y adaptando nombres y tipos.
6. Respeta exactamente estructura, contenido, estilo, inyección, logs, JSDoc, aliases y registro del proyecto.
7. Prohibido inventar rutas, carpetas, capas o variantes no presentes en el módulo de referencia.
8. Prohibido usar `as { ... }`.
9. Usa copyright con año actual.
10. Genera archivos en CRLF.

## Salida
1. módulo de referencia
2. mapa de ubicaciones
3. archivos creados
4. archivos modificados
5. verificación breve final