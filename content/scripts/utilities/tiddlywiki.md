+++
title = 'TiddlyWiki'
weight = 10
+++

Ruta: `~/Scripts/utilities/tiddlywiki/`

A pesar del nombre, ya no gira en torno a TiddlyWiki sino a indexar y buscar el vault de
**Obsidian** en una base SQLite propia (`wiki_obsidian.db`).

| Script | Qué hace |
|---|---|
| `db_md_crear.py` | Script unificado (creación + actualización + optimización) que sincroniza el vault de Obsidian con la base SQLite; pensado para cron. |
| `db_md_optimize_db.py` | Optimización/mantenimiento de esa base por separado. |
| `db_md_consultas.py` | CLI de consultas sobre la base, con parseo flexible de fechas (ISO, "enero 2024"...) y salida en tabla (`tabulate`). |
| `db_md_async_search.py` | Búsqueda asíncrona sobre la base. |
| `db_md_fuzzy_menu.py` | GUI PyQt6 de búsqueda fuzzy sobre las notas indexadas. |
| `crear_obs_md.sh` | Crea un nuevo archivo Markdown en la carpeta sincronizada de Obsidian, comprobando primero qué navegador/ventana está activa. |
| `crear_tiddler.sh` | Homólogo del anterior con detección de ventana activa (Firefox/Chromium/Thorium), resto del nombre heredado de cuando esto sí usaba TiddlyWiki. |
| `add_scripts_metadata_obsidian.py` | Añade metadata (fecha, localizada en español) a notas de scripts dentro del vault. |
| `formato_cmd.sh` / `formato_cmd.py` | Detectan/formatean bloques de comandos (`sudo apt update`...) dentro de una nota, para resaltarlos como código. |
