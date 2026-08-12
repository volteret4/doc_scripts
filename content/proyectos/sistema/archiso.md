+++
title = 'Archiso'
weight = 1
+++

Definición de una **ISO de Arch Linux a medida** ("arch-pollo") usando
[archiso](https://wiki.archlinux.org/title/Archiso): `packages.x86_64` /
`bootstrap_packages.x86_64` (listas de paquetes), `profiledef.sh` (metadatos de la
imagen), y configuración de arranque tanto BIOS (`syslinux/`) como UEFI (`efiboot/`,
`grub/`), más `airootfs/` con los archivos de sistema a incluir tal cual en la imagen
final. `isos/` guarda las imágenes generadas; la carpeta `familia@192.168.1.226/`
sugiere una instalación/ISO específica para el equipo de otro miembro de la familia.
