+++
title = 'Dotfiles editor'
weight = 2
+++

Ruta: `~/Scripts/menus/dotfiles/`

Herramienta en dos partes para buscar y editar dotfiles rápidamente, con `CLAUDE.md`
propio documentando la arquitectura:

1. **`dotfiles_indexer.py`** — CLI que indexa los archivos de `~/.local/share/chezmoi`
   (el gestor de dotfiles que usa) en una base SQLite (`dotfiles.db`, modo WAL). Detecta
   cambios por mtime+hash para reindexar solo lo necesario.
2. **`dotfiles_quick_editor.py`** — GUI PyQt6 que busca en esa base y abre el resultado
   en un editor externo.

## Flujo de datos

```
chezmoi files → dotfiles_indexer.py → dotfiles.db → dotfiles_quick_editor.py → editor externo
```

## Uso

```bash
source ~/Scripts/python_venv/bin/activate

python dotfiles_quick_editor.py                  # abrir la GUI
python dotfiles_quick_editor.py --theme gruvbox  # con un tema concreto

python dotfiles_indexer.py              # reindexado incremental
python dotfiles_indexer.py --force      # reindexado completo
python dotfiles_indexer.py --stats      # estadísticas de la base
python dotfiles_indexer.py --search vim # buscar desde la CLI
```

## Detalles

- La tabla `dotfiles` guarda path, filename, extensión, si es config, si es ejecutable,
  origen, hash y mtime; la vista `dotfiles_with_categories` añade categorías
  auto-clasificadas.
- La búsqueda en la GUI corre en un `QThread` aparte para no bloquear la interfaz, y
  ordena resultados por relevancia (match exacto de nombre → prefijo → path → resto),
  con un tope de 500 resultados.
- Temas de color en `themes.yml` (catppuccin, forest-dark, gruvbox, kanagawa, neon,
  solarized-dark, tokyo-night).
- `EXCLUDE_PATHS` en el indexador descarta directorios pesados/irrelevantes (cachés de
  Chrome, Firefox, Steam, Discord...).

{{% notice tip %}}
Este mismo patrón (indexador SQLite + GUI PyQt6 + temas YAML) se repite en
`menus/iconos/` y `menus/scripts/`.
{{% /notice %}}
