# Planificación: Nova Servicios

Este documento reúne la planificación del portal académico: brief de cinco dimensiones, cinco historias de usuario con criterios medibles, prioridades MoSCoW y wireframe de baja fidelidad con seis zonas. Los criterios son requisitos para comprobar, no afirmaciones de que todas las pruebas ya se realizaron.

## Brief de cinco dimensiones

El brief resume qué se construye, para quién y con qué límites. Para este documento se organiza en las siguientes cinco dimensiones.

| Dimensión | Definición para Nova Servicios |
|---|---|
| Objetivo | Crear un portal estático de soporte TI para consultar servicios, simular una solicitud y revisar estados ficticios. Debe permitir llegar al formulario desde el inicio en un máximo de dos clics. |
| Público | Usuarios de Nova Servicios que necesitan orientación sobre conectividad, hardware, software y accesos. Se considera el uso desde móvil, tablet y escritorio, así como la navegación con teclado. |
| Contenido | Encabezado y navegación; presentación; cuatro tarjetas de servicio; formulario; tabla de estados ficticios; cinco preguntas frecuentes en al menos dos categorías; contacto y horario ficticios; pie de página. |
| Funcionalidad | Navegación por secciones, enlaces al formulario, validación nativa y confirmación simulada. El menú y la confirmación reutilizan `ui.js` de la guía 2, sin modificarlo. Los estados son ejemplos estáticos, no consultas de tickets reales. |
| Restricciones y calidad | HTML semántico y CSS propio, sin frameworks, backend, persistencia ni JavaScript nuevo. Diseño mobile first, al menos tres variables CSS y Grid o Flexbox. Comprobar 320, 768 y 1440 px, foco de teclado, zoom al 200 % y contraste de texto normal de al menos 4.5:1. Usar datos ficticios y declarar el apoyo de IA. |

## Cinco historias de usuario

Una historia expresa una necesidad del usuario. Los criterios indican cómo decidir si está atendida: dado un contexto, cuando ocurre una acción, entonces debe observarse un resultado concreto.

### HU01: llegar al formulario

Como usuario que necesita ayuda, quiero encontrar un acceso visible a la solicitud de soporte para llegar al formulario sin buscar entre todas las secciones.

Criterios de aceptación:

- Dado que estoy en el inicio, cuando activo «Solicitar soporte», entonces llego al formulario en un máximo de dos clics. El diseño propuesto permite hacerlo en uno.
- Dado que recorro la navegación con Tab, cuando llego a un enlace o botón, entonces su foco es visible.
- Dado que la navegación se presenta como menú móvil, cuando activo Menú con Enter o Espacio, entonces aparecen sus enlaces; cuando presiono Escape, entonces se cierra y el foco vuelve al botón.

### HU02: consultar servicios

Como usuario que todavía no sabe qué tipo de ayuda solicitar, quiero consultar el catálogo para identificar el servicio relacionado con mi incidencia.

Criterios de aceptación:

- Dado que llego al catálogo, cuando reviso sus tarjetas, entonces encuentro exactamente cuatro: Conectividad y red, Hardware, Software, y Accesos y cuentas.
- Dado que reviso una tarjeta, entonces encuentro un título, una descripción y un enlace al formulario.
- Dado que activo cualquiera de los cuatro enlaces de servicio, entonces llego a la sección del formulario.

### HU03: simular una solicitud

Como usuario que quiere practicar el registro de una incidencia, quiero completar un formulario con instrucciones claras para validar los datos sin enviar ni guardar un ticket real.

Criterios de aceptación:

- Dado que dejo campos obligatorios sin completar y trato de confirmar, entonces la validación nativa impide continuar.
- Dado que escribo un nombre de menos de 3 caracteres o un correo inválido, entonces no aparece una confirmación válida.
- Dado que no selecciono un tipo de incidencia, cuya opción inicial tiene valor vacío, entonces no puedo confirmar.
- Dado que selecciono una prioridad mediante radios del mismo grupo, entonces solo una opción puede quedar seleccionada; la ausencia de una selección impide confirmar.
- Dado que escribo una descripción de menos de 10 caracteres, entonces no puedo confirmar; el control limita la entrada a 500 caracteres.
- Dado que todos los datos cumplen las restricciones, cuando confirmo, entonces aparece un mensaje que indica explícitamente que no se envió ni guardó ningún ticket.
- Dado que reviso el formulario, entonces cada control tiene una etiqueta visible y la prioridad está agrupada con `fieldset` y `legend`.

### HU04: comprender los estados

Como usuario que quiere entender el seguimiento de una incidencia, quiero consultar solicitudes ficticias para reconocer los estados de atención.

Criterios de aceptación:

- Dado que llego a Estados, entonces encuentro una tabla estática identificada como información ficticia.
- Dado que reviso los ejemplos, entonces están representados Pendiente, En proceso, Resuelto y Cerrado/Cancelado.
- Dado que abro la tabla en una pantalla de 320 px, entonces puedo acceder a todas sus columnas, permitiendo desplazamiento dentro de su contenedor sin ensanchar toda la página.
- Dado que leo esta sección, entonces no se presenta como seguimiento real ni permite cambiar los estados.

### HU05: consultar ayuda y contacto

Como usuario con dudas antes de solicitar soporte, quiero consultar preguntas frecuentes y datos de contacto para conocer las instrucciones y el horario de atención de ejemplo.

Criterios de aceptación:

- Dado que llego a Preguntas frecuentes, entonces encuentro cinco preguntas con sus respuestas.
- Dado que reviso las preguntas, entonces están organizadas en al menos dos categorías.
- Dado que llego a Contacto, entonces encuentro un horario y un medio de contacto identificados como ficticios.
- Dado que utilizo los enlaces de navegación, entonces puedo llegar a las secciones de preguntas y contacto.

## Prioridades MoSCoW

MoSCoW separa lo obligatorio, lo recomendable, lo opcional y lo que no se realizará. Ningún requisito obligatorio del examen se considera opcional.

| Prioridad | Contenido |
|---|---|
| Must have: obligatorio | Todas las secciones y cantidades exigidas; acceso al formulario en un máximo de dos clics; restricciones, etiquetas, `fieldset`/`legend`, validación nativa y confirmación simulada; ausencia de envío o almacenamiento de tickets; HTML/CSS propios y `ui.js` original; diseño mobile first, variables CSS, Grid o Flexbox y comprobaciones de tamaños, teclado, zoom y contraste. |
| Must have: documentación y entrega | Este brief, cinco historias, MoSCoW y wireframe de seis zonas; modelo conceptual de cinco entidades con atributos, PK/FK, cardinalidades y reglas de auditoría; análisis de 1001/1005 y del evento 5004 de la solicitud 1002; README, pruebas y evidencias, incluidas dos correcciones reales; registro de Lighthouse o revisión manual equivalente si no está disponible; rama `feature/parcial-portal` desde `main` actualizado, commits descriptivos, PR, Preview, SHA completo y ZIP consistente sin archivos prohibidos. |
| Should have: recomendable | Ejemplos breves de datos ficticios junto a los campos, redacción uniforme y documentación organizada para facilitar la comprensión y la sustentación. Son mejoras de claridad; no sustituyen los requisitos obligatorios. |
| Could have: opcional | Una tarjeta visualmente destacada o pequeños ajustes decorativos hechos solo con CSS. No se añaden si retrasan el cierre de la entrega. |
| Won't have: fuera de alcance | Backend, base de datos real, login, envío o almacenamiento de tickets, persistencia en el navegador, consulta real de estados, frameworks, nuevas dependencias y JavaScript nuevo o modificaciones de `ui.js`. |

## Wireframe de baja fidelidad: seis zonas

El wireframe representa la distribución del contenido, no su diseño final. Se usa una estructura vertical para móvil; en pantallas más amplias, las tarjetas y el formulario pueden distribuirse en columnas.

Las seis zonas son agrupaciones visuales. Preguntas frecuentes, contacto y pie se incluyen en la zona de ayuda y cierre; conservan sus secciones propias en el HTML.

```text
+------------------------------------------------------+
| ZONA 1: ENCABEZADO Y NAVEGACIÓN                       |
| Nova Servicios                         [Menú]        |
| Inicio | Servicios | Soporte | Estados | FAQ | Contacto|
|                         [Solicitar soporte]          |
+------------------------------------------------------+
| ZONA 2: PRESENTACIÓN                                 |
| Título principal                                    |
| Explicación breve del portal                         |
| [Solicitar soporte]       [Ver servicios]             |
| Información de atención ficticia                     |
+------------------------------------------------------+
| ZONA 3: CATÁLOGO                                     |
| [Conectividad y red] -> formulario                    |
| [Hardware]           -> formulario                   |
| [Software]           -> formulario                   |
| [Accesos y cuentas]  -> formulario                    |
+------------------------------------------------------+
| ZONA 4: FORMULARIO                                   |
| Aviso: simulación y uso de datos ficticios            |
| Nombre [________________________]                    |
| Correo [________________________]                    |
| Tipo   [Selecciona una opción  v]                    |
| Prioridad: ( ) Alta  ( ) Media  ( ) Baja              |
| Descripción [___________________]                    |
| [Validar solicitud de prueba]                        |
| Confirmación: no se envió ni guardó ningún ticket     |
+------------------------------------------------------+
| ZONA 5: ESTADOS FICTICIOS                             |
| Solicitud | Servicio | Prioridad | Estado             |
| Ejemplos de los cuatro estados                       |
| Tabla con desplazamiento interno si es necesario     |
+------------------------------------------------------+
| ZONA 6: AYUDA Y CIERRE                               |
| FAQ: cinco preguntas en dos categorías               |
| Contacto: medio y horario ficticios                   |
| Pie: identificación del portal académico             |
| Recordatorio: no registra tickets reales             |
+------------------------------------------------------+
```

### Adaptación prevista

- A 320 px: contenido en una columna y menú desplegable.
- A 768 px: navegación visible y distribución en columnas donde el contenido lo permita.
- A 1440 px: contenido con ancho limitado y catálogo organizado con Grid.
- Al 200 % de zoom: mantener disponibles el contenido y los controles, sin solapamientos que impidan usarlos.

## Alcance del modelo conceptual y del análisis

El diagrama se entrega por separado como `docs/modelo-datos.png`. Representa Usuario, Servicio, Solicitud, Actualización y Auditoría, sin implementar una base real.

- Relaciones obligatorias: Usuario 1:N Solicitud; Servicio 1:N Solicitud; Solicitud 1:N Actualización; Usuario 1:N Auditoría.
- Relación explicativa adicional: Usuario 1:N Actualización, coherente con el usuario responsable registrado en cada actualización.
- Solo el rol técnico puede cambiar el estado.
- Cada cambio de estado debe generar Actualización y Auditoría, conservando quién, qué, cuándo, entidad afectada y valores anterior y nuevo.
- El README explica qué comparar para investigar una posible duplicidad entre 1001 y 1005, sin darla por confirmada.
- El README relaciona el evento de auditoría 5004 con la solicitud 1002 y explica cómo investigar los permisos y autorizaciones vigentes cuando la prioridad cambió de Media a Alta.
