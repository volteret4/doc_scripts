+++
title = 'Spotify'
weight = 8
+++

Ruta: `~/Scripts/menus/spotify/`

`sp_menu_playlists.py` — ventana Tkinter que lee `playlists.txt` (ternas de nombre / ID
/ línea en blanco) y muestra un botón por playlist más un botón "NUEVA LISTA"; al hacer
clic imprime el ID elegido por stdout para que lo consuma otro script (p. ej. uno que
añada la pista actual a esa playlist).
