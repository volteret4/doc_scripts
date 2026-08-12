+++
title = 'Menús'
weight = 3
+++

Lanzadores y menús flotantes (rofi/dmenu/Tkinter/PyQt6) para moverse por el sistema sin
tocar el teclado más de lo necesario: editar dotfiles, lanzar scripts, buscar en la wiki
de Obsidian, elegir playlists, publicar posts de blog o lanzar una VM con Claude Code.

- **[dmenu](dmenu)**: lanzadores clásicos basados en `dmenu` (dotfiles, scripts, búsqueda web, MPD, supermenú).
- **[dotfiles](dotfiles)**: editor rápido de dotfiles (PyQt6 + SQLite).
- **[emoticonos](emoticonos)**: selector de emojis con tags.
- **[iconos](iconos)**: navegador de iconos del sistema con búsqueda difusa.
- **[mihitas](mihitas)**: convierte notas de Obsidian en posts de Hugo para varios blogs.
- **[rofi](rofi)**: la colección más grande — buscadores fuzzy (wiki, librería musical), marcadores, hotkeys, layouts de zellij para Claude.
- **[scripts (fuzzy)](scripts-fuzzy)**: lanzador/editor rápido de todo `~/Scripts` con base de datos y tags.
- **[spotify](spotify)**: selector de playlists de Spotify.
- **[vm](vm)**: arranca una VM Arch aislada y lanza Claude Code dentro, montado por sshfs.
- **[sueltos](sueltos)**: búsqueda/canales de YouTube y un par de utilidades pequeñas.

{{% notice note %}}
Varias de estas herramientas (dotfiles, iconos, scripts-fuzzy) comparten el mismo patrón:
un `*_indexer.py` que vuelca archivos a una base SQLite, y una GUI PyQt6 que la busca y
la muestra. El entorno virtual de Python (`~/Scripts/python_venv/`) es compartido entre
todas.
{{% /notice %}}
