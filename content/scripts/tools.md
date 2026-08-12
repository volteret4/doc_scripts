+++
title = 'Tools'
weight = 6
+++

Ruta: `~/Scripts/tools/sopsdotenv/`

Único paquete Python empaquetado (con su propio `pyproject.toml`) de todo `~/Scripts`:
**`sopsdotenv`**, un sustituto de `python-dotenv` que en vez de leer un `.env` en claro,
descifra uno cifrado con [SOPS](https://github.com/getsops/sops) + `age`.

```python
from sops_env import load_sops_env
load_sops_env()
```

`load_sops_env()` busca `.encrypted.env` subiendo desde el directorio de trabajo (o usa
la ruta que se le pase), lo descifra con `sops --decrypt` y vuelca el resultado en
`os.environ` — mismo interfaz que `load_dotenv()`, para poder sustituirlo sin tocar el
resto del código.

{{% notice note %}}
Varios proyectos de `~/gits/pollo` tienen un `.encrypted.env` en su raíz — es este el
mecanismo que lo consume.
{{% /notice %}}
