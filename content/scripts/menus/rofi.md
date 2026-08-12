+++
title = 'Rofi'
weight = 6
+++

Ruta: `~/Scripts/menus/rofi/`

La carpeta más variada de `menus/`: buscadores fuzzy sobre la wiki de Obsidian y sobre
la librería musical, gestión de marcadores del navegador, un generador/visor de hotkeys,
y los lanzadores de layouts de zellij para Claude Code.

## Buscador fuzzy de la wiki (Obsidian)

`fuzzy.py` es una mini-app Tkinter que busca en `/mnt/windows/FTP/wiki/Obsidian/` por
nombre y contenido, y muestra el markdown renderizado (`tkinterweb`) del resultado.
Hay varias iteraciones sueltas del mismo concepto en la carpeta —
`fuzzy_funcional.py`, `fuzzy2.py`, `fuzzy3.py`, `fuzzy copy.py` — con pequeñas
diferencias de comportamiento (los propios comentarios de `fuzzy_funcional.py` listan
bugs pendientes tipo "no muestra coincidencias por contenido"). No se documentan una a
una: son variantes de desarrollo, no herramientas independientes.

`obsidian-fuzzy.sh` resuelve una necesidad parecida por otra vía: busca con `ripgrep`
sobre `~/notes/`, lista los archivos con coincidencias en rofi y permite copiar al
portapapeles (`copyq`) el contenido seleccionado.

## Buscador fuzzy de la librería musical

`NFS_fuzzy.py` (~1500 líneas) es, con diferencia, la app más grande de todo `~/Scripts`:
un navegador Tkinter de la librería musical en NFS/moode con lectura de metadatos
(`mutagen`), caché en SQLite, y enriquecimiento de datos vía Discogs, MusicBrainz,
Wikipedia y scraping web. `nfs_fuzzy_funcional.py` es una versión más ligera centrada en
localizar y abrir álbumes (sin las integraciones externas). Ambas tienen variantes de
respaldo en la carpeta (`NFS_fuzzy.py.COPIA`, `NFS_fuzzy.py_PERFECT`,
`nfs_fuzzy_funcional.py_perfect`) que no se documentan por separado.

`db_musica.py` cubre una necesidad relacionada pero distinta: indexa una carpeta de
música (mp3/flac) en SQLite enriqueciendo con Last.fm (`pylast`), y luego permite
filtrar/reproducir/abrir carpeta desde una interfaz con esos datos.

`busqueda_fuzzy.sh` es más simple: navega con `fd` + `rofi` cualquier directorio (por
defecto `/mnt/windows/Mix`), con atajos para abrirlo en Thunar o controlar Deadbeef
(play/pausa) sin salir del menú.

## Marcadores del navegador

| Script | Qué hace |
|---|---|
| `actualizar_marcadores.py` | Copia `places.sqlite` (perfil de Floorp) a la wiki como backup. |
| `marcadores_fuzzy.py` | Lee ese mismo `places.sqlite`, reconstruye la jerarquía de carpetas de marcadores y la exporta a la wiki excluyendo dominios ruidosos (Google, GitHub, Bandcamp, redes locales...). |
| `marcadores_rofi.sh` | Lee un JSON de marcadores ya filtrado y los muestra en rofi (título + tags + resumen con marcado), abriendo la URL elegida con `xdg-open`. |

## Hotkeys

| Script | Qué hace |
|---|---|
| `generar_hotkeys_csv.py` | Genera `~/.config/hotkeys/hotkeys.csv` parseando los atajos definidos en AwesomeWM (`rc.lua`), alias/bindkeys de zsh y la config de zellij. Re-ejecutarlo preserva la columna `enabled` editada a mano. |
| `ver_hotkeys.py` | Muestra ese CSV en rofi como buscador; si la entrada tiene una `action` asociada, la copia al portapapeles al seleccionarla. |

## Layouts de zellij para Claude Code

Generan y lanzan pestañas de zellij con un layout por proyecto, para trabajar con Claude
Code (local o dentro de la VM — ver [vm](../vm)) en un panel dedicado por proyecto:

| Script | Qué hace |
|---|---|
| `generar_layouts_claude.sh` | Por cada ruta en `rutas_proyectos_claude.txt`, genera un `.kdl` de zellij a partir de una plantilla (`claude_proyecto.kdl`), sustituyendo el directorio del proyecto local y su equivalente remoto. |
| `generar_layouts_claude_vm.sh` | Lo mismo pero con la plantilla `claude_vm_proyecto.kdl`, para la variante que corre dentro de la VM. |
| `zellij_claude_tab.sh` | Menú rofi con los layouts ya generados; al elegir uno, abre una pestaña nueva de zellij con ese layout. |
| `zellij_claude_vm_tab.sh` | Igual que el anterior pero sobre los layouts de `layouts/claude-vm`. |
