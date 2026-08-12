+++
title = 'dmenu'
weight = 1
+++

Ruta: `~/Scripts/menus/dmenu/`

Lanzadores clásicos basados en `dmenu`, la mayoría pensados para ejecutarse desde un
atajo de teclado del gestor de ventanas.

| Script | Qué hace |
|---|---|
| `dmenu_supermenu.sh` | Menú raíz: elige entre dotfiles / edit_scripts / web / yt_channels / yt_busqueda / search_google / mpd / mix y ejecuta el script correspondiente. |
| `dmenu_dotfiles.sh` | Lista con `fd` los archivos de `~/.dotfiles`, y al elegir uno lo abre con **helix** dentro de una ventana nueva de **tmux** (arrancando tmux/kitty si hace falta). |
| `dmenu_dotfiles_old.sh` | Versión anterior y más simple: menú fijo de "config conocidas" (alacritty, awesomewm, rofi, zshrc...) que abre el archivo correspondiente con `vim` en `termite`. Sustituida por `dmenu_dotfiles.sh`, se mantiene como referencia. |
| `dmenu_edit_scripts.sh` | Igual que `dmenu_dotfiles.sh` pero para buscar y editar cualquier script ejecutable de `~/Scripts`. |
| `dmenu_launch_scripts.sh` | Busca scripts ejecutables en `~/Scripts` con `fd` + `dmenu` y los **lanza** (no los edita) en una terminal. |
| `dmenu_web.sh` | Buscador multi-motor: lee `dmenu-websearch-sources` (tabla de atajo → URL) y abre el resultado con `xdg-open`. |
| `dmenu-websearch-sources` | Tabla de datos de `dmenu_web.sh`: atajos de 2 letras a buscadores (Google, DuckDuckGo, Bandcamp, YouTube, Wikipedia, GitHub, Arch Wiki, Amazon, Spotify...). |
| `dmenu_search.sh` | Buscador con historial persistente (`.{gs}hist`); si el término empieza por `m ` busca en Bandcamp, si empieza por `i ` busca en Stack Overflow/GitHub/Quora, si no en Google. Marcado como *work in progress* en sus propios comentarios. |
| `dmenu_mpd.sh` | Control de MPD por menú: añadir álbum/pista, seleccionar pista de la cola, activar/desactivar aleatorio, mostrar notificación con lo que suena. El propio script lo etiqueta de "gpt powered". |
| `ssgen.sh` | Utilidad de apoyo: dado un nombre, crea (si no existe) un script vacío ejecutable en `~/.local/bin` y lo abre con `geany`. Usado como dependencia por `dmenu_dotfiles.sh`/`dmenu_edit_scripts.sh` para "crear si no existe". |

{{% notice note %}}
`dmenu_dotfiles_old.sh` y `dmenu_dotfiles.sh` resuelven lo mismo de dos formas distintas;
la versión "old" está documentada por si sigue en uso en algún atajo, pero la activa es
la nueva.
{{% /notice %}}
