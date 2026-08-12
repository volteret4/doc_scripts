+++
title = 'MoverMusica'
weight = 6
+++

Ruta: `~/Scripts/Musica/MoverMusica/`

Conversión, deduplicado y traslado de archivos de audio entre carpetas/servidores.

| Script | Qué hace |
|---|---|
| `mover_mix_playerctl.py` | GUI PyQt6 (`.ui` cargado con `uic`): mueve la canción que suena ahora mismo (vía `playerctl`) a una subcarpeta de "Mix" clasificada por criterio propio (género, etc.). |
| `actualizar_old_mix.py` | Renombra en bloque los archivos de esas subcarpetas al formato `artista - canción (fecha álbum) [sello]` y marca cada tema como "loved" en Last.fm. Explícitamente basado en `mover_mix_playerctl.py`. |
| `eliminar_duplicados_mix.py` | Calcula un hash MD5 del contenido binario de cada archivo para detectar y eliminar duplicados exactos. |
| `convert_to_flac16_44.py` | Analiza FLACs con `ffprobe` (sample rate, bits) y los reconvierte a 16-bit/44.1kHz cuando hace falta. |
| `convertir_mp3_320.sh` | Convierte una carpeta de FLAC a MP3 320kbps, pensado para subir el resultado a un VPS. |
| `Mover_torrents.sh` | Vigila `~/Descargas` y envía los `.torrent` encontrados por `rsync`/`ssh` a las carpetas *watch* de un tracker remoto (dietpi). |
| `NewPipe/add_item_to_playlist.sh` | Añade un vídeo a una playlist de NewPipe vía `adb` (marcado *WIP*, requiere el móvil conectado). |
