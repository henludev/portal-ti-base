# Pruebas — Nova Servicios

| ID | Prueba | Resultado obtenido | Estado | Ruta de evidencia |
|---|---|---|---|---|
| P01 | Navegación y semántica | Los enlaces principales apuntan a `#inicio`, `#servicios`, `#preguntas`, `#contacto` y `#soporte`. El CTA del inicio llega al formulario en 1 clic. Se detecta un `h1` y existen `header`, `nav`, `main`, `section`, `article` y `footer`. | Cumple | `index.html`; comprobación automatizada |
| P02 | Móvil de 320 px | Se cargó la página a 320 px y se verificó ausencia de overflow horizontal y existencia del formulario. Se guardó captura completa. | Cumple | `docs/capturas/320px.png` |
| P03 | Tablet de 768 px | Se cargó la página a 768 px; navegación horizontal, tarjetas y formulario permanecen dentro del viewport. Se guardó captura completa. | Cumple | `docs/capturas/768px.png` |
| P04 | Escritorio de 1440 px | Se cargó la página a 1440 px; contenido con ancho controlado y recursos locales cargados. Se guardó captura completa. | Cumple | `evidencias/1440px.png` |
| P05 | Teclado y zoom | Se verificó mediante automatización que los elementos interactivos reciben foco y que el botón del menú existe para viewport móvil. La prueba manual de recorrido completo con Tab/Shift+Tab y zoom al 200 % queda pendiente de demostración. | No ejecutada | `README.md`; pendiente de comprobación manual |
| P06 | Formulario inválido | Se comprobaron vacío, nombre de 2 caracteres, `usuario@`, tipo sin seleccionar, prioridad sin seleccionar y descripción de 9 caracteres. Para el máximo se intentó introducir 501 caracteres: el control con `maxlength="500"` limita el valor a 500 caracteres, y se verificó una longitud efectiva de 500. | Cumple | `docs/capturas/formulario-invalido.png` |
| P07 | Formulario válido | Con Ana Pérez, `ana@example.test`, Hardware, Media y una descripción de al menos 10 caracteres, la validación permite el submit y aparece el mensaje de simulación: no se envió ni guardó ningún ticket. | Cumple | `docs/capturas/formulario-valido.png` |
| P08 | Calidad y Preview | Metadatos, estructura, recursos y foco básico fueron inspeccionados. **Lighthouse no se ejecutó** en este entorno, por lo que no se registran puntuaciones. | No ejecutada | `docs/pruebas.md`; ejecutar Lighthouse sobre el Preview de Vercel |

## Verificaciones adicionales

- **320 px:** sin scroll horizontal detectado.
- **768 px:** menú en una fila y tarjetas adaptadas mediante Grid.
- **1440 px:** catálogo en cuatro columnas, con tarjeta destacada ocupando dos columnas.
- **Validación nativa:** no se utiliza `novalidate`.
- **Simulación:** `ui.js` conserva `preventDefault()` y muestra que no se envió ni guardó ningún ticket.
- **Datos:** todos los datos de contacto, correo, teléfono y horario son ficticios.
