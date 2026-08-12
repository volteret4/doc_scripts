+++
title = 'Éxodo Musical'
weight = 12
+++

Herramienta de sincronización entre dos colecciones de música en un servidor: la web
muestra qué álbumes de la "Colección 2" (origen) **no** están en la "Colección 1"
(destino/principal), permite seleccionarlos y copiarlos, y borrar álbumes de cualquiera
de las dos.

```bash
export COLLECTION_1_PATH=/mnt/music/coleccion1
export COLLECTION_2_PATH=/mnt/music/coleccion2

python scan.py                 # escanea ambas carpetas y sincroniza music.db
python scan.py --musicbrainz   # además enriquece vía MusicBrainz (lento, 1 req/s)
python app.py                  # servidor Flask, 0.0.0.0:5000 por defecto
```

`scan.py` hace altas incrementales (añade nuevo, elimina lo que ya no está) sin
recrear la base cada vez. Frontend de una sola página (`templates/index.html`, vanilla
JS, tema negro/verde eléctrico) servido por `app.py`.

```sql
artists(id, name UNIQUE COLLATE NOCASE, mbid)
albums(id, artist_id FK, title, label, genre, year, path UNIQUE, collection 1|2, mbid)
```
