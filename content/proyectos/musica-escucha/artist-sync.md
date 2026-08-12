+++
title = 'Artist Sync'
weight = 3
+++

Comparador web (Flask) interactivo de artistas entre **Muspy** (seguidos), **Airsonic**
(biblioteca local), **qBittorrent** (descargas, cruzando tags FLAC) y **Last.fm**
(escuchados) — para ver de un vistazo qué artistas están en cada sitio y decidir a
cuáles seguir/dejar de seguir en Muspy, que es la fuente que luego consumen los bots de
lanzamientos (ver [Discos nuevos]({{% relref "scripts/musica/discos-nuevos" %}}) y el
proyecto [Discos Nuevos](../discos-nuevos)).

Pensado para poder correr suelto o integrado dentro del proyecto **tumtumpa** (comparte
con él el volumen `lastfm_data` y el servicio `lastfm-scrobbles` que sincroniza a diario
Last.fm + ListenBrainz deduplicados). El propio README documenta con detalle las
diferencias de configuración de red según se ejecute suelto o dentro de ese
`docker-compose` (p. ej. `QB_HOST=host.docker.internal` vs `localhost`, y
`QB_REMOTE_PATH` para reescribir rutas si qBittorrent corre en su propio contenedor).

Usa [`sops_env.py`]({{% relref "scripts/tools" %}}) para las credenciales.
