+++
title = 'Escritorio'
weight = 3
+++

Ruta: `~/Scripts/Apps/` (sueltos, junto a las subcarpetas)

| Script | Qué hace |
|---|---|
| `filtros_masivos_thunderbird.sh` | Lee una lista de nombres de artistas (uno por línea) y genera, para cada uno, una regla de filtro de Thunderbird que mueve los correos de "New release from `<artista>`" de Bandcamp a una carpeta IMAP concreta; añade todas las reglas a `msgFilterRules.dat`. |
| `foobar.sh` | Lanza foobar2000 a través de Wine; si se le pasa una ruta de archivo como argumento, la convierte a formato Windows (`z:\...`) antes de abrirla. |
| `kp_busqueda.sh` | Abre KeePassXC, localiza su ventana con `xdotool` y le manda el atajo de buscar (`Ctrl+F`) para dejarlo listo con el cuadro de búsqueda enfocado. |
| `obsidian_calendario.sh` | Descarga (vía `curl` autenticado) los calendarios de un servidor **Radicale** propio en formato `.ics`, los sirve con un servidor HTTP temporal (`python3 -m http.server`) para que el plugin de calendario de Obsidian pueda leerlos, espera unos minutos mientras Obsidian los procesa y luego mata el servidor. |
