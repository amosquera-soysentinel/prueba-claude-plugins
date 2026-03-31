Elimina de forma segura el módulo indicado por `TARGET_MODULE`, ajustando únicamente las referencias necesarias para que el proyecto quede consistente.

## Parámetros
- `TARGET_MODULE` obligatorio
- `RUN_TESTS` opcional, por defecto `true`
- `ENFORCE_COVERAGE` opcional, por defecto `false`

## Reglas
1. Analiza primero solo lo relacionado con `TARGET_MODULE`.
2. No inventes rutas ni módulos.
3. Elimina carpeta(s), archivos, pruebas y referencias del módulo.
4. Limpia imports, exports, registros y rutas relacionadas.
5. Ejecuta `pnpm test` solo una vez al final si `RUN_TESTS=true`.
6. Ajusta pruebas solo si fallan o si `ENFORCE_COVERAGE=true`.
7. Conserva CRLF en todos los archivos modificados.
8. Reporta en formato breve y no repitas contexto innecesario.

## Salida esperada
1. Hallazgos
2. Plan
3. Cambios realizados
4. Resultado de validación
5. Pendientes o bloqueos