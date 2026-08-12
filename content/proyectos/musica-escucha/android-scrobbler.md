+++
title = 'Android Scrobbler'
weight = 2
+++

App nativa Android (Kotlin + Jetpack Compose, Clean Architecture + MVVM, Hilt) para
**escanear discos físicos y hacer scrobble en Last.fm**: usa la cámara para leer códigos
de barras, busca la edición en **Discogs** (OAuth 1.0a, firmado HMAC-SHA1) y permite
marcarla como escuchada contra la API de Last.fm.

- **Capas**: `domain/` (modelos y casos de uso, sin dependencias externas), `data/`
  (Retrofit + Room + implementaciones de repositorio), `ui/` (una pantalla Compose + un
  ViewModel por feature: auth, colección, escáner, búsqueda, detalle, ajustes).
- **Persistencia**: Room (`ScrobblerDatabase`). Credenciales OAuth en
  `EncryptedSharedPreferences`.
- Compilación: `./gradlew assembleDebug` / `installDebug`; claves de API en
  `local.properties` (gitignored), inyectadas como `BuildConfig`.

Es la contraparte "de bolsillo" de proyectos como [Artist Sync](../artist-sync) o
[Back RYM Last.fm](../back-rym-lastfm): en vez de analizar la colección ya existente,
sirve para ir añadiendo discos nuevos sobre la marcha.
