+++
title = 'MB Series'
weight = 15
+++

Dos herramientas de un solo propósito para crear **series en MusicBrainz** a partir de
listas curadas propias:

- **`musictree_to_mb.py`** — scrapea los ~1100 álbumes canónicos de
  [musicgenretree.org](https://www.musicgenretree.org/text_classics.html), los busca en
  MusicBrainz y crea/rellena la serie "Music Genre Tree – Classics" (misma herramienta
  que aparece en [`Musica/playlists/musicbrainz`]({{% relref "scripts/musica/playlists" %}})
  de `~/Scripts`). Autenticación por cookie de sesión del navegador
  (`musicbrainz_server_session`), con `--dry-run` para simular sin escribir.
- **`db_to_mb_series.py`** — crea series de MusicBrainz directamente desde las
  colecciones curadas de `must_hear_rym_new.db`: por década según el ranking de
  Scaruffi (`--scaruffi-decades`), por puntuación de Scaruffi (`--scaruffi-scores`), o
  por año según AOTY (`--aoty-years`), entre otros modos combinables en una misma
  ejecución.
