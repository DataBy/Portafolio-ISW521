# FASE 2 — Ingeniería de Prompts para Refactorización HTML5

## 1. Datos generales

**Curso:** ISW-521 Programación en Ambiente Web I 
**Laboratorio:** HTML5 Avanzado — Auditoría y Refactorización de Código 
**Archivo original analizado:** `v1_base_feria_innovacion.html` 
**Archivo generado por la IA:** `v2_feria_refactorizado_ia.html` 
**Objetivo de esta fase:** construir un prompt técnico de alta precisión para que una IA refactorice correctamente el código HTML deficiente, aplicando HTML5 semántico, accesibilidad básica, estructura correcta de formularios, tabla bien formada, video completo, iframe más seguro y corrección del anidamiento inválido.

---

## 2. Prompt técnico construido

### Sección A — Rol y contexto

Actúa como un Desarrollador Frontend Senior especializado en HTML5 semántico, accesibilidad web básica, estándares W3C, estructura correcta del DOM y buenas prácticas de mantenimiento en sitios institucionales.

Vas a recibir el código HTML completo de un sitio web llamado **Feria Nacional de Innovación Estudiantil 2025**. El código fue generado de forma deficiente y debe ser refactorizado sin cambiar el contenido principal del sitio.

Tu tarea es devolver una versión corregida, moderna y semánticamente válida del documento HTML.

### Sección B — Descripción del problema

El archivo recibido presenta varios problemas técnicos:

- Uso excesivo de `<div>` para construir toda la estructura del documento, generando un problema de tipo **Div-Soup**.
- Ausencia de etiquetas HTML5 semánticas como `<header>`, `<nav>`, `<main>`, `<section>`, `<article>` y `<footer>`.
- Formulario de inscripción sin etiquetas `<label>` correctamente vinculadas con `for` e `id`.
- Campos del formulario sin agrupación semántica mediante `<fieldset>` y `<legend>`.
- Campo “Carrera o programa académico” construido con `<select>`, aunque debería permitir escribir o seleccionar opciones mediante `<input list="...">` y `<datalist>`.
- Tabla de agenda sin `<caption>`, `<thead>`, `<tbody>`, `<tfoot>` ni atributos `scope` en sus encabezados.
- Elemento `<video>` sin `controls`, sin `poster` y con una sola fuente de video.
- `<iframe>` de Google Maps sin `loading="lazy"`, sin `sandbox` y sin `title` descriptivo.
- Errores de anidamiento donde elementos de bloque aparecen dentro de elementos de línea, especialmente `<div>` y `<h3>` dentro de `<span>`, y `<div>` dentro de `<a>`.

### Sección C — Restricciones técnicas explícitas

DEBES cumplir todas estas reglas:

1. DEBES conservar el contenido textual principal del sitio original.
2. DEBES reemplazar los `<div>` estructurales por etiquetas semánticas HTML5 correctas: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>` y `<footer>`.
3. DEBES dejar `<header>`, `<nav>`, `<main>` y `<footer>` como elementos principales dentro del `<body>`.
4. DEBES organizar el contenido principal en secciones claras mediante `<section>` y usar `<article>` para cada proyecto finalista.
5. DEBES usar `<h1>` solo para el título principal del sitio y mantener una jerarquía lógica con `<h2>` y `<h3>`.
6. DEBES corregir el formulario para que todos los campos tengan `<label>` asociado con `for`, y que cada campo tenga un `id` coincidente.
7. DEBES agrupar los campos del formulario usando `<fieldset>` y `<legend>`, creando al menos estos grupos: datos del equipo, detalles del proyecto y confirmaciones.
8. DEBES cambiar el campo “Carrera o programa académico” de `<select>` a `<input>` vinculado a un `<datalist>` con las mismas opciones.
9. DEBES mantener `<select>` solo donde sea más adecuado, por ejemplo para institución y categoría de participación.
10. DEBES corregir la tabla de agenda agregando `<caption>`, `<thead>`, `<tbody>` y `<tfoot>`.
11. DEBES agregar `scope="col"` a los encabezados superiores de la tabla y `scope="row"` a los encabezados de cada fila cuando corresponda.
12. DEBES mover la fila de totales de horas al `<tfoot>`.
13. DEBES corregir el elemento `<video>` agregando `controls`, `poster` y al menos dos elementos `<source>` con tipos `video/mp4` y `video/webm`.
14. DEBES agregar texto alternativo dentro de `<video>` para navegadores que no soporten video HTML5.
15. DEBES corregir el `<iframe>` agregando `loading="lazy"`, un atributo `sandbox` con permisos limitados y un `title` descriptivo.
16. DEBES evitar anidar elementos de bloque dentro de elementos de línea.
17. DEBES eliminar los casos de `<div>` dentro de `<span>` y `<div>` dentro de `<a>`.
18. DEBES usar `<address>` para los datos de contacto de la feria.
19. DEBES agregar `lang="es"` al elemento `<html>`.
20. DEBES agregar `<meta name="viewport" content="width=device-width, initial-scale=1.0">` en el `<head>`.
21. DEBES conservar un CSS simple dentro del mismo documento, sin usar archivos externos.
22. NO DEBES agregar JavaScript.
23. NO DEBES cambiar el tema visual general del sitio.
24. NO DEBES entregar explicaciones fuera del código final.

### Sección D — Criterios de validación

Antes de responder, verifica manualmente lo siguiente:

1. El documento usa `<!DOCTYPE html>` y `<html lang="es">`.
2. El `<body>` contiene estructura semántica principal: `<header>`, `<nav>`, `<main>` y `<footer>`.
3. No quedan `<div>` usados como estructura principal.
4. Los proyectos finalistas están representados como `<article>`.
5. Todos los campos del formulario tienen `<label for="...">` y un campo con `id` correspondiente.
6. El formulario tiene al menos dos grupos `<fieldset>` con `<legend>` descriptivo.
7. El campo carrera usa `<input list="...">` y `<datalist>`, no `<select>`.
8. La tabla contiene `<caption>`, `<thead>`, `<tbody>` y `<tfoot>`.
9. Todos los `<th>` tienen `scope="col"` o `scope="row"` según corresponda.
10. El `<video>` incluye `controls`, `poster`, un `<source>` MP4 y un `<source>` WebM.
11. El `<iframe>` incluye `loading="lazy"`, `sandbox` y `title`.
12. No existe ningún `<div>`, `<p>` ni `<h1>`-`<h6>` dentro de `<span>` o `<a>`.
13. La jerarquía de encabezados es lógica.
14. El documento puede pegarse en el Validador W3C para revisión.

### Sección E — Formato del resultado

Devuelve únicamente el código HTML completo y corregido, sin explicaciones, sin comentarios adicionales y sin texto antes o después del bloque de código. El resultado debe estar listo para guardarse como:

`v2_feria_refactorizado_ia.html`

---

## 3. Iteración documentada

### Primer intento

El prompt se construyó de forma específica incluyendo rol, contexto, descripción del problema, restricciones técnicas, criterios de validación y formato final esperado.

### Resultado de la iteración

El resultado fue satisfactorio porque el HTML generado:

- Sustituye la estructura basada en `<div>` por etiquetas semánticas.
- Corrige el formulario con `<label>`, `id`, `<fieldset>` y `<legend>`.
- Cambia el campo de carrera a `<input>` con `<datalist>`.
- Corrige la tabla con `<caption>`, `<thead>`, `<tbody>`, `<tfoot>` y `scope`.
- Agrega `controls`, `poster` y fuentes alternativas al video.
- Agrega `loading="lazy"`, `sandbox` y `title` al iframe.
- Elimina el anidamiento inválido de bloques dentro de elementos de línea.

No fue necesario realizar una segunda iteración del prompt porque el resultado cumplió los criterios principales de la Fase II.

---

## 4. Código HTML generado por la IA

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Feria de Innovación Estudiantil</title>
    <style>
        body { font-family: Georgia, serif; margin: 0; padding: 0; background: #f5f5f0; }
        header { background: #1a472a; color: white; padding: 24px; text-align: center; }
        nav { background: #2d6a4f; padding: 10px; }
        nav a { color: white; margin: 0 12px; text-decoration: none; }
        main { padding: 24px; max-width: 1100px; margin: auto; }
        footer { background: #1a472a; color: white; padding: 16px; text-align: center; }
        section, article { background: white; border: 1px solid #ccc; padding: 18px; margin: 14px 0; border-radius: 4px; }
        table { width: 100%; border-collapse: collapse; }
        caption { font-weight: bold; margin-bottom: 8px; text-align: left; }
        td, th { border: 1px solid #bbb; padding: 9px; text-align: left; }
        th { background: #2d6a4f; color: white; }
        input, select, textarea { width: 100%; padding: 9px; margin: 6px 0 14px; box-sizing: border-box; }
        input[type="checkbox"] { width: auto; margin-right: 8px; }
        fieldset { border: 1px solid #bbb; padding: 16px; margin: 14px 0; }
        legend { font-weight: bold; }
        video, iframe { width: 100%; }
        .boton { background: #2d6a4f; color: white; padding: 10px 22px; border: none; cursor: pointer; border-radius: 3px; }
        .enlace-tarjeta { display: block; color: #1a472a; text-decoration: none; border: 1px solid #ccc; padding: 12px; border-radius: 4px; }
    </style>
</head>
<body>

    <header>
        <h1>Feria Nacional de Innovación Estudiantil 2025</h1>
        <p>ITCR Campus Cartago · 22, 23 y 24 de Octubre 2025</p>
        <p>Creando soluciones para los retos del mañana</p>
    </header>

    <nav aria-label="Menú principal">
        <a href="#inicio">Inicio</a>
        <a href="#proyectos">Proyectos</a>
        <a href="#agenda">Agenda</a>
        <a href="#inscripcion">Inscripción</a>
        <a href="#sede">Sede</a>
    </nav>

    <main>
        <section id="inicio" aria-labelledby="titulo-inicio">
            <h2 id="titulo-inicio">Acerca de la Feria</h2>
            <p>
                La Feria Nacional de Innovación Estudiantil es el espacio anual donde estudiantes
                de todo el país presentan sus proyectos de investigación aplicada, prototipos tecnológicos
                y propuestas de emprendimiento ante un jurado de expertos nacionales e internacionales.
            </p>
            <p>
                Esta edición centra su atención en cuatro categorías: Robótica y Automatización,
                Biotecnología, Ciudades Inteligentes y Economía Circular.
            </p>
        </section>

        <section aria-labelledby="titulo-video">
            <h2 id="titulo-video">Video de Presentación</h2>
            <video controls poster="img/feria_poster.jpg">
                <source src="video/feria_presentacion.mp4" type="video/mp4">
                <source src="video/feria_presentacion.webm" type="video/webm">
                Su navegador no soporta la reproducción de video HTML5.
            </video>
            <p>Si el video no carga, verifique su conexión a internet.</p>
        </section>

        <section id="proyectos" aria-labelledby="titulo-proyectos">
            <h2 id="titulo-proyectos">Proyectos Finalistas</h2>

            <article aria-labelledby="titulo-ecosensor">
                <h3 id="titulo-ecosensor">EcoSensor Pro</h3>
                <p><strong>Equipo:</strong> Universidad de Costa Rica — Ingeniería Eléctrica</p>
                <p>
                    Sistema de monitoreo ambiental de bajo costo para comunidades rurales,
                    basado en microcontroladores ESP32 y red de sensores IoT.
                </p>
            </article>

            <article aria-labelledby="titulo-biofiltro">
                <h3 id="titulo-biofiltro">BioFiltro Urbano</h3>
                <p><strong>Equipo:</strong> TEC Campus San José — Ingeniería Ambiental</p>
                <p>
                    Prototipo de filtro biológico modular para la recuperación de agua gris
                    en edificios residenciales de alta densidad urbana.
                </p>
            </article>

            <article aria-labelledby="titulo-agrobot">
                <h3 id="titulo-agrobot">AgroBot CR</h3>
                <p><strong>Equipo:</strong> UNA Heredia — Agronomía e Informática</p>
                <p>
                    Robot autónomo de bajo costo para detección temprana de enfermedades
                    en cultivos de piña y banano usando visión computacional.
                </p>
            </article>
        </section>

        <section id="agenda" aria-labelledby="titulo-agenda">
            <h2 id="titulo-agenda">Agenda del Evento</h2>
            <table>
                <caption>Horario oficial de actividades de la Feria Nacional de Innovación Estudiantil 2025</caption>
                <thead>
                    <tr>
                        <th scope="col">Hora</th>
                        <th scope="col">Miércoles 22 Oct</th>
                        <th scope="col">Jueves 23 Oct</th>
                        <th scope="col">Viernes 24 Oct</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <th scope="row">7:30 - 8:30</th>
                        <td>Registro y acreditación</td>
                        <td>Apertura de sala</td>
                        <td>Apertura de sala</td>
                    </tr>
                    <tr>
                        <th scope="row">8:30 - 10:00</th>
                        <td>Ceremonia inaugural</td>
                        <td>Ronda de evaluación — Categoría A y B</td>
                        <td>Ronda final — Proyectos seleccionados</td>
                    </tr>
                    <tr>
                        <th scope="row">10:00 - 10:30</th>
                        <td>Receso</td>
                        <td>Receso</td>
                        <td>Receso</td>
                    </tr>
                    <tr>
                        <th scope="row">10:30 - 12:00</th>
                        <td>Montaje de stands y exposición libre</td>
                        <td>Ronda de evaluación — Categoría C y D</td>
                        <td>Deliberación del jurado</td>
                    </tr>
                    <tr>
                        <th scope="row">12:00 - 13:30</th>
                        <td>Almuerzo</td>
                        <td>Almuerzo</td>
                        <td>Almuerzo de gala</td>
                    </tr>
                    <tr>
                        <th scope="row">13:30 - 15:30</th>
                        <td>Talleres de pitch y presentación</td>
                        <td>Charlas de mentores e inversores</td>
                        <td>Ceremonia de premiación</td>
                    </tr>
                    <tr>
                        <th scope="row">15:30 - 17:00</th>
                        <td>Sesión de networking</td>
                        <td>Actividades culturales</td>
                        <td>Cierre oficial</td>
                    </tr>
                </tbody>
                <tfoot>
                    <tr>
                        <th scope="row">Total horas</th>
                        <td>9 horas</td>
                        <td>9 horas</td>
                        <td>7 horas</td>
                    </tr>
                </tfoot>
            </table>
        </section>

        <section id="inscripcion" aria-labelledby="titulo-inscripcion">
            <h2 id="titulo-inscripcion">Formulario de Inscripción</h2>
            <form action="#" method="post">
                <fieldset>
                    <legend>Datos del equipo</legend>

                    <label for="nombre-proyecto">Nombre del equipo o proyecto:</label>
                    <input id="nombre-proyecto" name="nombre-proyecto" type="text" placeholder="Nombre oficial del proyecto" required>

                    <label for="responsable">Nombre del responsable principal:</label>
                    <input id="responsable" name="responsable" type="text" placeholder="Nombre y apellidos completos" required>

                    <label for="correo">Correo de contacto:</label>
                    <input id="correo" name="correo" type="email" placeholder="correo@institucion.ac.cr" required>

                    <label for="telefono">Número de teléfono:</label>
                    <input id="telefono" name="telefono" type="tel" placeholder="XXXX-XXXX" required>

                    <label for="institucion">Institución de procedencia:</label>
                    <select id="institucion" name="institucion" required>
                        <option value="">Seleccione su institución</option>
                        <option value="ucr">Universidad de Costa Rica (UCR)</option>
                        <option value="tec">Instituto Tecnológico de CR (TEC)</option>
                        <option value="una">Universidad Nacional (UNA)</option>
                        <option value="utn">Universidad Técnica Nacional (UTN)</option>
                        <option value="earth">Universidad EARTH</option>
                        <option value="otra-publica">Otra institución pública</option>
                        <option value="privada">Institución privada</option>
                    </select>

                    <label for="carrera">Carrera o programa académico:</label>
                    <input id="carrera" name="carrera" type="text" list="lista-carreras" placeholder="Escriba o seleccione su carrera" required>
                    <datalist id="lista-carreras">
                        <option value="Ingeniería en Computación"></option>
                        <option value="Ingeniería Eléctrica"></option>
                        <option value="Ingeniería Ambiental"></option>
                        <option value="Biotecnología"></option>
                        <option value="Diseño Industrial"></option>
                        <option value="Administración de Empresas"></option>
                        <option value="Agronomía"></option>
                        <option value="Arquitectura"></option>
                        <option value="Otra"></option>
                    </datalist>
                </fieldset>

                <fieldset>
                    <legend>Detalles del proyecto</legend>

                    <label for="categoria">Categoría de participación:</label>
                    <select id="categoria" name="categoria" required>
                        <option value="robotica">Robótica y Automatización</option>
                        <option value="biotecnologia">Biotecnología</option>
                        <option value="ciudades-inteligentes">Ciudades Inteligentes</option>
                        <option value="economia-circular">Economía Circular</option>
                    </select>

                    <label for="descripcion">Descripción breve del proyecto:</label>
                    <textarea id="descripcion" name="descripcion" rows="4" placeholder="Describa en pocas líneas el problema que resuelve su proyecto..." required></textarea>

                    <label for="requerimientos">Requerimientos especiales para el stand:</label>
                    <textarea id="requerimientos" name="requerimientos" rows="2" placeholder="Indique cualquier requerimiento logístico especial..."></textarea>
                </fieldset>

                <fieldset>
                    <legend>Confirmaciones</legend>

                    <label for="originalidad">
                        <input id="originalidad" name="originalidad" type="checkbox" required>
                        Confirmo que el proyecto es original y de nuestra autoría
                    </label>

                    <label for="reglamento">
                        <input id="reglamento" name="reglamento" type="checkbox" required>
                        Acepto el reglamento de la Feria Nacional de Innovación
                    </label>
                </fieldset>

                <button class="boton" type="submit">Enviar Inscripción</button>
            </form>
        </section>

        <section id="sede" aria-labelledby="titulo-sede">
            <h2 id="titulo-sede">Sede del Evento</h2>
            <p>ITCR Campus Central Cartago, Cartago, Costa Rica</p>
            <p>Avenida 14, entre calles 5 y 7, frente al Estadio Fello Meza</p>
            <iframe
                src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3929.4567891234!2d-83.9134567!3d9.8634567!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zOcKwNTEnNDguNCJOIDgzwrA1NCc0OC40Ilc!5e0!3m2!1ses!2scr!4v9876543210"
                height="420"
                style="border:0;"
                loading="lazy"
                sandbox="allow-scripts allow-same-origin allow-popups"
                title="Mapa de ubicación del ITCR Campus Central Cartago"
                allowfullscreen>
            </iframe>
        </section>

        <section aria-labelledby="titulo-contacto">
            <h2 id="titulo-contacto">Contacto y Consultas</h2>
            <p>Para consultas sobre inscripción, logística o alianzas estratégicas, comuníquese con la comisión organizadora:</p>

            <article aria-labelledby="titulo-secretaria">
                <h3 id="titulo-secretaria">Secretaría de la Feria</h3>
                <address>
                    Correo: <a href="mailto:feria.innovacion@itcr.ac.cr">feria.innovacion@itcr.ac.cr</a><br>
                    Teléfono: 2550-9000 ext. 3100
                </address>
            </article>

            <p>Síganos en redes sociales para actualizaciones en tiempo real:</p>

            <a class="enlace-tarjeta" href="https://www.tec.ac.cr">
                <strong>Portal oficial del ITCR</strong><br>
                www.tec.ac.cr · Campus Cartago
            </a>
        </section>
    </main>

    <footer>
        <p>© 2025 Instituto Tecnológico de Costa Rica. Todos los derechos reservados.</p>
        <p>Feria Nacional de Innovación Estudiantil</p>
        <p>Organizado por la Vicerrectoría de Investigación y Extensión</p>
    </footer>

</body>
</html>

```
