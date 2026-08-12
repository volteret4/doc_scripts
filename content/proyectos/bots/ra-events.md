+++
title = 'RA Events'
weight = 6
+++

Cruza eventos scrapeados de **Resident Advisor** con los artistas seguidos en Muspy,
para saber cuándo tocan en las ciudades que interesan. Tres scripts independientes
conectados solo por archivos (SQLite + JSON), sin imports compartidos entre ellos:

```
urls.txt  ──►  scraper.py  ──►  events.db
                                    │
muspy.com ──►  get_artists.py ──►  artists.json
                    │
              MusicBrainz (valida actividad)
                                    │
events.db + artists.json  ──►  match_events.py  ──►  followed_events.json
```

```bash
python get_artists.py --user <usuario_muspy>                    # pide contraseña; genera artists.json
python get_artists.py --user <usuario> --include-inactive       # incluye artistas disueltos
python scraper.py                                                # ventana Chrome visible (recomendado)
python scraper.py --headless                                     # menos fiable contra Cloudflare
```

Requiere Chrome instalado; `undetected-chromedriver` descarga el driver compatible
automáticamente.
