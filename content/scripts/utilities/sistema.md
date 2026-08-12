+++
title = 'Sistema'
weight = 2
+++

Tres subcarpetas pequeñas de `~/Scripts/utilities/` agrupadas aquí.

## android/

Desbloatear un Xiaomi por `adb` (UID de dispositivo fijo en el script):
`debloat_xiaomi.sh` desinstala (`pm uninstall`, vía `install-existing` para poder
reinstalar luego) apps de sistema no deseadas; `repair_debloat.sh` reinstala paquetes
concretos que un debloat previo dejó rotos.

## apis/

`spotify_login.py` — gestiona el login OAuth de Spotify (`spotipy`), abriendo el
navegador para autorizar cuando hace falta un token nuevo.

## awesomewm/

`alacritty_fullscreen.sh` — permite que el atajo de pantalla completa de AwesomeWM
funcione también dentro de Alacritty (detecta si se ejecuta dentro de una sesión
Alacritty vía `$ALACRITTY_LOG`).
