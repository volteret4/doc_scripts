+++
title = 'Sueltos'
weight = 13
+++

Ruta: `~/Scripts/utilities/` (raíz) y `~/Scripts/utilities/alarms/`

| Script | Qué hace |
|---|---|
| `menu_pollo.py` / `menu_pollo2.py` | Dos menús flotantes Tkinter con tema oscuro propio (colores distintos entre versiones); `menu_pollo2.py` añade iconos con Pillow. |
| `debug_scripts.sh` | Recoge nombre/ruta del script que falló, hostname, IP local y la última línea del syslog, y lo manda a un servidor [ntfy](https://ntfy.sh) — pensado para invocarse desde el `trap ERR` de otros scripts (varios lo referencian en comentarios, como `conciertos.sh`). |
| `alarms/safe_shutdown.sh` | Script **vendorizado** de terceros (Serg Kolo, 2016, licencia permisiva) que impide apagar el sistema si hay aplicaciones abiertas sin avisar antes. Escrito para Ubuntu/Unity (`qdbus`, `bamf`) — probablemente no funcional tal cual en el AwesomeWM/Arch actual del usuario. |
