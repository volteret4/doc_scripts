+++
title = 'WordPress'
weight = 12
+++

Ruta: `~/Scripts/utilities/wordpress/`

A pesar del nombre de la carpeta, son sobre todo utilidades de búsqueda/playlists
musicales sueltas, sin relación directa con WordPress:

| Script | Qué hace |
|---|---|
| `buscar_album_desde_firefox.sh` / `buscar_album_en_todo.sh` | Toman el título de la ventana activa (o el portapapeles) y buscan el álbum correspondiente. |
| `spotify.sh` / `playlist.sh` | Piden artista/canción por `zenity` y consultan la API de Spotify. |
| `Crear_playlists_yt_sp.sh` | Formulario `zenity` de varios campos para crear una playlist tanto en YouTube como en Spotify a la vez. |
| `chat_GPT.sh` | Llama a la API de OpenAI (`curl` con el token leído de `.env`) con un prompt. |
