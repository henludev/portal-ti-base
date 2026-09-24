# Nova Servicios — Portal de soporte TI

## Punto de partida

Se utilizó **el ejemplo resuelto de la semana 2/guía 2 como punto de partida**, conservando `assets/js/ui.js` porque la consigna permite reutilizarlo para el menú y la confirmación del formulario.

El HTML y CSS fueron ampliados y modificados para completar el caso de Nova Servicios. El proyecto no usa frameworks ni base de datos y la solicitud es una simulación: el navegador valida los campos, pero no se envía ni se guarda ningún ticket.

## Aportes individuales

| Archivo | Cambio | Evidencia |
|---|---|---|
| `index.html` | Ampliación de contenido: se incorporaron las cuatro áreas de servicio de Nova Servicios, cinco preguntas frecuentes en dos categorías y una sección de contacto con horario ficticio. | Secciones `#servicios`, `#preguntas` y `#contacto` del archivo final. |
| `index.html` + `styles.css` | Mejora técnica: se añadieron `meta description`, estructura semántica completa, atributos de ayuda para controles, diseño mobile-first, Grid para tarjetas y Flexbox para navegación. | Metadatos del `<head>`, `header/nav/main/section/article/footer`, `.services__grid` y `.navbar`. |
| `index.html` + `styles.css` | Corrección detectada durante pruebas: el formulario no explicaba de forma suficientemente directa qué ocurría con los datos; ahora el aviso aparece junto al formulario y la confirmación de `ui.js` declara explícitamente que no se envió ni guardó información. También se añadieron ayudas visibles para tipo, prioridad y descripción. | `.form-note`, ayudas `*-help` y `#form-status`; comprobado en la prueba válida. |

## Dos problemas corregidos: antes y después

### 1. Formulario incompleto
- **Antes:** el ejemplo resuelto tenía el formulario, pero el contenido del caso era genérico y no incluía una explicación completa de la simulación ni ayudas para todos los campos.
- **Después:** el formulario incorpora instrucciones visibles, ayudas asociadas con `aria-describedby`, restricciones solicitadas y un mensaje de confirmación que indica que no se guarda información.

### 2. Contenido insuficiente para el caso
- **Antes:** el ejemplo resuelto terminaba después del formulario y no tenía FAQ ni contacto.
- **Después:** se añadieron cinco FAQ agrupadas en dos categorías y una sección de contacto con datos ficticios y horario.

## Decisiones CSS

- Se usan variables en `:root` para color, borde, radio y sombra, y se reutilizan en los componentes.
- La navegación utiliza **Flexbox** y las tarjetas utilizan **CSS Grid**.
- El diseño parte de móvil y añade cambios a 600, 768 y 1024 px.
- Se utiliza el combinador `.navbar__menu li + li` para controlar la separación entre elementos y el selector de atributo `a[href^="#"]` para aplicar una transición solo a enlaces internos.
- La pseudo-clase `:focus-visible` mantiene un indicador de foco claro para teclado. También se usa `:hover` para una respuesta visual en enlaces/botones.
- Decisión de cascada/especificidad: los estilos generales de `.button` definen la estructura común y `.button--primary` / `.button--secondary` modifican únicamente apariencia. En la navegación, `.js-menu .navbar__menu` tiene prioridad sobre `.navbar__menu` cuando `ui.js` activa el modo menú móvil; a partir de 768 px, la regla de media query restaura la presentación horizontal.

## Accesibilidad y recorrido

- `lang="es"`, UTF-8, viewport y meta description incluidos.
- Un único `h1` y jerarquía `h2`/`h3`/`h4` coherente.
- Cada control tiene una etiqueta visible.
- `fieldset` y `legend` agrupan datos de contacto, incidencia y prioridad.
- El foco de teclado es visible mediante `:focus-visible`.
- El menú reutiliza `ui.js`: botón accesible, apertura con activación normal de botón y cierre con Escape.
- El enlace «Solicitar soporte» está en el hero y en la navegación; desde el inicio se llega al formulario en un clic.

## IA y apoyo utilizado

Se utilizó **ChatGPT** como apoyo para estructurar y revisar la solución a partir de los requisitos de la consigna.

## Evidencias

Las capturas de 320, 768 y 1440 px se guardan en `docs/capturas/`. Los resultados de las pruebas se registran en `docs/pruebas.md`.
