## Capturas

| Archivo                       | Qué demuestra                                                                                    | Tamaño de la imagen                                                              |
| ----------------------------- | ------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| `vista-320px.png`             | Página completa con el menú cerrado, a 320 px de ancho.                                          | 320 × 6874 px                                                                    |
| `vista-768px.png`             | Página completa a 768 px de ancho.                                                               | 768 × 4795 px                                                                    |
| `vista-1440px.png`            | Página completa a 1440 px de ancho.                                                              | 1440 × 4456 px                                                                   |
| `menu-movil-antes.jpg`        | Problema real: logo, botón y enlaces compiten por una misma fila a 320 px.                       | 320 × 900 px                                                                     |
| `menu-movil-despues.jpg`      | Corrección: logo y botón arriba; enlaces en una fila completa debajo.                            | 320 × 900 px                                                                     |
| `foco-teclado.jpg`            | Foco visible al llegar con Tab al enlace del inicio «Solicitar soporte».                         | 320 × 900 px                                                                     |
| `formulario-invalido.jpg`     | Nombre «An», de dos caracteres: el navegador bloquea la confirmación y marca el campo inválido.  | 768 × 1000 px                                                                    |
| `formulario-valido.jpg`       | Datos ficticios válidos y mensaje «Validación completada. No se envió ni guardó ningún ticket.». | 1087 × 1057 px                                                                   |
| `contraste-boton-antes.jpg`   | Segunda corrección, antes: fondo oscuro y texto oscuro al recibir foco de teclado.               | Viewport de 1440 × 900 px; imagen reducida proporcionalmente por la herramienta. |
| `contraste-boton-despues.jpg` | Segunda corrección, después: fondo amarillo, texto legible y contorno de foco conservado.        | Viewport de 1440 × 900 px; imagen reducida proporcionalmente por la herramienta. |

Las tres vistas completas conservan sus dimensiones originales. La imagen del formulario válido es una captura de un viewport de 1440 × 1400 px reducida proporcionalmente por la herramienta; no se utiliza como evidencia del ancho de 1440 px, que tiene su propia captura PNG.

## Resultados observados

- A 320, 768 y 1440 px, el ancho desplazable de la página no superó el ancho disponible para el contenido.
- En este navegador, la barra vertical ocupa 15 px: los anchos disponibles fueron 305, 753 y 1425 px, respectivamente. Esta diferencia no es desbordamiento horizontal.
- A 320 px con el menú abierto, el menú quedó debajo del logo y la página siguió sin desbordamiento horizontal.
- Escape cerró el menú y devolvió el foco al botón Menú.
- Tab mostró un contorno de foco de 3 px en el enlace «Solicitar soporte».
- Shift+Tab desde el botón del formulario devolvió el foco al campo de descripción.
- El nombre de dos caracteres activó `validity.tooShort`; el mensaje de confirmación quedó vacío.
- Con Ana Pérez, `ana@example.test`, Hardware, prioridad Media y «La impresora de prueba no responde al enviar documentos.», el formulario fue válido y mostró la confirmación simulada.
- Después de la segunda corrección, el botón del menú conservó fondo RGB(244, 185, 66), texto RGB(18, 32, 51) y contorno de 3 px al recibir foco de teclado.
- Al mover el mouse sobre ese botón se comprobó `:hover` activo y los mismos colores legibles.
- Se volvió a comprobar la vista de 320 px: la barra conservó `flex-wrap: wrap` y la página no tuvo desbordamiento horizontal.

La tabla de estados usa desplazamiento horizontal interno en móvil. Esto no ensancha toda la página.

Las capturas de las vistas generales y el formulario proceden de la revisión anterior, realizada después de la primera corrección. La segunda corrección solo cambia los estados hover/foco del botón de navegación; no se presentan esas capturas anteriores como pruebas completas ejecutadas nuevamente.
