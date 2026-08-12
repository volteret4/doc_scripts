+++
title = 'Estadísticas'
weight = 5
+++

Ruta: `~/Scripts/Musica/estadisticas/`

| Script | Qué hace |
|---|---|
| `artistas_en_bluesky.py` | Comprueba, para una lista de artistas (`~/Scripts/.content/artistas.txt`), si existen como cuenta en Bluesky. |
| `musicbuttler_add_artists.py` | Añade artistas a [MusicButler](https://www.musicbutler.io) autenticándose por cookie de sesión + token CSRF capturados manualmente del navegador. |
| `lastfm/lastfm.py` | Wrapper simple sobre la API de Last.fm para consultar info de usuario. |
| `lastfm/sincronizar_scrobbles_con_airsinic.py` | Sincroniza scrobbles de Last.fm hacia **Airsonic-Advanced**, cacheando en SQLite (`scrobbles.db`) lo ya sincronizado para no duplicar. |
| `lastfm/listenbrainz_to_lastfm/listenbrainz_to_lastfm.py` | Reenvía (scrobblea) el historial de escucha de **ListenBrainz** hacia Last.fm. |
| `lastfm/listenbrainz_to_lastfm/get_lastfm_sig.py` | Calcula la firma MD5 (`api_sig`) que exige el flujo de autenticación por escritorio de la API de Last.fm, a partir de `api_key`/`secret`/`token`. |

{{% notice note %}}
`lastfm/sincronizar_scrobbles_con_airsinic.py` es la contraparte de escritorio de lo que
hace el proyecto `back_rym_lastfm`/`rym_lastfm` en `~/gits/pollo`.
{{% /notice %}}
