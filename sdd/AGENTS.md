# Instrucciones para agentes — <proyecto>

> Las reglas generales (código, SDD, verificación) viven en el `AGENTS.md` global
> y en las skills `development` + packs de stack. Aquí va solo lo del proyecto.

## Proyecto
<Qué es, en una o dos frases.>

## Stack
<Lenguajes, frameworks y versiones.>

## Convenciones del proyecto
- …

## Capas / módulos
- …

## Verificación (antes de cerrar un cambio)
```bash
# comandos exactos de tests, lint y formato (los mismos que en .kiro/steering/tech.md)
```

## SDD (cc-sdd)
- Specs en `.kiro/specs/<feature>/`; conocimiento en `.kiro/steering/`.
- Flujo: `/kiro-discovery` → `/kiro-spec-init` → `/kiro-spec-requirements` →
  `/kiro-spec-design` → `/kiro-spec-tasks` → `/kiro-impl` → `/kiro-validate-impl`.
- **No implementar sin spec aprobada** (`spec.json`).
