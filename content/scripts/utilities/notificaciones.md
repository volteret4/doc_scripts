+++
title = 'Notificaciones'
weight = 6
+++

Ruta: `~/Scripts/utilities/notificaciones/`

Puentes entre distintas fuentes de eventos y los canales de notificación del usuario
(Telegram, ntfy, dunst).

| Script | Qué hace |
|---|---|
| `docker-monitor.sh` | Escucha eventos de Docker (`docker events`) y los reenvía a un bot de Telegram. |
| `github_notif.sh` | Consulta las notificaciones de GitHub (`gh api /notifications`) y las muestra como notificación de escritorio; exporta `DISPLAY`/`DBUS_SESSION_BUS_ADDRESS` a mano para poder lanzarse desde cron. |
| `kopia_exitosa.sh` / `kopia_fallida.sh` | Avisan por [ntfy](https://ntfy.sh) del resultado de un backup de Kopia (éxito/fallo), como hooks del propio Kopia. |
| `nc_to_dunst.sh` | Escucha en un puerto TCP con `nc` y reenvía cualquier mensaje recibido como notificación `dunst` — un "webhook" de notificaciones minimalista para la LAN. |
| `termometro.sh` | Consulta un sensor de temperatura expuesto por Home Assistant y lo imprime/notifica. |
| `telegram/telegram_notify.sh` | Envío genérico a Telegram, descifrando el token con `sops` desde `.encrypted.env` en vez de un `.env` en claro. |

## debug/ — sistema de notificaciones con botones

`debug.py` es un módulo (pensado para importarse: `from debug import notify_info, ...`)
que muestra notificaciones `dunst` con **botones de acción configurables**;
`controlar_opciones_debug.sh` es el manejador que se ejecuta cuando el usuario pulsa uno
de esos botones (recupera de `/tmp` qué acción y qué script originaron la notificación).
