+++
title = 'Claude Resumen'
weight = 4
+++

Convierte transcripciones de podcast en fichas de historia musical estructuradas en
Markdown, usando Claude como motor de extracción. No es tanto un script como un
**prompt documentado** (en el propio `CLAUDE.md`) más el andamiaje de entrada/salida:

- **Entrada**: `.txt` de transcripciones (típicamente en `old_prompt/`, symlink a
  `../podcast_to_text/ongoing_history_old/old_prompt`).
- **Salida**: un `.md` por entrada en `output/`, con el mismo nombre base.
- **Prompt**: "eres un historiador y crítico musical reconocido, extrae toda la
  información musicalmente significativa de la transcripción" — con instrucciones
  explícitas de ser exhaustivo (fechas, nombres, cifras, anécdotas) y de **ignorar por
  completo** cualquier pasaje que mencione al presentador del podcast (comentario
  personal/meta-referencias), quedándose solo con el contenido factual sobre artistas:
  miembros, bandas de las que forman parte, géneros, sellos, conciertos...

`redownload_old_promts.py` gestiona la descarga/recuperación de transcripciones previas;
`ongoing_history_of_music/` es la colección de fichas ya generadas.
