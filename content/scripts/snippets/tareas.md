+++
title = 'Tareas'
weight = 2
+++

Ruta: `~/Scripts/snippets/tareas/`

{{% notice note %}}
El propio `README.md` de esta carpeta lo resume mejor que cualquier descripción externa:

> *"Esto es un desastre! Hay un par de scripts usados medio frecuentemente... he intentado
> hacer puentes entre muchas apps (caldav, todoman, taskwarrior, todo.txt), y no ha sido
> fácil de mantener."*

Por eso esta página agrupa por **función** en vez de listar cada archivo: hay bastante
solape y varias versiones bash/Python del mismo puente.
{{% /notice %}}

## Captura rápida de tareas/eventos

| Script | Qué hace |
|---|---|
| `crear_tarea_TODO.sh` | Toma el portapapeles (`copyq`), pide un título con `zenity` y crea una tarea con `todo` (todo.txt), detectando si el contenido es un enlace de música (YouTube/Bandcamp/SoundCloud) para mandarla al calendario "musica" en vez de "tareas". |
| `crear_tarea_caldav.py` | Versión GUI (PyQt6) del mismo flujo: añade la tarea al calendario CalDAV correspondiente (Radicale), a todo.txt en Obsidian, a `todofi.sh` y a Taskwarrior a la vez. |
| `crear_evento_caldav.sh` | Crea un evento con fecha (`zenity --calendar`) en el calendario CalDAV "discos" vía `khal`, usando el portapapeles como descripción, y sincroniza con `vdirsyncer`. |
| `disco_pendiente.sh` | Comprueba qué navegador/reproductor está activo ([`if_firefox_active.sh`](../utilidades)), toma el álbum del portapapeles y, según el género elegido en un diálogo, lo añade a todo.txt con el tag correspondiente (`+ambient`, `+deep`, `+techno`...) para escucharlo más tarde. |

## Interfaz rofi para todo.txt

`todofi.sh` y `todofi_alb.sh` son dos copias casi idénticas de un frontend rofi para
todo.txt (basado en el proyecto `todofish`/`todofi.sh` de la comunidad): listan,
filtran, crean y marcan como hechas tareas de un archivo todo.txt, con atajos de teclado
configurables. Difieren sobre todo en la ruta del archivo de configuración y el editor
por defecto (`helix` vs `gedit`) — en la práctica solo una de las dos está en uso activo.

## Sincronización CalDAV ↔ todo.txt ↔ Taskwarrior

| Script | Qué hace |
|---|---|
| `tw_cald_sync.sh` | El más completo: exporta Taskwarrior a JSON (`task export`), lo convierte a todo.txt con [`tw_2_todo`](#tw_2_todo-conversor-vendorizado), extrae las tareas etiquetadas `@compras`/`+compras` a una lista aparte, y sincroniza con `vdirsyncer`. |
| `sync_todo_caldav.sh` / `sync_todo_caldav.py` | Dos implementaciones (bash y Python) del mismo cotejo: comparan la lista obtenida de CalDAV (`todo list`) contra el archivo de tareas completadas, buscando coincidencias de título para no duplicar. |
| `sync.sh` | Variante puntual: busca la última tarea marcada como hecha en `t_done.txt`, localiza su ID en `todo list` y la marca como completada, sincronizando después. |
| `sync_tareas/delete_duplicate_taskwarrior.py` | Recorre las tareas pendientes de Taskwarrior (vía `task status:pending`) buscando y eliminando duplicados. |
| `sync_tareas/obsidian_tasks_to_the_world.py` | Versión "en segundo plano" (sin GUI) de `crear_tarea_caldav.py`, con checkpoint para recordar la última fecha ya procesada. |
| `sync_tareas/vdirsyncer_to_the_workd.py` | Importa tareas desde **todoman** hacia todo.txt, Taskwarrior y Obsidian. |

## Conversión de formatos

| Script | Qué hace |
|---|---|
| `json_todotxt.py` | Parsea un archivo todo.txt línea a línea (prioridad, fecha, proyectos `+x`, contextos `@x`) y lo vuelca a JSON. |
| `import json.py` | Conversor puntual de un JSON concreto (viene de Tasker) al formato de import de Taskwarrior. |
| `import-todo.sh`, `import_todo_albums.pl`, `json_a_todotxt.pl` | Scripts **vendorizados** del propio proyecto Taskwarrior (cabecera de copyright de Beckingham/Hernandez) para importar/exportar entre Taskwarrior y todo.txt; `import_todo_albums.pl` es una adaptación para la lista de discos pendientes. |

### `tw_2_todo/` (conversor vendorizado)

Subcarpeta con su propio repositorio git y licencia: un fork del proyecto
[`tw_2_todo`](https://github.com/) que convierte exports de Taskwarrior a formato
todo.txt (`convert.py -i export.json -o todo.txt -a done.txt`), preservando proyecto,
estado, prioridad (`H`/`M`/`L` → `(A)`/`(B)`/`(C)`) y convirtiendo tags a contextos. Es
la pieza que usa `tw_cald_sync.sh` para el paso Taskwarrior → todo.txt.

## Escuchar (cola de música pendiente)

| Script | Qué hace |
|---|---|
| `escuchar_tareas/banbantonton.sh` | Vuelca la pestaña "banbantonton" del historial de CopyQ, extrae de cada enlace las URLs de YouTube/Bandcamp encontradas en la página, deduplica y arma una playlist para `Musica/mpv/vlc_playlist_file.sh` (ver sección Música). |
| `escuchar_tareas/escuchar.sh` | Menú de géneros (`zenity`) sobre el historial de CopyQ acumulado ("Escuchado", "URLs"): arma una playlist `.m3u` filtrando lo ya escuchado y la reproduce con el mismo script de mpv. |

## Notas

`obsidian/recomendaciones_a_tareas.py` lee archivos Markdown de un directorio de
"recomendaciones" (uno por tag, con secciones separadas por delimitadores) para
convertirlas en tareas.
