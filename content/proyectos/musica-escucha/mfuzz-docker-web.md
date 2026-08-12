+++
title = 'Mfuzz Docker Web'
weight = 16
+++

**Music Web Explorer**, versión "unificada": explorador web de la colección musical
(Flask + Nginx + Supervisor en un único contenedor Docker), la app solo lee la base de
datos SQLite (nunca los archivos directamente) y las descargas se disparan como comandos
`rsync` independientes contra el servidor `pepecono` (usuario `dietpi`).

```
mfuzz_docker_web/
├── (Flask app + music_manager.py + config.ini)
├── docker/{nginx.conf, supervisord.conf, entrypoint.sh}
├── Dockerfile / docker-compose.yml
└── templates/index.html
```

{{% notice note %}}
Es el mismo proyecto (mismo README, misma arquitectura) que
[`utilities/server/docker_web`]({{% relref "scripts/utilities/server" %}}) en
`~/Scripts` — este repo de `gits/pollo` es, con toda probabilidad, la fuente de verdad
versionada, y la copia en `Scripts/` un checkout de trabajo.
{{% /notice %}}
