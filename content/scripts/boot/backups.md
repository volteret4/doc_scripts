+++
title = 'Backups'
weight = 1
+++

Ruta: `~/Scripts/boot/backups/`

| Script | Qué hace |
|---|---|
| `back_cnt.sh` | Backup manual de contenedores Docker concretos: hace `docker commit` + `docker save` (a un `.tar` con la fecha) de `duplicati`, `radicale`, `wallabag` y `postgres`. El resto de contenedores (transmission, lidarr, portainer, jackett, syncthing, ttrss, mercury, wireguard) están comentados — se activan/desactivan editando el script. |
| `backup-arco.sh` | Copia con `rsync -av` `~/Scripts`, `/etc/fstab`, `~/.ssh` y `~/.dotfiles` a una carpeta local de backup (`.../backup-usb/arco`). Pensado para lanzarse por cron. |
| `borg.sh` | Backup real (no solo copia local) con [borg](https://www.borgbackup.org/): crea un snapshot con compresión zstd de `~/.dotfiles` en un repo borg remoto (`borg:arco::dotfiles-<fecha>`) y poda dejando solo los últimos 5. |
| `mover_scripts_wiki.sh` | Crea **hardlinks** de todos los `.sh` y `.py` de `~/Scripts` dentro de una carpeta del Wiki de Obsidian montado en `/mnt/Datos/FTP/Wiki/...`, para tenerlos indexados y buscables ahí. Admite origen/destino como argumentos. |
| `temp.sh` | Genera un `.service` + `.timer` de systemd de usuario que ejecuta `backup-arco.sh` a los 20 min de arrancar y luego semanalmente, y los instala (`~/.config/systemd/user`) y activa. Es el script que "instala" el backup periódico, no el que hace el backup en sí. |

{{% notice tip %}}
`temp.sh` + `backup-arco.sh` son en la práctica el mecanismo de backup automático:
`temp.sh` se ejecuta una vez para dar de alta el timer, y a partir de ahí systemd llama
periódicamente a `backup-arco.sh`.
{{% /notice %}}
