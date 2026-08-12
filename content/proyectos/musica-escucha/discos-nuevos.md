+++
title = 'Discos Nuevos'
weight = 10
+++

*(nombre interno del README: "discospatitunaitunai")*. Añade al calendario los discos
nuevos de los artistas seguidos en **Muspy**, en tres sabores de destino: CalDAV, `.ics`
o Google Calendar.

## Añadir artistas a Muspy (`add_artists_muspy/`)

| Script | Qué hace |
|---|---|
| `file_artists_to_muspy.py` | Añade artistas listados en un archivo. |
| `music_path_to_muspy.py` | Escanea la biblioteca local y añade lo que encuentra. |
| `spotify_to_muspy.py` | Añade los artistas seguidos en Spotify. |

## Publicar los lanzamientos (`add_releases/`)

Todas parten del feed Atom/RSS de Muspy (`https://muspy.com/feed?id=...`):

| Script | Destino |
|---|---|
| `add_releases_caldav.py` | Un calendario CalDAV (Radicale, Nextcloud...), con deduplicación automática (`--no-cleanup` para desactivarla). |
| `add_releases_ics.py` | Un archivo `.ics` local. |
| `add_releases_google_calendar.py` | Google Calendar, por OAuth2 o Service Account, con colores personalizables por tipo de lanzamiento (álbum/EP). |

Credenciales por `--flags`, variables de entorno o `.env`, en ese orden de prioridad.
Todas admiten `--quiet` pensado para crontab.

{{% notice note %}}
Es la versión "de proyecto propio" de lo que en `~/Scripts` cubren
[`Musica/discos-nuevos`]({{% relref "scripts/musica/discos-nuevos" %}}) (que trabaja
contra Radicale directamente) y el bot de Telegram de Muspy documentado ahí mismo.
{{% /notice %}}
