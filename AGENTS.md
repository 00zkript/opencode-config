# Convenciones globales (todos mis proyectos)

> Base reutilizable. Lo específico de cada proyecto vive en su propio `AGENTS.md`
> y en `.kiro/steering/`.

## Código
- Aplica la skill **`development`** al escribir, refactorizar o revisar código
  (negative programming, SOLID, funciones atómicas, DRY, clean code, patrones solo
  si el caso lo justifica, buenas prácticas del lenguaje, legibilidad).
- **Antes de crear un archivo, usa el generador del framework/CLI si existe**
  (`php artisan make:*`, `rails generate`, `nest g`, `ng generate`,
  `django-admin startapp`, `cargo new`, …). Si no hay, sigue su convención.
- Crea archivos con permisos razonables (`644`/`755`, nunca `777`). En Docker usa
  el UID/GID del host (`--user "$(id -u):$(id -g)"` o `user:` en compose) para que
  sean editables fuera.
- Nunca imprimas credenciales, cookies ni tokens.

## Especificación (SDD)
- Desarrollo guiado por especificación con **cc-sdd** (skills y comandos `kiro-*`):
  specs en `.kiro/specs/<feature>/`, conocimiento persistente en `.kiro/steering/`.
- **No implementes sin spec aprobada** (`spec.json`).
- Cada fase de `tasks.md` es un objetivo por flujo con un **gate** medible
  (comando + resultado esperado) como última subtarea.

## Verificación
- No declares algo terminado sin **evidencia real** (comando y salida, o URL y
  pasos de humo). Los comandos canónicos del proyecto van en su `AGENTS.md` o en
  `steering/tech.md`.
