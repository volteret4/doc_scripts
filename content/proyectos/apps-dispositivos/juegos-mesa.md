+++
title = 'Juegos de Mesa'
weight = 9
+++

App (FastAPI) para gestionar la colección de juegos de mesa vía
**BoardGameGeek (BGG)**, con `plays.db` (SQLite) llevando la cuenta de partidas.

`bgg_import_user_collection.py` importa la colección de un usuario desde la API XML de
BGG (`boardgamegeek.com/xmlapi2`, en lotes de 20) y la vuelca a una **Google Sheet**
(OAuth2 con `client_secret.json`/`app_token.json`, ID de la hoja en `bgg_sheet_id.txt`),
extrayendo mecánicas, categorías, familias, edad mínima, rating de BGG y del usuario.
`app.py` sirve la web (`static/`) sobre esos mismos datos.
