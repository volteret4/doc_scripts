+++
title = 'Sellos Discográficos'
weight = 21
+++

Navegador web de la colección de [Music Fuzzy](../music-fuzzy), organizada por
**Sellos → Artistas → Discos**, **Productores → Artistas → Discos** y
**Masters → Artistas → Discos**. Al pulsar cualquier elemento se abre un panel lateral
con imagen e información (biografía, país, enlaces a Discogs/MusicBrainz/Last.fm/
Wikipedia, créditos). Pulsar un disco que no encaja con el filtro activo salta
automáticamente a su propio sello/productor/master, conservando el artista seleccionado.

## Arquitectura

- **`api/`** — FastAPI, `sqlite3` de la librería estándar en modo **solo lectura**, sin
  ORM. `text_groups.py` construye en memoria (caché TTL 5 min) el índice de cada
  agrupación a partir de campos de texto libre de `albums` (`label`, `producers`,
  `mastering_engineers`) — no hay tablas normalizadas `producers`/`masters`, y aunque
  existe una tabla `labels`, **no se usa para agrupar** (esa tabla enlaza cada álbum con
  *todos* los sellos que MusicBrainz asocia al release-group, reediciones incluidas, no
  con el sello real de la copia del usuario; se usa solo como enriquecimiento opcional
  cuando el nombre coincide). `images.py` resuelve imágenes: BD local → caché en disco →
  Discogs/Cover Art Archive/Last.fm.
- **`web/`** — React 18 + Vite + Tailwind + `@tanstack/react-query`, servida por nginx en
  producción (proxy de `/api/` al contenedor de la API). Tres columnas (grupo → artistas
  → discos) más un `DetailPanel`.

Lee **directamente** `musica_local.sqlite` de Music Fuzzy. Sin normalización de
variantes de nombre todavía (primera versión).

{{% notice warning %}}
La copia más actualizada de `musica_local.sqlite` vive en el portátil del usuario, no en
el servidor: para que el contenedor en producción tenga datos frescos hay que copiarla a
mano antes de levantar el servicio — no hay sincronización automática.
{{% /notice %}}

Mismo patrón (FastAPI + React/Vite tras nginx) que [Mixxx Info](../mixxx-info), ambos
integrados en el orquestador [Tumtumpa](../tumtumpa).
