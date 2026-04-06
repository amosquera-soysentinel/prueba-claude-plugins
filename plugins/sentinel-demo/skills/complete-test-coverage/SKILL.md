---
name: complete-test-coverage
description: Ejecuta los tests del proyecto, valida el coverage y crea o ajusta los tests necesarios hasta alcanzar 100% de coverage.
---

# Objetivo

Ejecutar los tests del proyecto, validar el coverage real y, si no es igual a `100%`, crear o ajustar los tests necesarios hasta alcanzar `100%` de coverage, respetando exactamente la estructura, estilo, convenciones y patrón de pruebas existentes en el repositorio.

Debes ser conservador:
- no inventes patrones
- no refactorices producción salvo que sea estrictamente necesario para permitir testabilidad
- no cambies la arquitectura
- no agregues explicaciones largas
- no muestres razonamientos extensos
- no generes salidas innecesarias

# Parámetros requeridos

Solicita solo si faltan o no pueden inferirse con seguridad:

- `TEST_COMMAND`: comando para ejecutar los tests con coverage
- `TARGET_SCOPE`: alcance a validar, por ejemplo módulo, carpeta, archivo o proyecto completo

Si el proyecto permite inferir el comando desde `package.json`, `pnpm`, `npm`, `yarn`, `jest`, `vitest` u otra configuración existente, úsalo sin preguntar.

No hagas más preguntas si con eso puedes resolver.

# Instrucciones

## 1. Analiza antes de ejecutar
Antes de correr cualquier comando:

- identifica el gestor de paquetes real del proyecto
- identifica el framework de pruebas real del proyecto
- identifica cómo se ejecuta el coverage
- identifica dónde se ubican los tests
- identifica el patrón real de:
  - nombres de archivos de test
  - estructura de describe y it
  - mocks
  - spies
  - factories
  - builders
  - stubs
  - setup global
  - utilidades de pruebas
  - convenciones de imports
  - estilo de assertions

Usa siempre el patrón real del proyecto.

## 2. Limita el análisis al alcance necesario
No explores todo el proyecto si no hace falta.

Debes analizar únicamente:
- el alcance indicado por `TARGET_SCOPE`, o
- lo mínimo necesario para encontrar el comando correcto, ejecutar tests y crear los tests faltantes

Solo puedes salir de ese alcance si es estrictamente necesario para consultar:
- configuración global de tests
- helpers compartidos
- mocks globales
- setup común
- clases base o utilidades comunes usadas por las pruebas

No hagas exploración amplia del repositorio.
No escanees módulos no relacionados si no aportan al objetivo.

## 3. Ejecuta primero, no supongas
Debes ejecutar los tests reales y obtener el coverage real antes de modificar nada.

Orden obligatorio:
1. detectar el comando correcto
2. ejecutar tests con coverage
3. leer el resultado real
4. identificar exactamente qué archivos, ramas, funciones o líneas no están cubiertas
5. crear o ajustar tests
6. volver a ejecutar
7. repetir hasta llegar a `100%`

No supongas coverage.
No declares éxito sin ejecutar la validación final.

## 4. Prioriza agregar tests sobre cambiar producción
Si el coverage no es `100%`, primero intenta resolverlo agregando o ajustando tests.

Solo puedes modificar código productivo si es estrictamente necesario para habilitar testabilidad, por ejemplo:
- export faltante que el proyecto ya permite
- dependencia imposible de mockear por una limitación menor
- acoplamiento accidental que bloquea la prueba

Si debes tocar producción:
- haz el cambio mínimo
- respeta el patrón del módulo
- no refactorices de más
- no alteres comportamiento funcional
- no cambies nombres ni contratos públicos sin necesidad

## 5. Replica el patrón exacto de pruebas del proyecto
Debes copiar el estilo real del repositorio en:

- estructura del archivo de test
- nombres de suites
- nombres de casos de prueba
- estrategia de mocks
- uso de beforeEach / afterEach
- helpers de test
- fixtures
- builders
- factories
- convenciones de assertions
- organización del archivo
- imports
- orden del contenido

No inventes un estilo nuevo.
No mezcles estilos de otros módulos.
No introduzcas librerías nuevas si el proyecto ya tiene un patrón establecido.

## 6. Cubre todo lo faltante
El objetivo no es “mejorar coverage”, es llegar a `100%`.

Debes cubrir lo que falte, incluyendo si aplica:
- statements
- branches
- functions
- lines
- casos felices
- casos de error
- retornos tempranos
- ramas condicionales
- excepciones
- valores nulos o vacíos
- defaults
- callbacks
- paths asincrónicos

No te detengas mientras el coverage siga por debajo de `100%`.

## 7. Usa solo cambios necesarios
Crea o modifica solo los archivos estrictamente necesarios.

No dejes:
- tests duplicados
- mocks no usados
- imports no usados
- helpers huérfanos
- datos de prueba innecesarios
- archivos temporales
- comentarios innecesarios

## 8. Crea y guarda archivos con CRLF
Todos los archivos nuevos o modificados deben guardarse usando finales de línea `CRLF`.

Reglas:
- respeta `CRLF` en el archivo final generado
- no mezcles `LF` y `CRLF`
- si el proyecto ya usa `CRLF`, mantén ese formato
- si los tests de referencia usan `CRLF`, replica exactamente ese formato
- la salida final debe quedar lista para guardarse con `CRLF`

## 9. Reejecuta hasta validar éxito real
Después de cada ajuste:

- vuelve a ejecutar los tests
- vuelve a medir el coverage
- valida si ya llegó a `100%`

Solo finaliza cuando:
- todos los tests pasen
- el coverage sea exactamente `100%`

Si existe una restricción técnica real que impida llegar a `100%`, indícalo brevemente con evidencia concreta del resultado ejecutado.

## 10. Salida mínima
Responde solo con:

1. archivos creados o modificados
2. comando ejecutado
3. resultado final del coverage
4. código final de los tests creados o ajustados
5. observaciones mínimas solo si hubo un bloqueo real

No incluyas:
- análisis extensos
- resúmenes largos
- razonamiento paso a paso
- texto redundante
- logs completos innecesarios

Muestra solo la información mínima útil para verificar el resultado.

# Restricciones

- no inventes comandos si el proyecto ya define uno
- no inventes frameworks de test
- no refactorices producción sin necesidad real
- no cambies la arquitectura
- no agregues librerías nuevas salvo necesidad extrema y justificada
- no mezcles estilos de pruebas entre módulos
- no dejes archivos temporales
- no escribas texto innecesario
- no muestres logs largos del proceso
- no imprimas razonamiento paso a paso
- no declares éxito sin ejecutar la validación final

# Formato final obligatorio

## Archivos
- `<ruta 1>`
- `<ruta 2>`

## Comando ejecutado
```bash
<comando>