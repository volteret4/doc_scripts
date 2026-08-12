+++
title = 'Cron'
weight = 5
+++

Ruta: `~/Scripts/utilities/cron/`

Tareas pensadas para lanzarse periódicamente.

| Script | Qué hace |
|---|---|
| `actualizar_cert_letsencrypt.sh` | Renueva manualmente el certificado Let's Encrypt de `*.pollete.duckdns.org` extrayéndolo del contenedor de Nginx Proxy Manager. |
| `ansible_kopia.sh` | Despierta por Wake-on-LAN los hosts Proxmox/Debian (vía playbooks de Ansible) y arranca Kopia para el backup. |
| `kopia_wake_sync.sh` | Variante más directa: `wakeonlan` a las MACs de Proxmox/Debian y notificación por [ntfy](https://ntfy.sh) del resultado. |
| `sync_vdir.sh` | `vdirsyncer sync` y copia el resultado de los calendarios de tareas a la carpeta de Obsidian. |
| `m4a_to_flac.sh` | Convierte en bloque los `.m4a` de una carpeta del NFS a FLAC, usando un directorio temporal local para la conversión. |
| `obtener_json_datahoarder.py` | Obtiene por SSH datos de un [Hoarder](https://github.com/hoarder-app/hoarder) remoto y los exporta a JSON. |
| `formato_python.py` | Formateador de estilo propio: fuerza 2 líneas en blanco tras imports, 3 entre funciones y 5 entre clases. |
| `scripts_to_md.py` / `mfuz_to_md.py` | Vuelcan el contenido de scripts a Markdown (con el bloque de código en el lenguaje correcto según extensión) — el mismo mecanismo que usa este propio sitio de documentación, aplicado antes a mano para otros fines (`mfuz_to_md.py` específico para los scripts del blog music-fuzzy). |

{{% notice tip %}}
`scripts_to_md.py`/`mfuz_to_md.py` son, en cierto modo, el precedente casero de lo que
ahora hace este sitio Hugo de forma más completa.
{{% /notice %}}
