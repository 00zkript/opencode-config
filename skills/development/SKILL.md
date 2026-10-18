---
name: Development Standards
description: Estándares de desarrollo para escribir, refactorizar o revisar código en cualquier proyecto o lenguaje (negative programming, SOLID, funciones atómicas, reutilización, clean code, patrones de diseño y arquitectura, buenas prácticas del lenguaje, legibilidad, tests por flujo y documentación concisa). Úsala siempre que vayas a escribir o revisar código.
metadata:
  opencode/autoinvoke: true
---

# Development Standards

Guía general y reutilizable para cualquier proyecto o lenguaje. Aplícala al
escribir, refactorizar o revisar código.

## Antes de escribir código (obligatorio)

1. **Aclara primero.** Haz todas las preguntas necesarias hasta entender el
   problema, el alcance y el contrato esperado. No asumas requisitos.
2. **Verifica qué es realmente necesario.** Separa lo imprescindible de lo
   accesorio y evita la sobre-ingeniería.
3. **Propón antes de integrar.** Si una librería, paquete o herramienta
   disponible facilita el desarrollo, **pregunta** si usarla: presenta el
   beneficio, el costo y una alternativa sin ella. El usuario decide.
4. **Detecta el entorno.** Comprueba el lenguaje y su versión, el linter y el
   formateador del proyecto, y las herramientas rápidas disponibles (`rg`, `fd`,
   `bat`, etc.). Úsalas si existen en lugar de comandos lentos.
5. **Lee el contexto.** Revisa el código, los tests y las convenciones
   existentes antes de proponer cambios; respeta el estilo del proyecto.

## Principios

- **Negative programming:** valida las precondiciones al inicio, retorna temprano
  y falla con errores explícitos; no asumas el camino feliz ni silencies errores.
- **SOLID:** una responsabilidad por unidad, abierto a extensión y cerrado a
  modificación, sustituible, interfaces pequeñas y dependencias hacia
  abstracciones.
- **Funciones atómicas:** pequeñas, con una sola responsabilidad, nombre claro y
  pocos parámetros.
- **Reutilización (DRY):** no dupliques lógica; extrae y reutiliza, sin
  abstraer de más por anticipado.
- **Patrones de diseño y de arquitectura:** úsalos **solo si el caso lo amerita**;
  si los aplicas, verifica que resuelven el problema y justifica la elección.
  Evita añadir complejidad sin beneficio.

## Estilo y legibilidad

- **Clean code:** nombres descriptivos, sin código muerto ni duplicado, sin
  "números mágicos" (usa constantes con nombre), sin anidación innecesaria.
- **Una línea en blanco antes de cada bloque de código** para separarlo del
  texto o código previo, y entre bloques lógicos. Evita el código aglomerado.
- **Declaraciones arriba, cálculos abajo:** primero las entradas, variables y
  constantes; luego la lógica y los cálculos; al final el retorno. Se lee de
  arriba hacia abajo.
- **Indentación y espaciado consistentes** según el lenguaje: el código debe
  respirar.
- **Legibilidad primero:** si algo no se entiende al leerlo, reescríbelo.
- **Buenas prácticas del lenguaje:** sigue las guías idiomáticas (p. ej. PEP 8 y
  *type hints* en Python, ESLint/Prettier en JS/TS) y el linter/formateador del
  proyecto.
- **Comentarios concisos en bloques grandes:** antes de un bloque extenso, una
  breve línea que explique qué hace y por qué. No comentes lo obvio.

## Tests

- Enfoca los tests al **flujo completo**, no a multiplicar casos de una misma
  función que el flujo real no ejercita.
- Cubre el camino feliz, los errores esperados y los bordes del flujo.
- Si agregas lógica pura, acompáñala de su test; si un test no aporta al flujo,
  no lo agregues.

## Documentación

- Sé **conciso y preciso**: lo mínimo que permita entender y usar el código.
- Documenta decisiones y contratos, no la sintaxis obvia.

## Herramientas del proyecto (no reinventar)

- **Antes de crear un archivo desde cero, busca el generador del framework o del CLI y úsalo.**
  Ejemplos: `php artisan make:*` (Laravel), `rails generate` (Rails), `nest g`
  (NestJS), `ng generate` (Angular), `django-admin startapp` (Django), `cargo new`
  (Rust), `go generate` (Go). Los generadores respetan convenciones (nombres,
  timestamps, plantillas) que a mano se rompen: p. ej. una migración creada a mano
  con `0000_` en vez del timestamp real es mala práctica.
- Si no hay generador, sigue la convención del framework/lenguaje a mano.
- Registra los generadores y comandos canónicos en el conocimiento del proyecto
  (`AGENTS.md`, steering) para no re-descubrirlos en cada tarea.

## Entorno, archivos y permisos

- Crea archivos con permisos razonables (`644` archivos, `755` directorios, salvo
  necesidad); **nunca `777`**.
- **En contenedores (Docker)**, crea los archivos con el UID/GID del host para que
  sean editables fuera del contenedor (p. ej. desde el editor):
  - `docker run --user "$(id -u):$(id -g)" …`
  - o define `user:` / *build args* de UID/GID en `docker-compose`.
  - Evita archivos propiedad de `root`.
- Respeta el usuario/grupo que el proyecto ya define; no lo cambies.

## Búsqueda y contexto (economía de tokens)

- Para localizar código usa búsqueda rápida (`rg`, `grep`) en lugar de cargar
  archivos completos; lee solo lo relevante.
- Reutiliza el contexto ya presente en la conversación/spec: mantén la misma línea
  y no re-explores lo ya conocido.
- La información **fundamental y reutilizable** va en documentos **cortos y
  canónicos** (`AGENTS.md`, steering, README) que se referencian; los detalles van
  en archivos que se leen **solo cuando hacen falta**.
- No pegues bloques largos que no aportan a la tarea.

## Cómo verificar (evidencia)

- Define **cómo se prueba** cada cambio: el comando exacto y el resultado esperado
  (o la URL y los pasos de humo en apps web).
- Reporta la **evidencia real** (comando y salida), no supuestos.

## Checklist antes de dar algo por terminado

- [ ] Precondiciones validadas y errores explícitos (negative programming).
- [ ] Funciones atómicas con nombres claros; sin duplicación.
- [ ] Patrones (si los hay) justificados y verificados.
- [ ] Una línea en blanco antes de los bloques; declaraciones arriba.
- [ ] Indentación y espaciado consistentes; buenas prácticas del lenguaje.
- [ ] Linter y formateador en verde.
- [ ] Tests del flujo ejecutados (no solo "compila").
- [ ] Documentación y comentarios concisos.
- [ ] Usé el generador del framework si existía (no reinventé el archivo).
- [ ] Permisos y UID/GID correctos (editable desde el host si hay Docker).
- [ ] Verifiqué con un comando/URL real y tengo la evidencia.
