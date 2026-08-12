+++
title = 'Dieta Sonora'
weight = 2
+++

Sistema personal de gestión musical con dos componentes, usando Radicale (CalDAV) como
fuente de verdad:

1. **CSV Lanzamientos** — dashboard Flask con los discos pendientes de comprar.
2. **Web Estadísticas** — mide el tiempo entre lanzamiento → compra → escucha.

```
Radicale CalDAV
├─ VEVENT (eventos de calendario) → fechas de lanzamiento de álbumes
└─ VTODO (tareas)                 → fecha de compra (DTSTART) + fecha de escucha (COMPLETED)
         ↓
revisor_calendario.py → albums.csv (compras pendientes)
         ↓
airsonic_checker.py / qbittorrent_checker.py → limpia albums.csv
         ↓
estadisticas/albums_log/cal_to_estadisticas.py → SQLite + JSON para la web de stats
         ↓
html_generator.py → resumen_flacs.html (dashboard con embeds YouTube/Bandcamp)
         ↓
app.py (Flask) → sirve el dashboard, gestiona descargas de torrents, dispara escaneos de Airsonic
```

`main.sh` orquesta el ciclo diario: `revisor_calendario.py` → limpieza Airsonic →
regenerar HTML. Comparte la mecánica de "calendario como fuente de verdad" con
[Orpheus API]({{% relref "scripts/musica/orpheus-api" %}}) en `~/Scripts` (de hecho
importa directamente `airsonic_clean_csv.py`, `buscar_nuevos.py` y
`comparar_con_orpheus.py`, muy similares a los de ese otro proyecto). Integrado como
submodule del orquestador
[Tumtumpa]({{% relref "proyectos/musica-escucha/tumtumpa" %}}) (con dos perfiles:
`dieta_sonora` y `dieta_sonora_stats`).
