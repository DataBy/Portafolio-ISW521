# FASE 3 — Revisión Final del DOM

**Curso:** ISW-521 Programación en Ambiente Web I 
**Laboratorio:** HTML5 Avanzado — Auditoría y Refactorización de Código 
**Archivo revisado:** `v2_feria_refactorizado_final_OK.html` 
**Archivo original:** `v1_base_feria_innovacion.html` 
**Evidencia:** captura del Validador W3C adjunta como archivo aparte.

---

## 3.1 — Validación con el Validador W3C

Para validar el archivo final, se utilizó el validador oficial de W3C en la opción **Validate by Direct Input**. Se copió el contenido completo del archivo `v2_feria_refactorizado_final_OK.html`, se pegó en el área de texto del validador y se ejecutó la revisión con el botón **Check**.

Después de revisar el resultado inicial, se corrigieron los mensajes reportados por el validador. Los ajustes aplicados fueron los siguientes:

1. En el `<select>` de **Categoría de participación**, se agregó una primera opción vacía para cumplir correctamente con el uso de `required`:

```html
<option value="" selected>Seleccione una categoría</option>
```

2. En el `<iframe>` del mapa, se ajustó el atributo `sandbox`, eliminando `allow-same-origin` para evitar la advertencia generada por la combinación de permisos demasiado amplia. El valor final usado fue:

```html
sandbox="allow-scripts allow-popups"
```

3. Se verificó que el `iframe` conservara los atributos necesarios de rendimiento, accesibilidad y seguridad:

```html
loading="lazy"
title="Mapa de ubicación del ITCR Campus Central Cartago"
sandbox="allow-scripts allow-popups"
```

Luego de aplicar estas correcciones, el documento fue validado nuevamente. La captura tomada del resultado final del Validador W3C se entrega como evidencia en un archivo aparte.

**Captura de validación:**

![Captura del Validador W3C](captura_validacion_w3c.png)

---

## 3.2 — Inspección del DOM con DevTools

La revisión manual del DOM se realizó abriendo el archivo `v2_feria_refactorizado_final_OK.html` en el navegador y usando las DevTools con la tecla **F12**. En la pestaña **Elements**, se inspeccionó la estructura real que el navegador construyó a partir del HTML.

### Presencia de etiquetas principales

Se confirmó que la página usa correctamente las etiquetas principales de HTML5:

```html
<body>
    <header>...</header>
    <nav>...</nav>
    <main>...</main>
    <footer>...</footer>
</body>
```

Esto corrige el problema del archivo original, donde casi toda la estructura dependía de `<div>` con clases como `encabezado`, `menu`, `contenido`, `tarjeta` y `pie`.

### Organización del contenido principal

Dentro de `<main>`, el contenido quedó dividido en secciones claras:

- `section id="inicio"` para la información general de la feria.
- `section` para el video de presentación.
- `section id="proyectos"` para los proyectos finalistas.
- `section id="agenda"` para la agenda del evento.
- `section id="inscripcion"` para el formulario.
- `section id="sede"` para la ubicación.
- `section` para contacto y consultas.

Además, los proyectos finalistas fueron organizados con `<article>`, porque cada proyecto funciona como una unidad de contenido independiente dentro de la sección de proyectos.

### Revisión de anidamiento incorrecto

Se revisó que no existieran elementos de bloque colocados dentro de elementos de línea. En el archivo original sí existían problemas como:

```html
<span>
    <div>
        <h3>Secretaría de la Feria</h3>
    </div>
</span>
```

Y también:

```html
<a href="https://www.tec.ac.cr">
    <div>
        <div>Portal oficial del ITCR</div>
        <div>www.tec.ac.cr · Campus Cartago</div>
    </div>
</a>
```

En la versión corregida, estas estructuras fueron reemplazadas por elementos válidos. La sección de contacto usa `<article>`, `<address>`, `<p>` y enlaces correctamente ubicados. No se encontraron `<div>`, `<p>` ni encabezados `<h1>` a `<h6>` como hijos directos de un `<span>`.

### Revisión del formulario

El formulario fue inspeccionado en el DOM y se comprobó que los campos están agrupados con `<fieldset>` y `<legend>`:

```html
<fieldset>
    <legend>Datos del equipo</legend>
</fieldset>

<fieldset>
    <legend>Detalles del proyecto</legend>
</fieldset>

<fieldset>
    <legend>Confirmaciones</legend>
</fieldset>
```

También se confirmó que cada `<label>` utiliza el atributo `for` vinculado al `id` del campo correspondiente. Esto mejora la accesibilidad y permite que el usuario pueda activar el campo al hacer clic sobre el texto de la etiqueta.

El campo **Carrera o programa académico** fue corregido para usar `input` con `datalist`, permitiendo escribir una opción personalizada o seleccionar una opción sugerida:

```html
<input id="carrera" name="carrera" type="text" list="lista-carreras">
<datalist id="lista-carreras">
    <option value="Ingeniería en Computación"></option>
    <option value="Ingeniería Eléctrica"></option>
    <option value="Ingeniería Ambiental"></option>
</datalist>
```

### Revisión de la tabla

La tabla de agenda fue inspeccionada y ahora tiene una estructura semántica completa:

```html
<table>
    <caption>Horario oficial de actividades...</caption>
    <thead>...</thead>
    <tbody>...</tbody>
    <tfoot>...</tfoot>
</table>
```

También se verificó que los encabezados principales usan `scope="col"` y los encabezados de hora usan `scope="row"`. Esto permite interpretar mejor la relación entre las horas, los días y las actividades.

### Revisión del video

El video ahora tiene los atributos y fuentes requeridas:

```html
<video controls poster="img/feria_poster.jpg">
    <source src="video/feria_presentacion.mp4" type="video/mp4">
    <source src="video/feria_presentacion.webm" type="video/webm">
</video>
```

Con esto se corrige la falta de controles, la ausencia de imagen previa y la falta de una segunda fuente para mejorar compatibilidad entre navegadores.

### Revisión del iframe

El mapa embebido fue corregido con atributos de rendimiento, seguridad y accesibilidad:

```html
<iframe
    loading="lazy"
    sandbox="allow-scripts allow-popups"
    title="Mapa de ubicación del ITCR Campus Central Cartago">
</iframe>
```

El atributo `loading="lazy"` evita que el mapa cargue de inmediato si el usuario todavía no ha llegado a esa sección. El atributo `sandbox` limita permisos del contenido embebido y el atributo `title` permite identificar el propósito del iframe.

---

## Comparación entre versión original y versión refactorizada

La versión original estaba construida principalmente con `<div>`, lo que hacía que la estructura fuera menos clara para el navegador, para lectores de pantalla y para otros desarrolladores. Aunque visualmente la página podía funcionar, el documento no expresaba bien qué parte era encabezado, navegación, contenido principal, secciones o pie de página.

En la versión refactorizada, la jerarquía del documento es más clara. El `<body>` contiene directamente `header`, `nav`, `main` y `footer`. El contenido principal está separado en `section` y los proyectos se representan con `article`. La tabla tiene estructura completa, el formulario está agrupado correctamente y los elementos multimedia tienen atributos más seguros y accesibles.

El cambio principal no fue solo visual, sino estructural. El HTML final comunica mejor la intención de cada parte de la página.

---

## 3.3 — Checklist de Verificación Final

- [x] La página usa `<header>`, `<nav>`, `<main>` y `<footer>` en lugar de `<div>` estructural.
- [x] El contenido principal se divide en `<section>` o `<article>` con semántica apropiada.
- [x] El formulario tiene al menos dos grupos `<fieldset>` con `<legend>` descriptivos.
- [x] Todos los `<label>` usan `for` vinculado al `id` de su campo correspondiente.
- [x] El campo de carrera usa `<input list="...">` + `<datalist>` y no un `<select>`.
- [x] El `<video>` tiene `poster`, `controls` y mínimo dos `<source>` con distinto `type`.
- [x] El `<iframe>` tiene `loading="lazy"`, `sandbox` con valores apropiados y `title`.
- [x] No hay elementos de bloque como `<div>`, `<p>` o encabezados dentro de `<span>`.
- [x] La tabla tiene `<caption>`, `<thead>`, `<tbody>`, `<tfoot>` y los `<th>` tienen `scope`.
- [x] La validación W3C fue revisada después de aplicar las correcciones finales.

---

## Reflexión final

Trabajar con IA para refactorizar código puede ahorrar bastante tiempo, pero esta práctica me dejó claro que no se debe confiar ciegamente en el primer resultado. La IA puede generar una estructura aparentemente correcta, pero todavía pueden quedar detalles que solo se detectan revisando con herramientas como el Validador W3C o inspeccionando el DOM en el navegador. En este caso, el código generado mejoró mucho el uso de HTML5 semántico, el formulario, la tabla, el video y el iframe, pero fue necesario revisar errores puntuales como el primer `option` de un `select required` y una advertencia de seguridad en el `sandbox` del iframe. La parte más importante fue entender que usar IA no reemplaza el criterio técnico. Más bien, la IA ayuda a producir una base, pero el desarrollador sigue siendo responsable de validar, corregir y justificar que el resultado final cumpla con los estándares.

---

## Archivos relacionados para la entrega

- `v1_base_feria_innovacion.html`
- `v2_feria_refactorizado_final_OK.html`
- `captura_validacion_w3c.png`
- `FASE_3_Revision_Final_DOM.md`
