---
description: Crea un workspace nuevo (carpeta + git + base OpenCode/cc-sdd) sin salir de OpenCode
---

Crea un proyecto nuevo. Argumentos: `$ARGUMENTS` = `<nombre> [stack]`.

Reglas:
- Ejecútalo desde la carpeta **padre** donde quieres el proyecto; el destino es `./<nombre>`.
- No sobrescribas: si el destino ya existe, detente y avísalo.

## 1. Validar
- `<nombre>` es obligatorio (si falta, pregúntalo). Debe ser un nombre simple de carpeta, sin `/`.
- Destino: `./<nombre>`. Comprueba que no exista.

## 2. Crear el esqueleto
```bash
mkdir -p <nombre>
git -C <nombre> init
```

## 3. Stack
- Si el usuario lo pasó como argumento, úsalo.
- Si no, **pregúntale qué stack usará**.

## 4. ¿Generador del framework o a mano?
Pregunta si va a scaffoldear con el generador del framework (Laravel, Vite/Vue, Next, etc.) o si armará la estructura a mano:

- **Con generador** → deja la carpeta **vacía** (solo `.git`) y muéstrale el comando del generador (búscalo en el pack del stack, sección «Generadores / andamiaje»). No lo ejecutes salvo que te lo pida: suelen ser interactivos y exigen carpeta vacía. Al terminar el usuario ejecutará `/setup` dentro del proyecto.
- **A mano** → ejecuta ahora:
  ```bash
  cd <nombre> && ~/.config/opencode/bin/project-init
  ```
  y escribe el stack elegido en `.kiro/steering/tech.md` (`## Stack`).

## 5. Cerrar
Informa en pocas líneas:
- la ruta creada y el modo elegido;
- cómo continuar: **abre OpenCode en esa carpeta** (o mueve la sesión si tu OpenCode lo permite) y ejecuta `/setup` (si usaste generador) o `/kiro-discovery` (si ya quedó inicializado).
