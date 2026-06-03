# FASE 1 — Reporte Técnico de Auditoría HTML5

**Curso:** ISW-521 Programación en Ambiente Web I 
**Tema:** HTML5 Avanzado — Auditoría y Refactorización de Código 
**Archivo auditado:** `v1_base_feria_innovacion.html` 
**Sitio:** Feria Nacional de Innovación Estudiantil 2025 

---

## 1. Objetivo del reporte

El objetivo de esta auditoría es identificar, clasificar y documentar los principales problemas técnicos presentes en el archivo `v1_base_feria_innovacion.html`.

El código funciona visualmente en un navegador, pero presenta varios errores de estructura HTML5, semántica, accesibilidad, rendimiento, seguridad y mantenimiento. Esto significa que aunque la página “se ve”, internamente no está construida de una forma profesional ni fácil de escalar.

---

# 1.1 — Análisis del problema “Div-Soup”

## 1.1.1 Etiquetas HTML5 semánticas ausentes

En el archivo original se observa un uso excesivo de `<div>` para construir toda la estructura principal del documento.

Las etiquetas semánticas HTML5 que están completamente ausentes son:

- `<header>`
- `<main>`
- `<nav>`
- `<footer>`
- `<section>`
- `<article>`
- `<aside>`

Estas etiquetas deberían usarse para definir partes claras del documento. Por ejemplo:

- `<header>` para el encabezado principal.
- `<nav>` para el menú de navegación.
- `<main>` para el contenido principal.
- `<section>` para dividir bloques temáticos.
- `<article>` para contenido independiente, como cada proyecto finalista.
- `<footer>` para el pie de página.
- `<aside>` para contenido complementario, si existiera.

### Evidencia en el código original

```html
<div class="encabezado">
    <div>
        <div>
            <h1>Feria Nacional de Innovación Estudiantil 2025</h1>
            <div>ITCR Campus Cartago · 22, 23 y 24 de Octubre 2025</div>
            <div>Creando soluciones para los retos del mañana</div>
        </div>
    </div>
</div>

<div class="menu">
    <a href="#inicio">Inicio</a>
    <a href="#proyectos">Proyectos</a>
    <a href="#agenda">Agenda</a>
    <a href="#inscripcion">Inscripción</a>
    <a href="#sede">Sede</a>
</div>

<div class="contenido">
    ...
</div>

<div class="pie">
    ...
</div>
```

El problema es que estas partes sí tienen significado estructural, pero el código las trata como simples contenedores genéricos.

---

## 1.1.2 Problema del uso excesivo de `<div>` para SEO y estructura

El uso excesivo de `<div>` afecta negativamente la comprensión estructural del documento.

Un `<div>` no comunica significado por sí solo. Para el navegador, los motores de búsqueda y las tecnologías de asistencia, un `<div>` solamente indica que hay una división genérica. No dice si ese bloque es un encabezado, una navegación, una sección principal, un artículo o un pie de página.

Desde el punto de vista SEO, esto dificulta que los motores de búsqueda entiendan la jerarquía real del contenido. Google y otros buscadores pueden leer el texto, pero no reciben señales semánticas claras sobre qué parte del documento es más importante o qué función cumple cada sección.

Ejemplo problemático:

```html
<div class="menu">
    <a href="#inicio">Inicio</a>
    <a href="#proyectos">Proyectos</a>
    <a href="#agenda">Agenda</a>
</div>
```

Aunque visualmente funciona como menú, técnicamente debería ser:

```html
<nav>
    ...
</nav>
```

La etiqueta `<nav>` comunica explícitamente que ese bloque contiene navegación principal.

---

## 1.1.3 Qué es “Div-Soup” y su impacto real

“Div-Soup” significa una estructura HTML construida casi totalmente con `<div>`, sin usar etiquetas semánticas adecuadas.

En el archivo auditado, esto se observa porque casi todas las partes importantes de la página se construyen con `<div>`:

```html
<div id="inicio" class="tarjeta">
    <h2>Acerca de la Feria</h2>
    <div>
        <p>...</p>
    </div>
</div>
```

```html
<div id="proyectos" class="tarjeta">
    <h2>Proyectos Finalistas</h2>
    <div>
        <div class="tarjeta">
            ...
        </div>
    </div>
</div>
```

El impacto real en un proyecto profesional es alto:

1. **Mantenimiento más difícil:** otros desarrolladores deben adivinar qué representa cada `<div>`.
2. **Escalabilidad limitada:** al crecer el sitio, la estructura se vuelve confusa.
3. **Menor accesibilidad:** lectores de pantalla y herramientas de asistencia tienen menos información para navegar.
4. **Menor calidad técnica:** el documento pierde claridad semántica.
5. **Mayor riesgo de errores:** cambiar una parte puede afectar otra porque no hay una jerarquía clara.

---

# 1.2 — Análisis del Formulario de Inscripción

## 1.2.1 Uso incorrecto o ausente de `<label>`

En el formulario no se usan etiquetas `<label>` correctamente vinculadas a los campos mediante `for` e `id`.

En lugar de usar `<label>`, el código usa `<div>` como texto descriptivo:

```html
<div>Nombre del equipo o proyecto:</div>
<input type="text" placeholder="Nombre oficial del proyecto">

<div>Nombre del responsable principal:</div>
<input type="text" placeholder="Nombre y apellidos completos">

<div>Correo de contacto:</div>
<input type="text" placeholder="correo@institucion.ac.cr">

<div>Número de teléfono:</div>
<input type="text" placeholder="XXXX-XXXX">
```

Esto es un problema porque el navegador no puede asociar formalmente el texto con su campo correspondiente.

La forma correcta sería algo similar a:

```html
<label for="nombre-equipo">Nombre del equipo o proyecto:</label>
<input id="nombre-equipo" name="nombre-equipo" type="text">
```

### Impacto para el usuario final

La ausencia de `<label>` afecta especialmente la accesibilidad y la experiencia de usuario:

- Un lector de pantalla puede no identificar claramente qué debe escribir el usuario en cada campo.
- Al hacer clic sobre el texto, el campo no se activa.
- El formulario es más difícil de usar para personas con discapacidad visual o motora.
- Se depende demasiado del `placeholder`, pero el `placeholder` desaparece cuando el usuario escribe.

Además, varios campos tienen `type="text"` aunque deberían usar tipos más específicos:

```html
<input type="text" placeholder="correo@institucion.ac.cr">
<input type="text" placeholder="XXXX-XXXX">
```

El correo debería usar `type="email"` y el teléfono podría usar `type="tel"`.

---

## 1.2.2 Elementos semánticos para agrupar datos

El formulario no agrupa los datos por bloques lógicos. Todo está colocado en una misma secuencia de campos.

El elemento semántico correcto para agrupar datos relacionados es:

```html
<fieldset>
```

La etiqueta que describe el propósito de cada grupo es:

```html
<legend>
```

Para este formulario deberían existir al menos dos grupos:

1. **Datos del equipo o responsable**
2. **Detalles del proyecto**

Ejemplo de estructura recomendada:

```html
<fieldset>
    <legend>Datos del equipo</legend>
    ...
</fieldset>

<fieldset>
    <legend>Detalles del proyecto</legend>
    ...
</fieldset>
```

Esto mejora la comprensión del formulario y permite que el usuario entienda mejor qué información está completando.

---

## 1.2.3 Análisis del campo “Carrera o programa académico”

El campo “Carrera o programa académico” usa actualmente un `<select>`:

```html
<div>Carrera o programa académico:</div>
<select>
    <option>Seleccione su carrera</option>
    <option>Ingeniería en Computación</option>
    <option>Ingeniería Eléctrica</option>
    <option>Ingeniería Ambiental</option>
    <option>Biotecnología</option>
    <option>Diseño Industrial</option>
    <option>Administración de Empresas</option>
    <option>Agronomía</option>
    <option>Arquitectura</option>
    <option>Otra</option>
</select>
```

Un `<datalist>` sería técnicamente superior en este caso porque permite sugerir opciones sin obligar al usuario a elegir solamente una de ellas.

La diferencia funcional es:

- `<select>`: el usuario debe escoger una opción cerrada de una lista.
- `<datalist>`: el usuario puede escribir libremente, pero recibe sugerencias disponibles.

Para “Carrera o programa académico”, esto tiene más sentido porque pueden existir muchas carreras o programas que no estén en la lista.

Ejemplo recomendado:

```html
<label for="carrera">Carrera o programa académico:</label>
<input id="carrera" name="carrera" list="lista-carreras">

<datalist id="lista-carreras">
    <option value="Ingeniería en Computación">
    <option value="Ingeniería Eléctrica">
    <option value="Ingeniería Ambiental">
    <option value="Biotecnología">
    <option value="Diseño Industrial">
    <option value="Administración de Empresas">
    <option value="Agronomía">
    <option value="Arquitectura">
</datalist>
```

---

# 1.3 — Análisis de la Tabla de Agenda

## 1.3.1 Secciones estructurales ausentes

La tabla de agenda no tiene las secciones estructurales recomendadas:

- `<caption>`
- `<thead>`
- `<tbody>`
- `<tfoot>`

### Evidencia en el código original

```html
<table>
    <tr>
        <th>Hora</th>
        <th>Miércoles 22 Oct</th>
        <th>Jueves 23 Oct</th>
        <th>Viernes 24 Oct</th>
    </tr>
    <tr>
        <td>7:30 - 8:30</td>
        <td>Registro y acreditación</td>
        <td>Apertura de sala</td>
        <td>Apertura de sala</td>
    </tr>
    ...
    <tr>
        <td><strong>Total horas</strong></td>
        <td><strong>9 horas</strong></td>
        <td><strong>9 horas</strong></td>
        <td><strong>7 horas</strong></td>
    </tr>
</table>
```

La tabla funciona visualmente, pero está incompleta semánticamente.

---

## 1.3.2 Por qué `<thead>`, `<tbody>` y `<tfoot>` son funcionales

Estas etiquetas no son meramente estéticas. Ayudan a dividir la tabla según su función:

- `<thead>`: contiene los encabezados de columnas.
- `<tbody>`: contiene los datos principales.
- `<tfoot>`: contiene totales, resúmenes o conclusiones.

En esta tabla, la primera fila debería estar dentro de `<thead>`, las actividades deberían estar dentro de `<tbody>` y la fila de total de horas debería estar dentro de `<tfoot>`.

Esto ayuda a:

- Lectores de pantalla.
- Navegadores.
- Herramientas de análisis.
- Exportación o procesamiento de datos.
- Mantenimiento del código.

---

## 1.3.3 Falta del atributo `scope` en los encabezados `<th>`

Los encabezados de la tabla usan `<th>`, pero no tienen el atributo `scope`.

Código actual:

```html
<th>Hora</th>
<th>Miércoles 22 Oct</th>
<th>Jueves 23 Oct</th>
<th>Viernes 24 Oct</th>
```

Como estos encabezados describen columnas, deberían usar:

```html
<th scope="col">Hora</th>
<th scope="col">Miércoles 22 Oct</th>
<th scope="col">Jueves 23 Oct</th>
<th scope="col">Viernes 24 Oct</th>
```

Además, las horas de cada fila podrían marcarse como encabezados de fila usando `scope="row"`:

```html
<th scope="row">7:30 - 8:30</th>
```

El valor `colgroup` no sería necesario en esta tabla, porque no hay grupos de columnas definidos mediante `<colgroup>`.

### Impacto de omitir `scope`

Sin `scope`, las tecnologías de asistencia tienen menos información para relacionar cada celda con su encabezado. Esto puede causar que una persona usando lector de pantalla no entienda correctamente a qué día corresponde una actividad.

---

## 1.3.4 Ausencia de `<caption>`

No hay un elemento `<caption>` presente en la tabla.

El `<caption>` sirve para describir el propósito de la tabla. En este caso, podría ser:

```html
<caption>Agenda oficial de actividades de la Feria Nacional de Innovación Estudiantil 2025</caption>
```

Esto es importante porque el usuario entiende rápidamente qué representa la tabla antes de leer sus filas y columnas. También mejora la accesibilidad porque los lectores de pantalla pueden anunciar el propósito de la tabla.

---

# 1.4 — Análisis del Elemento Video

## 1.4.1 Atributo faltante para imagen previa

El video no tiene el atributo `poster`.

Código actual:

```html
<video width="100%">
    <source src="video/feria_presentacion.mp4" type="video/mp4">
</video>
```

El atributo que falta es:

```html
poster="img/feria-poster.jpg"
```

El `poster` permite mostrar una imagen previa antes de que el usuario reproduzca el video.

### Impacto en CLS y Core Web Vitals

La falta de `poster` puede afectar la experiencia visual porque el video puede aparecer como un bloque vacío o cargar de forma inestable. Si no se reservan correctamente dimensiones y contenido visual, puede generar movimientos inesperados en la página.

Esto se relaciona con el Cumulative Layout Shift (CLS), una métrica de Core Web Vitals que mide los cambios inesperados en el layout mientras carga la página.

Aunque el video tiene `width="100%"`, no tiene una imagen previa ni una proporción visual clara mediante `height` o CSS moderno como `aspect-ratio`. Esto puede afectar la estabilidad visual de la página.

---

## 1.4.2 Problema de tener un solo `<source>`

El video tiene únicamente una fuente en formato MP4:

```html
<source src="video/feria_presentacion.mp4" type="video/mp4">
```

Esto es limitado porque no todos los navegadores o contextos soportan los mismos formatos con la misma eficiencia.

Para mayor compatibilidad cruzada, deberían agregarse al menos dos formatos:

```html
<source src="video/feria_presentacion.mp4" type="video/mp4">
<source src="video/feria_presentacion.webm" type="video/webm">
```

Formatos recomendados:

- `video/mp4`
- `video/webm`

Opcionalmente también podría considerarse `video/ogg`, aunque hoy en día MP4 y WebM suelen ser los más comunes.

---

## 1.4.3 Falta del atributo `controls`

El video no tiene el atributo `controls`.

Código actual:

```html
<video width="100%">
```

Debería ser:

```html
<video width="100%" controls>
```

Sin `controls`, el usuario no tiene botones nativos para reproducir, pausar, cambiar volumen o avanzar en el video.

Esto representa un problema de usabilidad porque el contenido multimedia queda presente, pero no se puede controlar fácilmente.

---

# 1.5 — Análisis del iFrame del Mapa

## 1.5.1 Falta del atributo de rendimiento `loading`

El `<iframe>` de Google Maps no tiene el atributo `loading`.

Código actual:

```html
<iframe
    src="https://www.google.com/maps/embed?pb=..."
    width="100%"
    height="420"
    style="border:0;"
    allowfullscreen="">
</iframe>
```

El atributo recomendado es:

```html
loading="lazy"
```

Este atributo hace que el mapa no cargue inmediatamente al abrir la página, sino hasta que el usuario se acerque a esa parte del documento.

Esto mejora el rendimiento inicial, porque los mapas embebidos suelen ser pesados y pueden retrasar la carga de la página.

---

## 1.5.2 Falta del atributo de seguridad `sandbox`

El iframe tampoco tiene el atributo `sandbox`.

El atributo faltante es:

```html
sandbox
```

Este atributo limita lo que el contenido embebido puede hacer dentro de la página.

Una configuración posible para un mapa embebido podría ser:

```html
sandbox="allow-scripts allow-same-origin"
```

Sin embargo, debe usarse con cuidado, porque mientras más permisos se agreguen, menor es el aislamiento.

Al menos tres restricciones importantes que deberían mantenerse activas, salvo necesidad real, son:

1. No permitir formularios embebidos con `allow-forms`.
2. No permitir ventanas emergentes con `allow-popups`.
3. No permitir navegación superior con `allow-top-navigation`.

El problema del código actual es que el iframe queda sin una política explícita de aislamiento. Esto puede representar un riesgo, especialmente cuando se incrusta contenido externo.

---

## 1.5.3 Falta del atributo `title`

El iframe no tiene atributo `title`.

Código actual:

```html
<iframe
    src="https://www.google.com/maps/embed?pb=..."
    width="100%"
    height="420"
    style="border:0;"
    allowfullscreen="">
</iframe>
```

Debería incluir algo como:

```html
title="Mapa de ubicación del ITCR Campus Central Cartago"
```

El `title` es necesario porque ayuda a identificar el propósito del contenido embebido. Para usuarios con lector de pantalla, un iframe sin título puede resultar confuso porque no se comunica claramente qué contiene.

---

# 1.6 — Análisis del Anidamiento Incorrecto

## 1.6.1 Instancias donde un elemento de bloque está anidado dentro de un elemento de línea

En el código original existen errores de anidamiento donde elementos de bloque aparecen dentro de elementos de línea.

### Caso 1: `<div>` y `<h3>` dentro de `<span>`

```html
<span>
    <div>
        <h3>Secretaría de la Feria</h3>
        <div>feria.innovacion@itcr.ac.cr</div>
        <div>Teléfono: 2550-9000 ext. 3100</div>
    </div>
</span>
```

Este caso es problemático porque `<span>` es un elemento de línea pensado para contenido de frase, no para contener bloques como `<div>` o encabezados como `<h3>`.

Una mejor estructura sería:

```html
<section>
    <h3>Secretaría de la Feria</h3>
    <p>feria.innovacion@itcr.ac.cr</p>
    <p>Teléfono: 2550-9000 ext. 3100</p>
</section>
```

---

### Caso 2: `<div>` dentro de `<a>`

```html
<a href="https://www.tec.ac.cr">
    <div>
        <div>Portal oficial del ITCR</div>
        <div>www.tec.ac.cr · Campus Cartago</div>
    </div>
</a>
```

Este caso es riesgoso dentro del contexto del laboratorio porque se está usando un enlace como contenedor de bloques completos.

Nota técnica: en HTML5, un `<a>` puede envolver cierto contenido de flujo si no contiene elementos interactivos dentro. Aun así, para este ejercicio, la estructura es poco clara y conviene evitar usar el enlace como contenedor genérico. Una alternativa más limpia sería colocar el enlace dentro de un párrafo o dentro de una tarjeta estructurada correctamente.

Ejemplo recomendado:

```html
<p>
    <a href="https://www.tec.ac.cr">Portal oficial del ITCR</a>
</p>
<p>www.tec.ac.cr · Campus Cartago</p>
```

---

## 1.6.2 Por qué el navegador intenta corregir estos errores

Los navegadores intentan construir un DOM válido incluso cuando el HTML tiene errores. Por eso, al encontrar un anidamiento incorrecto, el navegador puede cerrar etiquetas automáticamente, mover nodos o reorganizar partes del árbol del documento.

Esto puede provocar que el DOM final no sea exactamente igual al código escrito.

El problema es que esa “corrección automática” puede romper el layout de maneras impredecibles. Por ejemplo:

- Un elemento puede terminar fuera del contenedor esperado.
- Un estilo CSS puede dejar de aplicarse correctamente.
- Una sección puede cambiar de jerarquía.
- Un lector de pantalla puede interpretar la estructura de forma diferente.
- El comportamiento de enlaces o bloques clicables puede ser inconsistente.

En proyectos profesionales esto es peligroso porque el error puede no verse inmediatamente, pero puede aparecer al cambiar CSS, agregar scripts o probar en otro navegador.

---

## 1.6.3 Cómo verificar este tipo de error con DevTools

Para verificar errores de anidamiento con DevTools se puede seguir este procedimiento:

1. Abrir el archivo `v1_base_feria_innovacion.html` en Google Chrome o Microsoft Edge.
2. Presionar `F12` o clic derecho y elegir “Inspeccionar”.
3. Ir a la pestaña **Elements**.
4. Buscar la sección de contacto.
5. Comparar el código fuente original con el árbol DOM que muestra DevTools.
6. Revisar si el navegador movió, cerró o reorganizó etiquetas automáticamente.
7. Expandir los nodos `<span>` y `<a>` para verificar si contienen elementos que no deberían.
8. Usar también el validador W3C para confirmar errores estructurales.

La clave es no revisar solamente el archivo fuente, sino también el DOM final interpretado por el navegador.

---

# 2. Resumen de hallazgos

| Área auditada | Problema encontrado | Impacto |
|---|---|---|
| Estructura general | Uso excesivo de `<div>` | Baja semántica, peor mantenimiento y menor claridad |
| Semántica HTML5 | Ausencia de `<header>`, `<main>`, `<nav>`, `<footer>`, `<section>`, `<article>`, `<aside>` | Documento poco estructurado |
| Formulario | No hay `<label>` con `for` e `id` | Problemas de accesibilidad y usabilidad |
| Formulario | No hay `<fieldset>` ni `<legend>` | Campos sin agrupación lógica |
| Campo de carrera | Uso de `<select>` en vez de `<datalist>` | Menor flexibilidad para el usuario |
| Tabla | No hay `<caption>`, `<thead>`, `<tbody>`, `<tfoot>` | Tabla menos accesible y menos funcional |
| Tabla | `<th>` sin `scope` | Relación débil entre encabezados y celdas |
| Video | Falta `poster` | Peor experiencia visual y posible impacto en CLS |
| Video | Falta `controls` | El usuario no puede controlar la reproducción |
| Video | Solo existe un formato fuente | Menor compatibilidad entre navegadores |
| Iframe | Falta `loading="lazy"` | Carga inicial más pesada |
| Iframe | Falta `sandbox` | Menor aislamiento de seguridad |
| Iframe | Falta `title` | Problema de accesibilidad |
| Anidamiento | Bloques dentro de elementos de línea | DOM impredecible y posible ruptura del layout |

---

# 3. Conclusión de la auditoría

El archivo `v1_base_feria_innovacion.html` presenta una estructura visualmente funcional, pero técnicamente deficiente. El principal problema es el uso excesivo de `<div>` como contenedor universal, lo que produce un caso claro de “Div-Soup”.

Además, el formulario carece de etiquetas accesibles, la tabla no está estructurada correctamente, el video no ofrece controles ni compatibilidad suficiente, el iframe no tiene atributos importantes de rendimiento, seguridad y accesibilidad, y existen errores de anidamiento que pueden afectar la interpretación del DOM.

La página debe refactorizarse usando HTML5 semántico, formularios accesibles, tablas estructuradas, multimedia controlable y contenido embebido con mejores prácticas de rendimiento y seguridad.

En resumen, el código necesita una refactorización completa para pasar de una página que solo “se ve bien” a una página correctamente construida, mantenible, accesible y alineada con estándares modernos de HTML5.

---

# 4. Recomendaciones principales para la siguiente fase

Para la Fase 2, el prompt de refactorización debería exigir como mínimo:

1. Reemplazar `<div>` estructurales por etiquetas semánticas.
2. Usar `<header>`, `<nav>`, `<main>` y `<footer>`.
3. Convertir cada bloque principal en `<section>`.
4. Convertir cada proyecto finalista en `<article>`.
5. Agregar `<label for="">` e `id` a todos los campos del formulario.
6. Agrupar el formulario con `<fieldset>` y `<legend>`.
7. Cambiar el campo de carrera a `<input list="">` con `<datalist>`.
8. Estructurar la tabla con `<caption>`, `<thead>`, `<tbody>` y `<tfoot>`.
9. Agregar `scope` a todos los encabezados `<th>`.
10. Agregar `poster`, `controls` y fuentes alternativas al video.
11. Agregar `loading="lazy"`, `sandbox` y `title` al iframe.
12. Corregir todo anidamiento incorrecto de elementos.

---
