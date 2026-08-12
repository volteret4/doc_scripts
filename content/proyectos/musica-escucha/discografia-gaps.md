+++
title = 'Discografía Gaps'
weight = 8
+++

Para cada artista de tu "universo" (unión de seguidos en **Muspy**, biblioteca de
**Airsonic** y, opcionalmente, artistas por encima de un umbral de scrobbles en
**Last.fm**), calcula la discografía completa vía **MusicBrainz** (release-groups:
álbumes + EPs) y marca qué tienes frente a lo que falta. Para un disco que falta,
bajo demanda, comprueba disponibilidad en **Orpheus** (con descarga por qBittorrent
confirmada explícitamente), **YouTube** o **Bandcamp**.

- **`config.py`** — credenciales/rutas (override por env var), carga `.encrypted.env` vía `sops_env.py`.
- **`clients/`** — un módulo por API externa (Muspy, Airsonic, qBittorrent, Last.fm/espejo, MusicBrainz, Orpheus, YouTube, Bandcamp) más `flac_scan.py` (lee tags FLAC) y `normalize.py` (clave de cruce de nombres de artista).
- **`scan.py`** — orquesta 3 fases: `universe` → `discography` → `have`, y actualiza `discografia_gaps.db`.
- **`app.py`** — Flask: sirve la web + API REST + panel de ajustes (mismo patrón que [Artist Sync](../artist-sync) y [Trasvase]({{% relref "proyectos/sistema/trasvase" %}})).

## Esquema (`discografia_gaps.db`)

```sql
artists(id, name, norm_name UNIQUE, mbid, discography_synced_at)
artist_sources(id, artist_id FK, source IN (muspy|airsonic|lastfm))
release_groups(id, artist_id FK, mbid UNIQUE, title, norm_title,
                primary_type, first_release_date, have, have_sources)
availability(id, release_group_id FK, source IN (orpheus|youtube|bandcamp),
             url, meta, checked_at)
```

`scan.py` reemplaza por completo `artist_sources` por fuente en cada sincronización
(misma filosofía que `presence` en Artist Sync) y luego poda los artistas sin ninguna
fuente — el `ON DELETE CASCADE` se lleva por delante sus `release_groups`/`availability`.
Comparte variables de entorno y la lógica de resolución de `QB_HOST`/`QB_REMOTE_PATH`
con [Artist Sync](../artist-sync).
