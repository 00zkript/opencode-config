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

## Subagentes (disciplina de ejecución)
- **Profundidad máx. 1**: un subagente **nunca** despacha otros subagentes. Los roles
  de controlador/orquestador (`kiro-impl`, `kiro-spec-*`, `kiro-validate-*`) solo
  corren en el contexto principal, nunca dentro de un subagente.
- **Skills bajo evaluación**: un subagente **sí** puede cargar skills, pero **solo
  las que su tarea concreta necesite** — evalúa primero y carga ese subconjunto.
  Para codificar, casi siempre hace falta `development` (negative programming,
  indentación, saltos de línea, comentarios concisos) y el pack del lenguaje
  (`python`, `typescript`, …). **No** cargues skills ajenas a la tarea.
- **Ante un fallo de herramienta** (`aborted`, `cancelled`, permiso denegado):
  máximo **1 reintento**; si vuelve a fallar, **para y reporta** al usuario con el
  motivo exacto. Nunca improvises un reintento en bucle.
- **Presupuesto de ejecución**: si una sesión autónoma supera ~20–30 min o un
  número razonable de despachos, **para y reporta progreso parcial** con el punto
  de re-entrada (el flujo `kiro-impl` es re-entrable: lo ya commiteado se retoma).
