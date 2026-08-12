+++
title = 'Deadbeef'
weight = 3
+++

Ruta: `~/Scripts/Musica/deadbeef/`

## infobar/ — plugin nativo en C

Un plugin real de **DeaDBeeF** escrito en C (`plugin.c`, `ui.c`, `runner.c` + cabeceras,
con `Makefile` propio y el `.so` ya compilado): añade una barra de información dentro de
la GTKUI del reproductor. `runner.c` es quien lanza los scripts Python de esta misma
carpeta (biografía, letras, info de álbum...) y vuelca su resultado en la interfaz.

## Scripts Python de apoyo

Todos ejecutables con el intérprete del venv compartido
(`#!/home/huan/Scripts/python_venv/bin/python`), pensados para ser invocados por el
plugin `infobar` con el artista/álbum/canción actual como argumentos:

| Script | Qué hace |
|---|---|
| `bio_artista.py` | Biografía del artista combinando Last.fm y Wikipedia. |
| `info_album.py` | Información del álbum vía MusicBrainz, Last.fm y Wikipedia. |
| `similares.py` | Canciones similares por Last.fm, con fallback a artistas relacionados de MusicBrainz si Last.fm no da resultado. |
| `letras_genius.py` | Letras vía la API de Genius (`lyricsgenius`), con el token cargado a través de [`sops_env.py`](../../tools). |
| `letras_ovh.py` | Letras vía la API pública [lyrics.ovh](https://lyrics.ovh). |
| `control_music_player.py` | Control unificado de reproducción para **Deadbeef y Airsonic** a la vez (mismo interfaz de comandos para ambos). |
| `sops_env.py` | Copia local del puente SOPS+age ([`tools/sopsdotenv`](../../tools)) para descifrar `.encrypted.env` sin depender de `python-dotenv`. |
