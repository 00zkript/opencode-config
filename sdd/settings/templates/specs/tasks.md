# Plan de implementación por fases

> **Fase = tarea mayor (`1.`, `2.`, …)**: un objetivo específico agrupado por
> **flujo de trabajo**, no una función suelta. Las subtareas (`X.Y`) son las
> unidades ejecutables (1–3 h) dentro de la fase.
>
> **Regla de fases (gate):** la **última subtarea de cada fase es su gate**: la
> verificación medible del objetivo de la fase (comando + resultado esperado). La
> fase se marca `[x]` solo cuando todas sus subtareas, incluido el gate, están
> `[x]`. Nunca se empieza la siguiente fase con el gate en rojo: se corrige dentro
> de la misma fase.
>
> El número de fases depende del trabajo: puede haber **una sola fase**.

## Formato de plantilla

### Fase con subtareas
- [ ] {{N}}. Fase: {{NOMBRE_DE_LA_FASE}} — {{OBJETIVO_ESPECIFICO_OBSERVABLE}}
- [ ] {{N}}.{{M}}{{PARALLEL_MARK}} {{TAREA_EJECUTABLE}}
  - {{DETALLE}} (incluir solo cuando aporte; omitir si la tarea se explica sola)
  - {{CONDICION_DE_TERMINADO_OBSERVABLE}} (al menos una viñeta debe decir "terminado" en términos observables)
  - _Boundary: {{COMPONENTES}}_ (solo para tareas `(P)`; omitir si el alcance es obvio)
  - _Depends: {{IDS}}_ (solo dependencias no obvias entre límites; la mayoría no lo necesita)
  - _Requirements: {{IDS}}_ (solo IDs numéricos, sin descripciones ni paréntesis)
- [ ] {{N}}.{{ULTIMO}} Gate de la fase: {{VERIFICACION_MEDIBLE}}
  - Comando: `{{COMANDO}}`
  - Resultado esperado: {{SALIDA_OBSERVABLE}}
  - _Requirements: {{IDS}}_

> **Marcador paralelo**: ` (P)` inmediatamente después del número, solo para
> subtareas que pueden ejecutarse en paralelo.
>
> **Cobertura de test opcional**: marca `- [ ]*` solo para trabajo de test
> diferible que ya cubre criterios satisfechos por la implementación principal.

## Ejemplo

- [ ] 1. Fase: Autenticación básica — el usuario inicia sesión y navega sin re-login
- [ ] 1.1 Persistir la sesión autenticada en `state/`
  - Reutilizar el `storage_state` de Playwright entre corridas
  - Terminado cuando una segunda corrida no vuelve a pedir credenciales
  - _Boundary: auth_
  - _Requirements: 1.1, 1.2_
- [ ] 1.2 Gate de la fase: la sesión se conserva entre dos corridas seguidas
  - Comando: `.venv/bin/python main.py --list-courses`
  - Resultado esperado: lista de cursos sin abrir el navegador en modo interactivo
  - _Requirements: 1.1_
