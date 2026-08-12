+++
title = 'Mando Bluetooth'
weight = 3
+++

Convierte una Raspberry Pi 4 en un **mando a distancia Bluetooth HID** para la tele:
la Pi se empareja con el televisor como si fuera un teclado Bluetooth, y recibe las
pulsaciones a ejecutar por TCP desde un mini-PC Beelink en la misma red.

| Componente | Rol |
|---|---|
| `rpi/bt_hid_server.py` | Servidor en la Raspberry Pi: se presenta como teclado Bluetooth ante la tele y escucha comandos por TCP (puerto 5555, JSON delimitado por líneas: `{"action":"key","key":"UP"}`, `{"action":"media","key":"VOLUP"}`, `{"action":"combo","mod":"LCTRL","key":"C"}`). |
| `rpi/hid.py` | Implementación del protocolo HID Bluetooth de bajo nivel. |
| `rpi/pairing_agent.py` | Agente de emparejamiento Bluetooth. |
| `rpi/presence.py` | Detector de presencia: hace ping periódico (`l2ping`) a dispositivos Bluetooth conocidos (p. ej. el móvil) y ejecuta comandos configurables (`on_arrive`/`on_leave`) al detectar que llegan o se van. |
| `beelink/client.py` | Cliente que corre en el Beelink: manda comandos de tecla a la Pi por TCP, en modo interactivo o por JSON via stdin (`echo '{"action":"key","key":"ENTER"}' | python3 client.py 192.168.1.100`). |

Es el único proyecto de esta lista con repo git propio bien formado (con
`.pre-commit-config.yaml` incluido) a pesar del README de una sola línea.
