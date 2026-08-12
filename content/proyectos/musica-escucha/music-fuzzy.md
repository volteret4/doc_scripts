+++
title = 'Music Fuzzy'
weight = 19
+++

**El proyecto musical más grande del monorepo**: "mfuz", una aplicación de gestión
musical PyQt6 con **arquitectura de plugins por pestañas**. Ya tiene su propio sitio de
documentación detallado ([music-fuzzy-doc](https://volteret4.github.io/music-fuzzy-doc/),
con tema hugo-theme-relearn, el mismo que este sitio), así que aquí solo un resumen para
ubicarlo entre el resto de proyectos.

```bash
python3 main.py config/config.json   # o: ./boot.sh
```

- **`main.py`** — `TabManager` (QMainWindow) que carga módulos dinámicamente según
  `config/config.json`.
- **`base_module.py`** — clase base que deben heredar todos los módulos.
- **`themes/themes.py`** — sistema de temas centralizado.
- **`db_creator.py`** — orquesta la población de la base de datos ejecutando scripts
  según config.
- Módulos activos: `music_fuzzy_module`, `jaangle_module` (juego de adivinar música),
  `muspy_releases_module`, `conciertos_module`, `estadisticas_module`, `url_playlist`.
  Los desactivados viven en `modulos_desactivados` dentro del config — mover una entrada
  entre ambos arrays activa/desactiva el módulo.
- **Base de datos**: `db/sqlite/musica_local.sqlite` (SQLite, WAL, ~1GB), tablas núcleo
  `artists`/`albums`/`tracks`. `db/tools/` tiene scripts sueltos de población desde
  Last.fm, MusicBrainz, Spotify, Discogs, charts...

Es la base de datos que leen en modo solo-lectura tanto
[Sellos Discográficos](../sellos-discograficos) como los paneles de
[Mixxx Info](../mixxx-info).
