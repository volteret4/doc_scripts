+++
title = 'Conciertos'
weight = 2
+++

Ruta: `~/Scripts/Musica/conciertos/`

## telegram/ — bot de búsqueda y notificación de conciertos

Bot de Telegram completo (README propio) que busca conciertos combinando
**Ticketmaster**, **Spotify** y **Setlist.fm**, con MusicBrainz y Last.fm como apoyo
para info de artista. Estructura modular: `bot/apis/` (un cliente por servicio),
`bot/handlers/` (comandos y calendario), `bot/database.py` (SQLite propio,
`artist_tracker.db`), `bot/concert_search.py` (orquesta la búsqueda combinando fuentes),
`bot/notifications.py` (avisos). `telegram_bot.py`/`bot.py` son los puntos de entrada;
`setup_notif.sh` + `notificaciones_conciertos.service` instalan la búsqueda diaria
automática (9:00) como servicio systemd.

Funciones principales: búsqueda por país, artistas favoritos con notificaciones
activables por artista, y estadísticas de uso por usuario.

## ticketmaster/ — comprobador de conciertos por cron (sin Telegram)

Dos variantes en bash del mismo concepto, pensadas para lanzarse por cron y avisar por
[ntfy](https://ntfy.sh) (`https://ntfy.pollete.duckdns.org/conciertos`) cuando aparece
un concierto nuevo:

| Script | Qué hace |
|---|---|
| `conciertos.sh` | Pide a la API de Ticketmaster los conciertos de música en España del año siguiente (200 resultados, el máximo permitido), filtra con `filtro.jq`, compara contra la consulta anterior (`filtrado.bak`) y notifica solo las entradas nuevas. |
| `ticketmaster_api.sh` | Misma idea pero filtrando además por una lista concreta de artistas (`artistas.txt`) en vez de traer todo el catálogo. |

{{% notice note %}}
`Musica/conciertos/telegram/` es, con toda probabilidad, el desarrollo local del
proyecto `bot_conciertos` de `~/gits/pollo` (ver sección Proyectos).
{{% /notice %}}
