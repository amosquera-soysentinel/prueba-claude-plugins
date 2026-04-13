Documenta con JSDoc todas las funciones/métodos nuevos o modificados en el diff actual (`git diff HEAD`).

Reglas de formato:
- Descripción siempre empieza con "Función que ..." en español
- `@param {Tipo} nombre - descripción` por cada parámetro
- `@returns {Tipo}` sin descripción adicional
- Agrega `@private` si el método es privado
- NO incluir `@memberof`

Ejemplo:
```typescript
/**
 * Función que obtiene las transacciones filtradas por fecha
 * @param {string} startDate - Fecha de inicio en formato ISO
 * @param {string} endDate - Fecha de fin en formato ISO
 * @returns {Observable<Transaction[]>}
 */
```

Pasos:
1. Ejecuta `git diff HEAD` para ver los cambios actuales
2. Identifica funciones/métodos nuevos o modificados que no tengan JSDoc
3. Edita cada archivo afectado agregando el JSDoc correspondiente
4. No modifiques la lógica del código, solo agrega documentación
