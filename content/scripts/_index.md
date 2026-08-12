+++
title = 'Scripts'
weight = 1
+++

Scripts sueltos de `~/Scripts/`, organizados por la misma carpeta temática en la que viven.

- **[Apps]({{% relref "scripts/apps" %}})** — Android (Join, NewPipe, scrcpy), Tampermonkey, escritorio.
- **[Boot]({{% relref "scripts/boot" %}})** — backups, servicios de arranque/apagado, aprovisionamiento.
- **[Menús]({{% relref "scripts/menus" %}})** — lanzadores rofi/dmenu, editor de dotfiles, VM con Claude Code.
- **[Música]({{% relref "scripts/musica" %}})** — blogs, conciertos, Deadbeef, discos nuevos, estadísticas, mpv, Orpheus, playlists.
- **[Snippets]({{% relref "scripts/snippets" %}})** — utilidades sueltas y el puente CalDAV↔todo.txt↔Taskwarrior.
- **[Second Brain]({{% relref "scripts/second-brain" %}})** — hotkeys de AwesomeWM para Doom Emacs/org-mode.
- **[Tools]({{% relref "scripts/tools" %}})** — `sopsdotenv`, el puente SOPS+age para `.encrypted.env`.
- **[UI]({{% relref "scripts/ui" %}})** — bocetos de Qt Designer.
- **[Utilities]({{% relref "scripts/utilities" %}})** — la carpeta más variada: aliases, notificaciones, servidores web, TiddlyWiki/Obsidian, Wireshark...

`actualizar-todotxt.sh`, suelto en la raíz de `~/Scripts/`, deduplica `todo.txt`
(`todo.sh deduplicate`) y lo sincroniza por `rsync` a Documentos — se lanza al apagar
el equipo (deja constancia en `~/uptime`).
