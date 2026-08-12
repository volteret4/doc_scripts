+++
title = 'Consejero RYM (MusicCircle)'
weight = 7
+++

**MusicCircle**: sistema de recomendación musical para un grupo de 11 amigos, basado en
sus scrobbles de Last.fm guardados en SQLite. En vez de un único algoritmo, implementa
**42 motores de recomendación** distintos (colaborativo, puentes de género, cadenas de
descubrimiento, tendencias, discografía, similitud externa, relaciones de grafo,
sello/productor, temporal, valoraciones, motores "computados", narrativos...), cada uno
genera candidatos con un score y el sistema los combina — con la idea de ir
desactivando/ponderando motores según los resultados reales con el tiempo.

```bash
python scripts/generate_recommendations.py        # genera todas las recomendaciones

# Pre-cálculos (antes de generar)
python scripts/precompute/user_profiles.py
python scripts/precompute/similarity_matrix.py
python scripts/precompute/session_clusters.py
python scripts/precompute/artist_embeddings.py     # Artist2Vec desde sesiones de escucha
python scripts/precompute/transition_matrix.py     # cadenas de Markov artista→artista
python scripts/precompute/loyalty_scores.py

# Enriquecimiento externo
python scripts/enrichment/fetch_lastfm_similar.py
python scripts/enrichment/fetch_musicbrainz_relations.py

# Frontend: HTML/JS/CSS estático, sin build — servir docs/ con cualquier servidor
python -m http.server 8000 --directory docs/
```

Dependencias: `numpy`, `scipy`, `networkx`, `python-louvain`, `gensim`, `requests`. La
base `db/lastfm_cache_rym_new_normalized.db` es preexistente y no se modifica su
estructura original.

{{% notice note %}}
Según su propio `CLAUDE.md`, el proyecto está en fase temprana: la especificación está
completa pero la mayoría del código todavía está por escribir.
{{% /notice %}}
