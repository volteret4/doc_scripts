+++
title = 'Android'
weight = 1
+++

Ruta: `~/Scripts/Apps/android/`

## Join (notificaciones y control remoto)

Los tres scripts usan la API de [Join](https://play.google.com/store/apps/details?id=com.joaomgcd.join)
para mandar acciones al móvil (Poco X3 o Poco F6) desde el escritorio. Todos leen
`API_KEY`/`APIKEY` y el ID del dispositivo (`POCOX3`, `POCOF6`) de un `.env` local.

| Script | Qué hace |
|---|---|
| `join_alarma.sh` | Hace sonar el móvil como "encuéntrame" (`find=true` en la API de Join). |
| `join_send_clipboard.sh` | Envía el contenido actual del portapapeles (leído con `copyq`) al móvil y lanza una notificación de escritorio confirmándolo. |
| `join_send_text.sh` | Envía la selección/portapapeles X (`xclip -o`) al móvil como texto. |

## scrcpy_poco.sh

Arranca el servidor ADB, se conecta por wifi a la IP fija del Poco (`adb connect`) y
lanza `scrcpy` para reflejar/controlar la pantalla del móvil desde el escritorio.

## gasolineras/

Busca las gasolineras más baratas cercanas a partir de un dataset descargado
(probablemente del Ministerio para la Transición Ecológica). Hay dos implementaciones
que hacen básicamente lo mismo por caminos distintos:

- **`gas.py`**: lee `gasolina_filtro.json`, normaliza los precios (coma → punto), filtra
  por un margen de ±0.1° alrededor de `LAT`/`LON` (variables de entorno) y escribe las
  10 más baratas ordenadas por precio de gasóleo en `gasolineras_cercanas.json`.
- **`gasolineras_cercanas.sh`**: variante en bash que calcula un radio en grados a partir
  de unas coordenadas de referencia fijas (Madrid) y filtra con `grep` sobre el mismo tipo
  de fichero.
- **`index.html`**: página estática que hace `fetch('./gasolineras_cercanas.json')` y
  pinta el resultado en una tabla (rótulo, municipio, dirección, diésel, 95, 98).

## newpipe/

Herramientas para tocar directamente la base de datos SQLite local de NewPipe
(`newpipe.db`), fuera de la app:

| Script | Qué hace |
|---|---|
| `bandcamp_metadata.py` | Dada una URL de YouTube o Bandcamp, extrae título y miniatura (scraping con BeautifulSoup) y añade una entrada a una playlist existente de NewPipe insertándola directamente en las tablas `stream` / `playlist_stream_join`. |
| `newpipe-links.py` | Exporta a CSV (por stdout) las playlists de NewPipe: URL, título, tipo, duración, autor y miniaturas, vía un `JOIN` sobre `streams` / `playlist_stream_join` / `playlists`. |
| `test_newpipe.sh` | Marcado como *WIP* en sus propios comentarios: hace `adb pull` de la base de datos de NewPipe del móvil, inserta un vídeo de prueba a mano con `sqlite3`, y la sube de vuelta con `adb push`. Sirve más de plantilla/experimento que de script terminado. |

## tasker/

Un prototipo HTML suelto (`Tasker Web UI Proof Of Concept.html`/`.mhtml` y
`edit-task.html`), sin lógica de servidor: una prueba de concepto de interfaz web para
editar tareas de Tasker.
