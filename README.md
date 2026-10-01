# Nova Servicios — Portal de soporte TI

## Punto de partida

Se utilizó **el ejemplo resuelto de la semana 2/guía 2 como punto de partida**, conservando `assets/js/ui.js` porque la consigna permite reutilizarlo para el menú y la confirmación del formulario.

El HTML y CSS fueron ampliados y modificados para completar el caso de Nova Servicios. El proyecto no usa frameworks ni base de datos y la solicitud es una simulación: el navegador valida los campos, pero no se envía ni se guarda ningún ticket.

## Aportes individuales

| Archivo                     | Cambio                                                                                                                                                                                                                                                                                                                                      | Evidencia                                                                                        |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| `index.html`                | Ampliación de contenido: se incorporaron las cuatro áreas de servicio de Nova Servicios, cinco preguntas frecuentes en dos categorías y una sección de contacto con horario ficticio.                                                                                                                                                       | Secciones `#servicios`, `#preguntas` y `#contacto` del archivo final.                            |
| `index.html` + `styles.css` | Mejora técnica: se añadieron `meta description`, estructura semántica completa, atributos de ayuda para controles, diseño mobile-first, Grid para tarjetas y Flexbox para navegación.                                                                                                                                                       | Metadatos del `<head>`, `header/nav/main/section/article/footer`, `.services__grid` y `.navbar`. |
| `index.html` + `styles.css` | Corrección detectada durante pruebas: el formulario no explicaba de forma suficientemente directa qué ocurría con los datos; ahora el aviso aparece junto al formulario y la confirmación de `ui.js` declara explícitamente que no se envió ni guardó información. También se añadieron ayudas visibles para tipo, prioridad y descripción. | `.form-note`, ayudas `*-help` y `#form-status`; comprobado en la prueba válida.                  |

## Dos problemas corregidos: antes y después

### Menú móvil a 320 px

- **Problema observado:** al abrir el menú, el logo, el botón Menú y los enlaces competían por una misma fila y quedaban apretados.
- **Corrección:** se agregó `flex-wrap: wrap` a `.navbar` para que los enlaces ocupen una fila debajo del logo y el botón; desde 768 px, `flex-wrap: nowrap` conserva la navegación horizontal.
- **Comprobación:** se abrió el menú a 320 px y se confirmó que los enlaces quedaron debajo, sin desbordamiento horizontal de la página.
- **Evidencias:** `docs/evidencias/menu-movil-antes.jpg` y `docs/evidencias/menu-movil-despues.jpg`.

### Contraste del enlace «Solicitar soporte» en el menú

- **Problema observado:** al recibir foco del teclado, una regla general sustituía el fondo amarillo por uno oscuro semitransparente y dejaba texto oscuro sobre fondo oscuro.
- **Corrección:** una regla específica para `.navbar__menu .nav-cta:hover` y `.navbar__menu .nav-cta:focus-visible` mantiene el fondo `var(--color-accent)` y el texto `var(--color-ink)`, sin eliminar el contorno de foco.
- **Comprobación:** el contraste calculado para ese texto pasó de 1.44:1 a 9.27:1; con Tab, el botón siguió amarillo y mostró el contorno de foco. El estudiante también confirmó el resultado en su navegador.
- **Evidencias:** `docs/evidencias/contraste-boton-antes.jpg` y `docs/evidencias/contraste-boton-despues.jpg`.

El formulario, las preguntas frecuentes y el contacto son aportes al contenido del portal, pero no se presentan como las dos correcciones de pruebas exigidas. Las pruebas y sus límites se detallan en `docs/pruebas.md`.

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

## Modelo conceptual de datos

El modelo conceptual representa cinco entidades principales del portal:

- **Usuario:** representa a las personas que registran solicitudes y realizan acciones que pueden quedar registradas en auditoría.
- **Servicio:** representa los servicios de TI disponibles para los usuarios.
- **Solicitud:** representa un requerimiento o incidencia registrada por un usuario y asociada a un servicio.
- **Actualización:** registra cambios realizados sobre una solicitud, incluyendo quién realizó el cambio, el campo afectado, el valor anterior, el valor nuevo y la fecha.
- **Auditoría:** registra las acciones relevantes realizadas por los usuarios, indicando quién actuó, qué acción realizó, cuándo ocurrió y sobre qué entidad se realizó.

### Relaciones y cardinalidades

El modelo utiliza las siguientes relaciones:

- **Usuario 1:N Solicitud:** un usuario puede registrar varias solicitudes y cada solicitud pertenece a un usuario.
- **Servicio 1:N Solicitud:** un servicio puede estar asociado a varias solicitudes y cada solicitud corresponde a un servicio.
- **Solicitud 1:N Actualización:** una solicitud puede tener varias actualizaciones.
- **Usuario 1:N Actualización:** un usuario puede realizar varias
  actualizaciones y cada actualización identifica a un único usuario
  responsable mediante user_id.
- **Usuario 1:N Auditoría:** un usuario puede generar varios registros de auditoría.

### Reglas de negocio

Las solicitudes manejan los estados:

- Pendiente
- En proceso
- Resuelto
- Cerrado/Cancelado

Solo el **rol técnico** puede cambiar el estado de una solicitud.

Cada cambio de estado debe generar una **Actualización** y un registro de **Auditoría**, conservando quién realizó el cambio, qué cambió, cuándo ocurrió y la entidad afectada.

Para cambios relevantes, se conservan el valor anterior y el valor nuevo para permitir reconstruir el historial del cambio.

El archivo del modelo conceptual se encuentra en `docs/modelo-datos.png`.

## Análisis de casos

### Solicitudes 1001 y 1005

Las solicitudes 1001 y 1005 podrían corresponder al mismo incidente, por lo que antes de considerarlas duplicadas se deberían comparar:

- usuario que registró cada solicitud;
- servicio asociado;
- tipo de incidencia;
- descripción del problema;
- fecha y hora de creación;
- ubicación o equipo afectado, si estuviera disponible;
- evidencias o información adicional relacionada con el incidente.

Aunque se determine que existe una posible duplicidad, se deben conservar ambas solicitudes y su historial. La relación entre ellas podría registrarse como una posible duplicidad para mantener la trazabilidad y dejar constancia de la decisión tomada.

### Solicitud 1002 y auditoría 5004

La consigna indica que la prioridad de la solicitud 1002 cambió de
Media a Alta sin autorización. El registro de auditoría 5004
identifica al actor con user_id=9, la acción CAMBIO_PRIORIDAD
y la fecha 2026-09-30 14:32.

### Relación del evento con la solicitud

Para vincular el evento con la solicitud, el registro de Auditoría
debería identificar la entidad afectada y su clave primaria:

| Dato           | Valor            |
| -------------- | ---------------- |
| audit_id       | 5004             |
| user_id        | 9                |
| entidad        | Solicitud        |
| entidad_id     | 1002             |
| accion         | CAMBIO_PRIORIDAD |
| fecha          | 2026-09-30 14:32 |
| valor_anterior | Media            |
| valor_nuevo    | Alta             |

Los valores de entidad, entidad_id, valor_anterior y valor_nuevo
representan cómo debería documentarse el cambio descrito en el
caso. No se afirma que esos campos estuvieran completos en el
registro original.

El campo entidad_id=1002 se relaciona con request_id=1002 de
Solicitud, cuando entidad tiene el valor Solicitud. user_id=9
identifica al usuario registrado como actor del evento.

También se buscaría una Actualización relacionada con
request_id=1002, con campo=prioridad, valor_anterior=Media,
valor_nuevo=Alta y una fecha compatible con el evento de auditoría.
Se compararía su actor con el usuario 9 para detectar diferencias
o registros faltantes.

### Investigación de la autorización

Para investigar el cambio se revisaría:

1. Qué rol y permisos tenía el usuario 9 en la fecha y hora del evento,
   no únicamente cuáles tiene actualmente.
2. Qué regla de negocio establecía quién podía cambiar la prioridad.
3. Si existía una autorización o aprobación registrada antes del cambio,
   quién la otorgó y qué modificación permitía.
4. Si los registros de Actualización y Auditoría coinciden en solicitud,
   actor, fecha y valores anterior y nuevo.
5. Si hubo cambios de permisos u otros eventos relevantes cerca de
   2026-09-30 14:32.

La consigna establece que solo el rol técnico puede cambiar el
estado de una solicitud, pero no define expresamente quién puede
cambiar su prioridad. Por eso, no se debe asumir que tener el rol
técnico autoriza automáticamente este cambio.

El registro de auditoría permite rastrear la acción, pero no
demuestra por sí solo que estuviera autorizada. La investigación
debe contrastarlo con los permisos vigentes y las aprobaciones
disponibles en ese momento.

### Información que se debe conservar

Se conservarían el registro de auditoría 5004, la solicitud 1002,
las actualizaciones relacionadas y las evidencias de permisos
y autorizaciones disponibles.

Si corresponde corregir la prioridad, se registraría un nuevo
cambio con sus valores anterior y nuevo, responsable y fecha.
No se borraría el evento original, para mantener la trazabilidad.

Este análisis es conceptual. No se implementa una base de datos real.

## IA y apoyo utilizado

Se utilizó **ChatGPT** como apoyo para estructurar y revisar la solución a partir de los requisitos de la consigna.
El estudiante incorporó manualmente los cambios en su proyecto, revisó el modelo y comprobó el zoom y el recorrido con teclado. `ui.js` se conservó sin modificaciones.

## Evidencias

Las evidencias actuales de las tres vistas, foco, formulario y dos correcciones están preparadas para guardarse en `docs/evidencias/`; comprueba que esa carpeta y todos los archivos citados estén en tu proyecto antes de empaquetar. Los resultados de las pruebas se registran en `docs/pruebas.md`. Las capturas antiguas de `docs/capturas/` no sustituyen las evidencias actuales.

## Comprobación manual de zoom y teclado

Se comprobó el zoom al 200 % y el recorrido con Tab, Shift+Tab, Enter y Escape sin encontrar problemas. El detalle se centraliza en `docs/pruebas.md`.

## Planificación del proyecto

El brief de cinco dimensiones, las cinco historias de usuario,
las prioridades MoSCoW y el wireframe de seis zonas se encuentran
en [Planificación del proyecto](docs/planificacion.md).
