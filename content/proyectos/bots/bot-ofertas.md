+++
title = 'Bot Ofertas (Odesli Termux)'
weight = 4
+++

*(nombre real del README: "Odesli Termux")*. Obtiene enlaces universales de
[Odesli](https://odesli.co) y YouTube Music **desde el propio móvil**, usando Termux +
Tasker en vez de un servidor: se conecta a Airsonic a través de la Tailnet (Tailscale)
para saber qué está sonando, o acepta artista/álbum manuales.

```
odesli_termux.py                     # script principal (corre en Termux)
termux/
  setup.sh                           # instalación automática
  odesli_airsonic.sh                 # wrapper: now playing
  odesli_search.sh                   # wrapper: búsqueda manual
tasker/
  Odesli_Airsonic.tsk.xml            # tarea: widget Airsonic
  Odesli_Buscar.tsk.xml              # tarea reutilizable (%par1/%par2)
  Odesli_Manual.tsk.xml              # tarea: widget con input
  Odesli_From_Notification.prf.xml   # perfil: captura de notificaciones
```

Requiere Termux + Termux:API (F-Droid), Tasker, y un Airsonic/Airsonic-Advanced
accesible por Tailscale. Se despliega copiando la carpeta al móvil por `scp`/`adb` sobre
la misma Tailnet.
