+++
title = 'Discos nuevos'
weight = 4
+++

Ruta: `~/Scripts/Musica/discos-nuevos/`

Seguimiento de lanzamientos musicales próximos, apoyado en un calendario CalDAV
(Radicale) y en [Muspy](https://muspy.com).

| Script | Qué hace |
|---|---|
| `add_release_calendar.py` | Lee el RSS de lanzamientos de Muspy y añade los discos nuevos como eventos al calendario CalDAV. |
| `discos_escuchados_calendario.py` | Cruza los scrobbles recientes de Last.fm contra el calendario de Radicale para marcar automáticamente como "escuchados" los discos ya sonados; admite `--since N` para revisar los últimos N días (pensado para cron diario). |
| `deduplicate.py` / `delete_caldav_duplicates.py` | Dos utilidades de limpieza para eliminar eventos `VTODO`/duplicados del mismo calendario CalDAV. |

## telegram_bot/ — bot de Muspy

`muspy_bot.py` (con README propio) es un bot de Telegram independiente sobre la API de
Muspy, instalado como servicio (`muspy_bot.service`):

| Comando | Función |
|---|---|
| `/buscar artista` | Busca nuevos lanzamientos del artista. |
| `/guardar artista` | Añade el artista a Muspy. |
| `/mostrar` | Muestra los próximos lanzamientos de los artistas seguidos. |
| `/artistas` | Lista los artistas ya añadidos. |

{{% notice tip %}}
`deduplicate.py` tenía la URL, usuario y contraseña del servidor Radicale escritos
directamente en el código; ya se movieron a `.encrypted.env` (SOPS + age, vía
[`sops_env.py`]({{% relref "scripts/tools" %}})), igual que el resto de scripts de esta
carpeta.
{{% /notice %}}
