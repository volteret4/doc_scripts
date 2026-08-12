+++
title = '1-locura'
weight = 6
+++

Prototipo temprano de la misma arquitectura de plugins por pestañas que luego se
convertiría en [Music Fuzzy]({{% relref "proyectos/musica-escucha/music-fuzzy" %}}):
`music_padre.py` importa `BaseModule`/`THEMES` desde `base_module.py` y monta una
`QTabWidget` (PyQt6) que carga módulos definidos en `config.json`, con
`designer_module.py` como módulo de ejemplo/plantilla y `modules/` para el resto.
`multi_module_manager.log` sugiere que este es el nombre interno con el que empezó el
proyecto antes de convertirse en "mfuz".
