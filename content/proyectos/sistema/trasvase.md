+++
title = 'Trasvase'
weight = 2
+++

*("trasvase_moode_lidarr")*: herramienta de sincronización de colección musical con dos
vistas web (Flask):

- **`/`** — Trasvase: álbumes de la "Colección 2" (torrents/Lidarr) ausentes de la
  "Colección 1" (Moode, el reproductor principal), con opción de copiarlos.
- **`/temp`** — Gestor de temporales: álbumes dentro de `coleccion1/temp/`, resalta
  duplicados y se integra con Airsonic.

```bash
export COLLECTION_1_PATH=/mnt/NFS/moode/moode
export COLLECTION_2_PATH=/mnt/NFS/lidar/torrents_backup
export TEMP_PATH=/mnt/NFS/moode/moode/temp/auto-dietpi   # default

python scan.py                 # escanea y sincroniza ambas colecciones a music.db
python scan.py --musicbrainz   # + enriquecido MusicBrainz (lento, 1 req/s)
python app.py                  # Flask en 0.0.0.0:5000
```

Las rutas reales de producción llegan cifradas vía `.encrypted.env` +
[`sops_env.py`]({{% relref "scripts/tools" %}}). Mismo patrón general que
[Éxodo Musical]({{% relref "proyectos/musica-escucha/exodo-musical" %}}) (comparar dos
colecciones y copiar lo que falta), pero integrando además Airsonic para la gestión de
temporales. Integrado como submodule del orquestador
[Tumtumpa]({{% relref "proyectos/musica-escucha/tumtumpa" %}}).
