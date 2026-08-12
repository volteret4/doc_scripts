+++
title = 'Aliases'
weight = 1
+++

Ruta: `~/Scripts/utilities/aliases/`

Según su propio README: *"Funciones muy específicas, normalmente usadas en otros
scripts"*. Es el cajón de sastre de `~/Scripts`: 43 archivos sin estructura de
subcarpeta común, agrupados aquí por tema.

## Meta: scripts sobre scripts

| Script | Qué hace |
|---|---|
| `hacer_ejecutables.sh` | Da permiso de ejecución (`chmod u+x`) a todos los archivos que ya son ejecutables dentro de una carpeta (recursivo). |
| `encontrar_scripts_en_uso.sh` | Analiza `~/Scripts` para averiguar qué scripts están realmente en uso (referenciados desde otros sitios), con opción de hacer backup. |
| `detectar_scripts_dependientes.py` | Analiza un directorio buscando llamadas de un script a otro, para mapear dependencias entre scripts. |
| `detectar_rutas_en_otro_script.sh` | Dado un script, extrae todas las rutas absolutas y relativas que contiene. |
| `recuento_scripts.sh` | Lleva la cuenta de cuántas veces se ha lanzado un script concreto. |
| `add_text_to_files_on_dir.sh` | Añade una cabecera de comentario estándar (nombre, descripción, autor...) a los scripts de una carpeta que no la tengan. |
| `crear_requeriments_proyecto.py` | Genera un `requirements.txt` detectando los imports realmente usados en el proyecto (con una tabla de casos especiales tipo `dotenv` → `python-dotenv`). |
| `paquetes_python_en_venv.py` | Lista los paquetes instalados en el venv compartido leyendo directamente los `.dist-info`, para cuando `pip list` falla. |
| `clean_apis_scripts.py` | Busca una cadena de texto en un directorio y abre los archivos que la contienen en VSCodium. |
| `replace_specific_line.py` | Reemplaza una línea concreta de un archivo mostrando contexto (diff) antes de aplicar el cambio. |

## Audio y música

| Script | Qué hace |
|---|---|
| `en_reproduccion.sh` | Devuelve qué está sonando ahora (Deadbeef o, si no, `playerctl`) — lo usa `vvmm_post_creator.sh` (ver [Blog]({{% relref "scripts/musica/blog" %}})) y varios más. |
| `cortar_flac_con_cue.sh` | Divide un FLAC en pistas individuales a partir de su `.cue`. |
| `replay_gain.py` | Calcula y aplica ReplayGain con `ffmpeg` a una colección de audio. |
| `tag_genres_punto_y_coma.py` | Normaliza el tag `GENRE` de los archivos de música, sustituyendo comas/puntos/guiones por `;`. |
| `comparar_musica_moode_de_lidarr.py` | Compara dos bibliotecas de música por metadatos (artista/álbum), no por nombre de archivo. |
| `picard_loader.sh` | Carga en MusicBrainz Picard la lista de álbumes sin género pendientes de etiquetar. |
| `muspy_list_artists.py` | Exporta a `artists.txt` los artistas seguidos en Muspy. |
| `spoti.sh` | Abre una URI de Spotify (arrancando el cliente con adblock vía `LD_PRELOAD` si no estaba abierto). |

## Sistema y red

| Script | Qué hace |
|---|---|
| `dns-test.py` | Comprueba resolución DNS de una lista de dominios. |
| `new_lan_ip_detected.sh` | Escanea la LAN con `nmap`, compara contra un fichero de hosts conocidos y notifica si aparece una IP nueva. |
| `kitty_cambia_fuente.sh` | Menú para cambiar la fuente de Kitty entre las instaladas en el sistema. |
| `dunstrc_centro.sh` | Cambia temporalmente la config de `dunst` para centrar y agrandar las notificaciones (con backup del archivo original). |
| `nerd-dictation.sh` | Activa/desactiva `nerd-dictation` (dictado por voz) con notificación persistente de estado. |
| `qr_code_from_url.sh` | Genera un QR de la URL en el portapapeles y lo muestra. |
| `copiar_color_clipboard.sh` | Captura un color de pantalla con `xcolor` y lo manda al portapapeles (CopyQ). |
| `mostrar_tabla_sqlite.py` | Vuelca por terminal la estructura de todas las tablas de una base SQLite. |
| `server.py` | Levanta un servidor HTTP temporal sirviendo la carpeta actual. |
| `git.sh` | `git add . && git commit` rápido, pidiendo el mensaje si no se pasa como argumento. |
| `tmux_boot_and_resurrect.sh` | Arranca tmux con una config concreta y restaura la última sesión (plugin `tmux-resurrect`). |
| `tmux/tmux_session_manager.py` | Guardar/restaurar sesiones de tmux nombradas. |
| `limpia_var.sh` | Sanea un string dejando solo caracteres alfanuméricos. |

## Archivos y sincronización

| Script | Qué hace |
|---|---|
| `mantener_archivos_del_listado.sh` | Borra de una carpeta todo lo que **no** esté en un listado de archivos a conservar (con modo `DRY_RUN`). |
| `ordenar_descargas.py` | Ordena `~/Descargas` por fecha. |
| `sync_film_to_proxmox.sh` | Copia por `rsync` los archivos listados en un `.txt` a otro servidor, eliminando del listado solo lo que se copió con éxito. |
| `wallabag_to_datahoarder.rb` | Convierte un export de Wallabag al formato de import de [Hoarder](https://github.com/hoarder-app/hoarder). |
| `barra_progreso.sh` | Barra de progreso mostrada con `yad` en vez de en terminal. |

## VM Arch desechable (`maquina virtual desechable/`)

Cuatro scripts para levantar un contenedor Arch "de usar y tirar" con
`systemd-nspawn` + Docker (red bridge propia `br-systemd-nspawn`):
`maquina_virtual_desechable.sh` (crea/lanza el contenedor desde una plantilla),
`arch_docker.sh` (variante más simple), `fix_dns.sh` (arregla resolución DNS dentro del
contenedor) y `reparar_template.sh` (limpieza/reparación de emergencia de la plantilla).

## docker/

`update_invidious_env.sh` — lanza el contenedor
`quay.io/invidious/youtube-trusted-session-generator`, extrae `visitor_data`/`po_token`
de su salida y actualiza con ellos el `.env` de la instancia propia de Invidious.

{{% notice warning %}}
`pause_obsidian.sh` (pausa una carpeta de Syncthing mientras se usa Obsidian) tenía la
API key de Syncthing escrita directamente en el script — resultó ser código muerto (no
la leía nadie; `syncthing cli` se autentica con su propia config local) y ya se
eliminó. Pero ese valor sigue expuesto en el historial de git de este repo, ya
empujado a GitHub: sigue pendiente **regenerar la API key desde la propia GUI de
Syncthing**, borrar la línea no retira nada del historial.
{{% /notice %}}
