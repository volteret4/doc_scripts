+++
title = 'Hotkeyz'
weight = 5
+++

App Flask (puerto 5757) para gestionar `~/.config/hotkeys/hotkeys.csv` y construir una
chuleta (*cheatsheet*) visual de atajos, con `data/cheatsheets/` como salida.

`scripts/generar_hotkeys_csv.py` y `scripts/ver_hotkeys.py` son las mismas herramientas
(por nombre y propósito) que aparecen como scripts sueltos en
[`menus/rofi`]({{% relref "scripts/menus/rofi" %}}) dentro de `~/Scripts` — este repo es
casi con toda seguridad su origen, con una interfaz web añadida encima del CSV que
generan/leen esos mismos scripts.
