+++
title = 'Blog'
weight = 1
+++

Ruta: `~/Scripts/Musica/blog/`

Generadores de contenido para los distintos blogs/colecciones musicales del usuario.
Cada subcarpeta es prácticamente un mini-proyecto independiente (varias tienen su propio
`README.md` extenso).

## bandcamp/ — colección de correos de Bandcamp

Convierte las notificaciones de "new release" de Bandcamp (ver también
[`filtros_masivos_thunderbird.sh`]({{% relref "scripts/apps/escritorio" %}})) en una
colección navegable. Hay **dos vías de entrada** y varias generaciones de la misma idea:

- **`imap/`** — lee los correos directamente por IMAP (`bc_html_generator_imap_v2.py`),
  genera un HTML por género con botones para marcar como leído/eliminar el correo
  (servidos por `api_server.py`, un pequeño servidor Flask), y un índice
  (`bc_index_generator.py`).
- **`imap/github version/`** — variante pensada para publicarse en **GitHub Pages**:
  exporta los correos a JSON (`bc_export_to_json.py`), genera un sitio estático
  (`bc_static_generator.py`) que guarda el estado "escuchado" en `localStorage` del
  navegador (así no depende de un backend), y se sincroniza de vuelta con
  `bc_sync.py` a partir de un export manual del `localStorage`.
- **`thunderbird/`** — variante que en vez de IMAP lee directamente los mboxes locales
  de Thunderbird (`bc_html_generator.py`, `find_thunderbird_folders.py`), con un
  servidor local aparte (`thunderbird_server.py`) para poder marcar correos como leídos
  desde el HTML generado.

## rss/ — FreshRSS → embeds

`freshrss_html_generator.py` se conecta a un **FreshRSS** propio (API compatible con
Google Reader) y extrae enlaces de Bandcamp/YouTube/SoundCloud de los artículos de
feeds o categorías completas, generando páginas HTML paginadas con lazy loading.
`freshrss_html_index.py` genera el índice general, `freshrss_sync.py` elimina del HTML
los embeds ya marcados como escuchados en el navegador, y `server_html.py` sirve los
HTML por HTTP (necesario porque YouTube no reproduce embeds en `file://`).

## rym/ — importar usuarios de Last.fm desde una hoja de cálculo

`rymers_lastfm_csv.py`: descarga una Google Sheet pública en CSV y extrae de ahí la
lista de nombres de usuario de Last.fm del grupo.

## rym_lastfm/ — estadísticas de coincidencias entre usuarios de Last.fm

`lastfm_stats_generator` (ver README propio, muy extenso) genera HTML con estadísticas
de qué música tienen en común varios usuarios de Last.fm: artistas/canciones/álbumes/
géneros/sellos coincidentes, en periodos semanal/mensual/anual, cacheadas en SQLite.
Pensado para correr por cron/GitHub Actions y publicarse como página estática. El README
incluye además un backlog largo de gráficas pendientes de implementar (streaks,
descubrimientos, "golden oldies"...) — es más una libreta de ideas que documentación de
lo ya construido.

## sesiones/ — reproductor HTML de una carpeta de MP3

`html_index.py`: genera un único HTML con un reproductor de audio embebido a partir de
una carpeta de mp3.

## sobrinos/ — colección de discos físicos con tarjetas NFC para los sobrinos

El más peculiar de todos: un sistema tipo "Yoto/Tonie" casero. Versión completa (incluye
también cine/series, no solo música) documentada en
[Proyectos → Sobrinos]({{% relref "proyectos/personal/sobrinos" %}}).

- `album_web_generator.py` + `modules/` — genera una página web por álbum (portada,
  letras, enlaces) a partir de los metadatos de los archivos de música.
- `nfc/nfc_generar_portada.py` — genera dos imágenes verticales de 52×82mm (carátula +
  lista de pistas) para imprimir como tarjeta física del álbum.
- `nfc/nfc_detect_uid.py` — lee el UID de una tarjeta NFC acercada a un lector.
- `nfc/nfc_reaccionar.py` — mapea UIDs de tarjetas concretas a comandos a ejecutar (p.
  ej. lanzar la reproducción del álbum correspondiente): el "launcher" que convierte
  acercar la tarjeta en poner el disco.

## tumtumpa/ — recolector de información de artista/álbum

`recolector_info.py`: agrega información de un artista/álbum desde Wikipedia, Last.fm y
Spotify (con scraping/placeholders para AllMusic, WhoSampled, entrevistas y reseñas de
prensa musical) — alimenta al blog tumtumpa (ver también el proyecto
`tumtumpa` en Proyectos).

## vvmm/ — creador de posts automático (el más completo)

`vvmm_post_creator.sh` (con README propio extenso): detecta qué se está reproduciendo
(Deadbeef/Strawberry vía `playerctl`), busca metadatos e información del álbum en
Spotify, Discogs, Last.fm, YouTube, MusicBrainz, Bandcamp y Wikipedia, descarga la
carátula, deja elegir tags y playlist de Spotify por interfaz gráfica (`yad`), genera el
post en Hugo para el blog `vvmm` y hace commit/push automático a git.

## mfuz/ y `music_fuzzy` (suelto) — Obsidian → Hugo para el blog music-fuzzy

`mfuz/padre.sh` orquesta `mfuz/hugo_blog_relearn_theme.py`, que convierte notas de
Obsidian a posts de Hugo (tema Relearn) para el blog de **music-fuzzy**, resolviendo
además referencias a scripts/imágenes citadas en la nota. `mfuz/debug.py` es una
utilidad de depuración para ver qué referencias detecta el conversor. El archivo suelto
`music_fuzzy` (sin extensión, en la raíz de `blog/`) es una versión más simple y
anterior del mismo conversor Obsidian→Hugo.
