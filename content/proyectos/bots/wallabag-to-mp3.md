+++
title = 'Wallabag to MP3'
weight = 7
+++

*("Sistema de Podcast TTS")*: convierte artículos guardados en **FreshRSS** y
**Wallabag** a MP3 (texto a voz) y genera un feed RSS que cualquier app de podcasts
(AntennaPod) puede suscribir — todo empaquetado en Docker.

```bash
cp config.json.example_v3 config.json   # editar con credenciales de FreshRSS/Wallabag
tailscale ip -4                          # IP para exponer el servicio en la Tailnet
# editar docker-compose.yml -> BASE_URL=http://TU-IP-TAILSCALE:8005
docker compose up -d
# añadir a AntennaPod: http://TU-IP-TAILSCALE:8005/podcast.xml
```

`articles_to_mp3.py`/`convert_url.py` hacen la conversión texto→audio,
`process_selection.py` gestiona qué artículos entran en el feed, y `server.py` sirve el
feed RSS y la web de selección (`web/`, `index.html`). Pensado para exponerse solo
dentro de la Tailnet, no públicamente.

{{% notice warning %}}
Mismo README y propósito que
[Podcast TTS]({{% relref "proyectos/apps-dispositivos/podcast-tts" %}}) — parecen dos
copias del mismo proyecto; ver esa página para la versión con `CLAUDE.md` y notas de
migración a Docker.
{{% /notice %}}
