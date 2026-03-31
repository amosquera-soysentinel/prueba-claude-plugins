Extrae un proyecto base desde un archivo zip ubicado en la raíz, analiza su estructura, solicita o usa parámetros de personalización, reemplaza variables de configuración, limpia referencias heredadas, instala dependencias y ajusta pruebas hasta alcanzar 100% de coverage.

## Propósito
Toma un proyecto base comprimido en un archivo `.zip` ubicado en la carpeta raíz del workspace, lo extrae, analiza su estructura real y lo transforma en un nuevo proyecto limpio y consistente.

El proceso incluye:
- extracción del zip sin crear una carpeta artificial adicional
- análisis estructural previo a cualquier cambio
- personalización de variables de entorno y metadatos del proyecto
- limpieza de referencias heredadas del template base
- eliminación de archivos y variables sobrantes
- instalación de dependencias
- ejecución y ajuste de pruebas hasta alcanzar 100% de coverage
- eliminación del archivo `.zip` al finalizar

---

## Cuándo usar esta skill
Usa esta skill cuando:
- exista un proyecto base empaquetado en un `.zip`
- se necesite crear una nueva base a partir de ese template
- se deban reemplazar valores del `.env` y del `package.json`
- se requiera dejar el proyecto listo para continuar desarrollo o personalización

No uses esta skill si:
- no existe un `.zip` en la raíz
- el proyecto ya está configurado y solo se requiere un cambio puntual
- no se desea modificar estructura, tests o configuración base

---

## Entradas esperadas

### Parámetros requeridos
- `NAME`
- `DESCRIPTION`
- `PORT`
- `PROJECT_INITIALS`
- `ROUTER_COMPONENT`
- `ISSUER`

### Parámetros opcionales
- `ZIP_FILE_NAME`: nombre exacto del archivo zip si el usuario lo proporciona

Si faltan parámetros requeridos, solicítalos antes de ejecutar cambios.

El valor de `NAME` debe reutilizarse también para:
- reemplazar el campo `name` de `package.json`
- reemplazar referencias textuales a `BackendTsTemplate`
- reemplazar referencias textuales a `backend-ts-template`

El valor de `DESCRIPTION` debe usarse para:
- reemplazar el campo `description` de `package.json`
- insertarse como línea 3 del archivo `README.md` ubicado en la raíz del proyecto

No solicites un parámetro adicional para `package.json.name` ni para `package.json.description`.

---

## Reglas obligatorias

1. No modifiques ningún archivo antes de terminar el análisis inicial.
2. No inventes rutas. Trabaja únicamente con la estructura real encontrada.
3. No elimines archivos fuera del alcance definido, con excepción del `.zip` en el paso final.
4. Si algún archivo, variable o referencia no existe, repórtalo sin fallar innecesariamente.
5. Prioriza dejar el proyecto consistente por encima de seguir ciegamente una instrucción incompatible con la estructura real.
6. No finalices el proceso afirmando éxito si `pnpm install` o `pnpm test` fallan.
7. Intenta alcanzar 100% de coverage ajustando pruebas y, solo si es estrictamente necesario, realiza refactors menores que no cambien el comportamiento funcional esperado.
8. Si una referencia a `BackendTsTemplate` o `backend-ts-template` corresponde a algo externo que no deba tocarse, repórtalo y evita un cambio destructivo.
9. El `.zip` solo debe eliminarse después de que todas las validaciones finales hayan sido superadas correctamente. No lo elimines si el proceso terminó con errores no resueltos.

---

## Flujo de ejecución

### Paso 1. Detectar el zip en raíz
- Busca en la carpeta raíz del workspace un archivo `.zip`.
- Si se recibió `ZIP_FILE_NAME`, úsalo como prioridad.
- Si hay varios `.zip`, identifica el más probable como proyecto base y repórtalo.
- Si no existe ningún `.zip`, detén la ejecución y explica el problema.

### Paso 2. Extraer el contenido al mismo nivel del zip
- Extrae el contenido del `.zip` directamente en el mismo nivel donde se encuentra el archivo comprimido.
- No crees una carpeta contenedora adicional para la extracción, salvo que el contenido interno del zip ya venga organizado de esa forma.
- Respeta la estructura original contenida dentro del `.zip`.
- Confirma que la extracción fue exitosa antes de continuar.
- Después de extraer, identifica la raíz real del proyecto a partir de archivos como `package.json`, `.env`, `src`, `test`, `pnpm-lock.yaml` u otros equivalentes.

## REGLA OBLIGATORIA — ARCHIVOS CON FORMATO CRLF

### Regla

**TODOS** los archivos generados DEBEN usar terminación de línea **CRLF** (`\r\n`), correspondiente al estándar de Windows.

### Prohibición
```
// ❌ PROHIBIDO — Archivos con LF (\n) como fin de línea
```

### Instrucción

- Al crear o escribir cualquier archivo, asegúrate de que cada salto de línea sea `\r\n` (Carriage Return + Line Feed).
- Si la herramienta o entorno de generación usa LF por defecto, convierte explícitamente todas las líneas a CRLF antes de escribir el archivo.
- Esto aplica a **TODOS** los archivos: `.ts`, `.json`, `.md`, o cualquier otro formato generado.

### Validación

Antes de dar por finalizada la generación, verifica que los archivos creados usan CRLF. Si el entorno no permite controlarlo directamente, indica al usuario que ejecute una conversión con:
```bash
# Unix/Mac
sed -i 's/$/\r/' archivo.ts

# O con dos2unix inverso
unix2dos archivo.ts
```

---

### Paso 3. Analizar la estructura
Inspecciona la estructura del proyecto extraído e identifica como mínimo:

- archivo `.env`
- archivo `package.json`
- archivo `README.md` en la raíz del proyecto
- referencias textuales a `BackendTsTemplate`
- referencias textuales a `backend-ts-template`
- archivo `src\modules\common\application\enum\action-upsert.enum.ts`
- ubicación del directorio de pruebas
- scripts de test definidos en `package.json`
- configuración de coverage si existe

Reporta:
- estructura general encontrada
- archivos clave detectados
- coincidencias heredadas de template encontradas
- estado actual de las líneas del `README.md`

### Paso 4. Validar parámetros requeridos
Verifica si ya tienes estos valores:
- `NAME`
- `DESCRIPTION`
- `PORT`
- `PROJECT_INITIALS`
- `ROUTER_COMPONENT`
- `ISSUER`

Si falta uno o más, solicita solamente los faltantes.
No continúes con los cambios hasta tenerlos todos.
No solicites `PACKAGE_NAME` ni `PACKAGE_DESCRIPTION`, porque los valores de `NAME` y `DESCRIPTION` también se usan para reemplazar los campos correspondientes de `package.json`.

### Paso 5. Reemplazar configuraciones y referencias base
Una vez tengas todos los parámetros:

#### En `.env`
Reemplaza los valores de:
- `NAME`
- `PORT`
- `PROJECT_INITIALS`
- `ROUTER_COMPONENT`
- `ISSUER`

Elimina completamente la línea o variable:
- `PARALLEL_PROMISES_LIMIT`

#### En `package.json`
Reemplaza:
- `name` con el valor de `NAME`
- `description` con el valor de `DESCRIPTION`

#### En `README.md`
- Inserta el valor de `DESCRIPTION` exactamente en la línea 3 del archivo `README.md` ubicado en la raíz del proyecto.
- Si la línea 3 ya tiene contenido, reemplázala con el nuevo valor.
- Si el archivo tiene menos de 3 líneas, extiéndelo agregando líneas vacías hasta alcanzar la posición 3 e inserta el valor allí.
- No modifiques ninguna otra línea del archivo.
- Inserta `DESCRIPTION` como texto plano, sin agregar marcadores markdown adicionales salvo que el contexto del archivo lo requiera explícitamente.

#### Reemplazos textuales adicionales
Busca y reemplaza en el proyecto todas las referencias heredadas a:
- `BackendTsTemplate`
- `backend-ts-template`

Ambas deben ser reemplazadas por el valor de `NAME`, siempre que correspondan a identificadores heredados del template base y no a referencias externas que deban conservarse.

Valida cuidadosamente que estos reemplazos no rompan rutas, imports, nombres de paquetes externos, valores técnicos sensibles o referencias que no pertenezcan al template.

### Paso 6. Eliminar archivo adicional
Elimina el archivo:
- `src\modules\common\application\enum\action-upsert.enum.ts`

Si no existe, repórtalo sin marcar la ejecución como fallida.

### Paso 7. Instalar dependencias
- Ejecuta `pnpm install`
- Verifica que la instalación finalice correctamente
- Si hay errores de dependencias, scripts o lockfile, analízalos y ajústalos dentro del alcance del proyecto para dejar la instalación funcional

### Paso 8. Ejecutar pruebas y ajustar coverage
- Ejecuta `pnpm test`
- Identifica si el proyecto genera reporte de coverage
- Revisa el porcentaje de cobertura global y por archivo si está disponible
- Si el coverage está por debajo de 100%, analiza qué caminos, ramas, funciones o líneas faltan por cubrir
- Crea o ajusta las pruebas necesarias
- Si hace falta hacer refactors menores para testabilidad, hazlos sin alterar el comportamiento funcional esperado
- Vuelve a ejecutar las pruebas tantas veces como sea necesario hasta alcanzar 100% de coverage
- No des por finalizado el proceso mientras el coverage siga por debajo de 100%, salvo que exista un bloqueo técnico real que debas reportar explícitamente

### Paso 9. Validaciones finales
Valida como mínimo:
- que `.env` contenga `NAME`, `PORT`, `PROJECT_INITIALS`, `ROUTER_COMPONENT` e `ISSUER` con los nuevos valores
- que `.env` ya no contenga `PARALLEL_PROMISES_LIMIT`
- que `package.json` tenga `name` actualizado con `NAME`
- que `package.json` tenga `description` actualizado con `DESCRIPTION`
- que la línea 3 del `README.md` contenga exactamente el valor de `DESCRIPTION`
- que ya no existan referencias heredadas a `BackendTsTemplate` ni a `backend-ts-template`
- que el archivo `src\modules\common\application\enum\action-upsert.enum.ts` ya no exista
- que `pnpm install` haya terminado correctamente
- que `pnpm test` ejecute correctamente
- que el coverage final sea del 100%
- que la estructura resultante siga siendo coherente

Si detectas problemas, repórtalos claramente antes de continuar al paso 10.

### Paso 10. Eliminar el archivo ZIP
- Elimina el archivo `.zip` original desde la raíz del workspace
- Confirma que el archivo fue eliminado correctamente
- Si la eliminación falla, repórtalo pero no marques el proceso como fallido, ya que el proyecto ya fue configurado correctamente

---

## Estrategia de trabajo esperada
Trabaja siempre en este orden:

1. Detectar zip
2. Extraer al mismo nivel del zip, sin crear carpeta adicional
3. Identificar la raíz real del proyecto extraído
4. Analizar estructura y referencias heredadas
5. Pedir parámetros faltantes
6. Reemplazar configuraciones, `description` en `package.json` y línea 3 del `README.md`
7. Eliminar archivo adicional
8. Instalar dependencias con `pnpm install`
9. Ejecutar pruebas con `pnpm test`
10. Ajustar pruebas o código hasta alcanzar 100% coverage
11. Validar consistencia final
12. Eliminar el archivo `.zip`
13. Entregar resumen final

No alteres este orden salvo que la estructura real del proyecto lo exija para mantener consistencia.

---

## Formato de salida

Organiza tu respuesta en estas secciones:

### 1. Hallazgos del análisis
- zip detectado
- raíz real del proyecto identificada
- estructura general encontrada
- ubicación de `.env`, `package.json` y `README.md`
- referencias relevantes encontradas
- coincidencias de `BackendTsTemplate` y `backend-ts-template`
- existencia o ausencia de `action-upsert.enum.ts`
- scripts de test y coverage detectados
- estado actual de las líneas del `README.md`

### 2. Parámetros requeridos
Si faltan datos, solicita únicamente los faltantes.

### 3. Plan de cambios
- qué archivos serán modificados
- qué carpetas o archivos serán eliminados
- qué referencias serán ajustadas
- qué validaciones se ejecutarán

### 4. Resultado final
- archivos modificados
- archivos y carpetas eliminados
- referencias limpiadas
- dependencias instaladas
- resultado de `pnpm test`
- coverage final alcanzado
- validaciones realizadas
- confirmación de eliminación del `.zip`
- advertencias, bloqueos o pendientes encontrados

---

## Criterios de éxito
La ejecución se considera exitosa si:
- el zip fue extraído correctamente sin crear carpeta adicional
- el proyecto fue analizado antes de modificar
- `.env` y `package.json` fueron actualizados correctamente
- `package.json.name` quedó con el valor de `NAME`
- `package.json.description` quedó con el valor de `DESCRIPTION`
- la línea 3 del `README.md` contiene exactamente el valor de `DESCRIPTION`
- las referencias heredadas a `BackendTsTemplate` y `backend-ts-template` fueron reemplazadas
- se eliminó `PARALLEL_PROMISES_LIMIT`
- se eliminó `src\modules\common\application\enum\action-upsert.enum.ts`
- `pnpm install` terminó correctamente
- `pnpm test` terminó correctamente con 100% de coverage
- no quedaron referencias rotas relacionadas con lo eliminado
- el archivo `.zip` fue eliminado al finalizar
- se entregó un resumen claro y verificable

---

## Manejo de errores
Si ocurre algún problema:
- explica exactamente qué falló y en qué paso
- muestra qué sí alcanzó a validarse o modificarse
- no afirmes que el proceso terminó correctamente si hay errores no resueltos
- si el único paso fallido fue la eliminación del `.zip`, el proceso puede considerarse exitoso con advertencia

---

## Notas adicionales
- Si el proyecto tiene una arquitectura distinta, adapta la ejecución a la estructura encontrada sin salirte del alcance funcional pedido.
- Si el proyecto requiere comandos de test distintos derivados del análisis real del `package.json`, repórtalo claramente, pero mantén `pnpm test` como comando principal esperado.
- Si el reporte de coverage necesita flags, configuración o ejecución adicional, analízalo y ajústalo dentro del alcance del proyecto para obtener un resultado verificable.