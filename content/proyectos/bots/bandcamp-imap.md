+++
title = 'Bandcamp IMAP'
weight = 1
+++

Lee los correos de "new release" de Bandcamp por IMAP y publica una web estática con
los embeds de cada álbum organizados por género, servida con SSL vía
[SWAG](https://docs.linuxserver.io/general/swag) (proxy Nginx + Let's Encrypt en Docker).

```
IMAP (correos de Bandcamp)
        ↓
bc_export_to_json.py   →  bc_data.json   (caché en .bandcamp_cache.json)
        ↓
bc_static_generator.py →  docs/*.html
        ↓
server.py (Flask, puerto 8765)
        ↓
SWAG / Nginx  (SSL, subdominio público)
```

La web incluye un botón flotante "Actualizar colección" que dispara el pipeline
completo sin usar el terminal; un timer systemd (`bandcamp-update.timer`) lo repite
automáticamente cada lunes.

Es la versión "para producción/servidor" del mismo problema que
[`Musica/blog/bandcamp`]({{% relref "scripts/musica/blog" %}}) resuelve en local en
`~/Scripts` (que además tiene una variante por Thunderbird); comparte el patrón con
[FreshRSS Embeeds](../freshrss-embeeds), también servido por SWAG. Integrado como
submodule del orquestador [Tumtumpa]({{% relref "proyectos/musica-escucha/tumtumpa" %}}).
