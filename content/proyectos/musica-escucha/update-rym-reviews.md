+++
title = 'Update RYM Reviews'
weight = 23
+++

`open_rym_reviews.py`: localiza y abre en el navegador las páginas de
**RateYourMusic** de álbumes pendientes de puntuar/reseñar, en dos fases:

```bash
# Fase 1 — recopilar URLs (se pueden combinar varias fuentes, sin duplicados)
python open_rym_reviews.py --discogs-coll --save rym_queue.json
python open_rym_reviews.py --lastfm-scrobbles-json file.json --save rym_queue.json
python open_rym_reviews.py --db --save rym_queue.json --chromedriver-all
```

Las fuentes posibles son la colección de Discogs, un JSON de scrobbles de Last.fm, o la
base de datos local (`musica_local.sqlite`) resolviendo URLs con Selenium/chromedriver.
El progreso se guarda en `rym_queue.json` para poder retomarlo entre ejecuciones.
