# Sentinel UI Style Guide

## 1. Propósito

Este documento define las reglas visuales base para construir interfaces Sentinel con consistencia gráfica, especialmente para pantallas administrativas tipo listado, filtros, formularios y modales.

Su objetivo es servir como referencia textual principal para herramientas de generación asistida por IA y para desarrolladores que deban construir nuevas vistas respetando el diseño institucional existente.

Este documento debe ser usado junto con la imagen de referencia visual:

- `docs/ui/sentinel-generative-agents-reference.png`

Y, si se requiere validación adicional, con el documento fuente:

- `docs/ui/sentinel-ui-style-guide-source.pdf`

---

## 2. Prioridad de uso

Cuando este documento se utilice junto con estándares técnicos del proyecto, debe aplicarse esta prioridad:

1. estándares técnicos y de arquitectura del proyecto
2. estructura real del módulo base a replicar
3. este documento de estilo visual
4. imagen de referencia
5. decisiones visuales inferidas

No deben inventarse patrones nuevos si ya existe una convención real dentro del proyecto.

---

## 3. Principios generales de diseño

Las pantallas Sentinel deben transmitir:

- claridad
- jerarquía visual simple
- orientación administrativa/empresarial
- consistencia entre listados y formularios
- baja carga visual innecesaria
- acciones visibles y directas
- alineación estricta de espaciados y tamaños

El diseño esperado corresponde a aplicaciones internas empresariales con:

- menú lateral oscuro
- área de contenido clara
- encabezado de vista
- acciones superiores
- área de filtros o búsqueda
- tabla de resultados
- paginación inferior
- formularios y modales de apariencia sobria

---

## 4. Layout general

### 4.1 Estructura visual típica

La composición general esperada para una pantalla tipo Sentinel es:

1. sidebar o menú lateral institucional
2. barra superior de contexto del sistema
3. área principal de contenido
4. título de la vista
5. botones de acción superiores
6. buscador y/o filtros
7. tabla o grilla principal
8. paginación al pie
9. modal o formulario emergente cuando aplique

### 4.2 Distribución del contenido

La pantalla debe mantener una estructura limpia y alineada. El contenido principal debe organizarse así:

- encabezado superior del contenido con título y acciones
- controles de búsqueda o filtros alineados con la tabla
- tabla ocupando el bloque principal de contenido
- paginación al pie de la tabla
- formularios laterales o modales alineados con la misma guía visual

### 4.3 Sensación visual

La vista debe percibirse:

- estable
- institucional
- limpia
- compacta
- predecible
- sin adornos innecesarios

---

## 5. Márgenes y espaciados

La guía visual utiliza principalmente múltiplos de 5px, con predominio de 10px, 15px y 30px. :contentReference[oaicite:1]{index=1}

### 5.1 Espaciados base recomendados

Usar de forma preferente:

- `5px`
- `10px`
- `15px`
- `30px`

### 5.2 Regla general de espaciado

- separación pequeña entre controles relacionados: `5px` a `10px`
- separación estándar entre campos, botones y bloques cortos: `15px`
- separación entre bloques mayores o secciones: `30px`

### 5.3 Márgenes recomendados por contexto

#### Encabezados de contenido
- margen superior: `15px`
- margen inferior: `15px`
- separación entre título y acciones: `15px` o `30px` según densidad

#### Tablas
- separación entre encabezado de la vista y tabla: `15px`
- separación entre filtros y tabla: `15px`
- separación entre tabla y paginación: `15px` a `30px`

#### Formularios
- separación vertical entre campos: `15px`
- separación entre grupos: `30px`

#### Modales
- padding interno general: `15px`
- separación entre cuerpo y acciones: `30px`

---

## 6. Tipografía

La guía usa como fuente principal `Open Sans`, y para iconografía `Font Awesome`. :contentReference[oaicite:2]{index=2}

### 6.1 Fuentes oficiales

- Fuente principal: `Open Sans`
- Fuente de iconos: `Font Awesome`

### 6.2 Regla general de uso

- todo el texto general debe renderizarse con `Open Sans`
- los iconos deben mantenerse coherentes con la convención institucional ya usada en el proyecto
- no mezclar familias tipográficas nuevas sin justificación

### 6.3 Tamaños base

Los tamaños visibles de referencia son principalmente:

- texto estándar: `13px`
- títulos principales o destacados: `25px`

:contentReference[oaicite:3]{index=3}

### 6.4 Aplicación recomendada de tamaños

#### Texto base
- `13px`

Usar para:
- labels
- headers de tabla
- contenido de tabla
- placeholders
- textos de botones pequeños y medianos
- mensajes informativos cortos

#### Título principal de vista
- `25px`

Usar para:
- título principal del módulo o pantalla
- títulos destacados del área de contenido

### 6.5 Peso visual

Mantener pesos visuales sobrios:

- regular para texto general
- semibold o equivalente para encabezados y labels principales
- evitar exceso de bold

---

## 7. Paleta de colores

La guía define una paleta institucional con neutros, azules de marca y colores de estado. :contentReference[oaicite:4]{index=4}

### 7.1 Colores base

#### Neutros oscuros y de estructura
- `#181d23`
- `#2b333d`
- `#74797b`
- `#bcc3c8`
- `#dfe0e7`
- `#f1f2f7`

#### Azules institucionales
- `#0066a6`
- `#0076c0`
- `#59baf7`

#### Verdes
- `#46a600`
- `#5bb875`

#### Naranjas
- `#c96a0d`
- `#e2954a`

#### Rojos / rosados
- `#c90d31`
- `#d9556e`

#### Tonos claros de apoyo
- `#cce0ed`
- `#ebf6fd`

### 7.2 Uso recomendado por categoría

#### Estructura principal
- fondo sidebar: `#181d23` o `#2b333d`
- divisores, bordes suaves y componentes apagados: `#bcc3c8`, `#dfe0e7`
- fondo general claro: `#f1f2f7`

#### Marca y acciones primarias
- azul principal: `#0066a6`
- azul secundario/activo: `#0076c0`
- azul claro para selección/realce: `#59baf7`

#### Estados positivos
- verde fuerte: `#46a600`
- verde suave: `#5bb875`

#### Advertencias
- naranja fuerte: `#c96a0d`
- naranja suave: `#e2954a`

#### Errores o alertas críticas
- rojo fuerte: `#c90d31`
- rojo suave/alerta secundaria: `#d9556e`

### 7.3 Reglas de uso

- mantener el azul institucional como color primario de interacción
- no introducir paletas externas
- los colores de estado deben conservar su semántica
- no saturar la interfaz con demasiados acentos simultáneos

---

## 8. Estados visuales

La guía muestra reglas para vista actual, mouse encima y opciones activas. :contentReference[oaicite:5]{index=5}

### 8.1 Vista actual
Color sugerido:
- `#eeeef0` o equivalente muy claro de fondo

Uso:
- resaltar la vista, ítem o bloque actualmente seleccionado
- indicar contexto actual sin competir con acciones activas

### 8.2 Hover
Color sugerido:
- `#0066a6`

Uso:
- iconos al pasar el mouse
- acciones interactivas
- botones según patrón existente

### 8.3 Activo / seleccionado
Color sugerido:
- `#59baf7`

Uso:
- iconos o acciones activas
- opción seleccionada
- pestaña o estado seleccionado cuando el componente base ya siga ese comportamiento

### 8.4 Reglas

- hover debe ser visible pero no agresivo
- activo debe ser claramente distinguible del hover
- vista actual debe sentirse contextual, no como acción primaria

---

## 9. Sidebar o menú lateral

### 9.1 Apariencia general

El menú lateral debe ser oscuro, institucional y compacto.

Colores sugeridos:
- fondo principal: `#181d23`
- fondo alterno o bloques secundarios: `#2b333d`
- texto e iconos claros sobre contraste alto

### 9.2 Comportamiento visual

- ítem activo con realce azul o contraste superior
- agrupadores consistentes
- iconos de tamaño homogéneo
- espaciado vertical controlado
- sin elementos decorativos innecesarios

### 9.3 Reglas de implementación

- no alterar estructura del sidebar si ya existe en el proyecto
- no recrear sidebar desde cero si ya existe un layout contenedor
- el nuevo desarrollo debe adaptarse al contenedor real del proyecto

---

## 10. Encabezado de contenido

### 10.1 Título principal

El título de la pantalla debe:

- usar `Open Sans`
- conservar un tamaño prominente, idealmente cercano a `25px`
- ser el principal punto de jerarquía de la pantalla
- ubicarse en el encabezado del contenido

### 10.2 Acciones superiores

Las acciones principales deben ubicarse cerca del título o en el mismo bloque superior del contenido.

Ejemplos comunes:
- crear
- descargar
- exportar
- recargar
- limpiar filtros

### 10.3 Reglas

- mantener acciones agrupadas
- usar iconografía consistente
- no dispersar acciones primarias por toda la pantalla

---

## 11. Botones

### 11.1 Apariencia general

Los botones deben ser:

- compactos
- legibles
- coherentes con la paleta institucional
- alineados al patrón del módulo base

### 11.2 Colores recomendados

#### Primario
- fondo: `#0066a6` o `#0076c0`
- texto: claro/blanco

#### Secundario o neutro
- fondo: tonos claros o gris institucional
- borde suave si aplica
- texto oscuro o medio según contraste

#### Positivo
- verde institucional si el patrón existente lo requiere

#### Peligro
- rojo institucional solo para acciones destructivas

### 11.3 Reglas

- mantener tamaños homogéneos
- no usar botones excesivamente altos
- conservar espaciados consistentes entre botones
- preferir icono + acción cuando el sistema ya lo use
- evitar más de una acción primaria compitiendo en el mismo bloque

---

## 12. Inputs y campos de formulario

La guía muestra controles de formulario sobrios, claros y compactos. :contentReference[oaicite:6]{index=6}

### 12.1 Estilo general

Los inputs deben ser:

- rectangulares
- de borde ligero o fondo claro según patrón
- de lectura simple
- visualmente alineados
- consistentes en altura

### 12.2 Tamaños

La guía sugiere múltiples anchos, según uso. No deben inventarse anchos arbitrarios si ya existe una grilla o layout base.

Recomendación:
- usar clases reutilizables o layout responsive del proyecto
- conservar alturas consistentes
- evitar campos visualmente desproporcionados

### 12.3 Labels

Los labels deben:

- ser claros
- mantener tamaño cercano a `13px`
- alinearse sobre o junto al campo según el patrón del módulo base
- no competir visualmente con el valor del input

### 12.4 Selects

Los selects deben:
- conservar la apariencia institucional
- alinearse en altura con los inputs
- usar iconografía nativa o institucional del proyecto
- respetar spacing uniforme

### 12.5 Checkboxes / toggles

- deben verse limpios y consistentes
- usar el azul institucional cuando estén activos
- no reemplazar el patrón ya existente del proyecto

### 12.6 Estados de campos

Deben contemplarse, según aplique:
- normal
- hover
- focus
- disabled
- readonly
- error
- success si el patrón del proyecto lo usa

### 12.7 Errores de validación

El estado de error debe:
- ser claro
- usar color de alerta o error institucional
- no romper el layout
- acompañarse de mensaje breve y útil

---

## 13. Filtros

La guía incluye una composición visual clara para filtros en listados administrativos. :contentReference[oaicite:7]{index=7}

### 13.1 Ubicación

Los filtros deben ubicarse:
- sobre la tabla
- alineados al ancho útil del contenido
- con separación clara respecto del título y respecto de la tabla

### 13.2 Composición

Pueden incluir:
- ícono de filtro
- fechas
- usuario
- estado
- tipo
- país
- selects
- búsqueda textual

### 13.3 Reglas visuales

- mantener altura uniforme de los controles
- no sobrecargar una sola fila
- usar espaciamiento controlado
- si hay muchos filtros, agruparlos con claridad
- el área de filtros debe leerse como un bloque funcional separado del listado

### 13.4 Búsqueda

El buscador debe:
- estar visible
- tener tamaño compacto
- alinearse correctamente con las acciones o el bloque de filtros
- no desplazar elementos de forma abrupta

---

## 14. Tablas y listados

La imagen de referencia muestra una tabla administrativa clásica con columnas, acciones superiores y paginación. :contentReference[oaicite:8]{index=8}

### 14.1 Estructura

La tabla debe incluir, cuando aplique:
- encabezado de columnas
- filas de datos
- estados vacíos
- ordenamiento si aplica
- paginación
- acciones por fila o generales

### 14.2 Encabezado de tabla

- usar fondo gris claro o equivalente institucional
- mantener contraste suficiente
- usar tipografía sobria
- alinear encabezados con sus columnas
- evitar exceso de decoración

### 14.3 Celdas

- texto legible
- alineación consistente
- no truncar información crítica sin estrategia
- aplicar formato solo cuando sea necesario

### 14.4 Filas

- fondo claro
- separación visual limpia
- hover sutil
- posibilidad de resalte si la tabla del proyecto ya lo maneja

### 14.5 Acciones de tabla

Si existen acciones por fila:
- usar iconos coherentes
- mantener separación uniforme
- evitar demasiadas acciones visibles a la vez si afecta legibilidad

### 14.6 Estado vacío

Cuando no haya datos:
- mostrar mensaje claro
- no dejar espacios ambiguos
- mantener consistencia con diseño institucional

### 14.7 Loading

El estado de carga debe:
- ser visible
- no romper el layout
- integrarse bien con la tabla o área de contenido

---

## 15. Paginación

### 15.1 Ubicación

La paginación debe ubicarse al pie de la tabla.

### 15.2 Apariencia

Debe ser:
- compacta
- clara
- alineada con el ancho útil del listado
- consistente con la librería base del proyecto

### 15.3 Elementos frecuentes

Puede incluir:
- número de página actual
- total de páginas
- tamaño de página
- cantidad de registros
- navegación adelante/atrás

### 15.4 Reglas

- no sobredimensionar los controles
- evitar separaciones irregulares
- conservar la misma línea gráfica del resto de la vista

---

## 16. Formularios

### 16.1 Apariencia general

Los formularios Sentinel deben verse:
- estructurados
- sobrios
- espaciados
- con labels claros
- con agrupación lógica

### 16.2 Organización

- agrupar campos relacionados
- mantener separación vertical uniforme
- no mezclar demasiadas intenciones en una sola sección

### 16.3 Acciones de formulario

Las acciones deben ubicarse claramente al final:
- cancelar
- aceptar / guardar
- otras solo si son necesarias

---

## 17. Modales

La guía muestra modales tipo Bootstrap con ancho cercano a `598px`, padding interno controlado y acciones al pie. :contentReference[oaicite:9]{index=9}

### 17.1 Dimensiones y composición

Referencia visual aproximada:
- ancho modal cercano a `598px`
- padding interno visible de `15px`
- separación entre contenido y acciones cercana a `30px`

### 17.2 Partes del modal

- encabezado con título
- cuerpo con contenido o formulario
- pie con acciones

### 17.3 Colores y fondos

- fondo del modal claro
- overlay oscurecido sobre la pantalla de fondo
- botones alineados al patrón institucional

### 17.4 Reglas

- no crear modales gigantes sin necesidad
- mantener título claro
- alinear acciones al final
- evitar exceso de campos si el modal no lo soporta bien
- si el proyecto usa drawer o panel lateral en vez de modal, respetar el patrón real del módulo base

---

## 18. Iconografía

### 18.1 Fuente de iconos

Usar la librería institucional ya presente en el proyecto. La guía referencia `Font Awesome`. :contentReference[oaicite:10]{index=10}

### 18.2 Reglas

- los iconos deben tener tamaño visual homogéneo
- no mezclar estilos incompatibles
- usar iconos solo cuando aporten claridad funcional
- mantener consistencia entre acciones equivalentes

---

## 19. Comportamiento responsive

Aunque la referencia es principalmente desktop, toda nueva vista debe adaptarse razonablemente a resoluciones menores sin romper estructura.

### 19.1 Reglas

- priorizar layout desktop administrativo
- evitar desbordes horizontales innecesarios
- permitir reacomodo de filtros cuando el ancho disminuya
- mantener tabla usable dentro de las capacidades del proyecto
- si el módulo base ya tiene una estrategia responsive, replicarla exactamente

---

## 20. Reutilización de estilos del proyecto

Antes de crear nuevos estilos, se debe revisar si el proyecto ya tiene:

- variables SCSS
- mixins
- tokens
- clases utilitarias
- componentes compartidos
- wrappers de formularios
- wrappers de tabla
- helpers de espaciado

### Regla obligatoria

Siempre reutilizar primero lo existente.

No crear nuevas reglas visuales si ya existe una convención equivalente dentro del proyecto.

---

## 21. Reglas para generación asistida por IA

Cuando una herramienta de IA cree una vista Sentinel, debe cumplir obligatoriamente esto:

1. leer primero este documento
2. leer la imagen de referencia visual
3. leer los estándares técnicos del proyecto
4. pedir al usuario el módulo base a escanear
5. escanear solo ese módulo
6. replicar exactamente su estructura y patrón
7. reutilizar componentes existentes
8. respetar esta guía visual
9. no crear arquitecturas paralelas
10. no cambiar librerías ni estructura fuera del alcance

---

## 22. Reglas específicas para vistas tipo listado administrativo

Cuando la pantalla sea similar a una vista de agentes/listado:

- el título debe estar en el encabezado del contenido
- las acciones principales deben estar arriba
- el buscador debe estar visible
- la tabla debe ocupar el bloque central
- la paginación debe quedar al pie
- el espaciado debe ser consistente
- la grilla no debe verse comprimida ni dispersa
- el resultado debe sentirse como una pantalla administrativa Sentinel nativa

---

## 23. Do / Don’t

### 23.1 Do

- usar `Open Sans`
- respetar el azul institucional
- usar espaciados de `5px`, `10px`, `15px` y `30px`
- mantener texto base de `13px`
- usar títulos destacados alrededor de `25px`
- reutilizar estilos, componentes y patrones existentes
- respetar el módulo base
- priorizar claridad y consistencia
- mantener tablas, filtros y acciones bien alineados

### 23.2 Don’t

- no inventar una nueva línea visual
- no introducir librerías visuales nuevas sin necesidad
- no mezclar múltiples familias tipográficas
- no usar colores ajenos a la paleta institucional
- no sobrecargar la vista con decoraciones
- no crear espaciados arbitrarios
- no romper la estructura del módulo base
- no implementar una solución “parecida”; debe sentirse nativa del sistema

---

## 24. Resumen operativo para implementación

Si vas a construir una nueva vista Sentinel, aplica este resumen:

- usa `Open Sans`
- usa iconografía institucional compatible con `Font Awesome`
- usa colores institucionales:
  - `#181d23`
  - `#2b333d`
  - `#74797b`
  - `#bcc3c8`
  - `#dfe0e7`
  - `#f1f2f7`
  - `#0066a6`
  - `#0076c0`
  - `#59baf7`
  - `#46a600`
  - `#5bb875`
  - `#c96a0d`
  - `#e2954a`
  - `#c90d31`
  - `#d9556e`
- usa espaciados base:
  - `5px`
  - `10px`
  - `15px`
  - `30px`
- usa texto general de `13px`
- usa títulos destacados de `25px`
- crea vistas administrativas sobrias
- mantén encabezado, filtros, tabla y paginación bien definidos
- replica exactamente la estructura del módulo base
- reutiliza todo lo posible antes de crear algo nuevo

---

## 25. Referencias internas

Archivos recomendados de apoyo:

- `docs/ui/sentinel-generative-agents-reference.png`
- `docs/ui/sentinel-ui-style-guide-source.pdf`

Este documento debe considerarse la referencia textual principal de estilo para nuevas vistas Sentinel.