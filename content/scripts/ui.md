+++
title = 'UI'
weight = 7
+++

Ruta: `~/Scripts/ui/`

Carpeta de bocetos de interfaz con **Qt Designer**, sin lógica de aplicación propia:

- `main.py` + `main.qml` — el esqueleto por defecto de un proyecto Qt Quick/PySide6
  ("Hello World" en una `Window` vacía), sin desarrollar.
- `copy_mix_playerctl.ui`, `emojis.ui`, `scripts_fuzzy.ui` — diseños de Qt Designer
  (`QDialog`/`QMainWindow`) sin el `.py` que los cargue en esta misma carpeta. Por nombre
  y estructura parecen los mockups de partida de herramientas que ya viven
  implementadas en otro sitio: `emojis.ui` ↔ [`menus/emoticonos`]({{% relref "scripts/menus/emoticonos" %}}),
  `scripts_fuzzy.ui` ↔ [`menus/scripts`]({{% relref "scripts/menus/scripts-fuzzy" %}}), y
  `copy_mix_playerctl.ui` ↔ `Musica/MoverMusica/mover_mix_playerctl.py`.
