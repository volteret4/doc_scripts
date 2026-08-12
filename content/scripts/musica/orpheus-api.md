+++
title = 'Orpheus API'
weight = 8
+++

Ruta: `~/Scripts/Musica/orpheus-api/`

Compara la colección local/calendario de deseos contra el catálogo de
**Orpheus.network** (tracker privado de música) y contra qBittorrent, con un pequeño
dashboard Flask para revisar el resultado. Es, junto a `vvmm/`, uno de los sistemas más
completos de `Musica/`.

## Flujo principal

| Script | Qué hace |
|---|---|
| `revisor_calendario.py` | Exporta a CSV los eventos `$artist - $album` pendientes del calendario Radicale de discos. |
| `buscar_nuevos.py` | Busca en la API de Orpheus (`ORPHEUS_APIKEY`) qué de esos álbumes existe como FLAC en el tracker, y guarda el resultado en `resultado_flacs.json`/`albums.csv`. |
| `comparar_con_orpheus.py` | Variante de comparación contra el catálogo completo de Orpheus. |
| `airsonic_checker.py` | Filtra del CSV los álbumes que ya existen en Airsonic (modo `--mode clean` para eliminarlos directamente de la lista). |
| `comparar_qbitorrent.py` / `qbittorrent_checker.py` | Cruzan la lista contra lo que ya se está descargando/sembrando en qBittorrent (cacheando resultados en `.cache/`). |
| `html_generator.py` / `app.py` | Generan `resumen_flacs.html` y sirven un pequeño dashboard Flask (`app.py`) para revisar/filtrar el resultado desde el navegador, con embeds enriquecidos. |
| `main.sh` | Orquesta el ciclo básico: `revisor_calendario.py` → `airsonic_checker.py --mode clean`, registrando cuántas líneas cambiaron. |
| `discos_nuevos.service` | Unidad systemd para correr el flujo periódicamente. |

## estadisticas/ — dashboard de estadísticas de escucha

Subsistema aparte que cruza Radicale (calendario de compras/escuchas), Last.fm,
ListenBrainz y MusicBrainz en una base SQLite y exporta `data.json` para un dashboard:

| Script | Qué hace |
|---|---|
| `extraer_estadisticas.py` | Extrae de Radicale + CSV + MusicBrainz y vuelca todo a SQLite, exportando `data.json` para el dashboard. |
| `extraer_scrobbles.py` | Descarga y deduplica historial de Last.fm + ListenBrainz (`lastfm_stats.json`/`lastfm_detail.json`). |
| `cal_to_estadisticas.py` | Sincroniza usando los `VTODO` del calendario como fuente de verdad (fecha de compra/escucha). |
| `old_albums.py` | Sincroniza eventos de lanzamiento (`VEVENT`) con las tareas (`VTODO`) y rellena fechas de escucha desde la base de scrobbles. |
| `repair_stats_db.py` | Rellena huecos en la base (fecha de publicación/compra/escucha) consultando Radicale, MusicBrainz y Airsonic por orden de prioridad. |
| `eliminar_sin_tarea.py` | Elimina del CSV/JSON los discos que ya no tienen `VTODO` asociado en Radicale (huérfanos). |

{{% notice tip %}}
`comparar_qbitorrent.py` tenía la API key de Orpheus **y** la contraseña de qBittorrent
escritas directamente en el código. Ya se movieron a un `.encrypted.env` propio de esta
carpeta (SOPS + age, vía [`sops_env.py`]({{% relref "scripts/tools" %}})), igual que el
resto de credenciales del proyecto.
{{% /notice %}}
