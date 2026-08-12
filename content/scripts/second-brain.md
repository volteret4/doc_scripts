+++
title = 'Second Brain'
weight = 5
+++

Ruta: `~/Scripts/second_brain/`

Cinco hotkeys de AwesomeWM para un sistema de notas en **Doom Emacs + org-mode**, con
`~/notes/` como vault. Todos comparten el patrón de asegurar primero que el daemon de
Emacs esté vivo (`emacsclient` sobre un socket de usuario, reiniciando el servicio si
hace falta) y abrir el frame sin bloquear el hotkey (`-n`).

| Script | Qué hace |
|---|---|
| `sb_open_notes.sh` | Abre un frame de Emacs y cambia al workspace "notes" (`+workspace/switch-to`), creándolo si es la primera vez. |
| `sb_add_task.sh` | Sin argumentos: pide el texto por `rofi` y añade `- [ ] texto` directamente a `~/notes/Important/inbox.md`, sin pasar por Emacs. Con `--emacs`: lanza la plantilla de `org-capture` `"t"`. |
| `sb_add_event.sh` | Lanza la plantilla de `org-capture` `"e"` (evento + `SCHEDULED`), que se sincroniza vía `org-caldav` contra el servidor Radicale. |
| `sb_add_event_rofi.sh` | Variante sin Emacs: pide título y fecha por `rofi` y añade directamente una entrada `org` con `SCHEDULED` a `~/notes/inbox.org`. |
| `sb_search_notes.sh` | Terminal flotante (clase `sb-search`, para reglas de floating en AwesomeWM) con `fzf` sobre `~/notes/`: búsqueda de contenido (`rg`) por defecto, o solo nombre de archivo con `--files` (`fd`). Al seleccionar, abre la nota en `emacsclient -n` (con `hx` como fallback). |

{{% notice tip %}}
`sb_add_task.sh`/`sb_add_event_rofi.sh` existen como atajo rápido "sin Emacs" para cuando
solo hace falta anotar algo sin esperar a que arranque el daemon.
{{% /notice %}}
