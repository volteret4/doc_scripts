+++
title = 'Playlists'
weight = 9
+++

Ruta: `~/Scripts/Musica/playlists/`

Gestión de playlists a través de varios servicios: Airsonic, Mixxx, MusicBrainz y
Spotify.

## airsonic/

| Script | Qué hace |
|---|---|
| `create_music_db.py` | Indexa (mutagen) toda la música del NFS en una base SQLite local. |
| `create_new_playlists.py` | Convierte playlists `.m3u` locales a playlists que apuntan a las rutas del servidor NFS, resolviendo cada pista por artista/álbum contra esa base. |
| `search_missing.py` | Modo interactivo para resolver a mano las pistas que no se encontraron automáticamente. |
| `import_to_airsonic.py` | Sube las playlists `.m3u` resultantes a Airsonic vía la API Subsonic. |
| `.old/airsonic_sync_*.py` | Versiones anteriores de sincronización (loved tracks, metadata, playlists) — sustituidas por el flujo de arriba. |

## mixxx/

`embeed_cover.py` — incrusta la carátula del álbum en los tags (ID3/FLAC) de los
archivos que no la tienen, para que Mixxx la muestre.

## musicbrainz/

`musictree_to_mb.py` (con `CLAUDE.md` propio): scrapea los ~1100 álbumes canónicos de
[musicgenretree.org](https://www.musicgenretree.org/text_classics.html), los busca en
MusicBrainz y crea/rellena ahí una Serie "Music Genre Tree – Classics". Soporta
`--dry-run`, reanudar desde un CSV cacheado (`--load-csv`) y añadir a una serie ya
existente por MBID.

## spotify/

| Script | Qué hace |
|---|---|
| `sp_menu_playlists.py` | Selector Tkinter de playlists (ver también [`menus/spotify`]({{% relref "scripts/menus/spotify" %}})). |
| `sp_create_playlist_from_txt.py` | Crea una playlist de Spotify a partir de un `.txt` con líneas `artista - canción`. |
| `spotify_add_song.py` | Añade la canción que suena ahora mismo a una playlist de Spotify elegida por GUI (PyQt6). |
| `sp_sync_lastfm_loved_tracks.py` | Sincroniza los "loved tracks" de Last.fm hacia una playlist de Spotify (crea o actualiza). |
| `sp_sync_mixxx.py` | Sincronización incremental de playlists `.m3u` de Mixxx hacia Spotify, leyendo metadata de los archivos de audio en vez de parsear nombres, pensado para cron. |

## m3u_to_txt.py

Suelto en la raíz de `playlists/`: convierte un `.m3u` a un `.txt` de líneas
`Artista - Canción`, leyendo metadata con mutagen y usando el nombre de archivo como
fallback.
