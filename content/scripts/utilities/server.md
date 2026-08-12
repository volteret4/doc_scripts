+++
title = 'Server'
weight = 9
+++

Ruta: `~/Scripts/utilities/server/`

Generadores de páginas web index/dashboard, más un servidor HTTP mínimo suelto.

## "crear index musica web" / docker_web — explorador web de la colección musical

Dos generaciones de la misma app **Music Web Explorer** (Flask + SQLite):
`docker_web/` es la versión más reciente y "unificada" (con `README.md` propio):
Flask sirve la API/lógica, Nginx hace de proxy inverso, todo en un único contenedor
Docker (`Dockerfile` + `docker-compose.yml` + `docker/entrypoint.sh` +
`docker/supervisord.conf`), la app **solo lee la base de datos** (no accede a los
archivos directamente) y las descargas se hacen por `rsync` independiente contra el
servidor `pepecono`. `crear index musica web/` es la versión previa, sin Docker
(`install.sh`/`quick_start.sh`/`setup.remote.sh` para desplegarla a mano).

## "crear index app web" — dashboard de apps corriendo

`dashboard_generator.py` detecta qué apps/servicios están corriendo en la red (puertos,
`requests` a sus endpoints) y genera una página web de estado con `dashboard_utils.py`/
`dashboard_extensions.py`, servida detrás de Nginx (`nginx.conf`, `docker-compose.yml`).

## server.py

Suelto en la raíz de `server/`: servidor HTTP temporal de un solo archivo
(`http.server` en el puerto 678) para compartir rápidamente la carpeta actual.
