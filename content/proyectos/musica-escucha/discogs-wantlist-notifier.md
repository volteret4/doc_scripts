+++
title = 'Discogs Wantlist Notifier'
weight = 9
+++

Revisa por IMAP el correo (buzón de disroot) buscando los avisos de Discogs de "un ítem
de tu wantlist está a la venta", extrae los datos de cada oferta (artista, título,
condición, vendedor, precio, enlace) y los envía por Telegram. Al enviarlos con éxito,
marca el correo como leído (`\Seen`) — es también el único mecanismo de deduplicación:
un correo ya leído no se vuelve a procesar. Pensado para ejecutarse cada pocas horas vía
[Ofelia](https://github.com/mcuadros/ofelia); como solo mira correos `UNSEEN`, cada
ejecución recoge tanto ofertas nuevas como las acumuladas si llevaba tiempo sin correr.

El HTML de los correos de Discogs anida la imagen del producto y sus metadatos
(artista, `Media:`, `Sleeve:`, vendedor, precio, enlace real) en bloques `hse-column`
**hermanos** en vez de juntos — `parse_wantlist_email()` ancla la búsqueda en cada
`<img>` de producto y navega al `div` hermano siguiente para extraer el texto, porque un
regex directo sobre el HTML aplanado se rompe con la basura de tracking intercalada.

Variable de entorno destacable: `IMAP_FOLDERS` va separada por `|` (no por espacio,
porque los nombres de carpeta pueden contener espacios). El bot/token de Telegram puede
reutilizar el mismo bot admin ya configurado en [Bot Conciertos]({{% relref "proyectos/bots/bot-conciertos" %}}).
