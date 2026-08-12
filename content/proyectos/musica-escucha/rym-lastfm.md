+++
title = 'RYM Last.fm'
weight = 20
+++

Otra copia/rama del mismo **Last.fm Statistics Generator** que
[Back RYM Last.fm](../back-rym-lastfm) — genera estadísticas de coincidencias musicales
entre varios usuarios de Last.fm (artistas, canciones, álbumes, géneros, sellos vía
Discogs) en HTML estático, publicado por GitHub Pages desde `docs/`.

```bash
bash main.sh                          # pipeline completo

python3 html_usuarios.py              # páginas por usuario
python3 html_grupo.py                 # análisis de música compartida
python3 html_temporal.py weekly
python3 html_temporal.py monthly 2025-03
python3 html_temporal.py yearly 2024
python3 html_index.py                 # regenerar el índice al final
```

Añade respecto a la otra copia: `html_musthear_estadisticas.py` /
`html_musthear_index.py` / `html_rym_genre_mermaid.py` (diagramas Mermaid de géneros) y
un subsistema `claude/` para el seguimiento de "must hear". Configuración vía `.env`
(`LASTFM_API_KEY`, `LASTFM_USERS`, `DISCOGS_TOKEN`).
