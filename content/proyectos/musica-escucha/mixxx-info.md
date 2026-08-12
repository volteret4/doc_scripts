+++
title = 'Mixxx Info'
weight = 17
+++

Archivo/enciclopedia musical personal: escanea la biblioteca local en
`/mnt/windows/Mix` (organizada por carpetas/gustos), enriquece cada pista con metadata
profunda de APIs externas y de IA, y lo expone todo en un dashboard web — pensado como
un "Discogs personal" útil durante sesiones de DJ.

```bash
python main.py scan [--root /mnt/windows/Mix] [--output library.json]   # Fase A: escaneo
python main.py enrich [--input library.json] [--limit 50]               # Fase B: enriquecido por API
python main.py ai-enrich [--limit 50]                                    # Fase C: huecos rellenados con Gemini
python main.py query --artist "Daft Punk" --taste "Electronic"           # consulta rápida a la BD
```

Backend en Python (FastAPI), integrado como submodule del orquestador
[Tumtumpa](../tumtumpa) — comparte el patrón "API FastAPI + web React/Vite tras nginx,
cada una en su contenedor" con [Sellos Discográficos](../sellos-discograficos).
