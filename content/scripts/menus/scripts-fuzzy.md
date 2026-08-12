+++
title = 'Scripts (fuzzy)'
weight = 7
+++

Ruta: `~/Scripts/menus/scripts/`

Gestor de scripts con búsqueda difusa, mismo patrón indexador+GUI que
[dotfiles](../dotfiles) e [iconos](../iconos):

- **`fuzzy_scripts_indexer.py`** — indexa scripts en `scripts.db` (SQLite) según lo
  configurado en `script_config.yaml`.
- **`fuzzy_scripts.py`** — GUI PyQt6 (`fuzzywuzzy` + `pyyaml`) que busca sobre esa base,
  permite editar tags por script y lanzar/editar el seleccionado. Temas en
  `script_themes.yaml`.

Es, en la práctica, un menú flotante alternativo a `dmenu_launch_scripts.sh`/
`dmenu_edit_scripts.sh` (ver [dmenu](../dmenu)) pero con base de datos, tags y búsqueda
difusa en vez de un simple listado de `fd`.
