+++
title = 'Sobrinos'
weight = 4
+++

**NFC Music Player**: repo propio (`github.com/volteret4/sobrinos`) del sistema de
tarjetas NFC para discos/películas/series ya visto de pasada en
[`Musica/blog/sobrinos`]({{% relref "scripts/musica/blog" %}}) — este es el proyecto
completo, más general de lo que sugería esa carpeta de `~/Scripts` (no solo álbumes,
también cine y series).

Al escanear una tarjeta NFC se lanza la reproducción en el reproductor configurado;
paralelamente se genera una web en `docs/` con información del elemento, accesible por
un QR impreso en la propia tarjeta.

## Hardware

Tarjetas NFC de 52×82mm (adaptable), lector compatible (chip **ACR122U** recomendado en
Linux), y un dispositivo que pueda correr Linux (Raspberry Pi 4 con Raspbian en el caso
del autor — *"probablemente overkill"*, según el propio README) conectado al
reproductor: deadbeef, moOde, MPD, mpv, Spotify, VLC...

```bash
sudo apt-get install libacsccid1 pcscd pcsc-tools
sudo systemctl enable pcscd.socket
# desactivar los módulos nfc del kernel para poder leer con pcsc_scan:
# /etc/modprobe.d/blacklist.conf → install nfc /bin/false ; install pn533 /bin/false
```

## Flujo de uso

```bash
python nfc/nfc_detect_uid.py                 # obtener el UID de cada tarjeta
python nfc/nfc_config_gen.py                 # asociar UID → ruta de reproducción (nfc_playlist.json)
python nfc/nfc_reaccionar.py                 # monitoriza tarjetas y lanza la reproducción

python nfc/nfc_generar_portada.py /ruta/al/album [--custom-url ...]           # tarjeta de álbum
python nfc/nfc_generar_portada_artista.py /ruta/ARTISTA [--custom-url ...]   # tarjeta de artista
python nfc/nfc_tarjetas_cine.py /carpeta/con/posters [-o /carpeta/salida]     # tarjetas de cine, por lotes
```

`album_web_generator.py` + `modules/` generan la web de detalle por elemento;
`orquestar.py` coordina el flujo completo; credenciales en `secrets.enc.yaml`.
