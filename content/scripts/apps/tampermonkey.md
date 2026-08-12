+++
title = 'Tampermonkey'
weight = 2
+++

Ruta: `~/Scripts/Apps/tampermonkey/`

Userscripts de navegador (Tampermonkey/Violentmonkey), pensados para saltarse paywalls
y sustituir servicios por sus instancias propias auto-alojadas.

| Script | Qué hace |
|---|---|
| `add_prefix_to_medium.js` | En Medium y un par de diarios (La Voz, El Confidencial), antepone `12ft.io/` a la URL para intentar saltarse el paywall. |
| `reddit_redlib_switcher.js` | Redirige automáticamente cualquier dominio de Reddit (`reddit.com`, `old.`, `new.`, `np.`, `amp.`, `i.`) a una instancia propia de **Redlib** (`redlib.pollete.duckdns.org`), incluso si la URL cambia dinámicamente (SPA). |
| `redirect_to_login.js` | En last.fm, GitHub y ChatGPT, detecta si la sesión no está iniciada (comprobando la ausencia de enlaces de logout/auth en el DOM) y redirige a la pantalla de login, una sola vez por sesión (marca de `localStorage`). |
| `yt_invidious_switcher.js` | Sustituye los iframes embebidos de YouTube por una instancia propia de **Invidious** (`yt.pollete.duckdns.org`) y añade un botón flotante sobre cada vídeo para alternar entre YouTube e Invidious. |
