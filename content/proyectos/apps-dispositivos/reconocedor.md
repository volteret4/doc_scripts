+++
title = 'Reconocedor'
weight = 4
+++

App Android nativa (Kotlin + Jetpack Compose + Hilt, paquete `com.pollo.reconocedor`)
de **reconocimiento de audio** (tipo Shazam): permisos de `RECORD_AUDIO` e `INTERNET`,
pantalla de autenticación (`AuthViewModel`) y navegación por Compose
(`AppNavigation`/`MainActivity`). Incluye un MP3 de prueba en la raíz del repo para
pruebas manuales de reconocimiento. Mismo patrón arquitectónico (Compose + Hilt) que
[Android Scrobbler]({{% relref "proyectos/musica-escucha/android-scrobbler" %}}).
