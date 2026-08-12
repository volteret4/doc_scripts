+++
title = 'Servicios'
weight = 2
+++

Ruta: `~/Scripts/boot/` y `~/Scripts/boot/services/`

## Aprovisionamiento

| Script | Qué hace |
|---|---|
| `docker.sh` | Instala Docker en un sistema basado en Debian: actualiza repos, descarga e instala Docker vía el script oficial (`get-docker.sh`), pide con un diálogo `zenity` a qué usuario añadir al grupo `docker`, activa los servicios `docker`/`containerd`, e instala `docker-compose` con pip. Nota propia en el script: pendiente de adaptar para Arch. |
| `instalar_apps.sh` | Una línea: instala con `pacman` el set base de apps de escritorio (picard, firefox, chromium, keepassxc, vscodium, flac, deadbeef, copyq, xdotool). |

## KeePass

| Script | Qué hace |
|---|---|
| `keepass_merge.sh` | Hace copia `.BAK` de dos bases KeePass (personal y de trabajo) y las fusiona con `keepassxc-cli merge`, pidiendo la contraseña por diálogo `zenity`. |
| `restart_agent_4_keepass.sh` | Reinicia el servicio de usuario `ssh-agent` (fijando `SSH_AUTH_SOCK`) antes de lanzar KeePassXC — soluciona que el agente SSH quede en mal estado. |

## Varios

| Script | Qué hace |
|---|---|
| `fiio_sd.sh` | Monta por UUID la tarjeta SD de un reproductor FiiO, deja preparado (comentado) un `rsync` de una carpeta de mezclas, desmonta y avisa con un diálogo `yad` de que ha terminado. |

## Notificaciones de arranque/apagado (systemd)

Dos unidades systemd a nivel de sistema que avisan al móvil (vía la API de Join, igual
que los scripts de `Apps/android/`) de cuándo se enciende o apaga la máquina:

| Archivo | Qué hace |
|---|---|
| `services/inicio.service` | Unidad `multi-user.target` que, tras `network.target`, ejecuta `at_boot.sh`. |
| `services/at_boot.sh` | Registra la hora en `~/uptime` y envía una notificación "Arcolinux_On" al móvil por Join. |
| `services/shutdown.service` | `RemainAfterExit`, ligada a `shutdown.target`; ejecuta `boot/shutdown.sh` al apagar. |
| `services/shutdown.sh` | Igual que `at_boot.sh` pero envía "Arcolinux_Off". |

Ambos scripts leen `APIKEY`/`POCOX3` de un `.env` en `services/`.
