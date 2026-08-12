+++
title = 'Varios'
weight = 8
+++

Media docena de subcarpetas pequeñas y sueltas de `~/Scripts/utilities/`.

| Carpeta / script | Qué hace |
|---|---|
| `maquinas-virtuales/test_groups.sh` | Lista los grupos IOMMU del sistema y qué dispositivos PCI hay en cada uno — paso previo típico para configurar passthrough de GPU a una VM. |
| `nginx_configs_generator/nginx_configs_generator.py` | Genera configuraciones de Nginx (proxys inversos) a partir de una lista de apps/dominios en `apps-config.json`. |
| `pdf/crear_indice.py` | Genera marcadores/índice interactivo en un PDF (PyMuPDF + PyPDF2) a partir de un índice textual con sus números de página. |
| `pihole/music_on.sh` | Consulta la API de Pi-hole las peticiones DNS a YouTube de los últimos minutos (para detectar si hay música sonando en algún dispositivo de la LAN). `pihole/pihole` es una base SQLite de datos, no un script. |
| `ping_antonio/ping_monitor.sh` | Monitor de conectividad: hace ping periódico a un host, y si falla varias veces seguidas (umbral configurable) avisa por Telegram — edita el mismo mensaje mientras la caída continúa en vez de spamear uno nuevo cada vez, y avisa también al recuperarse. Instalable como servicio (`ping_monitor.service`). |
| `pomodoro/pomodoro.py` | Temporizador Pomodoro con interfaz Tkinter e icono en la bandeja del sistema (`pystray`). `pomodoro.py2` es una copia/variante antigua. |
