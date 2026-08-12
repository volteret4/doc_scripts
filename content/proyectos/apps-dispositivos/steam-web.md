+++
title = 'Steam Web'
weight = 8
+++

*("steam_categories")*: web local (Flask) para explorar la biblioteca de Steam de un
grupo familiar (~500 juegos), con vistas por tags de comunidad, categorías de Steam,
puntuación (Metacritic/% de reseñas) y **categorías propias** creadas desde la propia
app — Steam no expone por API las carpetas/colecciones personales del cliente, así que
esas viven solo en la base de datos local.

```bash
python3 -m venv .venv && .venv/bin/pip install -r requirements.txt
cp config.example.json config.json   # steam_api_key desde steamcommunity.com/dev/apikey
```

- **`sync.py`** — descarga los datos de Steam (una vez, o periódicamente) a
  `steam_library.db` (SQLite).
- **`app.py`** — servidor Flask que sirve la web leyendo la base local (no llama a Steam
  en caliente, así que va instantánea).
- **`epic.py`/`gog.py`/`roms.py`/`external_metadata.py`** — soporte para librerías más
  allá de Steam (Epic, GOG, ROMs) y metadatos externos adicionales.
