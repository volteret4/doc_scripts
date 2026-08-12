+++
title = 'Second Brain'
weight = 3
+++

Repositorio de **planificación** (no solo código) para migrar el segundo cerebro del
usuario desde Obsidian hacia herramientas más ligeras. En palabras del propio `DOC.md`:
*"Tengo un directorio con cientos de notas semi-organizadas por carpetas y tags muy
mejorables [...] No quiero aplicaciones Electron ni nada pesado. Adoro las TUI, uso
zellij y zsh a diario [...] Manejo helix usualmente"*. La fuente de verdad sigue siendo
el vault de Obsidian montado en `/mnt/windows/FTP/wiki/Obsidian/` — las notas son
Markdown plano para poder seguir procesándolas con scripts.

`DOC.md`, `GUIA.md`, `INSTALL.md` y `PLAN.md` documentan el diseño; `configs/` y
`scripts/` la implementación.

## Arquitectura del pipeline (cron)

```
Obsidian vault (/mnt/windows/FTP/wiki/Obsidian/)
    │
    ├── db_md_crear.py     → SQLite con FTS5 (búsqueda de notas)
    ├── scripts_to_md.py   → ~/Scripts/ → Obsidian/Spaces/Scripts/ (scripts como snippets MD)
    ├── mfuz_to_md.py      → music-fuzzy/ → Obsidian/Spaces/Blogs/ (igual, para ese proyecto)
    └── sync_vdir.sh       → vdirsyncer → Obsidian/calendars/ (tareas y calendarios CalDAV)
```

## Capa de búsqueda

| Script | Uso |
|---|---|
| `db_md_fuzzy_menu.py` | GUI PyQt6 (tema Catppuccin Mocha) para buscar notas en la base. |
| `db_md_async_search.py` | Worker de búsqueda FTS asíncrono para esa GUI. |
| `db_md_consultas.py` | CLI de consultas con filtros de fecha y tags. |
| `crear_obs_md.sh` | Crea notas nuevas desde el portapapeles del navegador activo. |

{{% notice note %}}
Estos son los mismos scripts (mismo nombre, mismo propósito) que viven además en
[`utilities/tiddlywiki`]({{% relref "scripts/utilities/tiddlywiki" %}}) y
[`utilities/cron`]({{% relref "scripts/utilities/cron" %}}) dentro de `~/Scripts` — este
repo es su documento de diseño y contexto, la carpeta de `~/Scripts` donde realmente se
ejecutan a diario.
{{% /notice %}}
