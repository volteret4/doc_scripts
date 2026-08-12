+++
title = 'Apps'
weight = 1
+++

Scripts que integran o controlan aplicaciones externas: notificaciones y control del
móvil vía **Join**, un espejo de pantalla con **scrcpy**, manipulación de la base de
datos local de **NewPipe**, userscripts de **Tampermonkey** y varios lanzadores/utilidades
de escritorio sueltos.

- **[Android](android)**: Join (alarmas, portapapeles, texto), scrcpy, gasolineras cercanas, NewPipe.
- **[Tampermonkey](tampermonkey)**: userscripts para el navegador.
- **[Escritorio](escritorio)**: Thunderbird, foobar2000, KeePassXC, Obsidian + calendarios.

{{% notice note %}}
La mayoría de estos scripts leen credenciales o IDs de dispositivo desde un archivo
`.env` en su misma carpeta (API keys de Join, coordenadas, usuario/contraseña de
Radicale...). Esos `.env` no se versionan ni se documentan aquí.
{{% /notice %}}
