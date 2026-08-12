+++
title = 'Last.fm Stats Web'
weight = 14
+++

**Fork vendorizado** de [felhag/lastfm-stats-web](https://github.com/felhag/lastfm-stats-web)
(remote git original, no es código propio): una app Angular que muestra estadísticas
adicionales sobre el perfil de Last.fm/Spotify de un usuario — streaks, listas, gráficas,
rango de fechas personalizado, import/export. Corresponde a los sitios públicos
[lastfmstats.com](https://lastfmstats.com) y [spotifystats.app](https://spotifystats.app)
del proyecto original.

```bash
docker build -t lastfm-stats .
docker run -p 4200:4200 lastfm-stats
```

No confundir con [Back RYM Last.fm](../back-rym-lastfm)/[RYM Last.fm](../rym-lastfm),
que son generadores propios de estadísticas de **grupo** (coincidencias entre varios
usuarios), mientras que este es un dashboard individual de terceros.
