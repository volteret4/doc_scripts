+++
title = 'Mix Rater'
weight = 18
+++

Herramienta personal de valoración de la colección: escanea archivos de audio a una
base SQLite y deja puntuar cada pista en **12 dimensiones subjetivas** (p. ej.
alegre/melancólica, relajada/energética), para luego sugerir recomendaciones por
similitud coseno entre los vectores resultantes.

Dos interfaces:

- **CLI** (`music_rater.py`) — escanea un directorio y permite valorar pista a pista por
  terminal, reproduciendo con `deadbeef`.
- **Web** (`web/app.py`) — Flask en el puerto 5001, con reproducción aleatoria, búsqueda
  por vector y estadísticas de la colección.

```bash
python music_rater.py scan /ruta/a/musica
python music_rater.py rate alegre_melancolica
python web/app.py --port 5002 --host 0.0.0.0
```

Integrado como submodule del orquestador [Tumtumpa](../tumtumpa).
