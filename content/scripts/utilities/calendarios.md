+++
title = 'Calendarios'
weight = 3
+++

Ruta: `~/Scripts/utilities/calendarios/`

| Script | Qué hace |
|---|---|
| `import_ics.py` | Importa eventos de varios archivos `.ics` a distintos calendarios de Radicale, según lo definido en `calendarios_config.json` (permite mapear cada `.ics` a un calendario distinto). |
| `eliminar_duplicados.py` | Elimina eventos duplicados de un calendario CalDAV concreto (Radicale). |

La carpeta también guarda los `.ics` de partida (Calendario, Conciertos, Diario,
Discos, Música, Personal, Tareas) que alimentan a `import_ics.py`.
