+++
title = 'Escuchowsky'
weight = 11
+++

Conjunto de mini-apps Flask sobre scrobbles de Last.fm y las bases `must_hear`
compartidas con [Back RYM Last.fm](../back-rym-lastfm)/[Tumtumpa]({{% relref "proyectos/musica-escucha/tumtumpa" %}}),
desplegado en un **servidor externo en AWS** (no en la infraestructura local del
usuario), detrás de Nginx + ModSecurity.

## Apps

| App | Qué hace |
|---|---|
| `app_discover.py` ("mustdiscover") | Compara los scrobbles del usuario principal contra los de usuarios secundarios: descubre qué escucha otro que tú todavía no. |
| `app.py` ("mustlisten") | Cruza scrobbles de Last.fm con `must_hear.db` para mostrar qué discos de las listas curadas te faltan por escuchar. |
| `app_musthear.py` | Muestra las colecciones curadas (Scaruffi, AOTY, Pitchfork...) agrupadas por fuente, compatible con el mismo formato de sesión que `app_discover.py`. |
| `app_genres.py` / `app_genre_mermaid.py` | Visualizaciones de género (la segunda genera diagramas Mermaid). |

## Infraestructura y seguridad

El propio repo tiene un `CLAUDE.md` dedicado por completo a una "misión de seguridad",
con un objetivo explícito y único: **reducir la superficie de ataque del servidor**, sin
tocar funcionalidad ni rendimiento. Pila declarada:

- Dos apps Flask + Gunicorn en contenedores separados, Docker en modo *rootless*.
- Nginx como reverse proxy con **ModSecurity** (WAF) integrado.
- **CrowdSec** analizando logs de sistema y aplicación.
- Monitorización externa con Prometheus + Grafana (en otro servidor aparte).
- Solo 80/443 expuestos públicamente (redirigidos por `iptables` a Nginx); certificados
  renovados con `acme.sh`.

`crowdsec-metrics.sh` expone métricas de CrowdSec; hay un `Dockerfile` por app
(`Dockerfile.escuchowsky`, `Dockerfile.musthear`, `Dockerfile.tumtumpa`) más
`entrypoint_escuchowsky.sh`/`entrypoint_nginx.sh`.
