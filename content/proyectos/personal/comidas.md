+++
title = 'Comidas'
weight = 1
+++

*("comidas-bot")*: bot de Telegram que planifica comidas y cenas de la semana según el
calendario de turnos de trabajo, y genera la lista de la compra.

## Cómo funciona

Lee el calendario `Turnos` de Radicale: cada día trabajado tiene un evento codificado
como `MT` (7-22), `M` (7-15) o `T` (15-22); los días sin evento se consideran libres.
Según el turno, cada comida/cena de ese día exige un plato `tupper` (para llevar),
`rapido`, o ninguna restricción.

Para cada una de las 14 franjas de la semana (comida/cena × 7 días) el bot ofrece 3
platos candidatos del catálogo que cumplen la restricción. Si el plato elegido no es
`fresco` (carne/pescado fresco), pregunta para cuántos días más repetirlo y rellena esos
días automáticamente; si un plato rinde más días de los que caben en la semana, el
sobrante pasa a la semana siguiente. Al terminar, envía la lista de la compra agrupada
por tanda de cocina y la añade como tarea (`VTODO`) al calendario `Tareas` de Radicale.

El catálogo viene sembrado con 8 recetas de ejemplo (Thermomix, Airfryer, fuego normal);
se editan con `/borrarplato`/`/editplato`. `/addplatourl` usa Gemini para dar de alta un
plato a partir de una URL (opcional: sin `GEMINI_API_KEY` el resto del bot funciona
igual).

```bash
cp .env.example .env   # Telegram, Radicale, GEMINI_API_KEY, horario del job semanal
docker compose up -d --build
```

Por defecto, la planificación automática se dispara los domingos a las 20:00
(`Europe/Madrid`).
