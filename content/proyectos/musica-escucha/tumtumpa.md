+++
title = 'Tumtumpa'
weight = 22
+++

**Orquestador docker-compose** que agrupa como **submodules git** buena parte de los
proyectos musicales del usuario, para poder levantarlos todos (o algunos) en local con
Docker sin dejar de ser cada uno su propio repo independiente (con su systemd/`main.sh`
habituales fuera de este orquestador):

| Submodule | Proyecto | Perfil compose |
|---|---|---|
| `services/dieta_sonora` | [Dieta Sonora](../../personal/dieta-sonora) (dashboard principal) | `dieta_sonora` |
| `services/dieta_sonora` | Dieta Sonora (dashboard de estadísticas) | `dieta_sonora_stats` |
| `services/bandcamp_imap` | [Bandcamp IMAP](../../bots/bandcamp-imap) | `bandcamp` |
| `services/freshrss_embeeds` | [FreshRSS Embeeds](../../bots/freshrss-embeeds) | `freshrss` |
| `services/charts_orpheus` | [Charts Orpheus](../charts-orpheus) | `charts_orpheus` |
| `services/bot_conciertos` | [Bot Conciertos](../../bots/bot-conciertos) | `bot_conciertos` / `bot_conciertos_web` |
| `services/escuchowsky` | [Escuchowsky](../escuchowsky) (3 apps) | `escuchowsky` |
| `services/ensayos_musicales` | [Ensayos Musicales](../../personal/ensayos-musicales) — editor de correcciones | `ensayos_editor` |
| `services/ensayos_musicales` | Ensayos Musicales — mapa D3 estático | `ensayos_map` |
| `services/trasvase` | [Trasvase]({{% relref "proyectos/sistema/trasvase" %}}) (sync moode↔lidarr) | `trasvase` |
| `services/mixxx_info` | [Mixxx Info](../mixxx-info) | `mixxx_info` |
| `services/mix_rater` | [Mix Rater](../mix-rater) | `mix_rater` |

```bash
scripts/up.sh --profile index --profile bandcamp --profile escuchowsky up -d --build
# abre http://localhost:8760
```

## Índice general (`index/`)

`tumtumpa-index` (perfil `index`, puerto 8760) es un panel único que comprueba, por la
red interna `tumtumpa_net`, qué submodules elegidos están arriba ahora mismo y enlaza a
cada uno por su puerto externo (los apagados aparecen atenuados, sin enlace). Se
actualiza solo cada 5s. A diferencia de Ofelia, no usa el socket de Docker — solo intenta
una conexión TCP directa al `host:puerto` interno de cada servicio, así que no necesita
permisos extra.

## Notas de integración

- **Escuchowsky**: en producción corre en un servidor AWS endurecido con
  nginx+ModSecurity+CrowdSec (ver [Escuchowsky](../escuchowsky)); aquí solo se reutilizan
  sus 3 `Dockerfile` de app, sin el WAF, para poder correrlas también en local.
- **Dieta Sonora** tiene dos webs: el dashboard principal y el de estadísticas
  release→compra→escucha, que necesita `data.json`/`stats.json` generados a mano con
  `extraer_estadisticas.py`/`cal_to_estadisticas.py` (no se genera solo al levantar el
  contenedor).
- **Ensayos Musicales**: el editor necesita `services/ensayos_musicales/db/music_facts.db`
  real para funcionar del todo (sin ella, `/api/data` responde 500 con mensaje claro); el
  repo ya tiene el motor completo de transcripción (Whisper) + resumen (Gemini), pendiente
  construir la interfaz de podcasts sobre eso.
- **Mixxx Info**: su código nunca se había subido a git en el repo original — se
  comprometió como parte de esta integración, junto con un frontend React/Vite (`web/`)
  que la API no servía (se añadió `mixxx-info-web`, nginx con build multi-stage).
- **Mix Rater**: no era un repo git — se inicializó como parte de esta integración.
