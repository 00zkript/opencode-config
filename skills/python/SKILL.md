---
name: Python
description: Convenciones, generadores y comandos para proyectos Python. Úsala al trabajar en un proyecto Python.
---

# Python

## Entorno y andamiaje
- Entorno en `.venv`; instalar editable: `pip install -e .`.
- Preferir `uv` o `poetry`; `pyproject.toml` como fuente de verdad.
- Estructura `src/<paquete>/` con paquetes internos; tests en `tests/`.

## Convenciones
- PEP 8; formato con `ruff format`, lint con `ruff check`; tipos con `mypy`/`ty`.
- Funciones puras y pequeñas; sin estado global mutable; retorno temprano.
- Negative programming: validar precondiciones al inicio; error explícito, no asumir el camino feliz.
- Type hints en firmas públicas; docstrings concisos; `pathlib` en vez de `os.path`.
- Fechas con `datetime` (evitar `dateutil` si alcanza).

## Calidad y comandos
- Formato: `ruff format .`
- Lint: `ruff check .`
- Tipos: `mypy .`
- Tests: `pytest -q`
- Ejecutar: `python -m <paquete>`

## Errores comunes
- Dependencias sin fijar en `pyproject.toml`.
- `bare except` y errores silenciados.
- Rutas relativas al cwd en vez de `Path(__file__)`.
