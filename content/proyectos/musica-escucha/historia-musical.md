+++
title = 'Historia Musical'
weight = 13
+++

Visualización interactiva de la historia y relaciones entre géneros musicales, en un
único archivo HTML/CSS/JS (`ejemplo.html`, ~3000 líneas) sin frameworks ni build: se abre
directamente en el navegador.

- **`GENRES[]`** — array de datos con ~150 géneros (`id`, `num`, `genre`, `region`,
  `artist`, `title`, `year`, `rel_out[]` con los géneros a los que conecta cada uno).
- **`REGION_COLOR{}`** — mapeo de región a color.
- **`assignPositions()`** — layout manual: agrupa géneros por región en clusters y los
  posiciona en una rejilla (constantes `NW`/`NH`/`GAPX`/`GAPY`).
- **Render** — `#canvas` (SVG) dibuja las conexiones como curvas Bézier
  (`drawEdges()`/`bestAnchors()`/`curvePath()`) mientras `#graph` contiene las tarjetas
  de cada género como `<div>` posicionados.

Incluye barra de búsqueda, zoom y estados activo/atenuado por nodo. `build.py` y
`_test_ejemplo.py` son utilidades de construcción/verificación; `genretree.html` (y su
`.html_BAK`) es una version relacionada que también vive suelta en la raíz de
`~/gits/pollo`.
