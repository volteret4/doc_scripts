+++
title = 'Back RYM Last.fm'
weight = 4
+++

El backend real detrás de las estadísticas de Last.fm del grupo (con `CLAUDE.md`
propio muy detallado): descarga scrobbles de varios usuarios de Last.fm, los enriquece
con MusicBrainz/Discogs y genera páginas HTML estáticas servidas por GitHub Pages desde
`docs/`. Es el mismo sistema que documenta
[`Musica/blog/rym_lastfm`]({{% relref "scripts/musica/blog" %}}) en `~/Scripts`.

## Arquitectura en 3 capas (estricta)

1. **Base de datos** (`db/`, `tools/*/*_database.py`) — solo consultas SQLite.
2. **Analizador** (`tools/*/*_analyzer.py`) — lógica de negocio, sin tocar DB ni HTML.
3. **Generador** (`tools/*/*_html_generator.py`, `html_*.py`) — solo salida HTML.

**Flujo de datos**: API de Last.fm → `db/lastfm_cache.db` (caché en bruto, ~1.4GB) →
`db/lastfm_normalized.db` (normalizada, filtrada por MBID) → analizadores → HTML en
`docs/`.

## Puntos de entrada principales

```bash
python3 html_usuarios.py      # páginas de estadísticas por usuario
python3 html_grupo.py         # análisis de música compartida del grupo
python3 html_temporal.py      # estadísticas semanales/mensuales/anuales
python3 html_index.py         # página de índice

python3 db/update_database.py # trae datos frescos de la API de Last.fm
python3 db/status.py          # enriquece metadata desde MusicBrainz/Discogs

python3 claude/html_must_hear.py  # subsistema "must hear": cruza listas/series
                                   # de MusicBrainz con los scrobbles de cada
                                   # usuario y genera un grid en docs/must_hear/
```

Usa MBIDs para deduplicar (flags `--mbid-only` para filtrar solo registros de alta
confianza). Configuración vía `.env` (`LASTFM_API_KEY`, `LASTFM_USERS`, `DISCOGS_TOKEN`).
