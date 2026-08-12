+++
title = 'FreshRSS Embeeds'
weight = 5
+++

Extrae enlaces de Bandcamp/YouTube/SoundCloud de los artículos de **FreshRSS** (vía su
API compatible con Google Reader) y genera páginas HTML con los embeds correspondientes,
por feed o categoría — paginación con lazy loading, tema oscuro, navegación por teclado.
Desplegado igual que [Bandcamp IMAP](../bandcamp-imap): Flask + SWAG (Docker) con SSL,
más un timer systemd para republicar semanalmente (`publish_docs.sh`,
`freshrss-embeeds.service`).

Es la versión de servidor del mismo generador que documenta
[`Musica/blog/rss`]({{% relref "scripts/musica/blog" %}}) en `~/Scripts`. Integrado como
submodule del orquestador [Tumtumpa]({{% relref "proyectos/musica-escucha/tumtumpa" %}}).
