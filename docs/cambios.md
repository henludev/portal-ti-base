# Registro de cambios respecto del ejemplo resuelto

## 1. Ampliación de contenido del caso

**Antes (ejemplo resuelto):** cuatro tarjetas con descripciones breves y sin preguntas frecuentes ni contacto.

**Después (Nova Servicios):** cuatro servicios específicos —Conectividad y red, Hardware, Software y Accesos y cuentas— más cinco FAQ distribuidas en las categorías «Antes de solicitar soporte» y «Atención y seguimiento», y una sección de contacto con horario ficticio.

**Evidencia:** `index.html`, secciones `#servicios`, `#preguntas` y `#contacto`.

## 2. Mejora técnica de HTML/CSS

**Antes:** el `<head>` del ejemplo resuelto no tenía una meta description propia y el diseño no documentaba las necesidades adicionales de contenido del caso.

**Después:** se añadió meta description específica, se mantuvo la estructura semántica requerida, se incorporaron variables CSS reutilizadas, Grid para el catálogo, Flexbox para la navegación, selector de atributo, combinador y estados de foco.

**Evidencia:** `index.html` (`<meta name="description">`) y `assets/css/styles.css` (`:root`, `.navbar`, `.services__grid`, `a[href^="#"]`, `.navbar__menu li + li`, `:focus-visible`).

## 3. Corrección detectada en pruebas

**Antes:** las ayudas del formulario no cubrían todos los datos y el aviso de simulación era menos visible como contexto del formulario.

**Después:** se añadieron ayudas específicas para tipo, prioridad y descripción, además de un aviso destacado junto al formulario. La confirmación de `ui.js` se conserva y declara que no se envió ni guardó ningún ticket.

**Evidencia:** `index.html` (`.form-note`, `#tipo-help`, `#priority-help`, `#descripcion-help`, `#form-status`) y `evidencias/formulario-valido.png`.
