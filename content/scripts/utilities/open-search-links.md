+++
title = 'Open search links'
weight = 7
+++

Ruta: `~/Scripts/utilities/open_search_links/`

Búsqueda contextual: tomar texto/URL seleccionado y abrirlo en el sitio/motor
adecuado, casi siempre disparado por hotkey con el contenido ya en el portapapeles vía
`xclip`.

## Búsqueda general

| Script | Qué hace |
|---|---|
| `busqueda_en.sh` | Busca el texto del portapapeles en los motores pasados como argumento. |
| `abrir_url_en_chromium.sh` / `abrir_url_en_firefox.sh` / `url_en_otro_navegador.sh` | Reabren la URL de la ventana activa en otro navegador distinto al que la tiene abierta. |
| `google_translate_api.sh` / `google_translate_qutebrowser.sh` | Traducen el texto seleccionado con Google Translate (una vía API, otra abriendo qutebrowser directamente). |
| `busqueda_api/youtube-1arg.py` | Busca en la API de YouTube Data un vídeo/playlist a partir de artista + disco. |

## music_player/ — metadatos de lo que suena ahora

Un script por servicio: cada uno construye la URL de búsqueda de ese servicio para la
canción/álbum que está sonando y la abre en el navegador (mismo patrón que
[`en_reproduccion.sh`]({{% relref "scripts/utilities/aliases" %}}) para detectar qué
suena). Cubren Bandcamp, Discogs, Google, Orpheus (el tracker privado, ver
[Orpheus API]({{% relref "scripts/musica/orpheus-api" %}})), RuTracker, RateYourMusic,
Spotify, Wikipedia y YouTube.

`odesli.py`/`odesli_metadata.py`/`odesli_metadata_padre.sh` son el caso más elaborado:
en vez de enlazar a un solo servicio, usan la API de [Odesli](https://odesli.co) para
generar un enlace universal (MusicBrainz → Deezer → YouTube Music como cadena de
fallback), sin depender de la API de Spotify.
