+++
title = 'Bot Conciertos'
weight = 2
+++

*(nombre interno: "tumtumpá")*. Bot de Telegram para seguir conciertos y lanzamientos de
artistas favoritos: busca conciertos en **Ticketmaster** (filtrado por país), sincroniza
lanzamientos con **Muspy**, enriquece con **Last.fm** (géneros, oyentes) y
**MusicBrainz** (MBID, año de formación), exporta el calendario a `.ics` o lo empuja
directamente a Radicale (CalDAV) o Google Calendar, envía un resumen semanal
configurable y permite buscar vídeos de un artista en YouTube.

## Dos procesos independientes

```bash
python telegram_bot.py      # bot principal — long-polling, hasta 256 updates concurrentes
python notifications.py     # scheduler semanal — proceso aparte
```

`notifications.py` comprueba cada minuto si el día+hora configurado por algún usuario
coincide con el actual; cuando coincide, busca en Ticketmaster (por país), trae los
lanzamientos de Muspy de los próximos 90 días y manda un único resumen, llevando cuenta
de la última semana notificada por usuario para no duplicar. En producción corren como
dos servicios systemd separados: `bot_conciertos.service` y `bot_notifications.service`.

| Módulo | Rol |
|---|---|
| `database.py` | SQLite (`ArtistTrackerDatabase`) envuelta en `DatabaseConcurrentWrapper` para thread-safety: usuarios, artistas, conciertos, notificaciones enviadas, credenciales de Muspy, config de Radicale. |
| `concert_search.py` | Búsquedas async en Ticketmaster por país, deduplicación, persistencia. |
| `user_services.py` | Inicializadores singleton de Ticketmaster/Last.fm/países; clase `UserServices` para config por usuario. |
| `apis/ticketmaster.py` | Búsqueda de conciertos con caché JSON de 24h en `./cache/ticketmaster/`. |

Es, con toda probabilidad, la versión "de producción" (Docker + `Dockerfile.web`) del
mismo bot que documenta
[`Musica/conciertos/telegram`]({{% relref "scripts/musica/conciertos" %}}) en
`~/Scripts`. Integrado como submodule del orquestador
[Tumtumpa]({{% relref "proyectos/musica-escucha/tumtumpa" %}}).
