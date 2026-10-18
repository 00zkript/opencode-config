# Base de desarrollo OpenCode

Configuración **global** reutilizable para todos mis proyectos. Cada proyecto
extiende esto y solo define lo suyo: stack, steering, specs, skills locales y
tools.

## Estructura

- `AGENTS.md` — convenciones universales (se cargan siempre).
- `agents/` — subagentes genéricos: `reviewer`, `researcher`, `debugger`, `docs-writer`.
- `commands/` — comandos `/kiro-*` (envoltorios del motor SDD).
- `skills/`
  - `development` — estándares de código (cualquier lenguaje).
  - `kiro-*` — motor cc-sdd (descubrimiento, specs, diseño, tareas, implementación, validación).
  - `laravel`, `typescript`, `vue`, `react`, `python` — **packs de stack** (convenciones, generadores, comandos).
- `sdd/`
  - `settings/` — plantillas cc-sdd (incluye la plantilla de fases con *gate*).
  - `steering/` — esqueletos de `product.md`, `tech.md`, `structure.md`.
  - `packs/_template/SKILL.md` — plantilla para crear un pack de stack nuevo.
  - `opencode.jsonc` — config de proyecto de ejemplo.
- `bin/project-init` — prepara un proyecto: crea `.kiro/settings`, `.kiro/steering`
  y `.opencode/opencode.jsonc`.
- `bin/new-skill` — crea un pack de stack nuevo a partir de la plantilla
  (`new-skill rust`, `new-skill go`, …). Rellena y listo: se detecta en todos los proyectos.

## Cómo lo usa un proyecto

1. En la raíz del proyecto: `~/.config/opencode/bin/project-init`.
2. Edita `.kiro/steering/*` con el stack real.
3. Crea specs: `/kiro-discovery` → `/kiro-spec-init` → `/kiro-spec-requirements`
   → `/kiro-spec-design` → `/kiro-spec-tasks` → `/kiro-impl` → `/kiro-validate-impl`.
4. Añade en el proyecto solo lo específico: skills propias, tools, docs, `AGENTS.md`.

## Versionado

Este directorio es un repo git propio. `service.json` (específico de la máquina)
está ignorado.
