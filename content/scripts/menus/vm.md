+++
title = 'VM (Claude Code aislado)'
weight = 9
+++

Ruta: `~/Scripts/menus/vm/`

Sistema para correr **Claude Code dentro de una VM Arch aislada** (vía `libvirt`/`qemu`),
con el proyecto y el estado de Claude montados por `sshfs` desde el host — pensado para
lanzarse como un panel de zellij.

| Archivo | Qué hace |
|---|---|
| `claude-vm.xml` | Definición de dominio `libvirt` (KVM, 4 vCPU, 4 GiB RAM, `host-passthrough`) para la VM `claude-vm`. |
| `build_seed.sh` | Genera el `user-data`/`meta-data` de cloud-init para la VM: crea el usuario `huan`, instala `openssh`/`sshfs`, e inyecta un script `mount_and_claude.sh` que — dentro de la VM — monta por sshfs `~/.claude` y el proyecto indicado desde el host, y lanza `claude --continue`. |
| `vm_claude_ensure.sh` | Idempotente: si el dominio `claude-vm` no existe lo define desde `claude-vm.xml` (comprobando antes que existan la imagen base, el overlay y la ISO de seed), lo arranca si no está corriendo, espera a que SSH responda y a que `cloud-init` termine. |
| `vm_claude_pane.sh` | Pensado como comando de un panel de zellij: llama a `vm_claude_ensure.sh` y luego hace `ssh -t claude-vm` ejecutando `mount_and_claude.sh <proyecto>`; al terminar la sesión, cae a un shell local. |

Se invoca desde los lanzadores de layouts de zellij en [rofi](../rofi#layouts-de-zellij-para-claude-code)
(`generar_layouts_claude_vm.sh` / `zellij_claude_vm_tab.sh`), que crean una pestaña por
proyecto usando esta VM como entorno de ejecución.
