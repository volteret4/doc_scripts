+++
title = 'Mihitas (Obsidian → Hugo)'
weight = 5
+++

Ruta: `~/Scripts/menus/mihitas/`

Aplicación PyQt6 (`crear_post.py`) que convierte notas de Obsidian en posts de Hugo,
publicándolas en varios blogs a la vez. Es la herramienta que alimenta blogs como
`notas` y `mihitas` en `/mnt/NFS/blogs/`.

## Uso

```bash
python crear_post.py                          # modo interactivo
python crear_post.py /ruta/al/archivo.md       # carga directa de un archivo
python crear_post.py /ruta/al/archivo.md --all # + todos los blogs preseleccionados
```

`image_selector.py` es un selector de imágenes de ejemplo independiente (Picsum Photos,
PlaceImg...), usable también por su cuenta: `python image_selector.py /directorio/destino`.

## Blogs soportados

| Blog | Ruta | Frontmatter |
|---|---|---|
| notas | `/mnt/NFS/blogs/notas/content/post/` | YAML, requiere categoría |
| mihitas | `/mnt/NFS/blogs/mihitas/content/posts/` | TOML, sin categoría |

Las rutas están definidas en la clase `BlogConfig` dentro de `crear_post.py`.

## Interfaz

- **Panel izquierdo**: lista de `.md` de Obsidian ordenados por fecha, con hotkeys
  numéricas (1-9) para selección rápida.
- **Panel derecho**: título auto-generado, descripción libre, categoría (solo blog
  *notas*), tags (checkboxes persistentes vía `tags.json`) y selección de blog(s) destino.
- Al procesar: convierte la sintaxis de Obsidian a Hugo, copia las imágenes referenciadas,
  genera el frontmatter, crea la estructura de directorios necesaria y hace **commit a
  git** automáticamente.

`crear_post.sh`, `main.sh` y `publicado_md.sh` son wrappers en bash alrededor de este
flujo (lanzar la app, marcar una nota como publicada, etc.).

{{% notice note %}}
Requiere credenciales SSH configuradas (`ssh-add ~/.ssh/keys/github`) para que el commit
automático a git funcione.
{{% /notice %}}
