+++
title = 'mpv'
weight = 7
+++

Ruta: `~/Scripts/Musica/mpv/`

Reproducción y gestión de playlists con mpv (y algo de VLC), controlado por atajos de
teclado y el portapapeles.

| Script | Qué hace |
|---|---|
| `add_queue_vlc.sh` | Toma una URL del portapapeles; si es de YouTube la resuelve con `youtube-dl`/`yt-dlp` y la añade a la cola de mpv. |
| `vlc_playlist_file.sh` | Reproduce un archivo de playlist (`.m3u` u otro) dado como argumento con mpv. Lo reutilizan varios scripts de `snippets/tareas` (ver [Tareas]({{% relref "scripts/snippets/tareas" %}})) para reproducir colas de "para escuchar". |
| `youtube_en_mpv.sh` | Comprueba que el navegador esté activo, toma una URL de YouTube del portapapeles y la añade a `mpv/playlist` si no está ya (comprobando la fecha de modificación del archivo). |
| `playing_metadata_info.sh` | Consulta el socket IPC de mpv (`/tmp/mpvsocket` vía `socat`) para obtener posición y tiempo restante de la pista actual. |
| `save_playlist.sh` | Automatiza (con `xdotool`) el comando interno de mpv para guardar la playlist actual: enfoca la ventana, borra el nombre por defecto y escribe uno nuevo. |
| `recomendaciones_lastfm.sh` | Dada una lista de usuarios de Last.fm predefinida (o uno pasado por argumento), obtiene recomendaciones. |
| `playlistmanager.lua` | Script Lua del gestor de playlist visual de mpv (atajos configurables, por defecto `Shift+Enter` para mostrar/ocultar la playlist). |
