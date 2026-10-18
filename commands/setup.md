---
description: Configura el proyecto actual para OpenCode + cc-sdd (reconoce el entorno, prepara el steering y enruta)
---

Eres el **configurador** del proyecto actual. No inventes nada: lo que no se pueda confirmar es una pregunta o un `TODO`.

## 1. Reconocer el entorno
Ejecuta en el shell:

```bash
~/.config/opencode/bin/detect-stack
```

Lee el resultado y **respeta el `ESTADO`**.

### Si `ESTADO: vacio` (no hay proyecto aquí)
1. Informa en una sola línea: «No se detectó ningún proyecto en esta carpeta.» y **no crees ni modifiques nada**.
2. Pregunta: **«¿Deseas iniciar un nuevo workspace aquí?»**
   - **No** → termina, sin cambios.
   - **Sí** → pregunta qué stack usarás. Luego:
     ```bash
     git init            # solo si no es un repo git
     ~/.config/opencode/bin/project-init
     ```
     Escribe el stack elegido en `.kiro/steering/tech.md` y continúa en el paso 3 (ruta *proyecto nuevo*).

### Si `ESTADO: proyecto`
Continúa al paso 2. Si no se reconoció ningún stack, **pregunta** cuál es antes de escribir.

## 2. Bootstrap
Ejecuta:

```bash
~/.config/opencode/bin/project-init
```

Crea solo lo que falte (`.kiro/settings`, `.kiro/steering/*`, `.opencode/opencode.jsonc`, `AGENTS.md`); nunca sobrescribe.

## 3. Escribir el conocimiento del proyecto
- `.kiro/steering/tech.md` → `## Stack` (con versiones si se leen de los manifiestos) y `## Cómo probar` con los comandos del stack (o los `docker compose run …`).
- `.kiro/steering/structure.md` → `## Capas / módulos` real.
- `.kiro/steering/product.md` → solo si se infiere del README/código; si no, déjalo y pregunta.
- `AGENTS.md` del proyecto → stack y comando de verificación.
- Si algún stack aparece `[sin pack]` y es de uso real, **ofrece** `~/.config/opencode/bin/new-skill <stack>` y, si acepta, rellénalo con lo que observes.
- **No pises** secciones con contenido real: propón el cambio y espera confirmación.

## 4. Enrutar
- **Proyecto nuevo o recién creado** → sugiere scaffoldear con el generador del framework (el comando está en el pack del stack) y luego `/kiro-discovery`; si el stack no está cerrado, `/kiro-steering` en modo *decidir*.
- **Proyecto con código existente** → `/kiro-steering` en modo *documentar* y después `/kiro-validate-gap` antes de diseñar.
- **Ya tenía `.kiro/` y specs** → reporta el estado con `/kiro-spec-status` y pregunta qué sigue.

Cierra con 3 líneas: **qué se creó/actualizó**, **qué stack se reconoció** (con su evidencia) y **el comando sugerido**.
