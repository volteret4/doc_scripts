+++
title = 'Ensayos Musicales'
weight = 3
+++

Proyecto con dos frentes bien distintos bajo el mismo repo:

## Editor de correcciones + mapa D3

`correcciones/`, `db/mh_rym_nem.sql` y un editor web (`Dockerfile.editor`,
`ensayos_editor.service`) para gestionar datos musicales, más un mapa estático generado
con **D3.js v7** (`d3.v7.min.js`, `Dockerfile.map`) — perfiles `ensayos_editor` y
`ensayos_map` dentro del orquestador
[Tumtumpa]({{% relref "proyectos/musica-escucha/tumtumpa" %}}). El editor necesita la
base `db/music_facts.db` real para funcionar del todo.

## Pipeline de transcripción de podcast (Whisper + Gemini)

`main.sh` orquesta un flujo diario de dos pasos sobre episodios de podcast musical:

```bash
python3 audio_to_text.py      # Whisper en local, transcribe MP3 → TXT (sin límite de API)
python3 gemini_resumen.py     # genera resúmenes con Gemini
```

Si Gemini devuelve un error 429 (límite de API), el script de resumen sale con código 1
y `main.sh` detiene el flujo diario en vez de seguir fallando. `mp3_input/`,
`transcripts/`, `resumenes/` y `pendiente/` son las carpetas de trabajo del pipeline;
`ongoing_history_old/` guarda episodios ya procesados de series anteriores.

{{% notice note %}}
Este pipeline de transcripción es el que alimenta a
[Claude Resumen]({{% relref "proyectos/sistema/claude-resumen" %}}) — su `old_prompt`
apunta precisamente a `ongoing_history_old/old_prompt` de este mismo flujo. `main.sh`
referencia además una carpeta `~/gits/pollo/podcast_to_text` que no existe actualmente
como proyecto propio en `~/gits/pollo` — puede que haya sido renombrada/movida o que la
ruta esté desactualizada.
{{% /notice %}}
