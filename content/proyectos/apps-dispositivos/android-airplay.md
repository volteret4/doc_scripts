+++
title = 'Android AirPlay'
weight = 1
+++

App Android sin README propio, pero el `AndroidManifest.xml` es bastante explícito:
captura audio del dispositivo (`RECORD_AUDIO`, `FOREGROUND_SERVICE_MEDIA_PROJECTION`) y
lo transmite por red (multicast Wi-Fi: `CHANGE_WIFI_MULTICAST_STATE`) como servicio en
primer plano que sigue sonando con la pantalla apagada (`WAKE_LOCK`) — es decir, un
receptor/emisor tipo AirPlay para streamear audio del móvil a otro dispositivo en la
LAN. Paquete `com.pollo...`, tema `Theme.PolloAirPlay`.
