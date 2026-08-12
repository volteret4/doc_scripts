+++
title = 'Base de Datos Artistas'
weight = 5
+++

Generador de un sitio web estático de solo lectura a partir de una base SQLite de
biblioteca musical (`musica_local.sqlite`): una página HTML por artista
(`artista_<id>_<slug>.html`), con `generate_html.py` como generador clásico y
`generate_html_jsons.py` como variante que además exporta JSON para un índice
(`index_json.html`) que no necesita cargar la base de datos en el navegador.

```bash
python3 generate_html.py ruta/a/musica_local.sqlite [carpeta_salida]
python3 generate_html_jsons.py ruta/musica_local.sqlite [carpeta_salida] --export-json
```
