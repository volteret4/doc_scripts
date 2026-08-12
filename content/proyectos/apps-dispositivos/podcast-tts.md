+++
title = 'Podcast TTS'
weight = 7
+++

{{% notice warning %}}
Este repo y [Wallabag to MP3]({{% relref "proyectos/bots/wallabag-to-mp3" %}}) comparten
el mismo README ("Sistema de Podcast TTS - Docker") y el mismo propósito — parecen dos
copias del mismo proyecto en dos ubicaciones de `~/gits/pollo`. Esta página documenta la
copia con `CLAUDE.md` propio (más detallada y con notas de migración a Docker); si una de
las dos carpetas ya no se usa, puede que valga la pena eliminarla para no mantener dos
copias divergentes.
{{% /notice %}}

Convierte artículos de FreshRSS/Wallabag a MP3 (TTS) y sirve un feed RSS de podcast
para AntennaPod. `server.py` es un backend Flask que **solo** atiende `/api/*` y
`/health`; los estáticos (`index.html`, `web/`), el feed (`podcast.xml`) y los audios
(`audio_articles/`) los sirve **nginx directamente** (SWAG), no Flask.
`process_selection.py` procesa la selección manual desde la web,
`articles_to_mp3.py` corre por cron diario, y `convert_url.py` convierte una URL suelta;
`server.py` los lanza como subprocesos y todos deben vivir en el mismo `WORK_DIR`.

## Migración a Docker

Según su `CLAUDE.md`, hasta agosto de 2026 esto corría **fuera de Docker** como
servicio systemd (`podcast-tts-web.service`) + una entrada de crontab, en
`~/contenedores/podcast-tts` en el host. Ya está migrado a Docker como submodule de un
orquestador **"repeat-one"** (`services/podcast_tts`), pero con una particularidad: el
código va en la imagen (`COPY . .`), pero los **datos reales se montan individualmente**
desde su ubicación física original (`~/contenedores/podcast-tts/config.json`,
`/audio_articles`...) en vez de copiarse — porque SWAG sirve esos mismos estáticos
directamente desde esa ruta del host mediante bind-mount.

{{% notice note %}}
`~/gits/pollo/repeat-one` (excluido de esta documentación, ver la introducción de
Proyectos) no contiene actualmente ese orquestador — solo artefactos sueltos de una
sesión interrumpida, sin `services/` ni `docker-compose.yml`. La migración que describe
este `CLAUDE.md` parece no haberse completado (o se perdió) todavía.
{{% /notice %}}
