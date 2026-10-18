---
description: Reconoce e inicializa el proyecto para OpenCode + cc-sdd (bootstrap, detecta el stack y prepara el steering)
---

Eres el **inicializador** del proyecto. Trabaja en el directorio actual y sigue los pasos en orden. Sé breve y no inventes: lo que no se pueda confirmar es una pregunta o un `TODO`.

## 1. Bootstrap de la infraestructura
Ejecuta en el shell:

```bash
~/.config/opencode/bin/project-init
```

Crea solo lo que falte (`.kiro/settings`, `.kiro/steering/*`, `.opencode/opencode.jsonc`, `AGENTS.md`); nunca sobrescribe. Si ya existía todo, dilo en una línea y continúa para **revisar** que el steering esté al día.

## 2. Reconocer el entorno
Ejecuta en el shell:

```bash
~/.config/opencode/bin/detect-stack
```

Interpreta el resultado. Si `$ARGUMENTS` indica un stack, úsalo como override. Si no detecta nada o hay empate, **pregunta** al usuario qué stack es antes de escribir.

Si algún stack aparece como `[sin pack]` y es de uso real en el proyecto, **ofrece** crear su pack global:

```bash
~/.config/opencode/bin/new-skill <stack>
```

Si el usuario acepta, rellena `~/.config/opencode/skills/<stack>/SKILL.md` con las convenciones y comandos que observes en el repo (o que el usuario indique), y avísale de que quedará disponible en todos sus proyectos.

## 3. Escribir el conocimiento del proyecto
Con la evidencia detectada, actualiza:

- `.kiro/steering/tech.md` → sección `## Stack` (lenguajes/frameworks + versiones si se pueden leer de los manifiestos) y el bloque `## Cómo probar` con los comandos del stack. Si el proyecto usa Docker, pon ahí los `docker compose run …`.
- `.kiro/steering/structure.md` → `## Capas / módulos` real (o un plan si el proyecto está vacío).
- `.kiro/steering/product.md` → solo si se puede inferir del README/código; si no, deja el esqueleto y pregunta.
- `AGENTS.md` del proyecto → stack y comando de verificación.

Respeta lo que ya escribió el usuario: si una sección ya tiene contenido real, **no la pises**; propón el cambio y espera confirmación.

## 4. Decidir el siguiente paso
Según el estado, propón **una** ruta:

- **Proyecto nuevo/vacío** → `/kiro-discovery`; si el stack aún no está decidido, `/kiro-steering` en modo *decidir*.
- **Proyecto con código existente** → `/kiro-steering` en modo *documentar* y después `/kiro-validate-gap` antes de diseñar.
- **Ya tenía `.kiro/` y specs** → reporta el estado con `/kiro-spec-status` y pregunta qué sigue.

Cierra con un resumen de 3 líneas: **qué se creó/actualizó**, **qué stack se reconoció** (con su evidencia) y **el comando sugerido**.
