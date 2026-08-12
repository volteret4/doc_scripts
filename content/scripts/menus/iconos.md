+++
title = 'Iconos'
weight = 4
+++

Ruta: `~/Scripts/menus/iconos/`

Navegador de iconos del sistema con el mismo patrón indexador+GUI que el
[editor de dotfiles](../dotfiles):

- **`icon_indexer.py`** — recorre el sistema en busca de iconos (`.png`, `.jpg`, `.svg`,
  `.ico`, `.bmp`, `.gif`, `.xpm`, `.webp`, `.tiff`, `.tga`), calcula hash y los indexa en
  `icons.db` (SQLite), leyendo su configuración de `config.yaml`.
- **`icon_browser.py`** — GUI PyQt6 que muestra los iconos indexados en una rejilla,
  permite buscarlos con fuzzy matching (`fuzzywuzzy`) y gestionar tags persistentes
  (`tags.json`).

Temas de color en `themes.yaml`/`themes.yml`.
