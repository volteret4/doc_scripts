+++
title = 'Bot Infomusic'
weight = 3
+++

Bot de Telegram (Docker) que expone la base de datos musical
(`schema_musica_local.sql`) a consultas de usuario — un frontend conversacional para la
misma base de datos que usa [Music Fuzzy]({{% relref "proyectos/musica-escucha/music-fuzzy" %}}).

Stack: `python-telegram-bot` 22.6 (async) + SQLAlchemy 2.0 como capa de consultas sobre
el entorno virtual compartido (`~/Scripts/python_venv`). Credenciales en
`.encrypted.env` (SOPS + age), cargadas al arrancar con
[`sopsdotenv`]({{% relref "scripts/tools" %}}):

```python
from sopsdotenv import load_sops_env
load_sops_env()  # sube directorios desde el cwd hasta encontrar .encrypted.env
```
