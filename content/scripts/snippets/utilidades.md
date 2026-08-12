+++
title = 'Utilidades'
weight = 1
+++

Ruta: `~/Scripts/snippets/`

| Script | Qué hace |
|---|---|
| `funciones.sh` | Define `mostrar_barra_progreso()`, pensada para ser importada (`source`) por otros scripts y mostrar una barra de progreso ASCII de una duración dada. Marcada como *work in progress*. |
| `if case en terminal.sh` | Snippet de referencia: cómo montar un menú `select`/`case` de opciones en un script bash interactivo (ejemplo con géneros musicales). |
| `if_firefox_active.sh` | Detecta qué ventana/reproductor está activo (Firefox, Chromium, Floorp, Thorium, Zen, qutebrowser, Deadbeef, Strawberry vía `playerctl`) usando `xdotool`, y construye una cadena `"app - música actual"`. Lo usan otros scripts (p. ej. `disco_pendiente.sh`) como paso previo para saber qué se está escuchando/viendo. |
| `verificar_sig.sh` | Coge el último archivo descargado en `~/Descargas` de más de 2MB, busca su `.sig`/`checksum`/`SHA256SUMS` correspondiente (o pide uno con `zenity` si no lo encuentra) y lo verifica con `gpg --verify`, notificando el resultado. |
