+++
title = 'Charts Orpheus'
weight = 6
+++

Generador y visor de **collages/charts** (al estilo RYM) a partir de datos del tracker
privado **Orpheus.network**, con soporte Docker.

| Archivo | Qué hace |
|---|---|
| `yt-chart.py` | Consulta la API de Orpheus (`ORPHEUS_API_KEY`) y Discogs, guarda resultados en `charts_orpheus.db`, y busca los vídeos correspondientes en YouTube para armar el chart. |
| `dupe.py` | Limpia agresivamente títulos de YouTube (quita etiquetas, paréntesis, ruido) para poder deduplicar entradas del mismo tema. |
| `chart_server.py` | Servidor HTTP propio (sin framework) que sirve el visor de charts en `http://localhost:8745`. |
| `settings-panel.js`, `theme-picker.js`, `theme-palettes.css` | Frontend del visor: panel de ajustes y temas de color intercambiables. |

Usa [`sopsdotenv`]({{% relref "scripts/tools" %}}) para las credenciales, con fallback
silencioso si corre en Docker (las variables ya llegan descifradas vía
`docker-compose`/`scripts/up.sh`, sin `.encrypted.env` ni el binario `sops` en la
imagen). Es la contraparte de generación de contenido de
[Orpheus API]({{% relref "scripts/musica/orpheus-api" %}}), que se centra en comparar
la colección local contra el catálogo en vez de generar charts.
